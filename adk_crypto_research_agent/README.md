flowchart TD
    A[Start Job via /start_job] --> B{Payment Verified via Masumi}
    B -- No --> B1[Wait or Fail Job]
    B -- Yes --> C[CoordinatorAgent (LlmAgent)]
    
    C --> C1[MarketDataAgent (ToolAgent)]
    C --> C2[TVLAgent (ToolAgent)]
    C --> C3[FirecrawlAgent (ToolAgent)]
    C --> C4[WhitepaperRAGAgent (ToolAgent)]

    C1 --> D1[Token price JSON]
    C2 --> D2[TVL per chain]
    C3 --> D3[Site/docs content]
    C4 --> D4[RAG: Retrieved whitepaper context]

    C --> E[PriceChartAgent (ToolAgent)]
    C --> F[TVLChartAgent (ToolAgent)]
    C --> G[CorrelationChartAgent (ToolAgent)]

    E --> E1[Price chart PNG]
    F --> F1[TVL chart PNG]
    G --> G1[Correlation heatmap PNG]

    C --> H1[VolatilityAgent (LlmAgent)]
    C --> H2[SectorTrendAgent (LlmAgent)]
    C --> H3[TokenComparatorAgent (LlmAgent)]

    H1 --> H1out[Volatility summary]
    H2 --> H2out[Sector insights]
    H3 --> H3out[Comparative metrics]

    C --> I[WriterAgent (LlmAgent)]
    D1 & D2 & D3 & D4 & E1 & F1 & G1 & H1out & H2out & H3out --> I

    I --> J[Markdown report sections]
    C --> K[AssemblerAgent (ToolAgent)]
    J --> K

    K --> L[Markdown report]
    C --> M[PDFExporterAgent (ToolAgent)]
    L --> M

    M --> N[PDF Report Output Path]
    N --> O[Store Result in jobs[job_id]]
    O --> P[User retrieves report via /status]