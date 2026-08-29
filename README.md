# Automated Invoice and Document Extraction Pipeline (n8n)
An enterprise-grade document processing automation built with **n8n**, **OpenAI Multimodal API**, and **Google Sheets API**. This pipeline automates the ingestion, text extraction, structured schema validation, and database persistence of PDF invoices.
---
## Architecture Overview
1. **Ingestion Layer**: Receives binary PDF invoices via HTTP POST Webhook endpoints.
2. **Text Extraction Layer**: Parses raw text and line items from binary PDF files using native n8n document extractors.
3. **Structured Data Extraction**: Employs OpenAI multimodal models (`gpt-4o-mini`) configured with strict JSON schemas to extract vendor details, dates, line items, and totals.
4. **Data Persistence**: Automatically maps and appends verified records into Google Sheets / PostgreSQL with duplicate prevention.
---
## Key Features
- **Dynamic Binary Ingestion**: Accepts raw PDF files via multipart/form-data webhooks.
- **Strict JSON Schema Enforcement**: Guarantees typed outputs without unstructured text hallucinations.
- **Automated Line-Item Breakdown**: Extracts nested arrays of line items, quantities, unit prices, and sub-amounts.
- **Cloud Database Persistence**: Synchronizes extracted fields directly to Google Sheets using Google Cloud service account authentication.
---
## Tech Stack
- **Workflow Orchestration**: n8n
- **LLM / Vision Model**: OpenAI `gpt-4o-mini`
- **Document Processing**: n8n Native PDF Text Extractor
- **Database & Storage**: Google Sheets API / Google Cloud Console
- **Testing Interface**: PowerShell `curl.exe`
---
## Setup and Installation
### 1. Import Workflow
1. Download `automated_invoice_processing_pipeline.json` from this repository.
2. Open your n8n instance and navigate to **Workflows** > **Import from File**.
### 2. Configure Credentials
1. **OpenAI**: Add your OpenAI API key in the Model sub-node.
2. **Google Sheets**: Configure your Google OAuth2 or Service Account credentials with read/write access.
### 3. Execution & Testing
Run the following PowerShell command to send a local PDF invoice to the test endpoint:
```powershell
curl.exe -F "data=@C:\path\to\your\invoice.pdf" "http://localhost:5678/webhook-test/invoice-upload"
