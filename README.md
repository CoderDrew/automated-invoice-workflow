# 🧾 Automated Invoice Workflow

> **AI-powered document parsing and email alerts using n8n + GPT-4**

---

## 📌 Overview

This project automates the end-to-end processing of client invoices using [n8n](https://n8n.io/), Google Workspace, and OpenAI GPT-4. It streamlines a traditionally manual, error-prone process by:

- Monitoring a Google Drive folder for new invoice PDFs
- Extracting structured data from unstructured formats
- Appending the data to a Google Sheet
- Generating and sending a custom email notification to the billing team

---

## 💡 The Problem

Manually processing invoices from various clients was time-consuming, inconsistent, and prone to error. The formats were not standardized, making traditional automation brittle. We needed a solution that could intelligently extract key data from PDF invoices, log them into a tracking system, and notify our billing team.

---

## ⚙️ The Workflow

1. **Google Drive Trigger**  
   Watches a shared folder called `Invoice Bucket` for new PDF uploads.

2. **Download File**  
   Retrieves the uploaded invoice binary file by ID.

3. **Extract Text from PDF**  
   Uses the `Extract from File` node to convert the PDF into plain text.

4. **Information Extractor (AI)**  
   GPT-4 extracts the following structured fields from the invoice:
   - Invoice Number
   - Client Name
   - Client Address
   - Client Email
   - Client Phone
   - Total Amount Due
   - Invoice Date
   - Due Date

5. **Append to Google Sheet**  
   Maps the extracted fields to the corresponding columns in an `Invoice DB` spreadsheet.

6. **Generate Email Content (OpenAI)**  
   Uses GPT-4 to format the invoice summary into a Subject + Body email for billing.

7. **Send Email (Gmail)**  
   Automatically emails the invoice summary to the internal billing contact.

---

## 🧠 AI Prompt Engineering

**System Prompt for Extraction:**
```markdown
You are an expert extraction algorithm.  
Only extract relevant information from the text.  
If you do not know the value of an attribute asked to extract, you may omit the attribute's value.

# 🧾 Automated Invoice Workflow

> **AI-powered document parsing and email alerts using n8n + GPT-4**

---

## 📌 Overview

This project automates the end-to-end processing of client invoices using [n8n](https://n8n.io/), Google Workspace, and OpenAI GPT-4. It streamlines a traditionally manual, error-prone process by:

- Monitoring a Google Drive folder for new invoice PDFs
- Extracting structured data from unstructured formats
- Appending the data to a Google Sheet
- Generating and sending a custom email notification to the billing team

---

## 💡 The Problem

Manually processing invoices from various clients was time-consuming, inconsistent, and prone to error. The formats were not standardized, making traditional automation brittle. We needed a solution that could intelligently extract key data from PDF invoices, log them into a tracking system, and notify our billing team.

---

## ⚙️ The Workflow

1. **Google Drive Trigger**  
   Watches a shared folder called `Invoice Bucket` for new PDF uploads.

2. **Download File**  
   Retrieves the uploaded invoice binary file by ID.

3. **Extract Text from PDF**  
   Uses the `Extract from File` node to convert the PDF into plain text.

4. **Information Extractor (AI)**  
   GPT-4 extracts the following structured fields from the invoice:
   - Invoice Number
   - Client Name
   - Client Address
   - Client Email
   - Client Phone
   - Total Amount Due
   - Invoice Date
   - Due Date

5. **Append to Google Sheet**  
   Maps the extracted fields to the corresponding columns in an `Invoice DB` spreadsheet.

6. **Generate Email Content (OpenAI)**  
   Uses GPT-4 to format the invoice summary into a Subject + Body email for billing.

7. **Send Email (Gmail)**  
   Automatically emails the invoice summary to the internal billing contact.

---

## 🧠 AI Prompt Engineering

**System Prompt for Extraction:**
```markdown
You are an expert extraction algorithm.  
Only extract relevant information from the text.  
If you do not know the value of an attribute asked to extract, you may omit the attribute's value.

---

🧩 Tech Stack
🛠️ n8n – Workflow automation

🧠 OpenAI GPT-4 – Data extraction + email generation

📂 Google Drive – Invoice upload source

📄 Google Sheets – Invoice database

📧 Gmail – Notification delivery

📬 Sample Output
Subject: Invoice Received: INV-20394 from ACME Corp
Email Body:
An invoice (INV-20394) was received from ACME Corp on July 12, 2025, in the amount of $2,400. It is due by July 31, 2025. The billing contact is jane@acme.com.
