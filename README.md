# Azure Data Factory End-to-End Medallion Architecture Project

**Production-Grade Medallion Pipeline with Modern Linux SSH/SFTP Runtime Integration on Azure**

## 🚀 Key Achievement

Successfully designed, built, and executed a complete **end-to-end Medallion Architecture** (Bronze → Silver → Gold) data pipeline using **Azure Data Factory**. The solution ingests data from On-Prem SFTP sources, applies complex transformations via Mapping Data Flows, and delivers business-ready Gold layer outputs — all orchestrated dynamically with a modern, secure **Linux SSH/SFTP Runtime Integration** replacing the traditional Windows Self-Hosted Integration Runtime.

## 📸 Live Implementation Evidence

Full technical documentation with **20+ live screenshots** from the actual running environment, proving every layer and component works correctly:

**📄 Azure_Data_Factory_Medallion_Project_DE_Notes.pdf**

This document includes detailed figures for:
- Storage containers (Bronze, Silver, Gold)
- All pipeline executions (Parent Pipeline, onprem_ingestion, SQLTODataLake, SilverLayer, GoldLayer)
- Mapping Data Flow executions with joins, ranking, and business logic
- Linux SFTP Docker container + ngrok tunnel
- SFTP Linked Service configuration and successful connection test
- Git integration (Azure DevOps + GitHub)
- Logic App failure alerting workflow

## Architecture Overview

The pipeline follows a clean, production-grade layered approach:

- **Source Layer**: On-Prem SQL Database + Linux SFTP server (Docker container exposed securely via ngrok)
- **Bronze Layer**: Raw data landing in ADLS Gen2 with organized folder structure
- **Silver Layer**: Data Flow transformations (cleaning, derived columns, filtering, joins)
- **Gold Layer**: Business-ready outputs (ranking, Top-N, aggregated views)
- **Orchestration Layer**: Parent Pipeline triggering multiple child pipelines with parameters and Execute Pipeline activity
- **Runtime Integration (Key Modern Alteration)**: Lightweight Linux SFTP server + ADF SFTP Linked Service for secure on-prem connectivity (modern alternative to heavy Windows SHIR)
- **Governance & CI/CD**: Azure DevOps Git integration + ARM templates + Logic Apps for failure alerts

## Technology Stack

| Layer                  | Technology                              | Purpose |
|------------------------|-----------------------------------------|-------|
| Orchestration          | Azure Data Factory                      | Dynamic pipelines, ForEach, Execute Pipeline, Data Flows |
| Storage                | Azure Data Lake Storage Gen2            | Bronze, Silver, Gold containers with Medallion separation |
| Source (On-Prem Files) | Linux SFTP (Docker + ngrok)             | Secure file-based ingestion from on-premises |
| Source (SQL)           | Azure SQL Database                      | Transactional source with watermark-based incremental load |
| Transformation         | Mapping Data Flows                      | Complex joins, aggregations, ranking, and business logic |
| Runtime                | AutoResolveIntegrationRuntime + SFTP    | Modern secure connectivity (Linux SSH/SFTP pattern) |
| Version Control        | Azure DevOps Git + GitHub               | Full Git integration with publish branches |
| Alerting               | Azure Logic Apps                        | Automated failure email notifications |
| IaC                    | ARM Templates                           | Reproducible resource deployment |

## Project Structure

```
azure_adf/
├── pipeline/
│   ├── Parent Pipeline.json
│   ├── onprem_ingestion.json          # SFTP + ForEach file processing
│   ├── SQLTODataLake.json             # Incremental watermark load
│   ├── SilverLayer.json
│   └── GoldLayer.json
├── dataset/
│   ├── ds_onprem_src_param.json
│   ├── ds_sql_source.json
│   └── ... (14+ datasets)
├── linkedService/
│   ├── ls_onprem (SFTP)
│   ├── ls_azure_sql
│   ├── ls_datalake
│   └── ls_github
├── dataflow/
│   ├── SilverDataFlow.json
│   └── GoldDataFlow.json
└── factory/
```

## Key Implementation Highlights

### 1. Linux SSH/SFTP Runtime Integration (Modern Best Practice)
- Replaced traditional Windows Self-Hosted Integration Runtime with a lightweight Linux Docker container running OpenSSH SFTP server.
- Exposed securely via ngrok tunnel for development/testing.
- ADF connects using SFTP Linked Service with Basic authentication.
- Benefits: Lower maintenance, better security posture, easier to containerize and version control.

### 2. Dynamic & Parameterized Orchestration
- Parent Pipeline uses Lookup + ForEach + Execute Pipeline pattern.
- Child pipelines accept parameters for flexible, reusable execution.
- onprem_ingestion pipeline processes multiple files dynamically from SFTP.

### 3. Incremental Data Loading
- SQLTODataLake pipeline uses watermark pattern (LastLoad + LatestLoad lookups).
- Only new/changed records are processed on each run.

### 4. Complex Business Logic in Data Flows
- Silver Layer: Multiple transformations for cleaning, derived columns, gender flags, age filters.
- Gold Layer: Left outer joins, aggregations, ranking (Top 5/10), and business view creation.

### 5. Production-Grade DevOps Practices
- Full Azure DevOps Git integration with collaboration and publish branches.
- ARM templates for infrastructure reproducibility.
- Logic App triggered on pipeline failure for immediate alerting.

## Live Pipeline Execution Evidence (Selected Highlights)

- **onprem_ingestion** pipeline: Successful ForEach + SFTP Copy Data activities
- **SQLTODataLake** pipeline: Successful incremental load with watermark validation
- **SilverLayer** Data Flow: Completed with multiple transformations and data preview
- **GoldLayer** Data Flow: Successful joins, ranking, and sink to Gold container
- **Parent Pipeline**: Orchestrates all child pipelines end-to-end
- **Storage Verification**: Bronze, Silver, and Gold containers populated with correct folder structures
- **SFTP Connectivity**: Docker container running, ngrok tunnel active, Linked Service test connection successful

## Skills Demonstrated

- End-to-end **Medallion Architecture** design and implementation on Azure
- **Modern secure runtime integration** using Linux + SSH/SFTP (production-ready pattern)
- Complex **Mapping Data Flows** with joins, aggregations, ranking, and business logic
- Dynamic pipeline orchestration with parameters and Execute Pipeline activity
- Incremental loading patterns with watermarking
- Git integration and CI/CD readiness for Azure Data Factory
- Infrastructure-as-Code mindset with ARM templates
- Production-grade alerting and monitoring using Logic Apps
- On-premises to cloud secure connectivity patterns

## How to Reproduce

1. Clone this repository
2. Deploy ARM templates or import pipelines/datasets via Azure Data Factory Studio
3. Set up the Linux SFTP container using the provided `docker-compose.yml`
4. Configure ngrok (or expose publicly) for the SFTP endpoint
5. Update Linked Service credentials:
   - `ls_onprem` (SFTP host, port, username, password)
   - `ls_azure_sql` (Azure SQL connection)
   - `ls_datalake` (ADLS Gen2)
6. Trigger the **Parent Pipeline**

---

**This project demonstrates modern Azure Data Engineering best practices** with clean architecture, secure runtime integration, dynamic orchestration, and full live evidence of successful execution.

For complete technical details, architecture decisions, challenges & solutions, and all live screenshots, refer to the enhanced documentation file referenced above or find it in same directory as README.md.