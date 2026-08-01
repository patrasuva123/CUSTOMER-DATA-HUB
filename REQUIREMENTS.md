# Customer Data Hub - Product Requirements Document (PRD) - v2.0

**Version:** 2.0 (Updated with Enhanced Features)  
**Date:** July 28, 2026  
**Status:** Ready for Development  
**Target Platform:** Windows Desktop (.exe)  

---

## 📋 Executive Summary

**Project:** Customer Data Hub - Advanced customer management with comprehensive personal data, OCR-based document extraction, and professional bio-data generation.

**Target Users:** Individual business owners or small organizations (single user)

**Max Capacity:** Up to 5,000 customers

**Key Enhancement (v2.0):** Advanced personal data fields, OCR-powered document extraction, customizable document vault, improved UI with status tracking and activity timeline.

---

## 🎯 Core Features (MVP Phase 1 - v2.0)

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
  - ❌ No encryption (local storage only, no sensitive data transmission)

---

### 5. **Photo Management** ✅

- Built-in photo crop tool
- Supported formats: JPG, PNG
- User can: drag, resize, rotate before saving
- Auto-save cropped photo to customer profile

---

### 6. **Bio-Data Generator** ✅

- Generate PDF documents using Puppeteer
- Generate editable Word (.docx) documents
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
- User chooses save location (Save As dialog)
- Supported export: PDF + Word

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
- Open in default browser

#### **In Settings:**
- Manage websites:
  - Add new website (Name + URL)
  - Edit existing website
  - Delete website
  - Changes apply globally to all customers

---

### 8. **Customer Status Tracking** ✅

- **Status Column in Customer Directory:**
  - Options: Active, Inactive, Not Interested
  - Dropdown selector
  - Sortable/Filterable
  - Stored in customers.csv
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
- User chooses save location
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
- Changes apply globally

#### **Bio-Data Customization:**
- Select which sections to include in generated bio-data
- Choose default template (if multiple templates)

#### **Theme:**
- Light and Dark mode toggle
- Persistent (remembers user preference)

#### **Backup & Restore:**
- Manual backup only
- Button: "Backup Now"
- Creates backup of all CSV files to user-selected location
- Timestamp included in backup folder name
- Restore from backup

#### **Audit Logging:**
- View audit trail
- Filter by customer or action
- Export audit log to CSV
- High detail level (every field change logged)

#### **Timeline Configuration:**
- Set number of recent customers to display (5, 10, 15, 20)

---

## 📊 Data Storage Structure

### **Enhanced CSV Schema:**

**customers.csv:**
```
customer_id, name, father_name, mother_name, dob, gender, age, primary_language, religion, marital_status, spouse_name, phone, email, aadhaar_no, voter_id, ration_card_no, pan_number, caste, caste_cert_no, caste_cert_date, blood_group, photo_path, status, notes, created_date, last_modified
```

**addresses.csv:**
```
customer_id, address_id, address_type, street_address, state, block, gram_station, post_office, village, pin_code, is_primary, created_date
```

**bank_accounts.csv:**
```
customer_id, account_id, bank_name, branch, account_number, ifsc_code, account_type, is_primary, created_date
```

**education.csv:**
```
customer_id, education_id, level, course_name, institution, year_completed, board_university, admit_number, registration_number, total_marks, obtained_marks, percentage, grade, document_path, created_date
```

**documents.csv:**
```
doc_id, customer_id, document_type, file_name, file_path, upload_date, ocr_extracted_data, created_date
```

**important_websites.json:**
```json
[
  { "id": "web_001", "name": "Aadhaar", "url": "https://myaadhaar.uidai.gov.in/", "created_date": "2026-01-01" },
  { "id": "web_002", "name": "CSC", "url": "https://digitalseva.csc.gov.in/", "created_date": "2026-01-01" }
]
```

**audit_logs.json & audit_logs.csv:**
- High-detail change tracking with timestamps

**metadata.json:**
- App settings including:
  - theme (light/dark)
  - ocr_enabled (true/false)
  - ocr_confidence_threshold (90)
  - timeline_recent_count (10)
  - biodata_included_sections (array)
  - last_backup timestamp

---

## 🔍 Search Functionality

### **Search Scope: Phase 1**
- **Fields:** Name, Phone Number, Email ONLY
- **Type:** Simple text match (fast)
- **Case-insensitive**
- **Partial match supported**

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

## 🎨 UI/UX Structure

### **Main Navigation:**
1. **Dashboard** - Stats, recent customers, quick actions
2. **Add New Customer** - Form to create customer
3. **Customer Directory** - List view with status, sortable
4. **Customer Detail** - Full profile view/edit
5. **Bio-Data Generator** - Generate PDFs/Word docs
6. **Important Web Links** - Tab in Customer Detail
7. **Activity Timeline** - Sidebar showing recent activity
8. **System Settings** - OCR, Websites, Theme, Backup, Audit

### **Customer Detail Page Sections:**
- Customer Personal Profile (collapsible)
- Bank & Financial Details (collapsible)
- Address Details (collapsible, multiple)
- Education & Qualifications (collapsible, multiple)
- Document Vault (collapsible)
- Important Web Links (new tab)
- Work Experience (collapsible)
- Other Data (collapsible)

---

## 🔐 Security & Privacy

- **No encryption** (single-user, local storage)
- **No authentication** (single-user desktop app)
- **Aadhaar masked display** (XXXX-XXXX-1234)
- Audit logs track all changes for accountability
- Backup files for data recovery
- Local storage only (no cloud/internet)

---

## 📦 Technology Stack

| Component | Technology |
|-----------|-----------|
| **Framework** | Electron (Windows .exe) |
| **Backend** | Node.js + Express |
| **Frontend** | React or Vue.js |
| **Storage** | CSV files + JSON |
| **PDF Generation** | Puppeteer |
| **Excel Export** | xlsx library |
| **OCR Engine** | Tesseract.js (free, offline) |
| **UI Framework** | Material-UI or Ant Design |
| **File Operations** | Node.js fs module |
| **Image Crop** | React-easy-crop or similar |

---

## 📋 Acceptance Criteria

### **Phase 1 Complete When:**
- [ ] All new personal data fields working
- [ ] Address management (multiple, primary) working
- [ ] Bank account management (multiple, primary) working
- [ ] OCR extraction for all document types working
- [ ] Document vault with custom types working
- [ ] Status dropdown in customer directory working
- [ ] Activity timeline with last 10 customers working
- [ ] Important websites tab in customer detail working
- [ ] Settings page with all new options working
- [ ] Bio-data customizable sections working
- [ ] Photo upload with crop tool working
- [ ] Bulk import with warnings working
- [ ] CSV/Excel export functional
- [ ] Theme toggle works
- [ ] Audit logging captures all changes
- [ ] Manual backup functional
- [ ] .exe installer created and tested
- [ ] Search (Name/Phone/Email) working

---

## 🚀 Release Plan

| Phase | Timeline | Status |
|-------|----------|--------|
| Phase 1 (MVP v2.0) | Week 1-3 | Design → Build → Test |
| Phase 2 (Advanced) | Week 4-5 | Custom templates, advanced search |
| Phase 3 (Polish) | Week 6+ | UI refinement, performance |
| Production Release | TBD | .exe installer ready |

---

## ✅ Decision Log

All 21 original clarification questions + New v2.0 enhancements documented in CLARIFICATION_INTERVIEW.md

