graph TD
    Start[Start] --> Auth[User Authentication]
    Auth -->|Login| Dashboard[User Dashboard]
    Auth -->|Register| Onboarding[User Onboarding]
    Onboarding --> EmailVerification[Email Verification]
    EmailVerification --> WelcomeTutorial[Welcome Tutorial]
    WelcomeTutorial --> FeatureIntro[Feature Introduction]
    FeatureIntro --> Dashboard
    
    Dashboard --> StrategyInput[Strategy Input Phase]
    
    StrategyInput -->|Free Tier| TextInput[Text-based Strategy Description]
    StrategyInput -->|Premium Tier| MultiModal[Multi-Modal Input Options]
    
    MultiModal --> TextDesc[Written Description]
    MultiModal --> ImageUpload[Chart Image Upload]
    MultiModal --> VideoUpload[Video Upload]
    MultiModal --> AudioRec[Audio Recording]
    
    TextInput --> BasicValidation[Basic AI Validation & Interpretation]
    TextDesc --> AIAnalysis[AI Analysis & Learning]
    ImageUpload --> AIAnalysis
    VideoUpload --> AIAnalysis
    AudioRec --> AIAnalysis
    BasicValidation --> StrategyConfirmation[Strategy Confirmation]
    AIAnalysis --> StrategyConfirmation
    
    StrategyConfirmation --> AssetSelection[Asset Selection]
    
    AssetSelection -->|Free Tier| LimitedAssets[Select up to 3 assets]
    AssetSelection -->|Premium Tier| UnlimitedAssets[Select unlimited assets]
    
    LimitedAssets --> BasicMonitoring[Basic Real-time Monitoring]
    UnlimitedAssets --> AdvancedMonitoring[Advanced Real-time Monitoring]
    
    BasicMonitoring --> BasicAlerts[Basic Email Alerts - 5/day]
    AdvancedMonitoring --> AdvancedAlerts[Multi-Channel Alert System]
    
    AdvancedAlerts --> EmailNotif[Email Notifications]
    AdvancedAlerts --> TelegramBot[Telegram Bot]
    AdvancedAlerts --> WhatsApp[WhatsApp Integration]
    AdvancedAlerts --> PushNotif[In-app Push Notifications]
    
    BasicAlerts --> Dashboard
    EmailNotif --> Dashboard
    TelegramBot --> Dashboard
    WhatsApp --> Dashboard
    PushNotif --> Dashboard
    
    Dashboard --> UpgradePrompt{Upgrade to Premium?}
    UpgradePrompt -->|Yes| PaymentProcess[Payment Processing]
    UpgradePrompt -->|No| Dashboard
    
    PaymentProcess --> PremiumActivation[Premium Features Activation]
    PremiumActivation --> Dashboard
    
    Dashboard --> PerformanceAnalytics[Strategy Performance & Analytics]
    Dashboard --> SubscriptionManagement[Subscription Management]
    
    SubscriptionManagement --> ManageSubscription{Manage Subscription}
    ManageSubscription -->|Upgrade| PaymentProcess
    ManageSubscription -->|Downgrade| DowngradeFlow[Downgrade Process]
    ManageSubscription -->|Cancel| CancelFlow[Cancellation Process]
    
    DowngradeFlow --> Dashboard
    CancelFlow --> End[End]
    
    subgraph "Premium Features"
    MultiModal
    UnlimitedAssets
    AdvancedMonitoring
    AdvancedAlerts
    PerformanceAnalytics
    end
    
    subgraph "Free Features"
    TextInput
    LimitedAssets
    BasicMonitoring
    BasicAlerts
    end
