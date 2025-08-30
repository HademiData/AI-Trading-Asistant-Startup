
flowchart TD
  %% MVP Flow: Free tier with text + up to 2 images, timeframe, analysis, chart output

  U[User] -->|Open app| UI[Web UI (React/Next)]
  UI --> AUTH{Logged in?}
  AUTH -- No --> SSO[Sign up / Sign in (Magic link / OAuth)] --> AUTH
  AUTH -- Yes --> TIER{Free tier?}

  TIER -- Yes --> STRAT[Strategy Input Form\n- Text prompt\n- Upload ≤ 2 images\n- Select symbol & timeframe]
  TIER -- No --> PAY[Upgrade Paywall] --> STRAT

  STRAT --> VAL{Valid?\n(text present, ≤2 images, symbol, timeframe)}
  VAL -- No --> ERR[Inline validation errors]
  VAL -- Yes --> SUBMIT[Submit]

  SUBMIT --> Q{Quota OK?}
  Q -- No --> LIMIT[Show daily limit reached]
  Q -- Yes --> API[Backend API (Node/FastAPI)]

  API --> LOG[Persist request\n(Postgres/Supabase)]
  API --> STORE[Store images (S3/Cloud Storage)]
  API --> ORCH[Orchestrator]

  ORCH --> MD[Market Data Fetcher\n(Alpha Vantage / Twelve Data / Polygon)]
  ORCH --> TA[TA Engine (your code)\n- S/R\n- Break of Structure\n- FVG\n- Swing highs/lows]
  ORCH --> LLM[LLM (RAG/MCP tools)\n- Parse strategy text\n- Ground with docs/snippets]
  ORCH --> VISION[Vision Model\n- Read annotations from images]

  MD --> TA
  TA --> ORCH
  LLM --> ORCH
  VISION --> ORCH

  ORCH --> FUSE[Fuse Insights\n- Normalize signals\n- Score confidence\n- Create overlays]
  FUSE --> RENDER[Chart Renderer\n(TradingView Lightweight Charts)]
  FUSE --> REPORT[Explain result\n(Steps, levels, rationale)]

  RENDER --> UI
  REPORT --> UI
  UI --> FB[User feedback / thumbs up/down]
  FB --> TELEMETRY[Metrics & Logs (OpenTelemetry)]

  classDef box fill:#f7f7ff,stroke:#6366f1,stroke-width:1px;
  classDef svc fill:#f0fdf4,stroke:#16a34a,stroke-width:1px;
  classDef gate fill:#fff7ed,stroke:#fb923c,stroke-width:1px;
  class U,UI,STRAT,ERR,RENDER,REPORT,FB,TELEMETRY box;
  class AUTH,TIER,VAL,Q gate;
  class API,LOG,STORE,ORCH,MD,TA,LLM,VISION,FUSE,SSO, PAY svc;m
