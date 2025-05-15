adk_crypto_research_agent



flowchart TD
    A["Start Job via /start_job"] --> B{"Payment Verified via Masumi"}
    B -- No --> B1["Wait or Fail Job"]
    B -- Yes --> C["CoordinatorAgent - LlmAgent"]
    C --> C1["MarketDataAgent - ToolAgent"] & C2["TVLAgent - ToolAgent"] & C3["FirecrawlAgent - ToolAgent"] & C4["WhitepaperRAGAgent - ToolAgent"] & E["PriceChartAgent - ToolAgent"] & F["TVLChartAgent - ToolAgent"] & G["CorrelationChartAgent - ToolAgent"] & H1["VolatilityAgent - LlmAgent"] & H2["SectorTrendAgent - LlmAgent"] & H3["TokenComparatorAgent - LlmAgent"] & I["WriterAgent - LlmAgent"] & K["AssemblerAgent - ToolAgent"] & M["PDFExporterAgent - ToolAgent"]
    C1 --> D1["Token price JSON"]
    C2 --> D2["TVL per chain"]
    C3 --> D3["Site/docs content"]
    C4 --> D4["RAG: Retrieved whitepaper context"]
    D1 --> E & G & H1 & H2 & H3 & I
    D2 --> F & H2 & I
    E --> E1["Price chart PNG"]
    F --> F1["TVL chart PNG"]
    G --> G1["Correlation heatmap PNG"]
    D3 --> H2 & I
    H1 --> H1out["Volatility summary"]
    H2 --> H2out["Sector insights"]
    H3 --> H3out["Comparative metrics"]
    D4 --> I
    E1 --> I
    F1 --> I
    G1 --> I
    H1out --> I
    H2out --> I
    H3out --> I
    I --> J["Markdown report sections"]
    J --> K
    K --> L["Markdown report"]
    L --> M
    M --> N["PDF Report Output Path"]
    N --> O["Store Result in jobs_job_id"]
    O --> P["User retrieves report via /status"]