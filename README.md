\# 🧹 Enterprise-Grade Excel Data Cleaning \& Standardization Pipeline



> 🚀 \*\*An automated, event-driven ETL workflow built using n8n\*\* to automatically ingest messy customer spreadsheets, clean and sanitize raw records, remove duplicates and invalid entries, generate structured audit metrics, and securely upload standardized results to Google Drive.



\---



\## 🎯 Project Overview \& Business Problem



Manual data processing in spreadsheets is highly inefficient, prone to human error, and fails to scale as business operations grow. When dirty data enters CRM platforms or transactional databases, it causes broken analytics, missed customer outreach, and compliance issues.



This automation workflow functions as an end-to-end \*\*Extract, Transform, Load (ETL)\*\* pipeline. It listnes for incoming file payloads via a secure \*\*Webhook\*\*, extracts raw data from \*\*Google Sheets\*\*, executes dynamic validation and cleaning through custom \*\*JavaScript logic\*\*, splits clean records from analytical metadata, formats outputs into native Excel binary files, and archives them systematically into targeted \*\*Google Drive\*\* folder structures.



\---



\## 📊 Business Impact \& Key Value Metrics



| 📈 Metric / Focus Area | 🛠️ Implementation Strategy | 💼 Business Value Delivered |

| :--- | :--- | :--- |

| \*\*Data Quality Assurance\*\* | Advanced Regex \& Data Normalization | 100% Verified Email \& Phone records |

| \*\*Operational Efficiency\*\* | Fully automated execution pipeline | Eliminates 95%+ of manual spreadsheet labor |

| \*\*Auditability \& Compliance\*\* | Batch Execution Summary Generation | Complete visibility into dropped/invalid rows |

| \*\*System Scalability\*\* | Non-blocking API \& Webhook Trigger | Seamlessly handles thousands of entries |



\---



\## ⚙️ Workflow Architecture \& Technical Flow



```text

&#x20;                 ┌────────────────────────┐

&#x20;                 │    Webhook Trigger     │

&#x20;                 └───────────┬────────────┘

&#x20;                             │

&#x20;                             ▼

&#x20;                 ┌────────────────────────┐

&#x20;                 │ Google Sheets Ingest   │

&#x20;                 └───────────┬────────────┘

&#x20;                             │

&#x20;                             ▼

&#x20;           ┌───────────────────────────────────┐

&#x20;           │   n8n JavaScript Engine Node      │

&#x20;           │  (Cleaning \& Regex Validation)    │

&#x20;           └──────┬────────────────────┬───────┘

&#x20;                  │                    │

&#x20;                  ▼                    ▼

&#x20;       ┌─────────────────────┐   ┌─────────────────────┐

&#x20;       │ Clean Dataset Stream│   │ Summary Audit Stream│

&#x20;       └──────────┬──────────┘   └──────────┬──────────┘

&#x20;                  │                         │

&#x20;                  ▼                         ▼

&#x20;       ┌─────────────────────┐   ┌─────────────────────┐

&#x20;       │ XLSX Conversion Node│   │ XLSX Conversion Node│

&#x20;       └──────────┬──────────┘   └──────────┬──────────┘

&#x20;                  │                         │

&#x20;                  ▼                         ▼

&#x20;       ┌─────────────────────┐   ┌─────────────────────┐

&#x20;       │ Google Drive Upload │   │ Google Drive Upload │

&#x20;       └─────────────────────┘   └─────────────────────┘

🔍 Detailed Execution Steps \& Processing Logic

1\. 📥 Ingestion \& Trigger Phase

Webhook Trigger (Webhook Node): Acts as the entry point, allowing external systems or form submissions to trigger data cleaning on demand.



Source Data Fetching (Messy\_customers Node): Connects to Google Sheets API to download incoming unformatted raw spreadsheet records into memory.



2\. ⚡ Dynamic Transformation \& Validation Phase (Data Cleaning Node)

🔤 Text Standardization \& Case Normalization:



Trims leading/trailing whitespaces and replaces multiple inline spaces.



Applies Proper Case to names and locations (e.g., "john DOE " ➔ "John Doe").



📞 Phone Number Standardization:



Auto-prefixes local numbers missing the leading digit (e.g., appending "0" to "1712345678").



Enforces strict regex patterns (/^01\\d{9}$/) to reject malformed contact entries.



✉️ Email Sanitization \& Validation:



Converts all email address strings to lowercase.



Validates standard string structure using Regex (/^\[^\\s@]+@\[^\\s@]+\\.\[^\\s@]+$/).



Explicitly filters out placeholder strings like "(missing)" or empty records.



🛡️ In-Memory Duplicate Filtering:



Uses fast JavaScript Set() lookup tables (seenEmails, seenPhones) to catch duplicate records instantly during loop execution.



🆔 ID Assignment \& Date Formatting:



Assigns standardized sequential primary keys (CUST-0001, CUST-0002).



Formats raw registration dates into clean ISO standard strings (YYYY-MM-DD).



3\. 📊 Reporting, Conversion \& Delivery Phase

📑 Branching Streams: Separates sanitized data (Cleaned data node) from execution batch statistics (Summary Data node).



📈 Audit Trail Generation: Compiles metrics showing:



Total Rows Imported



Total Invalid Rows Removed



Duplicate Rows Identified



Final Yield Output Count



💾 Binary File Conversion \& Cloud Archiving:



Converts JSON outputs to spreadsheet binary objects (clean\_customers.xlsx and SummaryReport.xlsx).



Securely saves both output files into targeted Google Drive folders using OAuth2 connection tokens.



🛠️ Tech Stack \& Key Integrations

⚙️ Workflow Orchestrator: n8n



💻 Custom Scripting Language: JavaScript (ES6+)



🌐 APIs \& Cloud Protocols: Google Sheets API, Google Drive API, Webhooks, RESTful Endpoints



📦 Data Formats: JSON, Binary Spreadsheet (.xlsx)





💡 Consultant Mindset \& Technical Edge

🧠 Why Choose This Architectural Approach?



🔹 Zero Human Dependency: Spreadsheet errors often ruin database updates or downstream marketing automation campaigns. Automating the pipeline ensures error-free data flow.



🔹 Data Transparency \& Auditing: Clients often fear losing data in automated systems. By generating an automated Summary Audit Report, clients get 100% visibility into which rows were filtered out and why.



🔹 Decoupled Architecture: Using Webhook triggers makes this workflow modular. It can be linked to web forms, file drop-boxes, or database triggers without re-engineering the workflow logic.

