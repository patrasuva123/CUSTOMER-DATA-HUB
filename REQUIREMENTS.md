# Customer Data Hub - Product Requirements Document (PRD)

**Version:** 1.0  
**Date:** July 27, 2026  
**Status:** Ready for Development  
**Target Platform:** Windows Desktop (.exe)  

---

## 📋 Executive Summary

**Project:** Customer Data Hub - A Windows desktop application for managing customer information, education records, and generating professional bio-data documents.

**Target Users:** Individual business owners or small organizations (single user)

**Max Capacity:** Up to 5,000 customers

**Primary Goal:** Centralized customer management with automated bio-data PDF/Word generation and bulk import/export capabilities.

---

## 🎯 Core Features (MVP Phase 1)

### 1. **Customer Management** ✅
- **CRUD Operations:**
  - Create new customer record
  - Read/View customer details
  - Update customer information
  - Delete customer record
  - Search customers by: Name, Phone Number, Email

- **Customer Data Fields:**
  ```
  - Basic Info: ID, Name, Age, Gender, Phone, Email, Address
  - Education: Qualification, Institution, Year, Stream, Score
  - Documents: Upload & store PDFs/JPGs (certificates, admit cards)
  - Photos: Profile photo with crop tool
  - Bank Details: Bank Name, Account Number, IFSC (optional)
  - Additional Notes: Custom text field
  ```

### 2. **Photo Management** ✅
- Built-in photo crop tool
- Supported formats: JPG, PNG
- User can: drag, resize, rotate before saving
- Auto-save cropped photo to customer profile

### 3. **Education & Documents** ✅
- Upload education documents (optional with warning)
- Document types: PDF, JPG, PNG
- Suggested naming pattern (not enforced):
  - Example: `10th_Madhyamik_Admit_Card.pdf`
  - User can accept suggestion or use custom name
- Yellow warning badge if document missing for education record

### 4. **Bulk Import** ✅
- Import customers from CSV file
- **Duplicate Handling:** Show warning dialog
  - Display list of duplicates found
  - Let user choose: "Import anyway" or "Skip duplicates"
  - Don't silently skip
  
- **Error Handling:** Show error preview dialog
  - Display summary: "450 valid rows, 50 errors"
  - Show error details/examples
  - Let user choose: "Import valid rows" or "Cancel"
  - Support partial import (valid rows only)

### 5. **Bio-Data Generator (Basic)** ✅
- Generate PDF documents using Puppeteer
- Generate editable Word (.docx) documents
- Fully editable format (user can modify after generation)
- Fields included: Name, Photo, Education, Bank Details, Contact Info
- User chooses save location (Save As dialog)
- Supported export: PDF + Word

### 6. **Data Export** ✅
- **CSV Export:** All customer data to CSV file
- **Excel Export:** All customer data to XLSX with formatting
- User chooses save location
- Export includes all categories (customers, education, documents)

### 7. **System Settings** ✅
- **Audit Logging:** Track all changes
  - Detail level: HIGH (log every field change)
  - Format: "Customer CUST_001: First Name changed from 'Rajesh' to 'Rajesh Kumar' [timestamp]"
  - Storage: Both JSON (app use) + CSV (export/review)
  
- **Backup:** Manual backup only
  - Button: "Backup Now"
  - Creates backup of all CSV files to user-selected location
  - Timestamp included in backup folder name
  
- **Theme:** Light and Dark mode toggle
  - User can switch themes in Settings
  - Persistent (remembers user preference)

---

## 🎨 Phase 2 Features (Advanced)

### 8. **Bio-Data Template Customization** 🔄
- Fully custom template builder
- User can:
  - Drag-drop fields on canvas
  - Choose colors/fonts
  - Add organization logo
  - Set layout (1-page, multi-page)
  - Save custom templates for reuse
- Pre-built default template included

### 9. **Advanced Search** 🔄
- (Phase 1: Basic search on Name, Phone, Email only)
- Phase 2: Extended search with filters
  - Filter by qualification, age, location, etc.

### 10. **Data Recovery** 🔄
- Restore from backup files
- Version history (if applicable)

---

## 📊 Data Storage Structure

### Storage Format: CSV + JSON
**No database needed** (CSV-based for simplicity, max 5,000 records)

### File Structure:
```
AppData/
├── customers.csv (Main customer data)
├── education.csv (Education records)
├── documents.csv (Document tracking - file paths)
├── addresses.csv (Extended address info)
├── metadata.json (App settings, templates config)
├── audit_logs.json (High-detail change log - JSON)
├── audit_logs.csv (Export-friendly audit trail)
└── backups/
    ├── backup_2026-07-27_143022/
    │   ├── customers.csv
    │   ├── education.csv
    │   └── ...
```

### CSV Schema Details:

**customers.csv:**
```
customer_id, name, age, gender, phone, email, address, bank_name, account_number, ifsc, photo_path, notes, created_date, last_modified
```

**education.csv:**
```
customer_id, qualification, institution, year_completed, stream, score, document_path, created_date
```

**documents.csv:**
```
doc_id, customer_id, document_type, file_name, file_path, upload_date, created_date
```

**addresses.csv:**
```
customer_id, street_address, city, state, postal_code, country
```

**metadata.json:**
```json
{
  "app_version": "1.0.0",
  "last_backup": "2026-07-27T14:30:22Z",
  "theme": "dark",
  "custom_templates": [
    { "id": "template_1", "name": "Standard Bio-Data", "fields": [...] }
  ],
  "max_capacity": 5000
}
```

**audit_logs.json:**
```json
[
  {
    "timestamp": "2026-07-27T14:35:00Z",
    "customer_id": "CUST_001",
    "action": "field_updated",
    "field": "first_name",
    "old_value": "Rajesh",
    "new_value": "Rajesh Kumar",
    "user": "default_user"
  }
]
```

---

## 🔍 Search Functionality

### Search Scope: Phase 1 (BASIC)
- **Fields:** Name, Phone Number, Email ONLY
- **Type:** Simple text match (fast)
- **Case-insensitive**
- **Partial match supported**

### Search Scope: Phase 2+ (ADVANCED)
- Extended to: Address, Bank Name, Qualification, etc.
- Filter combinations
- Advanced query syntax

---

## ⚠️ Validation Rules

### Duplicate Detection:
- Phone number duplicate
- Email duplicate
- Name + Age combination duplicate
- **Action:** Show warning, let user decide

### Data Validation:
- Email format validation (RFC 5322 basic check)
- Phone format: 10 digits (Indian standard)
- Age: 1-120 range
- Required fields: Name, Phone, Email

### File Uploads:
- Photo: JPG, PNG (max 5 MB)
- Documents: PDF, JPG, PNG (max 10 MB each)
- No file size limit for entire record

---

## 🎨 UI/UX Requirements

### Main Sections:
1. **Dashboard/Home** - Quick stats, recent customers, actions
2. **Customers List** - Table view with sorting, pagination
3. **Customer Detail** - Full profile view/edit form
4. **Bio-Data Generator** - Generate PDF/Word
5. **Import/Export** - Bulk operations
6. **Settings** - Theme, backup, audit logs
7. **Search** - Global search bar

### Navigation:
- Main menu bar (File, Edit, View, Tools, Help)
- Left sidebar with main sections
- Consistent back/cancel buttons

### Dialogs/Modals:
- Import confirmation with duplicates/errors
- Save As dialogs
- Confirmation dialogs for delete
- Warning badges (yellow) for missing education documents

---

## 🔐 Security & Privacy

- **No encryption required** (single-user, local storage)
- **No authentication** (single-user desktop app)
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
| **UI Framework** | Material-UI or Ant Design |
| **File Operations** | Node.js fs module |
| **Image Crop** | React-easy-crop or similar |

---

## 📋 Acceptance Criteria

### Phase 1 Complete When:
- [ ] Customer CRUD fully functional
- [ ] Photo upload with crop tool working
- [ ] Bulk import with warnings working
- [ ] Bio-Data PDF generation (basic template)
- [ ] CSV/Excel export functional
- [ ] Settings > Theme toggle works
- [ ] Audit logging captures all changes
- [ ] Manual backup functional
- [ ] .exe installer created and tested
- [ ] Search (Name/Phone/Email) fast and accurate

### Phase 2 Complete When:
- [ ] Custom template builder with drag-drop
- [ ] Pre-built template designs included
- [ ] Advanced search with filters
- [ ] Data recovery from backups

---

## 📱 Minimum System Requirements

- **OS:** Windows 10 or later
- **RAM:** 2 GB minimum
- **Disk:** 500 MB for app + data
- **.NET Framework:** Not required (Electron bundles dependencies)

---

## 🚀 Release Plan

| Phase | Timeline | Status |
|-------|----------|--------|
| Phase 1 (MVP) | Week 1-2 | Design → Build → Test |
| Phase 2 (Advanced) | Week 3-4 | Custom templates |
| Phase 3 (Polish) | Week 5+ | UI refinement, performance |
| Production Release | TBD | .exe installer ready |

---

## 📞 Support & Maintenance

- Version: 1.0.0
- Built by: AI Agent (Copilot)
- Maintained by: Copilot Team
- Updates: Manual (user downloads new .exe)

---

## ✅ Decision Log (From Clarification Interview)

All 21 clarification questions answered and documented in `CLARIFICATION_INTERVIEW.md`. Reference for any ambiguities during development.

