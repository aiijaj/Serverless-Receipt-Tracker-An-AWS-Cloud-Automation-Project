# 🧾 Smart Receipt Processor with AWS Serverless Stack

This project is an **automated receipt processing pipeline** built using **AWS serverless services**. It enables users to upload receipts to an S3 bucket, extract and process key information (like Date, Amount, Items, and GST) using **Amazon Textract**, store structured data in **DynamoDB**, and receive a neatly formatted summary via **AWS SES**.

---

## 🚀 Features

- 📤 Upload receipts directly to an S3 bucket
- 🤖 Automatic text extraction using **Amazon Textract**
- 🧠 Intelligent parsing of:
  - Date of purchase
  - Total amount
  - List of items
  - GST (if applicable)
- 🗃️ Store parsed data in **DynamoDB**
- 📧 Send a summary email with all extracted info via **AWS SES**
- ⚙️ Fully serverless architecture using **AWS Lambda**

---

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| **AWS S3** | Stores uploaded receipts |
| **AWS Lambda** | Serverless function for processing |
| **Amazon Textract** | Extracts text and structured data from receipts |
| **AWS DynamoDB** | Stores parsed receipt information |
| **AWS SES** | Sends summary emails to the user |
| **IAM Roles** | Handles permissions securely |
| **Python** | Backend logic (Lambda function) |

---

## 🧩 Architecture Overview

```text
         [User Uploads Receipt]
                   |
               ┌───▼────┐
               │  S3    │
               └───┬────┘
                   │ Triggers
               ┌───▼────┐
               │ Lambda │─────> Calls Amazon Textract
               └───┬────┘
                   │
         Parses text (date, items, GST, amount)
                   │
               ┌───▼────┐
               │ Dynamo │ <── Stores extracted data
               └───┬────┘
                   │
               ┌───▼────┐
               │  SES   │─────> Sends summary email
               └────────┘
````

---

## 🧪 Example Output

```json
{
  "Date": "2025-05-26",
  "Items": ["Milk", "Bread", "Butter"],
  "Amount": "₹245.00",
  "GST": "₹12.25",
  "Store": "ABC Supermarket"
}
```

📧 **Email Summary:**

```
Receipt Processed!

Date: 26 May 2025
Store: ABC Supermarket
Items: Milk, Bread, Butter
Amount: ₹245.00
GST: ₹12.25
```

---

## 📦 Setup Instructions

1. **Upload Receipts to S3**

   * Create an S3 bucket (e.g., `receipt-uploads-bucket`)
   * Enable event notifications for `ObjectCreated` to trigger your Lambda

2. **Configure AWS Lambda**

   * Use Python (with boto3)
   * Permissions for Textract, DynamoDB, SES, and S3 required
   * Deploy using AWS Console or CLI

3. **Create DynamoDB Table**

   * Table Name: `Receipts`
   * Partition Key: `receipt_id` (or timestamp)

4. **Enable Amazon Textract**

   * No setup needed, used via API in Lambda

5. **Set Up SES (Simple Email Service)**

   * Verify sender and recipient emails
   * Use region where SES is available

---

## ✅ Future Improvements

* Support for PDFs and multi-page receipts
* Frontend UI for drag & drop uploads
* OCR accuracy improvements with AI post-processing
* Admin dashboard for receipt history & analytics

---

## 📄 License

MIT License. Free to use, share, and modify.

---

## 🙋‍♂️ Author

**Aijaj**
[LinkedIn](https://www.linkedin.com/in/aijaj-mulla/) • [GitHub](https://github.com/aiijaj)

