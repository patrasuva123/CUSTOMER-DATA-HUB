# Customer Data Hub - Product Requirements Document (PRD) - v2.1

**Version:** 2.1 (Web App - Vue.js, Local Storage)  
**Date:** July 28, 2026  
**Status:** Ready for Development  
**Target Platform:** Web Application (Browser-based, Local PC Only)  

---

## 📋 Executive Summary

**Project:** Customer Data Hub - Advanced customer management web application with comprehensive personal data, OCR-based document extraction, and professional bio-data generation.

**Target Users:** Individual business owners or small organizations (single user, local PC only)

**Max Capacity:** Up to 5,000 customers

**Platform:** Web Application (Vue.js + Local Backend)
- No installation required (just run from folder)
- Works in any modern browser (Chrome, Firefox, Edge, Safari)
- Responsive design (desktop optimized, mobile friendly)
- **Data stored ONLY on local PC** (no cloud, no internet required)
- Run offline completely
- Portable folder - can move entire app to USB/another PC

**Key Advantages:** 
- Access from browser on same PC
- No internet required
- All data stays on local machine
- No installation, just folder-based
- Can run on Windows, Mac, Linux

---

## 🎯 Core Features (MVP Phase 1 - v2.1)

### 1. **Customer Management with Enhanced Personal Data** ✅

#### **Personal Profile Section:**
- **Basic Info:**
  - Full Name, Father's Name, Mother's Name
  - Date of Birth, Gender, Age
  - Primary Language (Dropdown: English, Hindi, Bengali, Marathi, etc.)
  - Religion (Dropdown or free text)
  - Marital Status (Dropdown: Single, Married, Divorced, Widowed)
  - Spouse Name (Optional text field)
  - Mobile Number, Email ID

#### **Identity & Document Numbers:**
  - **Aadhaar Number** (12 digits, optional)
    - Validation: 12-digit format
    - Display: Masked (XXXX-XXXX-1234) for privacy
    - OCR auto-extract from Aadhaar image
  
  - **Voter ID Number** (Alphanumeric, Indian standard, optional)
    - OCR auto-extract
  
  - **Ration Card Number** (Alphanumeric, Indian standard, optional)
    - OCR auto-extract
  
  - **PAN Number** (Alphanumeric, optional)
    - OCR auto-extract
  
  - **Caste** (Dropdown + Certificate Details)
    - Options: General, OBC, SC, ST, Other
    - If "Other" selected: Show text input for Caste Certificate Number
    - Additional field: Date of Issue (date picker)
    - OCR auto-extract: Caste Number, Date of Issue from Caste Certificate image
    - Optional

#### **Bank & Financial Details (Multiple Accounts):**
  - Can add multiple bank accounts
  - Per account:
    - Bank Name (text)
    - Branch (text)
    - Account Number (text, OCR auto-extract from passbook)
    - IFSC Code (text, OCR auto-extract from passbook)
    - Account Type (Dropdown: Savings, Current, etc.)
    - **Mark as Primary Account** (checkbox, only one can be primary)
  - Passbook upload button with OCR extraction

#### **Blood Group** (Optional)
  - Dropdown: A+, A-, B+, B-, O+, O-, AB+, AB-

---

### 2. **Address Management - Multiple Addresses** ✅

- Add multiple addresses per customer
- Per address:
  - Address Type (Dropdown: Residential, Permanent, Office, Other)
  - Street Address (text)
  - State (text)
  - Block (text)
  - Gram Station (text)
  - Post Office (text)
  - Village (text)
  - Pin Code (text)
  - **Mark as Primary Address** (checkbox, only one can be primary)
- OCR auto-extract address from Aadhaar image

---

### 3. **Education & Qualifications** ✅

#### **Per Education Record:**
- **Education Level** (Dropdown: 10th, 12th, Diploma, Bachelor's, Master's, etc.)
  - When level selected, show these fields:
    - Course/Stream Name (text)
    - Institution Name (text)
    - Year of Completion (date picker)
    - Board/University (text)
    - **Admit Number** (text, linked to this education record)
    - **Registration Number** (text, linked to this education record)
    - Total Marks (number)
    - Obtained Marks (number)
    - Percentage of Marks (auto-calculated)
    - Grade (text)
    - Document Upload: Upload certificate with OCR
      - OCR auto-extract: Certificate Number, Board/University, Score

---

### 4. **Document Vault - Customizable** ✅

- **Pre-defined document types:**
  - Aadhaar
  - Voter ID
  - Ration Card
  - PAN Card
  - Caste Certificate
  - Passport
  - Mark Sheet
  - Admit Card
  - Registration Certificate
  - Driving License
  - (User can add custom document types)

- **Per document:**
  - Document name (text)
  - Document type (dropdown or custom)
  - Upload file (PDF, JPG, PNG)
  - **OCR auto-extraction** (when document uploaded, based on type):
    - Aadhaar → Extract: Number, Name, DOB, Address
    - Caste Cert → Extract: Caste Number, Date of Issue
    - PAN → Extract: PAN Number
    - Passbook → Extract: Account Number, IFSC, Bank Name
    - Voter ID → Extract: Voter Number
    - Ration Card → Extract: Ration Card Number
    - Education Cert → Extract: Certificate Number, Board, Score
  - **Extraction message:** "Successfully extracted: Aadhaar Number (XXXX-XXXX-1234), Name (Rajesh Sen), DOB (08/01/1990)"
  - User can review and edit extracted data before saving
  - ✅ Documents stored in local PC folder
  - No cloud upload

---

### 5. **Photo Management** ✅

- Built-in photo crop tool
- Supported formats: JPG, PNG
- User can: drag, resize, rotate before saving
- Auto-save cropped photo to local customer folder

---

### 6. **Bio-Data Generator** ✅

- Generate PDF documents using html2pdf
- Generate downloadable HTML with custom styling
- Fully editable format
- **Customizable content in Settings:**
  - Toggle which sections to include:
    - ✅ Personal Details
    - ✅ Full Name
    - ✅ DOB
    - ☐ Father's/Mother's Name
    - ✅ Marital Status
    - ✅ Education & Qualifications
    - ✅ Work Experience
    - ✅ Address Details
    - ✅ Important Web Links
    - ✅ Aadhaar (UIDAI)
    - (And more as per settings)
- User downloads bio-data as PDF or HTML
- Saved in app downloads folder
- Supported export: PDF + HTML

---

### 7. **Important Websites - Customizable** ✅

#### **Default Websites (Global, customizable in Settings):**
1. Aadhaar - https://myaadhaar.uidai.gov.in/
2. CSC (Common Service Centre) - https://digitalseva.csc.gov.in/
3. Voter - https://voters.eci.gov.in/login
4. Ration - https://food.wb.gov.in/

#### **In Customer Detail Page:**
- New tab: "Important Web Links"
- Display list of configured websites with clickable links
- Open in new browser tab

#### **In Settings:**
- Manage websites:
  - Add new website (Name + URL)
  - Edit existing website
  - Delete website
  - Changes apply globally to all customers
  - Stored in local PC

---

### 8. **Customer Status Tracking** ✅

- **Status Column in Customer Directory:**
  - Options: Active, Inactive, Not Interested
  - Dropdown selector
  - Sortable/Filterable
  - Stored locally on PC
  - Visible in Customer Detail page

---

### 9. **Dashboard with Activity Timeline** ✅

#### **Recent Activity Timeline (Sidebar):**
- Show last 10 customers added
- Configurable in Settings (change count: 5, 10, 15, 20)
- Track activities:
  - Customer added
  - Customer updated
  - Customer deleted
  - Bio-data generated
  - Document uploaded
- Display format: "Customer Name - Action - Date"
- Example: "Rajesh Sen - Added - Dev 21, 2022"

---

### 10. **Bulk Import** ✅

- Import customers from CSV file
- **Duplicate Handling:** Show warning dialog
  - Display list of duplicates found
  - Let user choose: "Import anyway" or "Skip duplicates"
  
- **Error Handling:** Show error preview dialog
  - Display summary: "450 valid rows, 50 errors"
  - Show error details/examples
  - Let user choose: "Import valid rows" or "Cancel"
  - Support partial import

---

### 11. **Data Export** ✅

- **CSV Export:** All customer data to CSV file
- **Excel Export:** All customer data to XLSX with formatting
- User chooses save location (browser download to local PC)
- Export includes all categories (customers, education, documents, addresses)

---

### 12. **System Settings - Enhanced** ✅

#### **OCR Settings:**
- Toggle: Enable/Disable OCR globally
- Select which document types support OCR:
  - ☑️ Aadhaar
  - ☑️ Caste Certificate
  - ☑️ PAN Card
  - ☑️ Passbook
  - ☑️ Voter ID
  - ☑️ Ration Card
  - ☑️ Education Certificates
- Confidence threshold: Accept extraction only if 90%+ confident
- Language: English only

#### **Website Management:**
- Add/Edit/Delete Important Websites
- Changes apply globally to all customers

#### **Bio-Data Customization:**
- Select which sections to include in generated bio-data
- Choose default template

#### **Theme:**
- Light and Dark mode toggle
- Persistent (remembers user preference)

#### **Data Backup & Export:**
- Export all data to JSON format
- Import from backup JSON file
- Manual download/upload only
- Button: "Backup Now" → Downloads all data as JSON
- Button: "Restore from Backup" → Upload JSON to restore

#### **Audit Logging:**
- View audit trail
- Filter by customer or action
- Export audit log to CSV
- High detail level (every field change logged)

#### **Timeline Configuration:**
- Set number of recent customers to display (5, 10, 15, 20)

---

## 📊 Data Storage Structure - Local PC Only

### **Folder Structure (App Root):**
```
customer-data-hub/
├── index.html (Entry point)
├── app.js (Vue app bootstrap)
├── server.js (Local Node.js server)
├── package.json
├── data/
│   ├── customers.json (All customer data)
│   ├── important_websites.json (Website list)
│   ├── audit_logs.json (Audit trail)
│   ├── settings.json (App settings)
│   ├── activity_timeline.json (Recent activities)
│   └── db/ (IndexedDB backup)
│       └── export.json (Full backup)
├── uploads/
│   ├── photos/
│   │   └── CUST_001.jpg (Customer photos)
│   └── documents/
│       └── CUST_001_Aadhaar.jpg (Uploaded documents)
├── dist/
│   └── (Compiled Vue app)
└── src/
    ├── components/
    └── pages/
```

### **Data Files Format - JSON (No Database):**

**data/customers.json:**
```json
{
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
          "village": "Village A",
          "pin_code": "110001",
          "is_primary": true
        }
      ],
      "bank_accounts": [
        {
          "id": "BANK_001",
          "bank_name": "HDFC Bank",
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
          "grade": "A"
        }
      ],
      "documents": [
        {
          "id": "DOC_001",
          "type": "Aadhaar",
          "file_path": "uploads/documents/CUST_001_Aadhaar.jpg",
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

**data/settings.json:**
```json
{
  "theme": "dark",
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
  "language": "English",
  "last_backup": "2026-07-28T14:30:22Z",
  "total_customers": 150
}
```

**data/important_websites.json:**
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
  }
]
```

---

## 🔍 Search Functionality

### **Search Scope: Phase 1**
- **Fields:** Name, Phone Number, Email ONLY
- **Type:** Full-text search
- **Case-insensitive**
- **Partial match supported**
- **Real-time search** (as user types)
- **Searches local data only** (no server calls)

---

## ⚠️ Validation Rules

### **OCR Extraction:**
- Confidence threshold: 90%+ (configurable)
- Manual review before saving
- User can edit extracted values
- Show extraction success message

### **Duplicate Detection:**
- Phone number duplicate
- Email duplicate
- Name + Age combination duplicate
- **Action:** Show warning, let user decide

### **Data Validation:**
- Email format validation
- Phone format: 10 digits (Indian standard)
- Age: 1-120 range
- Aadhaar: 12 digits (if provided)
- Required fields: Name, Phone, Email

---

## 🎨 UI/UX Structure - Web App

### **Responsive Design:**
- **Desktop:** Full sidebar, multi-column layout
- **Tablet:** Collapsible sidebar, responsive grid
- **Mobile:** Bottom navigation, single column

### **Main Navigation:**
1. **Dashboard** - Stats, recent customers, quick actions
2. **Add New Customer** - Form to create customer
3. **Customer Directory** - List view with status, sortable
4. **Customer Detail** - Full profile view/edit
5. **Bio-Data Generator** - Generate PDFs/HTML docs
6. **Settings** - OCR, Websites, Theme, Backup, Audit

### **Customer Detail Page Sections (Tabs/Accordion):**
- Customer Personal Profile
- Bank & Financial Details
- Address Details
- Education & Qualifications
- Document Vault
- Important Web Links
- Work Experience
- Other Data

---

## 🔐 Security & Privacy - Local PC Only

- ✅ **NO internet required** - Complete offline operation
- ✅ **All data on local PC** - No cloud, no server transmission
- ✅ **No encryption** (single-user, local storage only)
- ✅ **Aadhaar masked display** (XXXX-XXXX-1234)
- ✅ Audit logs track all changes locally
- ✅ JSON files stored in `data/` folder
- ✅ Backup/restore JSON format only
- ✅ No sensitive data in URLs
- ✅ Browser LocalStorage for UI preferences only
- ✅ All processing happens client-side (OCR in browser)

---

## 📦 Technology Stack - Local Web App

| Component | Technology |
|-----------|-----------|
| **Frontend** | Vue 3 + Vite |
| **State Management** | Pinia |
| **UI Components** | Vuetify 3 or PrimeVue |
| **Styling** | Tailwind CSS |
| **Backend** | Node.js + Express (lightweight local server) |
| **Data Storage** | JSON files (no database) |
| **PDF Generation** | html2pdf.js |
| **Excel Export** | xlsx library |
| **OCR Engine** | Tesseract.js (browser-based, offline) |
| **Image Crop** | vue-cropper |
| **Local Storage** | Browser LocalStorage + JSON files |
| **File System** | Node.js fs module (read/write JSON files) |

---

## 🚀 How to Run - Local PC

### **Setup (One-time):**
```bash
1. Download/unzip app folder
2. Navigate to folder in terminal
3. npm install
4. npm run dev
```

### **Daily Use:**
```bash
1. Open terminal in app folder
2. npm run dev
3. Browser opens at http://localhost:5173
4. Use app normally
5. Close terminal when done
```

### **No Installation Required:**
- Just a folder with files
- Can copy entire folder to USB
- Can move to another PC anytime
- All data travels with folder

---

## 📋 Acceptance Criteria

### **Phase 1 Complete When:**
- [ ] Web app runs in browser without installation
- [ ] All local data stored in JSON files
- [ ] All new personal data fields working
- [ ] Address management (multiple, primary) working
- [ ] Bank account management (multiple, primary) working
- [ ] OCR extraction for all document types working
- [ ] Document vault with custom types working
- [ ] Status dropdown in customer directory working
- [ ] Activity timeline with last 10 customers working
- [ ] Important websites tab in customer detail working
- [ ] Settings page with all new options working
- [ ] Bio-data PDF/HTML download working
- [ ] Photo upload with crop tool working
- [ ] Bulk import with warnings working
- [ ] CSV/Excel export functional
- [ ] Theme toggle works
- [ ] Audit logging captures all changes
- [ ] Backup/restore JSON working
- [ ] Search (Name/Phone/Email) working
- [ ] Works in Chrome, Firefox, Edge, Safari
- [ ] No internet required (works offline)
- [ ] All data stays on local PC
- [ ] Can copy folder to USB/another PC

---

## 🚀 Release Plan

| Phase | Timeline | Status |
|-------|----------|--------|
| Phase 1 (MVP v2.1) | Week 1-3 | Design → Build → Test |
| Phase 2 (Advanced) | Week 4-5 | Custom templates, advanced search, export templates |
| Phase 3 (Polish) | Week 6+ | UI refinement, performance, mobile optimization |
| Production Release | TBD | Local web app ready |

---

## ✅ Decision Log

All 21 original clarification questions + New v2.1 local web app enhancements documented in CLARIFICATION_INTERVIEW.md

