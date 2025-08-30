```mermaid
flowchart TD
    U[User] --> UI[Web App UI]
    UI --> AUTH{Logged in?}
    AUTH -- No --> SSO[Sign up / Sign in]
    AUTH -- Yes --> STRAT[Input Strategy\n(text + ≤2 images + timeframe)]
    STRAT --> API[Backend API]
    API --> DATA[Market Data Fetcher]
    API --> TA[TA Engine\n(S/R, BOS, FVG)]
    API --> LLM[LLM parses text]
    API --> VISION[Vision model parses images]
    DATA --> TA
    TA --> API
    LLM --> API
    VISION --> API
    API --> FUSE[Fuse insights]
    FUSE --> RENDER[Chart Renderer]
    FUSE --> REPORT[Generate explanation]
    RENDER --> UI
    REPORT --> UI
    UI --> FB[User feedback]
