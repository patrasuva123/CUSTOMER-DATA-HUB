# Customer Data Hub - Architecture Document - v2.0

**Version:** 2.0 (Updated with OCR, Enhanced Data Model, and Advanced Features)  
**Date:** July 28, 2026  
**Purpose:** Technical architecture and implementation guide for AI Agent development

---

## 🏗️ System Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│         Electron Main Process                       │
│    (Window Management, File I/O, System APIs)       │
└─────────────────────────────────────────────────────┘
           ↓                              ↓
┌──────────────────────────┐  ┌──────────────────────────┐
│   React/Vue Frontend     │  │   Express Backend API    │
│   (UI Components)        │  │   (Business Logic)       │
└──────────────────────────┘  └──────────────────────────┘
           ↓                              ↓
┌──────────────────────────────────────────────────────┐
│    CSV Storage Layer + JSON Config + OCR Engine      │
│  (Tesseract.js for document extraction)              │
└──────────────────────────────────────────────────────┘
           ↓                              ↓
┌──────────────────────────┐  ┌──────────────────────────┐
│   File System            │  │   External Libraries     │
│   (Photos, Documents)    │  │   (Puppeteer, xlsx, OCR) │
└──────────────────────────┘  └──────────────────────────┘
```

---

## 📂 Project Folder Structure - Enhanced

```
customer-data-hub/
├── public/
│   ├── icon.png (App icon with your org branding)
│   └── logo.png (Logo for bio-data templates)
│
├── src/
│   ├── main/
│   │   ├── index.js (Electron main process entry point)
│   │   ├── preload.js (IPC bridge for security)
│   │   └── menu.js (Application menu definition)
│   │
│   ├── renderer/
│   │   ├── index.js (React/Vue app entry)
│   │   ├── App.jsx/App.vue (Main app component)
│   │   ├── components/
│   │   │   ├── Dashboard.jsx (new: timeline, stats)
│   │   │   ├── CustomerList.jsx (new: status column)
│   │   │   ├── CustomerForm.jsx (new: enhanced fields)
│   │   │   ├── CustomerPersonalProfile.jsx (new: detailed form)
│   │   │   ├── AddressManager.jsx (new: multiple addresses)
│   │   │   ├── BankAccountManager.jsx (new: multiple accounts)
│   │   │   ├── DocumentVault.jsx (new: custom docs + OCR)
│   │   │   ├── PhotoUploader.jsx (with crop tool)
│   │   │   ├── BioDataGenerator.jsx (customizable sections)
│   │   │   ├── ImportExport.jsx
│   │   │   ├── Settings.jsx (enhanced settings)
│   │   │   ├── OCRSettings.jsx (new: OCR configuration)
│   │   │   ├── WebsiteManager.jsx (new: manage websites)
│   │   │   ├── ActivityTimeline.jsx (new: recent activity)
│   │   │   └── SearchBar.jsx
│   │   ├── pages/
│   │   │   ├── HomePage.jsx
│   │   │   ├── CustomersPage.jsx (with status column)
│   │   │   ├── CustomerDetailPage.jsx (multi-section)
│   │   │   └── SettingsPage.jsx (enhanced)
│   │   ├── styles/
│   │   │   ├── App.css (Light theme)
│   │   │   ├── dark.css (Dark theme)
│   │   │   └── components.css
│   │   └── utils/
│   │       ├── validators.js (Email, phone validation)
│   │       ├── formatters.js (Date, currency formatting)
│   │       └── ocrUtils.js (new: OCR helpers)
│   │
│   ├── backend/
│   │   ├── index.js (Express server entry)
│   │   ├── routes/
│   │   │   ├── customers.js (enhanced CRUD)
│   │   │   ├── addresses.js (new: address CRUD)
│   │   │   ├── bankAccounts.js (new: bank account CRUD)
│   │   │   ├── education.js (enhanced education)
│   │   │   ├── documents.js (new: document vault + OCR)
│   │   │   ├── biodata.js (customizable bio-data)
│   │   │   ├── websites.js (new: website management)
│   │   │   ├── import.js (bulk import)
│   │   │   ├── export.js (export endpoints)
│   │   │   ├── backup.js (backup/restore)
│   │   │   ├── audit.js (audit log endpoints)
│   │   │   └── ocr.js (new: OCR processing)
│   │   ├── services/
│   │   │   ├── CustomerService.js (enhanced)
│   │   │   ├── AddressService.js (new)
│   │   │   ├── BankAccountService.js (new)
│   │   │   ├── CSVService.js (enhanced for new tables)
│   │   │   ├── DocumentService.js (new: vault management)
│   │   │   ├── OCRService.js (new: Tesseract.js integration)
│   │   │   ├── BioDataService.js (customizable)
│   │   │   ├── WebsiteService.js (new)
│   │   │   ├── ImportService.js
│   │   │   ├── AuditService.js (enhanced)
│   │   │   ├── BackupService.js
│   │   │   └── TimelineService.js (new: activity tracking)
│   │   ├── models/
│   │   │   ├── Customer.js (enhanced schema)
│   │   │   ├── Address.js (new)
│   │   │   ├── BankAccount.js (new)
│   │   │   ├── Education.js (enhanced)
│   │   │   ├── Document.js (new)
│   │   │   ├── Website.js (new)
│   │   │   └── AuditLog.js
│   │   ├── templates/
│   │   │   ├── default-biodata.html (enhanced)
│   │   │   └── custom-templates.json (user templates)
│   │   └── utils/
│   │       ├── logger.js (logging utility)
│   │       ├── database.js (CSV database wrapper)
│   │       └── constants.js (app constants)
│   │
│   └── shared/
│       └── constants.js (shared constants)
│
├── data/ (User data storage - created at runtime)
│   ├── customers.csv (enhanced schema)
│   ├── addresses.csv (new)
│   ├── bank_accounts.csv (new)
│   ├── education.csv (enhanced schema)
│   ├── documents.csv (enhanced with OCR data)
│   ├── metadata.json (app settings + OCR config)
│   ├── important_websites.json (new: default websites)
│   ├── audit_logs.json
│   ├── audit_logs.csv
│   ├── photos/ (customer photos)
│   ├── documents/ (uploaded documents)
│   ├── biodata_templates/ (custom templates)
│   └── backups/ (backup files)
│
├── package.json (Dependencies)
├── electron-builder.json (Build configuration)
├── webpack.config.js (Build configuration)
├── REQUIREMENTS.md (PRD v2.0)
├── ARCHITECTURE.md (This file - v2.0)
├── DEVELOPMENT_PLAN.md (Enhanced task breakdown)
├── CLARIFICATION_INTERVIEW.md (Decision log)
└── README.md (Quick start guide)
```

---

## 🗃️ Enhanced Database Schema (CSV + JSON)

### **customers.csv - Enhanced**
```
customer_id,name,father_name,mother_name,dob,gender,age,primary_language,religion,marital_status,spouse_name,phone,email,aadhaar_no,voter_id,ration_card_no,pan_number,caste,caste_cert_no,caste_cert_date,blood_group,photo_path,status,notes,created_date,last_modified

CUST_001,Rajesh Kumar,Ram Kumar,Geeta Singh,1990-01-08,Male,35,English,Hindu,Married,Priya Kumar,9876543210,rajesh@email.com,123456789012,VOTER2024001,RC-2024-001,ABCDE1234F,OBC,CASTE-2024-001,2024-01-15,"data/photos/CUST_001.jpg",Active,"Senior executive",2026-01-15,2026-07-28
```

### **addresses.csv - New**
```
customer_id,address_id,address_type,street_address,state,block,gram_station,post_office,village,pin_code,is_primary,created_date

CUST_001,ADDR_001,Residential,"123 Main St","Delhi","North","Station 1","Post 1","Village A","110001",true,2026-01-15
CUST_001,ADDR_002,Permanent,"456 Secondary St","UP","South","Station 2","Post 2","Village B","201001",false,2026-01-20
```

### **bank_accounts.csv - New**
```
customer_id,account_id,bank_name,branch,account_number,ifsc_code,account_type,is_primary,created_date

CUST_001,BANK_001,HDFC Bank,Delhi Main,123456789012,HDFC0001234,Savings,true,2026-01-15
CUST_001,BANK_002,ICICI Bank,Delhi Branch,987654321098,ICIC0005678,Current,false,2026-02-10
```

### **education.csv - Enhanced**
```
customer_id,education_id,level,course_name,institution,year_completed,board_university,admit_number,registration_number,total_marks,obtained_marks,percentage,grade,document_path,created_date

CUST_001,EDU_001,B.Tech,Computer Science,IIT Delhi,2012,IIT,ADM-2012-001,REG-2012-001,1000,850,85,A,"data/documents/CUST_001_BTech_Cert.pdf",2026-01-15
CUST_001,EDU_002,12th,Science,Delhi Public School,2008,CBSE,ADM-2008-001,REG-2008-001,500,460,92,A+,"data/documents/CUST_001_12th_Cert.pdf",2026-01-15
```

### **documents.csv - Enhanced with OCR**
```
doc_id,customer_id,document_type,file_name,file_path,upload_date,ocr_extracted_data,ocr_confidence,created_date

DOC_001,CUST_001,Aadhaar,"Aadhaar_Card.jpg","data/documents/CUST_001_Aadhaar.jpg",2026-01-15,"{""aadhaar_no"":""123456789012"",""name"":""Rajesh Kumar"",""dob"":""1990-01-08"",""address"":""Delhi""}",95,2026-01-15
DOC_002,CUST_001,PAN,"Pan_Card.jpg","data/documents/CUST_001_PAN.jpg",2026-01-16,"{""pan_no"":""ABCDE1234F""}",92,2026-01-16
DOC_003,CUST_001,Passbook,"Passbook_Page.jpg","data/documents/CUST_001_Passbook.jpg",2026-01-17,"{""account_no"":""123456789012"",""ifsc"":""HDFC0001234"",""bank_name"":""HDFC Bank""}",88,2026-01-17
```

### **important_websites.json - New (Global Settings)**
```json
[
  {
    "id": "web_001",
    "name": "Aadhaar",
    "url": "https://myaadhaar.uidai.gov.in/",
    "created_date": "2026-01-01"
  },
  {
    "id": "web_002",
    "name": "CSC",
    "url": "https://digitalseva.csc.gov.in/",
    "created_date": "2026-01-01"
  },
  {
    "id": "web_003",
    "name": "Voter",
    "url": "https://voters.eci.gov.in/login",
    "created_date": "2026-01-01"
  },
  {
    "id": "web_004",
    "name": "Ration",
    "url": "https://food.wb.gov.in/",
    "created_date": "2026-01-01"
  }
]
```

### **metadata.json - Enhanced Settings**
```json
{
  "app_version": "2.0.0",
  "last_backup": "2026-07-28T14:30:22Z",
  "theme": "dark",
  "total_customers": 150,
  "ocr_enabled": true,
  "ocr_confidence_threshold": 90,
  "ocr_document_types": ["Aadhaar", "Caste", "PAN", "Passbook", "VoterID", "RationCard", "EducationCert"],
  "timeline_recent_count": 10,
  "biodata_included_sections": [
    "personal_details",
    "full_name",
    "dob",
    "marital_status",
    "education",
    "work_experience",
    "address_details",
    "important_websites",
    "aadhaar_uidai"
  ],
  "custom_templates": [
    {
      "id": "template_standard",
      "name": "Standard Bio-Data",
      "fields": ["name", "photo", "education", "bank", "contact"],
      "created_date": "2026-01-01"
    }
  ],
  "max_capacity": 5000
}
```

### **activity_timeline.json - New (Activity Tracking)**
```json
[
  {
    "timestamp": "2026-07-27T14:35:00Z",
    "customer_id": "CUST_001",
    "customer_name": "Rajesh Kumar",
    "action": "customer_added",
    "description": "New customer added"
  },
  {
    "timestamp": "2026-07-28T09:15:30Z",
    "customer_id": "CUST_001",
    "customer_name": "Rajesh Kumar",
    "action": "photo_uploaded",
    "description": "Customer photo uploaded"
  },
  {
    "timestamp": "2026-07-28T11:22:45Z",
    "customer_id": "CUST_001",
    "customer_name": "Rajesh Kumar",
    "action": "biodata_generated",
    "description": "Bio-data PDF generated"
  },
  {
    "timestamp": "2026-07-28T13:40:20Z",
    "customer_id": "CUST_002",
    "customer_name": "Aarti Das",
    "action": "customer_added",
    "description": "New customer added"
  }
]
```

---

## 🔄 OCR Architecture - Tesseract.js Integration

### **OCR Document Processing Flow:**
```
User Uploads Document
    ↓
Identify Document Type
    ↓
Check if OCR enabled for this type (Settings)
    ↓
Tesseract.js Processing (Local, Offline)
    ↓
Extract Text & Data
    ↓
Calculate Confidence Score
    ↓
Is Confidence >= 90%?
    ├─ YES → Show extracted data with message
    ├─ NO → Show warning "Low confidence, manual review recommended"
    ↓
User Reviews Extracted Data
    ├─ Can edit extracted values
    ├─ Can accept/reject extraction
    ↓
Save to documents.csv with OCR_extracted_data JSON
    ↓
Auto-populate related customer fields
    ↓
Log audit entry
```

### **OCR Extraction Mapping:**
```javascript
{
  "Aadhaar": ["aadhaar_no", "name", "dob", "address"],
  "Caste": ["caste_cert_no", "caste_cert_date"],
  "PAN": ["pan_no"],
  "Passbook": ["account_no", "ifsc_code", "bank_name"],
  "VoterID": ["voter_id"],
  "RationCard": ["ration_card_no"],
  "EducationCert": ["certificate_no", "board_university", "score"]
}
```

---

## 🔄 Data Flow Architecture - Enhanced

### **1. Customer Creation with Multiple Addresses/Bank Accounts:**
```
User Input Form
    ↓
React Component (CustomerPersonalProfile.jsx)
    ↓
Add Address(es) via AddressManager.jsx
    ↓
Add Bank Account(s) via BankAccountManager.jsx
    ↓
IPC Call → Main Process
    ↓
Express Route (POST /api/customers)
    ↓
CustomerService.js (Validation, duplicate check)
    ↓
CSVService.js (Write to customers.csv)
    ↓
AddressService.js (Write to addresses.csv)
    ↓
BankAccountService.js (Write to bank_accounts.csv)
    ↓
AuditService.js (Log: "Customer created")
    ↓
TimelineService.js (Add to activity timeline)
    ↓
Response → UI Update
```

### **2. OCR Document Processing:**
```
User Uploads Document (Aadhaar, PAN, etc.)
    ↓
DocumentVault.jsx (File selection)
    ↓
IPC Call → Main Process
    ↓
Express Route (POST /api/documents/upload)
    ↓
File saved to data/documents/
    ↓
OCRService.js (Tesseract.js processing)
    ↓
Check confidence >= 90%
    ├─ Extract relevant fields based on document type
    ├─ Show message: "Successfully extracted: Aadhaar No (XXXX), Name (YYY), DOB (ZZZ)"
    ↓
User Reviews in DocumentVault
    ├─ Can edit extracted values
    ├─ Click "Approve" to save
    ↓
DocumentService.js (Save to documents.csv)
    ├─ Store OCR_extracted_data as JSON
    ├─ Store OCR_confidence score
    ↓
Auto-populate customer fields:
    ├─ If Aadhaar extracted → update aadhaar_no, name, dob, address in customers.csv
    ├─ If PAN extracted → update pan_number
    ├─ etc.
    ↓
AuditService.js (Log: "Document uploaded + OCR extracted")
    ↓
TimelineService.js (Add to activity timeline)
```

### **3. Status Update & Activity Timeline:**
```
User Changes Customer Status
    ↓
Customer Directory (CustomerList.jsx)
    ↓
IPC Call → API (PUT /api/customers/:id/status)
    ↓
CustomerService.js (Update status in customers.csv)
    ↓
AuditService.js (Log: "Status changed from Active to Inactive")
    ↓
TimelineService.js (Add: "Rajesh Kumar - Status Changed - July 28")
    ↓
Dashboard Activity Timeline Refreshes
```

---

## 💾 Multi-Table Data Management

### **Customer Detail Page - Nested Data:**
```
Customer (Main Record)
├── Address(es) - Multiple records linked by customer_id
├── Bank Account(s) - Multiple records linked by customer_id
├── Education Record(s) - Multiple records linked by customer_id
└── Document(s) - Multiple records linked by customer_id
```

### **Service Layer - Coordinated Saves:**
```
CustomerService.save(customer, addresses, bankAccounts, education, documents)
    ├── Save customer to customers.csv
    ├── For each address → Save to addresses.csv
    ├── For each bank → Save to bank_accounts.csv
    ├── For each education → Save to education.csv
    ├── For each document → Save to documents.csv
    └── Return success/error for entire transaction
```

---

## 🔌 IPC (Inter-Process Communication) Bridge - Enhanced

### **New IPC Channels:**
```javascript
// Address Management
'add-address'
'update-address'
'delete-address'
'get-addresses'

// Bank Account Management
'add-bank-account'
'update-bank-account'
'delete-bank-account'
'get-bank-accounts'

// OCR Processing
'process-ocr'
'get-ocr-confidence'

// Website Management
'add-website'
'update-website'
'delete-website'
'get-websites'

// Activity Timeline
'get-activity-timeline'
'get-timeline-count'

// Document Vault
'upload-document'
'process-document-ocr'
'delete-document'
'get-documents'
```

---

## 🏃 Process Flow Diagrams

### **Multi-Address Customer Creation:**
```
1. Fill Personal Details → Click "Add Address"
2. Address Modal Opens → Fill Street, State, Village, etc.
3. Mark as Primary (checkbox)
4. Click "Save Address" → Add to list
5. Add more addresses? → Repeat steps 2-4
6. All addresses shown in table
7. Click "Final Save" → All data saved to CSVs
```

### **OCR Document Processing:**
```
1. Click "Upload Document" in Document Vault
2. Select file (Aadhaar, PAN, Passbook, etc.)
3. File uploaded
4. OCR processing starts → Show spinner
5. Extraction complete
6. Display message: "Successfully extracted: [data]"
7. Show extracted data in editable form
8. User reviews & edits if needed
9. Click "Approve" to auto-populate customer fields
10. Document saved with OCR metadata
```

---

## 📊 Performance Considerations - v2.0

### **Optimization for Enhanced Data:**

1. **Multi-Table Indexing:**
   - Create index on customer_id in: addresses, bank_accounts, education, documents
   - Fast lookup: `addresses.filter(a => a.customer_id === id)`

2. **Pagination:**
   - Customer list: 50 per page
   - Documents per customer: 20 per page
   - Activity timeline: Last 10 (configurable)

3. **Lazy Loading:**
   - Load customer basic info first
   - Load addresses on tab click
   - Load documents on vault tab click

4. **Caching:**
   - Cache important_websites in memory
   - Cache metadata.json settings
   - Cache activity timeline (last 100 activities)

5. **OCR Optimization:**
   - Tesseract.js runs on main thread (consider Web Worker if slow)
   - Process one document at a time
   - Show progress bar for large documents

---

## 🔐 Security - v2.0

- ✅ No encryption (local storage only)
- ✅ Aadhaar masked display (XXXX-XXXX-1234)
- ✅ Audit logs track all changes
- ✅ OCR data stored locally (no cloud transmission)
- ✅ No authentication (single-user)
- ✅ Backup files for recovery

---

## 📦 Dependencies - Enhanced v2.0

| Component | Package | Version |
|-----------|---------|---------|
| OCR Engine | tesseract.js | latest |
| Word Doc | docx | latest |
| CSV Parsing | csv-parser | latest |
| Excel Export | xlsx | latest |
| PDF Generation | puppeteer | latest |
| UI Components | @mui/material | latest |
| React | react | 18+ |
| Express | express | 4.18+ |
| Electron | electron | latest |

---

**Architecture v2.0 Ready for AI Agent Implementation!**

