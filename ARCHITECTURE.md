# Customer Data Hub - Architecture Document - v2.1

**Version:** 2.1 (Local Web App - Vue.js + Local JSON Storage)  
**Date:** July 28, 2026  
**Purpose:** Technical architecture and implementation guide for AI Agent development

---

## 🏗️ System Architecture Overview - Local Web App

```
┌─────────────────────────────────────────────────────┐
│         Browser (Chrome, Firefox, Edge, Safari)    │
│              Vue 3 + Vite Frontend                 │
└─────────────────────────────────────────────────────┘
           ↓                              ↓
┌──────────────────────────┐  ┌──────────────────────────┐
│   Vue Components         │  │   Local Node.js Server   │
│   (Pinia State Mgmt)     │  │   (Express, Port 5000)   │
└──────────────────────────┘  └──────────────────────────┘
           ↓                              ↓
┌──────────────────────────────────────────────────────┐
│        JSON File Storage + Tesseract.js OCR          │
│     (All processing client-side, offline capable)    │
└──────────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────────┐
│          Local PC File System (/data folder)         │
│   - data/customers.json                              │
│   - data/important_websites.json                     │
│   - data/audit_logs.json                             │
│   - data/settings.json                               │
│   - data/activity_timeline.json                      │
│   - uploads/photos/, uploads/documents/              │
└──────────────────────────────────────────────────────┘
```

---

## 📂 Project Folder Structure - Local Web App

```
customer-data-hub/
├── index.html (HTML entry point)
├── package.json (Dependencies)
├── vite.config.js (Vite bundler config)
├── server.js (Local Express server - lightweight)
│
├── src/
│   ├── main.js (Vue app entry point)
│   ├── App.vue (Root component)
│   ├── stores/
│   │   ├── customerStore.js (Pinia store - customers)
│   │   ├── addressStore.js (Pinia store - addresses)
│   │   ├── bankStore.js (Pinia store - bank accounts)
│   │   ├── educationStore.js (Pinia store - education)
│   │   ├── documentStore.js (Pinia store - documents)
│   │   ├── settingsStore.js (Pinia store - settings)
│   │   ├── timelineStore.js (Pinia store - activity)
│   │   └── auditStore.js (Pinia store - audit logs)
│   │
│   ├── components/
│   │   ├── Dashboard.vue (Dashboard component)
│   │   ├── CustomerList.vue (Customer directory)
│   │   ├── CustomerForm.vue (Add/edit customer)
│   │   ├── CustomerPersonalProfile.vue (Personal details form)
│   │   ├── AddressManager.vue (Multiple addresses)
│   │   ├── BankAccountManager.vue (Multiple bank accounts)
│   │   ├── EducationForm.vue (Education records)
│   │   ├── DocumentVault.vue (Document upload + OCR)
│   │   ├── PhotoUploader.vue (Photo upload with crop)
│   │   ├── BioDataGenerator.vue (PDF/HTML generation)
│   │   ├── ImportExport.vue (Bulk import/export)
│   │   ├── ActivityTimeline.vue (Recent activities)
│   │   ├── SearchBar.vue (Search component)
│   │   └── Settings/
│   │       ├── OCRSettings.vue (OCR configuration)
│   │       ├── WebsiteManager.vue (Website management)
│   │       ├── BioDataSettings.vue (Bio-data sections)
│   │       ├── ThemeSettings.vue (Theme toggle)
│   │       ├── BackupRestore.vue (Backup/restore)
│   │       ├── AuditLog.vue (Audit log viewer)
│   │       └── TimelineSettings.vue (Timeline config)
│   │
│   ├── pages/
│   │   ├── HomePage.vue (Dashboard page)
│   │   ├── CustomersPage.vue (Customer directory page)
│   │   ├── CustomerDetailPage.vue (Customer detail page)
│   │   ├── BioDataGeneratorPage.vue (Bio-data generation page)
│   │   └── SettingsPage.vue (Settings page)
│   │
│   ├── services/
│   │   ├── api.js (API communication with local server)
│   │   ├── customerService.js (Customer CRUD)
│   │   ├── addressService.js (Address CRUD)
│   │   ├── bankService.js (Bank account CRUD)
│   │   ├── educationService.js (Education CRUD)
│   │   ├── documentService.js (Document CRUD)
│   │   ├── ocrService.js (OCR processing - Tesseract.js)
│   │   ├── bioDataService.js (Bio-data generation)
│   │   ├── importExportService.js (CSV import/export)
│   │   ├── backupService.js (JSON backup/restore)
│   │   ├── auditService.js (Audit logging)
│   │   ├── timelineService.js (Activity timeline)
│   │   ├── fileService.js (File system operations)
│   │   └── validators.js (Data validation)
│   │
│   ├── utils/
│   │   ├── formatters.js (Date, currency formatting)
│   │   ├── ocrUtils.js (OCR helper functions)
│   │   ├── validators.js (Client-side validation)
│   │   └── constants.js (App constants)
│   │
│   └── styles/
│       ├── main.css (Global styles)
│       ├── light-theme.css (Light theme)
│       └── dark-theme.css (Dark theme)
│
├── data/ (Created at runtime, stores all customer data)
│   ├── customers.json (All customer records)
│   ├── important_websites.json (Website configurations)
│   ├── audit_logs.json (Audit trail)
│   ├── settings.json (App settings)
│   ├── activity_timeline.json (Recent activities)
│   └── db/
│       └── backup_TIMESTAMP.json (Backup files)
│
├── uploads/ (Created at runtime, stores uploaded files)
│   ├── photos/
│   │   └── CUST_001.jpg (Customer photos)
│   ├── documents/
│   │   └── CUST_001_Aadhaar.jpg (Uploaded documents)
│   └── biodata/
│       └── CUST_001_biodata.pdf (Generated PDFs)
│
├── dist/ (Built Vue app - generated by Vite)
│   └── (Compiled and optimized app)
│
├── README.md
├── REQUIREMENTS.md
├── ARCHITECTURE.md
└── DEVELOPMENT_PLAN.md
```

---

## 💾 Data Storage Structure - JSON Files (No Database)

### **data/customers.json - Single Source of Truth**
```json
{
  "version": "2.1",
  "last_updated": "2026-07-28T14:30:22Z",
  "customers": [
    {
      "id": "CUST_001",
      "name": "Rajesh Kumar",
      "father_name": "Ram Kumar",
      "mother_name": "Geeta Singh",
      "dob": "1990-01-08",
      "gender": "Male",
      "age": 35,
      "primary_language": "English",
      "religion": "Hindu",
      "marital_status": "Married",
      "spouse_name": "Priya Kumar",
      "phone": "9876543210",
      "email": "rajesh@email.com",
      "aadhaar_no": "XXXX-XXXX-1234",
      "voter_id": "VOTER2024001",
      "ration_card_no": "RC-2024-001",
      "pan_number": "ABCDE1234F",
      "caste": "OBC",
      "caste_cert_no": "CASTE-2024-001",
      "caste_cert_date": "2024-01-15",
      "blood_group": "O+",
      "status": "Active",
      "photo_path": "uploads/photos/CUST_001.jpg",
      "addresses": [
        {
          "id": "ADDR_001",
          "type": "Residential",
          "street": "123 Main St",
          "state": "Delhi",
          "block": "North",
          "gram_station": "Station 1",
          "post_office": "Post 1",
          "village": "Village A",
          "pin_code": "110001",
          "is_primary": true
        }
      ],
      "bank_accounts": [
        {
          "id": "BANK_001",
          "bank_name": "HDFC Bank",
          "branch": "Delhi Main",
          "account_number": "123456789012",
          "ifsc_code": "HDFC0001234",
          "account_type": "Savings",
          "is_primary": true
        }
      ],
      "education": [
        {
          "id": "EDU_001",
          "level": "B.Tech",
          "course_name": "Computer Science",
          "institution": "IIT Delhi",
          "year_completed": 2012,
          "board_university": "IIT",
          "admit_number": "ADM-2012-001",
          "registration_number": "REG-2012-001",
          "total_marks": 1000,
          "obtained_marks": 850,
          "percentage": 85,
          "grade": "A",
          "document_path": "uploads/documents/CUST_001_BTech.pdf"
        }
      ],
      "documents": [
        {
          "id": "DOC_001",
          "type": "Aadhaar",
          "file_name": "Aadhaar_Card.jpg",
          "file_path": "uploads/documents/CUST_001_Aadhaar.jpg",
          "upload_date": "2026-01-15",
          "ocr_extracted": {
            "aadhaar_no": "123456789012",
            "name": "Rajesh Kumar",
            "dob": "1990-01-08",
            "address": "Delhi"
          },
          "ocr_confidence": 95
        }
      ],
      "created_date": "2026-01-15",
      "last_modified": "2026-07-28"
    }
  ]
}
```

### **data/settings.json**
```json
{
  "version": "2.1",
  "theme": "dark",
  "language": "English",
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
  "last_backup": "2026-07-28T14:30:22Z",
  "total_customers": 150,
  "app_version": "2.1.0"
}
```

### **data/important_websites.json**
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

### **data/activity_timeline.json**
```json
{
  "activities": [
    {
      "id": "ACT_001",
      "timestamp": "2026-07-28T14:35:00Z",
      "customer_id": "CUST_001",
      "customer_name": "Rajesh Kumar",
      "action": "customer_added",
      "description": "New customer added"
    },
    {
      "id": "ACT_002",
      "timestamp": "2026-07-28T15:22:45Z",
      "customer_id": "CUST_001",
      "customer_name": "Rajesh Kumar",
      "action": "document_uploaded",
      "description": "Document uploaded: Aadhaar"
    }
  ]
}
```

### **data/audit_logs.json**
```json
{
  "logs": [
    {
      "id": "AUD_001",
      "timestamp": "2026-07-28T14:35:00Z",
      "action": "customer_created",
      "customer_id": "CUST_001",
      "field_changes": {
        "name": { "old": null, "new": "Rajesh Kumar" },
        "phone": { "old": null, "new": "9876543210" }
      },
      "user": "system"
    }
  ]
}
```

---

## 🔄 OCR Architecture - Tesseract.js in Browser

### **OCR Processing Flow (All Client-Side):**
```
User Uploads Document
    ↓
Identify Document Type (Aadhaar, PAN, etc.)
    ↓
Check if OCR enabled for this type (Settings)
    ↓
Load Tesseract.js in Browser
    ↓
Send image to Tesseract (Client-side processing)
    ↓
Extract Text & Data
    ↓
Calculate Confidence Score
    ↓
Is Confidence >= 90%?
    ├─ YES → Show extracted data with message
    ├─ NO → Show warning "Low confidence, manual review recommended"
    ↓
User Reviews Extracted Data in Modal
    ├─ Can edit extracted values
    ├─ Can accept/reject extraction
    ↓
Save to data/customers.json with OCR_extracted_data
    ↓
Auto-populate related customer fields
    ↓
Add audit entry to data/audit_logs.json
    ↓
Update activity timeline in data/activity_timeline.json
```

### **OCR Extraction Mapping:**
```javascript
{
  "Aadhaar": ["aadhaar_no", "name", "dob", "address"],
  "Caste": ["caste_cert_no", "caste_cert_date"],
  "PAN": ["pan_number"],
  "Passbook": ["account_number", "ifsc_code", "bank_name"],
  "VoterID": ["voter_id"],
  "RationCard": ["ration_card_no"],
  "EducationCert": ["certificate_no", "board_university", "score"]
}
```

---

## 🔌 API Endpoints - Local Express Server

### **Express Server (Port 5000, Lightweight)**
- Runs locally on same machine
- Handles file I/O (JSON read/write)
- Serves static files (photos, documents)
- CORS enabled for localhost only

### **API Routes (JSON Request/Response):**

**Customers:**
```
POST   /api/customers              (Create customer)
GET    /api/customers              (Get all customers)
GET    /api/customers/:id          (Get customer with all nested data)
PUT    /api/customers/:id          (Update customer)
PUT    /api/customers/:id/status   (Update status only)
DELETE /api/customers/:id          (Delete customer)
GET    /api/customers/search?q=... (Search by name/phone/email)
```

**Addresses:**
```
POST   /api/addresses              (Add address)
GET    /api/addresses/:customerId  (Get all addresses for customer)
PUT    /api/addresses/:id          (Update address)
DELETE /api/addresses/:id          (Delete address)
PUT    /api/addresses/:id/primary  (Set as primary)
```

**Bank Accounts:**
```
POST   /api/bank-accounts          (Add account)
GET    /api/bank-accounts/:customerId (Get all accounts)
PUT    /api/bank-accounts/:id      (Update account)
DELETE /api/bank-accounts/:id      (Delete account)
PUT    /api/bank-accounts/:id/primary (Set as primary)
```

**Documents & OCR:**
```
POST   /api/documents/upload       (Upload document)
POST   /api/documents/:id/ocr      (Process OCR)
GET    /api/documents/:customerId  (Get customer documents)
PUT    /api/documents/:id          (Update document)
DELETE /api/documents/:id          (Delete document)
```

**Settings & Configuration:**
```
GET    /api/settings               (Get all settings)
PUT    /api/settings               (Update settings)
GET    /api/websites               (Get all websites)
POST   /api/websites               (Add website)
PUT    /api/websites/:id           (Update website)
DELETE /api/websites/:id           (Delete website)
```

**Activity & Audit:**
```
GET    /api/timeline               (Get activity timeline)
GET    /api/audit-logs             (Get audit logs)
GET    /api/audit-logs?filter=...  (Filter audit logs)
```

**Import/Export:**
```
POST   /api/import/csv             (Import customers from CSV)
GET    /api/export/csv             (Export all to CSV)
GET    /api/export/excel           (Export all to XLSX)
POST   /api/backup/create          (Create JSON backup)
POST   /api/backup/restore         (Restore from JSON)
```

---

## 🔄 Data Flow - Customer Creation

```
1. User fills form in CustomerForm.vue
   ↓
2. Vue component calls customerService.createCustomer()
   ↓
3. Service validates data (validators.js)
   ↓
4. Service calls API: POST /api/customers
   ↓
5. Express server receives request
   ↓
6. Read data/customers.json (JSON file)
   ↓
7. Add new customer record to array
   ↓
8. Write updated JSON back to data/customers.json
   ↓
9. Check for duplicates and add audit entry
   ↓
10. Add activity timeline entry
    ↓
11. Return success response to Vue component
    ↓
12. Pinia store updates (customerStore, timelineStore, auditStore)
    ↓
13. Vue component re-renders with new data
    ↓
14. Show success message to user
```

---

## 🔄 Data Flow - OCR Document Processing

```
1. User selects document in DocumentVault.vue
   ↓
2. File selected → ocrService.processOCR(file, documentType)
   ↓
3. Service loads Tesseract.js in browser
   ↓
4. Tesseract processes image (client-side, offline)
   ↓
5. Extract text based on document type
   ↓
6. Calculate confidence score
   ↓
7. Show extracted data in modal for review
   ↓
8. User edits if needed and clicks "Approve"
   ↓
9. Call API: POST /api/documents/upload
   ↓
10. Express server saves file to uploads/documents/
    ↓
11. Save document record to data/customers.json
    ↓
12. Auto-populate customer fields (if Aadhaar, extract name, DOB, etc.)
    ↓
13. Update data/audit_logs.json with extraction details
    ↓
14. Update data/activity_timeline.json
    ↓
15. Return success response
    ↓
16. Pinia stores update
    ↓
17. Show success message with extracted data
```

---

## 🎯 Pinia State Management Architecture

### **Stores (Centralized State):**

**customerStore.js:**
```javascript
export const useCustomerStore = defineStore('customer', {
  state: () => ({
    customers: [],
    selectedCustomer: null,
    loading: false,
    error: null
  }),
  getters: {
    getCustomerById: (state) => (id) => state.customers.find(c => c.id === id),
    getCustomersByStatus: (state) => (status) => state.customers.filter(c => c.status === status),
    getTotalCustomers: (state) => state.customers.length,
    searchCustomers: (state) => (query) => {
      return state.customers.filter(c => 
        c.name.toLowerCase().includes(query) || 
        c.phone.includes(query) ||
        c.email.toLowerCase().includes(query)
      );
    }
  },
  actions: {
    async fetchCustomers() {
      this.loading = true;
      try {
        const response = await fetch('/api/customers');
        this.customers = await response.json();
      } catch (e) {
        this.error = e.message;
      }
      this.loading = false;
    },
    async createCustomer(customerData) {
      try {
        const response = await fetch('/api/customers', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(customerData)
        });
        const newCustomer = await response.json();
        this.customers.push(newCustomer);
        return newCustomer;
      } catch (e) {
        this.error = e.message;
      }
    }
  }
});
```

**Similarly for addressStore, bankStore, documentStore, settingsStore, timelineStore, auditStore**

---

## 🏃 Process Flows

### **Multi-Address Customer Creation:**
```
1. CustomerForm.vue → Fill personal details
2. AddressManager.vue → Click "Add Address"
3. Address modal opens → Fill address details
4. Mark as Primary checkbox
5. Click "Save Address" → Add to addresses array
6. Repeat for more addresses
7. All addresses shown in table
8. Click "Final Save" Customer
9. All data (customer + addresses + banks) sent to API
10. Express server saves all to data/customers.json
11. Success message shown
```

### **Bio-Data Generation:**
```
1. User goes to BioDataGenerator page
2. Select customer from dropdown
3. Check which sections to include
4. Select format (PDF or HTML)
5. Click "Generate"
6. bioDataService builds HTML from template
7. If PDF: Use html2pdf to convert
8. If HTML: Generate HTML file
9. Browser downloads file
10. File saved to user's Downloads folder
11. Success message with file path
```

### **Backup & Restore:**
```
Backup:
1. User clicks "Backup Now" in Settings
2. backupService reads all JSON files from data/
3. Zips or combines into single backup.json
4. Browser downloads backup_TIMESTAMP.json
5. File saved to user's Downloads folder

Restore:
1. User clicks "Restore from Backup"
2. Selects backup.json file from computer
3. Confirms "This will replace all data"
4. backupService reads backup file
5. Overwrites data/customers.json and other files
6. App reloads with restored data
7. Success message
```

---

## 🔐 Security - Local PC Only

- ✅ **No internet communication** - All processing local
- ✅ **No cloud storage** - Data stays in data/ folder
- ✅ **No database server** - JSON files only
- ✅ **Express server localhost only** - No external access
- ✅ **Aadhaar masked** - Display as XXXX-XXXX-1234
- ✅ **No encryption** - Single-user local app
- ✅ **Audit logs** - Track all changes locally
- ✅ **Backup/restore** - JSON export/import only

---

## 📦 Dependencies - Minimal, Local-Only

| Component | Package | Purpose |
|-----------|---------|---------|
| Frontend | vue@3 | UI framework |
| State Mgmt | pinia | Store management |
| UI | vuetify@3 | Material design components |
| Styling | tailwindcss | Utility CSS |
| Build | vite | Fast build tool |
| Backend | express | Local server |
| OCR | tesseract.js | Client-side text extraction |
| PDF | html2pdf.js | Browser-based PDF generation |
| Excel | xlsx | Excel export |
| Crop | vue-cropper | Image cropping |
| Validation | joi | Schema validation |
| File System | fs (node.js) | Read/write JSON files |

---

## 🚀 How to Run

### **Development:**
```bash
npm install              # Install dependencies
npm run dev             # Start Vite dev server + Express server
# Browser opens: http://localhost:5173
# Express running on: http://localhost:5000
# All data in: ./data/ folder
```

### **Production (Folder Distribution):**
```bash
npm run build           # Build Vue app with Vite
npm run server          # Run Express server
# App available at: http://localhost:5173
# Can copy entire folder to USB/another PC
```

---

## 📊 Performance & Scalability

| Metric | Value |
|--------|-------|
| Max customers | 5,000 |
| File size (10,000 customers) | ~50 MB (JSON) |
| Load time (1,000 customers) | <500ms |
| Search speed | Real-time (< 100ms) |
| OCR processing | 3-10 seconds per image |
| Backup file size (5,000 customers) | ~25 MB |

### **Optimization Strategies:**
- Lazy load customer data (first 100, then pagination)
- Cache OCR results to avoid re-processing
- Compress photos before upload
- Pagination for large lists (50 per page)
- Virtual scrolling for customer directory

---

**Architecture v2.1 Ready for AI Agent Implementation!**

