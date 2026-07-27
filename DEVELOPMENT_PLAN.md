# Customer Data Hub - Development Plan

**Version:** 1.0  
**Date:** July 27, 2026  
**Target Duration:** 2-3 weeks for MVP (Phase 1)  
**For:** AI Agent Development Guidance

---

## 🎯 Development Overview

This document provides a step-by-step implementation guide for building Customer Data Hub. Follow these tasks in sequence for optimal code organization and dependency management.

---

## 📋 PHASE 1: Foundation & Core Features (Week 1-2)

### **Sprint 1: Project Setup (Days 1-2)**

#### **Task 1.1: Initialize Electron + React Project**
- **Description:** Set up base Electron project with React frontend
- **Steps:**
  1. Create project folder structure (see ARCHITECTURE.md)
  2. Initialize package.json with dependencies:
     - electron
     - react, react-dom
     - express
     - webpack, webpack-cli
     - electron-builder
  3. Create webpack.config.js for bundling
  4. Set up scripts: dev, build, start, build:exe
- **Deliverable:** Working Electron window showing "App Ready"
- **Dependencies:** None
- **Testing:** Run `npm start` → Electron window launches

---

#### **Task 1.2: Folder Structure & File Organization**
- **Description:** Create all necessary folders and starter files
- **Files to Create:**
  ```
  src/main/index.js (Electron entry)
  src/main/preload.js (IPC bridge)
  src/main/menu.js (App menu)
  src/renderer/index.js (React entry)
  src/renderer/App.jsx
  src/backend/index.js (Express server)
  src/shared/constants.js
  data/ (empty - created at runtime)
  ```
- **Deliverable:** Full folder structure ready
- **Dependencies:** Task 1.1
- **Testing:** Verify all files exist, no import errors

---

#### **Task 1.3: Express Backend Server Setup**
- **Description:** Create Express server that runs within Electron
- **Implementation:**
  ```javascript
  // src/backend/index.js
  const express = require('express');
  const app = express();
  
  app.use(express.json());
  
  app.listen(3000, () => {
    console.log('Backend API running on port 3000');
  });
  ```
- **Deliverable:** Express server starts on port 3000 when app launches
- **Dependencies:** Task 1.2
- **Testing:** Check logs show "Backend API running on port 3000"

---

#### **Task 1.4: IPC Communication Bridge**
- **Description:** Set up secure IPC between main process and renderer
- **Files:**
  - `src/main/preload.js` - Expose safe IPC methods
  - `src/main/index.js` - Register IPC handlers
- **Implementation:**
  ```javascript
  // preload.js
  contextBridge.exposeInMainWorld('ipcRenderer', {
    invoke: (channel, ...args) => {
      const validChannels = ['test-channel'];
      if (validChannels.includes(channel)) {
        return ipcRenderer.invoke(channel, ...args);
      }
    }
  });
  
  // main/index.js
  ipcMain.handle('test-channel', async () => {
    return { message: 'IPC working' };
  });
  ```
- **Deliverable:** IPC communication tested and working
- **Dependencies:** Task 1.3
- **Testing:** React can call `window.ipcRenderer.invoke('test-channel')` and get response

---

### **Sprint 2: Data Layer (Days 3-4)**

#### **Task 2.1: CSV Service - Read/Write Operations**
- **Description:** Create service for reading and writing CSV files
- **File:** `src/backend/services/CSVService.js`
- **Functions:**
  ```javascript
  class CSVService {
    async readCustomers()        // Read customers.csv
    async writeCustomers(data)   // Write/update customers.csv
    async readEducation()        // Read education.csv
    async writeEducation(data)   // Write education.csv
    async appendCustomers(rows)  // Append new customers
    async getById(id)            // Get single customer by ID
  }
  ```
- **Dependencies:**
  - csv-parser (for reading)
  - Create data/ folder if not exists
- **Deliverable:** CSVService can read/write all CSV files
- **Testing:** 
  - Test reading non-existent file → creates empty CSV
  - Test writing data → file created with correct content
  - Test appending → new rows added without duplicating headers

---

#### **Task 2.2: Data Models**
- **Description:** Define data structures for validation
- **Files:**
  - `src/backend/models/Customer.js`
  - `src/backend/models/Education.js`
  - `src/backend/models/AuditLog.js`
- **Customer Model:**
  ```javascript
  {
    customer_id: string (unique),
    name: string (required),
    age: number (1-120),
    gender: string ('Male', 'Female', 'Other'),
    phone: string (10 digits, required),
    email: string (valid email, required),
    address: string,
    bank_name: string,
    account_number: string,
    ifsc: string,
    photo_path: string,
    notes: string,
    created_date: date,
    last_modified: date
  }
  ```
- **Deliverable:** Data models with validation rules
- **Testing:** Validation catches invalid data (bad email, age > 120, etc.)

---

#### **Task 2.3: Validation Utilities**
- **Description:** Create validators for common data checks
- **File:** `src/backend/utils/validators.js`
- **Functions:**
  ```javascript
  validateEmail(email)          // RFC 5322 basic check
  validatePhone(phone)          // Indian 10-digit format
  validateAge(age)              // 1-120 range
  validateRequired(value, field) // Check not null/empty
  ```
- **Deliverable:** Validators working for all data types
- **Testing:** Valid/invalid data passes/fails appropriately

---

### **Sprint 3: Customer CRUD API (Days 5-7)**

#### **Task 3.1: Customer Routes (CRUD)**
- **Description:** Create REST API endpoints for customer management
- **File:** `src/backend/routes/customers.js`
- **Endpoints:**
  ```
  POST   /api/customers              (Create)
  GET    /api/customers              (List all)
  GET    /api/customers/:id          (Get by ID)
  PUT    /api/customers/:id          (Update)
  DELETE /api/customers/:id          (Delete)
  GET    /api/customers/search?q=... (Search by name/phone/email)
  ```
- **Deliverable:** All CRUD endpoints working
- **Testing:** 
  - Create customer → stored in CSV
  - List customers → returns all
  - Get by ID → returns specific customer
  - Update → changes reflected in CSV
  - Delete → customer removed from CSV
  - Search → finds by name/phone/email

---

#### **Task 3.2: Customer Service (Business Logic)**
- **Description:** Handle validation, duplicate detection, ID generation
- **File:** `src/backend/services/CustomerService.js`
- **Functions:**
  ```javascript
  async createCustomer(data)        // Validate + check duplicates + save
  async updateCustomer(id, data)    // Validate + save
  async deleteCustomer(id)          // Delete and log
  async getAll()                    // Get all customers
  async getById(id)                 // Get specific customer
  async searchCustomers(query)      // Search by name/phone/email
  async checkDuplicates(data)       // Find duplicates (phone/email)
  generateCustomerId()              // Generate unique ID (CUST_001, etc.)
  ```
- **Deliverable:** Service methods handle all business logic
- **Testing:** Duplicates detected, validation works, IDs auto-generated

---

#### **Task 3.3: Education Routes & Service**
- **Description:** Create API for education records
- **File:** `src/backend/routes/education.js`
- **Endpoints:**
  ```
  POST   /api/education              (Add education)
  GET    /api/education/:customerId  (Get education for customer)
  PUT    /api/education/:id          (Update)
  DELETE /api/education/:id          (Delete)
  ```
- **Deliverable:** Education API working
- **Testing:** Can add/update/delete education records linked to customers

---

### **Sprint 4: Frontend UI - Customer Management (Days 8-9)**

#### **Task 4.1: React Component Structure**
- **Description:** Create main React components
- **Files:**
  ```
  src/renderer/components/CustomerList.jsx
  src/renderer/components/CustomerForm.jsx
  src/renderer/components/CustomerDetail.jsx
  src/renderer/components/SearchBar.jsx
  src/renderer/pages/CustomersPage.jsx
  src/renderer/pages/HomePage.jsx
  src/renderer/App.jsx (Main router)
  ```
- **Deliverable:** Component structure with basic props
- **Testing:** Components render without errors

---

#### **Task 4.2: Customer List View**
- **Description:** Display all customers in a table/list
- **Component:** `CustomerList.jsx`
- **Features:**
  - Fetch customers from API
  - Display in table: Name, Phone, Email, Created Date
  - Pagination (50 customers per page)
  - Click to view details
  - Delete button with confirmation
- **Deliverable:** List shows customers from database
- **Testing:** 
  - Add customer in CSV manually → appears in list
  - Delete via UI → removed from CSV
  - Pagination works

---

#### **Task 4.3: Customer Create/Edit Form**
- **Description:** Form for creating and editing customers
- **Component:** `CustomerForm.jsx`
- **Fields:**
  - Name, Age, Gender, Phone, Email
  - Address, Bank Name, Account Number, IFSC
  - Notes text area
- **Features:**
  - Validation before submit
  - Show error messages
  - Submit creates/updates customer
  - Cancel button
- **Deliverable:** Form works for creating and editing
- **Testing:**
  - Fill form → create customer → appears in list
  - Edit customer → changes saved to CSV
  - Validation catches bad email/phone

---

#### **Task 4.4: Customer Detail View**
- **Description:** Full view and edit of single customer
- **Component:** `CustomerDetail.jsx`
- **Features:**
  - Display all customer info
  - Edit button → shows form
  - Link to education records
  - Link to documents
  - Delete customer button
- **Deliverable:** Detail page shows all customer info
- **Testing:** Can view and edit customer from detail page

---

### **Sprint 5: Photo Upload & Crop Tool (Days 10-11)**

#### **Task 5.1: Photo Upload Component**
- **Description:** File input and preview
- **Component:** `PhotoUploader.jsx`
- **Features:**
  - File input (JPG, PNG only)
  - Show preview of selected image
  - Launch crop tool
- **Dependencies:**
  - react-easy-crop or similar
- **Deliverable:** Photo selection and preview working
- **Testing:** Select image → preview shows

---

#### **Task 5.2: Crop Tool Integration**
- **Description:** Embed crop tool in photo uploader
- **Features:**
  - Drag image to position
  - Resize handles to crop
  - Rotate button
  - Save cropped image
- **Deliverable:** Crop tool functional
- **Testing:** Crop and save → gets correct dimensions

---

#### **Task 5.3: Photo Save API**
- **Description:** Save cropped photo to file system
- **Endpoint:** `POST /api/customers/:id/photo`
- **Implementation:**
  1. Receive base64 or blob image
  2. Save to `data/photos/CUST_ID.jpg`
  3. Update customers.csv with photo_path
  4. Log audit entry
- **Deliverable:** Photo saved and linked to customer
- **Testing:** 
  - Upload photo → file created in data/photos/
  - Customer record has photo_path set
  - Audit log shows photo update

---

### **Sprint 6: Bio-Data PDF Generator (Days 12-13)**

#### **Task 6.1: Puppeteer Integration**
- **Description:** Set up Puppeteer for PDF generation
- **Installation:** `npm install puppeteer`
- **Test Script:**
  ```javascript
  const puppeteer = require('puppeteer');
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.setContent('<h1>Test</h1>');
  await page.pdf({ path: 'test.pdf' });
  ```
- **Deliverable:** Puppeteer installed and tested
- **Testing:** Can generate simple PDF

---

#### **Task 6.2: Bio-Data HTML Template**
- **Description:** Create default HTML template for bio-data
- **File:** `src/backend/templates/default-biodata.html`
- **Content:**
  ```html
  <html>
    <head>
      <style>
        /* Professional styling */
        body { font-family: Arial; padding: 20px; }
        .header { text-align: center; }
        .photo { width: 150px; height: 150px; }
        .section { margin: 20px 0; }
      </style>
    </head>
    <body>
      <div class="header">
        <h1>{{name}}</h1>
        <img class="photo" src="{{photo_path}}" />
      </div>
      <div class="section">
        <h2>Contact Information</h2>
        <p>Phone: {{phone}}</p>
        <p>Email: {{email}}</p>
        <p>Address: {{address}}</p>
      </div>
      <div class="section">
        <h2>Education</h2>
        {{education_html}}
      </div>
    </body>
  </html>
  ```
- **Deliverable:** Professional template ready
- **Testing:** Template renders correctly with sample data

---

#### **Task 6.3: Bio-Data Service**
- **Description:** Service to generate PDF from customer data
- **File:** `src/backend/services/BioDataService.js`
- **Functions:**
  ```javascript
  async generatePDF(customerId, templateId)   // Generate PDF
  async generateWord(customerId, templateId)  // Generate DOCX
  async mergeData(customer, template)         // Merge data with template
  ```
- **Deliverable:** PDF generation working
- **Testing:** Generate PDF → file created with correct data

---

#### **Task 6.4: Bio-Data Routes**
- **Description:** API endpoints for bio-data generation
- **File:** `src/backend/routes/biodata.js`
- **Endpoints:**
  ```
  POST /api/biodata/generate-pdf    (Generate PDF)
  POST /api/biodata/generate-word   (Generate Word)
  GET  /api/biodata/templates       (List templates)
  ```
- **Deliverable:** Routes call BioDataService
- **Testing:** Can generate PDF/Word for customer

---

#### **Task 6.5: Bio-Data Generator UI**
- **Description:** Frontend component to generate bio-data
- **Component:** `BioDataGenerator.jsx`
- **Features:**
  - Select customer from dropdown
  - Select format (PDF or Word)
  - Generate button
  - Shows "Saving..." during generation
  - Shows success message with file location
  - Save As dialog for user to choose location
- **Deliverable:** UI component working
- **Testing:** 
  - Click Generate → file created
  - User chooses save location
  - Success message shows

---

### **Sprint 7: Bulk Import (Days 14-15)**

#### **Task 7.1: Import Service**
- **Description:** Service to validate and import CSV file
- **File:** `src/backend/services/ImportService.js`
- **Functions:**
  ```javascript
  async validateImport(filePath)    // Parse + validate rows
  async detectDuplicates(rows)      // Find duplicates in existing data
  async importCustomers(rows, options) // Save valid rows
  ```
- **Implementation:**
  1. Parse CSV file
  2. Validate each row against data model
  3. Check for duplicates (phone/email)
  4. Return: { valid: 450, errors: 30, duplicates: 20 }
- **Deliverable:** Import validation working
- **Testing:** 
  - Valid data → accepted
  - Invalid data → errors listed
  - Duplicates → detected and shown

---

#### **Task 7.2: Import Routes**
- **Description:** API for importing CSV
- **File:** `src/backend/routes/import.js`
- **Endpoints:**
  ```
  POST /api/import/validate    (Validate file)
  POST /api/import/execute     (Execute import)
  ```
- **Request/Response:**
  ```
  POST /api/import/validate
  Body: { filePath: '/path/to/file.csv' }
  Response: {
    valid: 450,
    errors: 30,
    duplicates: 20,
    errorDetails: [...]
  }
  
  POST /api/import/execute
  Body: { 
    filePath: '...',
    action: 'import_all' or 'skip_duplicates'
  }
  Response: { success: true, imported: 450 }
  ```
- **Deliverable:** Routes handle import flow
- **Testing:** Validation → show dialog → execute import

---

#### **Task 7.3: Import UI Component**
- **Description:** Frontend for file selection and confirmation
- **Component:** `ImportExport.jsx`
- **Flow:**
  1. File input - user selects CSV
  2. Click "Validate" → shows dialog
  3. Dialog shows: Valid 450, Errors 30, Duplicates 20
  4. User clicks: "Import All" or "Skip Duplicates" or "Cancel"
  5. Shows success message
- **Deliverable:** Import UI complete
- **Testing:** 
  - Select file → validation runs
  - Dialog shows correct counts
  - Click import → customers added to list

---

### **Sprint 8: Export Functionality (Days 16-17)**

#### **Task 8.1: CSV/Excel Export Service**
- **Description:** Export customer data to CSV and Excel
- **File:** `src/backend/services/ExportService.js`
- **Functions:**
  ```javascript
  async exportCSV(filepath)    // Export all to CSV
  async exportExcel(filepath)  // Export all to XLSX with formatting
  ```
- **Dependencies:**
  - xlsx library for Excel
- **Deliverable:** Export service working
- **Testing:** 
  - Export CSV → valid CSV file created
  - Export Excel → valid XLSX file created
  - Data matches database

---

#### **Task 8.2: Export Routes**
- **Description:** API endpoints for export
- **File:** `src/backend/routes/export.js`
- **Endpoints:**
  ```
  POST /api/export/csv         (Export to CSV)
  POST /api/export/excel       (Export to Excel)
  ```
- **Deliverable:** Routes call export service
- **Testing:** Files created successfully

---

#### **Task 8.3: Export UI**
- **Description:** Buttons in ImportExport component
- **Features:**
  - "Export to CSV" button → Save As dialog → file saved
  - "Export to Excel" button → Save As dialog → file saved
  - Show success message with file location
- **Deliverable:** Export buttons working
- **Testing:** 
  - Click export → file created in chosen location
  - File opens correctly in Excel/text editor

---

### **Sprint 9: Audit Logging (Days 18-19)**

#### **Task 9.1: Audit Service**
- **Description:** Log all customer data changes
- **File:** `src/backend/services/AuditService.js`
- **Functions:**
  ```javascript
  async logChange(customerId, action, field, oldValue, newValue)
  async logAction(action, details)
  async getAuditLog(customerId)
  async exportAuditLog(filepath)
  ```
- **Storage:**
  - JSON format for app use
  - CSV format for export
- **Deliverable:** Audit service logging changes
- **Testing:** 
  - Create customer → audit log entry created
  - Update field → change logged with old/new values
  - Audit log shows in JSON and CSV

---

#### **Task 9.2: Integrate Audit Logging**
- **Description:** Add audit logging to all operations
- **Updates:**
  - CustomerService.js → call AuditService on all changes
  - BioDataService.js → log "bio-data generated"
  - ImportService.js → log "customers imported"
  - etc.
- **Deliverable:** All operations logged
- **Testing:** Check audit_logs.json → all changes recorded

---

#### **Task 9.3: Audit Log Viewer UI**
- **Description:** UI to view audit trail
- **Component:** Part of Settings page
- **Features:**
  - Show recent audit log entries (latest first)
  - Filter by customer or action
  - Export audit log to CSV
  - Search by date range
- **Deliverable:** Audit log viewer working
- **Testing:** 
  - Make change → appears in audit log
  - Filter works
  - Export generates CSV

---

### **Sprint 10: Settings & Theme (Days 20-21)**

#### **Task 10.1: Theme System**
- **Description:** Implement light/dark theme toggle
- **Files:**
  ```
  src/renderer/styles/light.css
  src/renderer/styles/dark.css
  src/renderer/utils/themeManager.js
  ```
- **Implementation:**
  - Store theme preference in metadata.json
  - Load theme on app start
  - Provide toggle function
  - Apply CSS class to body element
- **Deliverable:** Theme toggle working
- **Testing:** 
  - Toggle theme → colors change
  - Close app and reopen → theme persists

---

#### **Task 10.2: Settings Page**
- **Description:** Settings UI component
- **Component:** `Settings.jsx`
- **Features:**
  - Theme toggle (Light/Dark)
  - Backup button → Choose folder → backup created
  - Restore button → Choose backup folder → restore
  - Show app version
  - Show total customers count
  - Show last backup date
  - Audit log viewer section
- **Deliverable:** Settings page complete
- **Testing:** All settings functional

---

#### **Task 10.3: Backup & Restore Service**
- **Description:** Manual backup/restore functionality
- **File:** `src/backend/services/BackupService.js`
- **Functions:**
  ```javascript
  async createBackup(destinationPath)   // Copy all data to folder
  async restoreBackup(backupPath)       // Restore from backup
  ```
- **Backup folder structure:**
  ```
  backup_2026-07-27_143022/
  ├── customers.csv
  ├── education.csv
  ├── documents.csv
  ├── addresses.csv
  ├── metadata.json
  └── photos/ (if including photos)
  ```
- **Deliverable:** Backup/restore working
- **Testing:** 
  - Create backup → folder created with all files
  - Restore backup → data replaced correctly

---

### **Sprint 11: Build & Package (Day 22)**

#### **Task 11.1: Configure electron-builder**
- **Description:** Set up .exe builder configuration
- **File:** `electron-builder.json`
- **Configuration:**
  ```json
  {
    "appId": "com.customerdata.hub",
    "productName": "Customer Data Hub",
    "win": {
      "target": ["nsis"]
    },
    "nsis": {
      "oneClick": false,
      "allowToChangeInstallationDirectory": true
    }
  }
  ```
- **Deliverable:** Build config ready
- **Testing:** Config validates without errors

---

#### **Task 11.2: Create App Icon**
- **Description:** Professional app icon with custom branding
- **Files:**
  - `public/icon.png` (256x256)
  - `public/icon.ico` (Windows icon)
- **Branding:** Include organization name/initials
- **Deliverable:** Icons created and placed
- **Testing:** Icon displays correctly in installer and taskbar

---

#### **Task 11.3: Build .exe Installer**
- **Description:** Generate Windows .exe installer
- **Command:** `npm run build:exe`
- **Output:** `CustomerDataHub-1.0.0-Setup.exe` (~150-200 MB)
- **Installation Test:**
  1. Run .exe on clean Windows PC
  2. Complete installation
  3. Launch app from Start Menu
  4. Create test customer
  5. Generate bio-data
  6. All features work
- **Deliverable:** Working .exe installer
- **Testing:** Install on Windows → app works

---

#### **Task 11.4: Documentation & Handoff**
- **Description:** Create deployment documentation
- **Files to Create:**
  - `README.md` (Quick start)
  - `DEPLOYMENT.md` (How to run .exe)
  - `USER_MANUAL.md` (User guide)
- **Deliverable:** Documentation complete
- **Testing:** Follow README → can build and run app

---

---

## 📈 PHASE 2: Advanced Features (Week 3)

*(These can be added after Phase 1 MVP is complete)*

### **Task 12: Custom Template Builder**
- Drag-drop template editor
- Save custom templates
- Multiple template support

### **Task 13: Advanced Search**
- Filter by qualification, age, location
- Saved searches/filters

### **Task 14: Data Recovery UI**
- Restore from backup in UI
- Version history

---

## ✅ Quality Checklist

Before marking any task complete:

- [ ] Code follows project structure
- [ ] Error handling implemented
- [ ] Logging added
- [ ] Tested with sample data
- [ ] No console errors
- [ ] Follows existing code style
- [ ] Comments added for complex logic
- [ ] Dependencies installed and working

---

## 🐛 Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| Puppeteer takes long time to download | Pre-bundled binary or use Headless Chrome |
| CSV files getting corrupted | Use proper CSV library (csv-parser) |
| Photo path not found | Use absolute paths, not relative |
| IPC communication failing | Check preload.js exposes channel |
| Theme not persisting | Save to metadata.json, load on startup |

---

## 📊 Progress Tracking

| Sprint | Tasks | Status | Target Date |
|--------|-------|--------|-------------|
| 1 | 1.1-1.4 | Not Started | Day 2 |
| 2 | 2.1-2.3 | Not Started | Day 4 |
| 3 | 3.1-3.3 | Not Started | Day 7 |
| 4 | 4.1-4.4 | Not Started | Day 9 |
| 5 | 5.1-5.3 | Not Started | Day 11 |
| 6 | 6.1-6.5 | Not Started | Day 13 |
| 7 | 7.1-7.3 | Not Started | Day 15 |
| 8 | 8.1-8.3 | Not Started | Day 17 |
| 9 | 9.1-9.3 | Not Started | Day 19 |
| 10 | 10.1-10.3 | Not Started | Day 21 |
| 11 | 11.1-11.4 | Not Started | Day 22 |

---

## 🚀 Getting Started for AI Agent

1. Read this file completely
2. Read REQUIREMENTS.md for feature details
3. Read ARCHITECTURE.md for technical structure
4. Start with **Task 1.1** (Project Setup)
5. Complete tasks sequentially
6. Test after each task
7. Commit to GitHub after each sprint
8. Update progress tracking

---

## 📞 Reference Documents

- **REQUIREMENTS.md** - What to build (features, acceptance criteria)
- **ARCHITECTURE.md** - How to build (technical structure, data flow)
- **CLARIFICATION_INTERVIEW.md** - Why decisions were made (justification)

---

**Status:** Ready for AI Agent to begin development  
**Last Updated:** July 27, 2026  
**Next Review:** After Sprint 1 completion

