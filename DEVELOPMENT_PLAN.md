# Customer Data Hub - Development Plan - v2.1

**Version:** 2.1 (Local Web App - Vue.js + Express + JSON)  
**Date:** July 28, 2026  
**Target Duration:** 3-4 weeks for MVP (Phase 1)  
**Platform:** Browser-based web app (runs locally on PC, no internet required)  
**For:** AI Agent Development Guidance

---

## 🎯 Development Overview - v2.1

This document provides a step-by-step implementation guide for building Customer Data Hub v2.1 as a local web application. Follow these tasks in sequence for optimal code organization and dependency management.

---

## 📋 PHASE 1: Foundation & Enhanced Core Features (Week 1-3)

### **Sprint 1: Project Setup (Days 1-2)**

#### **Task 1.1: Initialize Vue 3 + Vite Project**
- **Description:** Set up Vue 3 web app with local Express backend
- **Steps:**
  1. Create project folder `customer-data-hub`
  2. Create `package.json` with dependencies:
     - vue@3, vite, @vitejs/plugin-vue
     - express, cors, multer
     - pinia, vuetify@3, tailwindcss
     - tesseract.js, html2pdf.js, xlsx, vue-cropper
  3. Create `vite.config.js` configuration
  4. Create `server.js` - lightweight Express server (port 5000)
  5. Set up npm scripts: `dev`, `build`, `preview`, `server`
- **Deliverable:** Working Vue app in browser at `http://localhost:5173`
- **Testing:** 
  - Run `npm run dev` → Vite dev server starts
  - Run `npm run server` in another terminal → Express starts on port 5000
  - Browser shows "App Ready" message

---

#### **Task 1.2: Folder Structure & File Organization - v2.1**
- **Description:** Create all necessary folders for local web app
- **Create Folders:**
  ```
  src/
  ├── stores/ (8 Pinia stores)
  ├── components/ (15+ Vue components)
  ├── pages/ (5 page components)
  ├── services/ (14 service files)
  ├── utils/
  └── styles/
  
  data/ (Created at runtime)
  uploads/ (Created at runtime)
  dist/ (Built app)
  ```
- **Deliverable:** Full folder structure ready
- **Testing:** Verify all folders exist, no import errors

---

#### **Task 1.3: Express Backend Server Setup**
- **Description:** Create lightweight local Express server for JSON file I/O
- **File:** `server.js`
- **Implementation:**
  ```javascript
  const express = require('express');
  const cors = require('cors');
  const path = require('path');
  const fs = require('fs');
  
  const app = express();
  app.use(cors());
  app.use(express.json());
  app.use(express.static('uploads'));
  
  const dataDir = path.join(__dirname, 'data');
  
  // Ensure data directory exists
  if (!fs.existsSync(dataDir)) {
    fs.mkdirSync(dataDir, { recursive: true });
  }
  
  // Example route
  app.get('/api/customers', (req, res) => {
    const filePath = path.join(dataDir, 'customers.json');
    if (fs.existsSync(filePath)) {
      const data = JSON.parse(fs.readFileSync(filePath, 'utf8'));
      res.json(data.customers || []);
    } else {
      res.json([]);
    }
  });
  
  app.listen(5000, () => {
    console.log('Local Express server running on port 5000');
  });
  ```
- **Deliverable:** Express server starts and serves data
- **Testing:** 
  - `npm run server` → Server starts on port 5000
  - Open browser console, check no CORS errors

---

#### **Task 1.4: Pinia State Management Setup**
- **Description:** Set up centralized state management
- **File:** `src/stores/customerStore.js` (main store example)
- **Setup Pinia:**
  ```javascript
  // src/main.js
  import { createPinia } from 'pinia'
  import App from './App.vue'
  import { createApp } from 'vue'
  
  const app = createApp(App)
  app.use(createPinia())
  app.mount('#app')
  ```
- **Create stores:**
  - customerStore.js (customers state)
  - addressStore.js (addresses state)
  - bankStore.js (bank accounts state)
  - documentStore.js (documents state)
  - settingsStore.js (app settings state)
  - timelineStore.js (activity timeline state)
  - auditStore.js (audit logs state)
  - educationStore.js (education records state)
- **Each store includes:**
  - state: data structure
  - getters: computed properties
  - actions: async operations
- **Deliverable:** All 8 Pinia stores created and working
- **Testing:** Store can dispatch actions and update state

---

### **Sprint 2: Data Layer & JSON File Management (Days 3-4)**

#### **Task 2.1: File Service for JSON Operations**
- **Description:** Service to read/write JSON files from Express backend
- **File:** `src/services/fileService.js`
- **Functions:**
  ```javascript
  async readCustomersJSON()
  async writeCustomersJSON(data)
  async readSettingsJSON()
  async writeSettingsJSON(data)
  async readWebsitesJSON()
  async writeWebsitesJSON(data)
  async readTimelineJSON()
  async writeTimelineJSON(data)
  async readAuditLogsJSON()
  async writeAuditLogsJSON(data)
  async backupAllData()           // Create backup.json
  async restoreFromBackup(data)   // Restore from backup
  ```
- **Deliverable:** File operations working
- **Testing:** Can read/write JSON files successfully

---

#### **Task 2.2: API Service for Express Communication**
- **Description:** Centralized API communication from Vue to Express
- **File:** `src/services/api.js`
- **Implementation:**
  ```javascript
  const API_URL = 'http://localhost:5000/api'
  
  export async function get(endpoint) {
    const response = await fetch(`${API_URL}${endpoint}`);
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }
  
  export async function post(endpoint, data) {
    const response = await fetch(`${API_URL}${endpoint}`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(data)
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }
  
  export async function put(endpoint, data) {
    const response = await fetch(`${API_URL}${endpoint}`, {
      method: 'PUT',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(data)
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }
  
  export async function delete_(endpoint) {
    const response = await fetch(`${API_URL}${endpoint}`, {
      method: 'DELETE'
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }
  ```
- **Deliverable:** API service working
- **Testing:** Can make GET/POST/PUT/DELETE requests to Express

---

#### **Task 2.3: Validators & Constants**
- **Description:** Data validation and app constants
- **Files:** 
  - `src/utils/validators.js` (validation functions)
  - `src/utils/constants.js` (app constants)
- **Validators:**
  ```javascript
  validateAadhaar(value)     // 12 digits
  validatePAN(value)         // PAN format
  validateIFSC(value)        // IFSC format
  validateEmail(email)       // Email format
  validatePhone(phone)       // 10 digits
  validateAge(age)           // 1-120
  validateLanguage(lang)     // Enum
  validateAddressType(type)  // Predefined types
  validateCasteNumber(num)   // Optional format
  ```
- **Constants:**
  ```javascript
  export const LANGUAGES = ['English', 'Hindi', 'Bengali', ...]
  export const RELIGIONS = ['Hindu', 'Muslim', 'Christian', ...]
  export const MARITAL_STATUSES = ['Single', 'Married', ...]
  export const CASTES = ['General', 'OBC', 'SC', 'ST', 'Other']
  export const BLOOD_GROUPS = ['A+', 'A-', 'B+', ...]
  export const ADDRESS_TYPES = ['Residential', 'Permanent', 'Office']
  export const DOCUMENT_TYPES = ['Aadhaar', 'Voter', 'PAN', ...]
  export const STATUSES = ['Active', 'Inactive', 'Not Interested']
  ```
- **Deliverable:** All validators and constants ready
- **Testing:** Validation catches invalid data

---

### **Sprint 3: Express Routes - Customer CRUD (Days 5-6)**

#### **Task 3.1: Customer Routes**
- **Description:** Express routes for customer CRUD operations
- **File:** `server.js` (or separate `routes/customers.js`)
- **Routes:**
  ```javascript
  // GET all customers
  app.get('/api/customers', (req, res) => {
    const data = readJSON('customers.json');
    res.json(data.customers || []);
  });
  
  // GET single customer with nested data
  app.get('/api/customers/:id', (req, res) => {
    const data = readJSON('customers.json');
    const customer = data.customers.find(c => c.id === req.params.id);
    res.json(customer || {});
  });
  
  // POST new customer
  app.post('/api/customers', (req, res) => {
    const data = readJSON('customers.json');
    const newCustomer = {
      id: `CUST_${Date.now()}`,
      ...req.body,
      created_date: new Date().toISOString(),
      last_modified: new Date().toISOString()
    };
    data.customers.push(newCustomer);
    writeJSON('customers.json', data);
    addAuditLog('customer_created', newCustomer.id);
    addActivity(newCustomer.id, newCustomer.name, 'customer_added');
    res.json(newCustomer);
  });
  
  // PUT update customer
  app.put('/api/customers/:id', (req, res) => {
    const data = readJSON('customers.json');
    const index = data.customers.findIndex(c => c.id === req.params.id);
    if (index === -1) return res.status(404).json({ error: 'Not found' });
    data.customers[index] = { ...data.customers[index], ...req.body, last_modified: new Date().toISOString() };
    writeJSON('customers.json', data);
    addAuditLog('customer_updated', req.params.id);
    res.json(data.customers[index]);
  });
  
  // PUT update status
  app.put('/api/customers/:id/status', (req, res) => {
    const data = readJSON('customers.json');
    const customer = data.customers.find(c => c.id === req.params.id);
    if (!customer) return res.status(404).json({ error: 'Not found' });
    customer.status = req.body.status;
    customer.last_modified = new Date().toISOString();
    writeJSON('customers.json', data);
    addAuditLog('status_changed', req.params.id, { status: req.body.status });
    addActivity(req.params.id, customer.name, 'status_changed');
    res.json(customer);
  });
  
  // DELETE customer
  app.delete('/api/customers/:id', (req, res) => {
    const data = readJSON('customers.json');
    const index = data.customers.findIndex(c => c.id === req.params.id);
    if (index === -1) return res.status(404).json({ error: 'Not found' });
    const deleted = data.customers.splice(index, 1);
    writeJSON('customers.json', data);
    addAuditLog('customer_deleted', req.params.id);
    addActivity(req.params.id, deleted[0].name, 'customer_deleted');
    res.json({ success: true });
  });
  
  // Search customers
  app.get('/api/customers/search', (req, res) => {
    const query = req.query.q.toLowerCase();
    const data = readJSON('customers.json');
    const results = data.customers.filter(c =>
      c.name.toLowerCase().includes(query) ||
      c.phone.includes(query) ||
      c.email.toLowerCase().includes(query)
    );
    res.json(results);
  });
  ```
- **Deliverable:** All customer routes working
- **Testing:** Create, read, update, delete customers via API

---

#### **Task 3.2: Address Routes**
- **Description:** Routes for address CRUD
- **File:** `server.js` (add address routes)
- **Routes:**
  ```
  POST   /api/addresses
  GET    /api/addresses/:customerId
  PUT    /api/addresses/:id
  DELETE /api/addresses/:id
  PUT    /api/addresses/:id/primary
  ```
- **Deliverable:** Address routes working
- **Testing:** Can add, edit, delete addresses for customer

---

#### **Task 3.3: Bank Account Routes**
- **Description:** Routes for bank account CRUD
- **Routes:**
  ```
  POST   /api/bank-accounts
  GET    /api/bank-accounts/:customerId
  PUT    /api/bank-accounts/:id
  DELETE /api/bank-accounts/:id
  PUT    /api/bank-accounts/:id/primary
  ```
- **Deliverable:** Bank account routes working
- **Testing:** Can manage multiple bank accounts

---

### **Sprint 4: OCR Engine Integration (Days 7-9)** ⭐ NEW

#### **Task 4.1: Tesseract.js Integration in Browser**
- **Description:** Set up OCR engine for client-side text extraction
- **Installation:** `npm install tesseract.js`
- **Test Script (in Vue component or console):**
  ```javascript
  import Tesseract from 'tesseract.js';
  
  async function testOCR() {
    const { data: { text } } = await Tesseract.recognize(
      imageElement,  // or image path
      'eng'
    );
    console.log('Extracted text:', text);
  }
  ```
- **Deliverable:** Tesseract.js working in browser
- **Testing:** Upload sample image, extract text successfully

---

#### **Task 4.2: OCR Service - Document Type Extraction**
- **Description:** Service to extract data based on document type
- **File:** `src/services/ocrService.js`
- **Functions:**
  ```javascript
  async extractAadhaar(imagePath)        // Extract: no, name, dob, address
  async extractPAN(imagePath)            // Extract: pan_no
  async extractCaste(imagePath)          // Extract: cert_no, date_of_issue
  async extractPassbook(imagePath)       // Extract: account_no, ifsc, bank_name
  async extractVoterID(imagePath)        // Extract: voter_id
  async extractRationCard(imagePath)     // Extract: ration_card_no
  async extractEducationCert(imagePath)  // Extract: cert_no, board, score
  
  async processDocumentOCR(imagePath, documentType)
    // Returns: { extractedData, confidence, message }
  ```
- **Implementation:**
  ```javascript
  import Tesseract from 'tesseract.js';
  
  export async function processDocumentOCR(imagePath, documentType) {
    const worker = await Tesseract.createWorker('eng');
    
    try {
      const result = await worker.recognize(imagePath);
      const text = result.data.text;
      const confidence = result.data.confidence;
      
      let extractedData = {};
      
      if (documentType === 'Aadhaar') {
        extractedData = {
          aadhaar_no: extractAadhaarNumber(text),
          name: extractName(text),
          dob: extractDateOfBirth(text),
          address: extractAddress(text)
        };
      } else if (documentType === 'PAN') {
        extractedData = {
          pan_no: extractPANNumber(text)
        };
      }
      // ... handle other document types
      
      await worker.terminate();
      
      return {
        extractedData,
        confidence,
        message: `Successfully extracted: Aadhaar No (${extractedData.aadhaar_no}), Name (${extractedData.name}), DOB (${extractedData.dob})`
      };
    } catch (error) {
      await worker.terminate();
      throw error;
    }
  }
  
  function extractAadhaarNumber(text) {
    const match = text.match(/\d{4}\s\d{4}\s\d{4}/);
    return match ? match[0] : '';
  }
  ```
- **Deliverable:** OCR extraction working for all document types
- **Testing:** Test each document type with sample images

---

#### **Task 4.3: OCR Routes in Express**
- **Description:** API endpoints for OCR processing
- **Routes:**
  ```
  POST /api/ocr/process       (Process document OCR)
  GET  /api/ocr/settings      (Get OCR settings)
  ```
- **Deliverable:** OCR routes working
- **Testing:** Upload document and extract data via API

---

### **Sprint 5: Document Vault with OCR (Days 10-11)**

#### **Task 5.1: Document Upload Route**
- **Description:** Express route to handle file uploads
- **Route:**
  ```javascript
  app.post('/api/documents/upload', upload.single('file'), (req, res) => {
    const customerId = req.body.customerId;
    const documentType = req.body.documentType;
    const filePath = req.file.path;
    
    // Save document record to customers.json
    const data = readJSON('customers.json');
    const customer = data.customers.find(c => c.id === customerId);
    
    const document = {
      id: `DOC_${Date.now()}`,
      type: documentType,
      file_name: req.file.filename,
      file_path: filePath,
      upload_date: new Date().toISOString()
    };
    
    if (!customer.documents) customer.documents = [];
    customer.documents.push(document);
    writeJSON('customers.json', data);
    
    addAuditLog('document_uploaded', customerId, { document_type: documentType });
    addActivity(customerId, customer.name, 'document_uploaded');
    
    res.json(document);
  });
  ```
- **Deliverable:** Document upload working
- **Testing:** Upload document, file saved to uploads/documents/

---

#### **Task 5.2: OCR Processing Route**
- **Description:** Route to process OCR on uploaded document
- **Route:**
  ```javascript
  app.post('/api/documents/:id/ocr', async (req, res) => {
    const documentId = req.params.id;
    const documentType = req.body.documentType;
    
    try {
      const ocrResult = await ocrService.processDocumentOCR(filePath, documentType);
      
      if (ocrResult.confidence < 90) {
        return res.json({
          ...ocrResult,
          warning: 'Low confidence, please review extracted data'
        });
      }
      
      // Save OCR data to document record
      const data = readJSON('customers.json');
      const customer = data.customers.find(c => 
        c.documents && c.documents.find(d => d.id === documentId)
      );
      const document = customer.documents.find(d => d.id === documentId);
      document.ocr_extracted = ocrResult.extractedData;
      document.ocr_confidence = ocrResult.confidence;
      writeJSON('customers.json', data);
      
      res.json(ocrResult);
    } catch (error) {
      res.status(500).json({ error: error.message });
    }
  });
  ```
- **Deliverable:** OCR processing route working
- **Testing:** Process OCR on uploaded document

---

#### **Task 5.3: Document Vault Vue Component**
- **Description:** Frontend for document management with OCR
- **Component:** `src/components/DocumentVault.vue`
- **Features:**
  - Document type selector (predefined + custom)
  - File upload input
  - Show uploaded documents list with thumbnails
  - OCR extraction display when document processed
  - Editable extracted data form
  - Delete document button
  - Show confidence score with extraction
  - Auto-populate customer fields from OCR extraction
- **Deliverable:** Document vault UI functional
- **Testing:** Upload document, see OCR extraction, edit, save

---

### **Sprint 6: Important Websites Management (Days 12-13)**

#### **Task 6.1: Website Routes**
- **Description:** Express routes for website management
- **Routes:**
  ```javascript
  app.get('/api/websites', (req, res) => {
    const data = readJSON('important_websites.json');
    res.json(data || []);
  });
  
  app.post('/api/websites', (req, res) => {
    const data = readJSON('important_websites.json');
    const website = {
      id: `web_${Date.now()}`,
      ...req.body,
      created_date: new Date().toISOString()
    };
    data.push(website);
    writeJSON('important_websites.json', data);
    addAuditLog('website_added', null, { website: req.body.name });
    res.json(website);
  });
  
  app.put('/api/websites/:id', (req, res) => {
    const data = readJSON('important_websites.json');
    const index = data.findIndex(w => w.id === req.params.id);
    data[index] = { ...data[index], ...req.body };
    writeJSON('important_websites.json', data);
    res.json(data[index]);
  });
  
  app.delete('/api/websites/:id', (req, res) => {
    const data = readJSON('important_websites.json');
    const index = data.findIndex(w => w.id === req.params.id);
    data.splice(index, 1);
    writeJSON('important_websites.json', data);
    res.json({ success: true });
  });
  ```
- **Deliverable:** Website routes working
- **Testing:** CRUD operations on websites

---

#### **Task 6.2: Website Manager Vue Component**
- **Description:** Settings page component to manage websites
- **Component:** `src/components/WebsiteManager.vue`
- **Features:**
  - List of all websites with edit/delete buttons
  - Add new website form (Name + URL)
  - Edit website modal
  - Delete confirmation
  - Load default websites if not set
- **Deliverable:** Website manager UI functional
- **Testing:** Add, edit, delete websites from settings

---

#### **Task 6.3: Important Web Links Tab**
- **Description:** Display websites in customer detail page
- **Component:** Tab in `CustomerDetailPage.vue`
- **Features:**
  - Display list of websites from settings
  - Clickable links that open in new tab
  - Show website name and URL
- **Deliverable:** Website links tab working
- **Testing:** Click link → opens in browser tab

---

### **Sprint 7: Frontend - Enhanced Customer Profile (Days 14-15)**

#### **Task 7.1: Customer Personal Profile Component**
- **Description:** Form for personal details with new v2.1 fields
- **Component:** `src/components/CustomerPersonalProfile.vue`
- **Form Sections:**
  ```
  Basic Info:
  - Full Name, Father's Name, Mother's Name, DOB, Gender, Age
  
  Language & Religion:
  - Primary Language (Dropdown)
  - Religion (Dropdown)
  
  Marital Info:
  - Marital Status (Dropdown)
  - Spouse Name (Optional)
  
  Contact:
  - Mobile Number, Email
  
  Identity Documents:
  - Aadhaar No (12 digits, masked, optional)
  - Voter ID, Ration Card No, PAN Number (all optional)
  
  Caste Information:
  - Caste Dropdown with conditional fields
  
  Blood Group (Optional)
  ```
- **Deliverable:** Personal profile form complete
- **Testing:** Fill form, validate all fields, save successfully

---

#### **Task 7.2: Address Manager Component**
- **Description:** UI to manage multiple addresses per customer
- **Component:** `src/components/AddressManager.vue`
- **Features:**
  - List of existing addresses in table
  - Add new address button → opens modal
  - Modal fields: Type, Street, State, Block, Gram Station, Post Office, Village, Pin Code
  - Mark as Primary checkbox
  - Edit button for each address
  - Delete button for each address
- **Deliverable:** Address manager working
- **Testing:** Add, edit, delete multiple addresses

---

#### **Task 7.3: Bank Account Manager Component**
- **Description:** UI to manage multiple bank accounts per customer
- **Component:** `src/components/BankAccountManager.vue`
- **Features:**
  - List of existing accounts in table
  - Add new account button → opens modal
  - Modal fields: Bank Name, Branch, Account Number, IFSC Code, Account Type
  - Mark as Primary checkbox
  - Edit button for each account
  - Delete button for each account
  - Passbook upload button with OCR extraction
- **Deliverable:** Bank account manager working
- **Testing:** Add, edit, delete multiple accounts

---

#### **Task 7.4: Activity Timeline Component**
- **Description:** Display recent activities in sidebar
- **Component:** `src/components/ActivityTimeline.vue`
- **Features:**
  - Show last N activities (configurable, default 10)
  - Format: "Customer Name - Action - Date"
  - Actions: Customer Added, Updated, Deleted, Bio-data Generated, Document Uploaded
  - Clickable to navigate to customer
  - Color coding for different action types
- **Deliverable:** Activity timeline displaying correctly
- **Testing:** Perform actions, see in timeline

---

### **Sprint 8: Photo, Bio-Data, Education (Days 16-17)**

#### **Task 8.1: Photo Upload with Crop Tool**
- **Description:** Photo management with built-in crop
- **Component:** `src/components/PhotoUploader.vue`
- **Features:**
  - File input (JPG, PNG only)
  - Preview of selected image
  - vue-cropper integration
  - Drag, resize, rotate image
  - Save cropped photo to uploads/photos/
- **Deliverable:** Photo upload and crop working
- **Testing:** Upload photo, crop, save

---

#### **Task 8.2: Enhanced Education Component**
- **Description:** Education records with Admit and Registration Numbers
- **Component:** `src/components/EducationForm.vue`
- **Per Education Record:**
  - Education Level, Course/Stream, Institution, Year, Board/University
  - **Admit Number (new field)**
  - **Registration Number (new field)**
  - Total Marks, Obtained Marks, Percentage (auto-calculated), Grade
  - Document upload with OCR extraction
- **Deliverable:** Education form with new fields
- **Testing:** Add education with admit and reg numbers

---

#### **Task 8.3: Bio-Data Generator Component**
- **Description:** Generate PDF/HTML bio-data with customizable sections
- **Component:** `src/components/BioDataGenerator.vue`
- **Features:**
  - Select customer from dropdown
  - Checkboxes to select which sections to include
  - Select format (PDF or HTML)
  - Generate button
  - Browser downloads file to Downloads folder
- **Deliverable:** Customizable bio-data working
- **Testing:** Generate with different section selections

---

### **Sprint 9: Customer Directory with Status (Days 18-19)**

#### **Task 9.1: Enhanced Customer List View**
- **Description:** Display customers with status tracking
- **Component:** `src/components/CustomerList.vue` or page `CustomersPage.vue`
- **Features:**
  - Table: ID, Name, Phone, Address (Village), Status, Actions
  - **Status column:** Dropdown (Active, Inactive, Not Interested)
  - Sortable by any column
  - Pagination (50 per page)
  - Click row to view details
  - Delete button with confirmation
  - Export to CSV/Excel button
- **Deliverable:** Enhanced customer list working
- **Testing:** 
  - Add customers, see in list
  - Change status via dropdown
  - Sort, paginate, export

---

#### **Task 9.2: Dashboard with Timeline**
- **Description:** Dashboard showing stats and recent activity
- **Page:** `src/pages/HomePage.vue`
- **Features:**
  - Total customers count
  - Recently added customers
  - Activity timeline (last 10 activities)
  - Quick action buttons (Add Customer, View Directory, Bio-Data, Settings)
  - Stats cards (Active, Inactive, Total)
- **Deliverable:** Dashboard with timeline functional
- **Testing:** Dashboard displays stats and timeline correctly

---

### **Sprint 10: Settings - OCR, Websites, Backup (Days 20-21)**

#### **Task 10.1: OCR Settings Component**
- **Description:** Configure OCR in settings
- **Component:** `src/components/OCRSettings.vue`
- **Features:**
  - Toggle: Enable/Disable OCR globally
  - Checkboxes for document types
  - Confidence threshold slider (0-100%, default 90%)
  - Language dropdown (English only)
  - Status indicator: "OCR Ready"
- **Deliverable:** OCR settings component working
- **Testing:** Toggle settings, verify applied globally

---

#### **Task 10.2: Backup & Restore**
- **Description:** Backup/restore all data as JSON
- **Routes:**
  ```javascript
  app.post('/api/backup/create', (req, res) => {
    const data = {
      customers: readJSON('customers.json'),
      websites: readJSON('important_websites.json'),
      audit: readJSON('audit_logs.json'),
      settings: readJSON('settings.json'),
      timeline: readJSON('activity_timeline.json'),
      backup_date: new Date().toISOString()
    };
    // Return as downloadable JSON
    res.json(data);
  });
  
  app.post('/api/backup/restore', (req, res) => {
    const backup = req.body;
    writeJSON('customers.json', backup.customers);
    writeJSON('important_websites.json', backup.websites);
    writeJSON('audit_logs.json', backup.audit);
    writeJSON('settings.json', backup.settings);
    writeJSON('activity_timeline.json', backup.timeline);
    res.json({ success: true });
  });
  ```
- **Component:** `src/components/BackupRestore.vue`
- **Features:**
  - "Backup Now" button → downloads backup.json
  - "Restore" button → upload backup file
  - Confirmation dialog before restore
  - Shows backup date
- **Deliverable:** Backup & restore working
- **Testing:** Backup, then restore, verify data

---

#### **Task 10.3: Audit Log Viewer**
- **Description:** View and filter audit logs
- **Component:** `src/components/AuditLog.vue`
- **Features:**
  - Table of audit logs with timestamp, action, customer
  - Filter by customer, action type
  - Export to CSV
  - Show timestamp, action, changes
- **Deliverable:** Audit log viewer working
- **Testing:** Perform action, see in audit logs

---

#### **Task 10.4: Other Settings**
- **Description:** Theme, timeline count, bio-data sections
- **Features:**
  - Theme toggle (Light/Dark)
  - Timeline recent count (5, 10, 15, 20)
  - Bio-data sections checkboxes
- **Deliverable:** All settings working
- **Testing:** Toggle settings, verify applied

---

### **Sprint 11: Import, Export, Search (Days 22-23)**

#### **Task 11.1: Bulk Import**
- **Description:** Import customers from CSV file
- **Component:** `src/components/ImportExport.vue`
- **Features:**
  - CSV file input
  - Validate file with all fields
  - Detect duplicates
  - Show error summary
  - Import valid rows or cancel
  - Show success message with count
- **Route:**
  ```javascript
  app.post('/api/import/csv', upload.single('file'), async (req, res) => {
    const csv = require('csv-parser');
    const fs = require('fs');
    const customers = [];
    
    fs.createReadStream(req.file.path)
      .pipe(csv())
      .on('data', (row) => customers.push(row))
      .on('end', () => {
        // Process and save customers
        res.json({ imported: customers.length });
      });
  });
  ```
- **Deliverable:** Import working
- **Testing:** Import CSV with customers

---

#### **Task 11.2: CSV/Excel Export**
- **Description:** Export all customers to CSV/Excel
- **Routes:**
  ```javascript
  app.get('/api/export/csv', (req, res) => {
    const data = readJSON('customers.json');
    // Convert to CSV format
    res.setHeader('Content-Type', 'text/csv');
    res.attachment('customers.csv');
    res.send(convertToCSV(data.customers));
  });
  
  app.get('/api/export/excel', (req, res) => {
    const data = readJSON('customers.json');
    const workbook = xlsx.utils.json_to_sheet(data.customers);
    // Send Excel file
    res.attachment('customers.xlsx');
    res.send(excelBuffer);
  });
  ```
- **Deliverable:** Export working
- **Testing:** Export CSV/Excel, open in programs

---

#### **Task 11.3: Search Functionality**
- **Description:** Real-time search by name/phone/email
- **Component:** `src/components/SearchBar.vue`
- **Features:**
  - Text input with real-time search
  - Search by name, phone, email
  - Show results as user types
  - Click result to navigate to customer
- **Route:** Already created in Task 3.1 (GET /api/customers/search)
- **Deliverable:** Search working
- **Testing:** Search for customers, see results

---

### **Sprint 12: Pinia Stores Implementation (Days 24-25)**

#### **Task 12.1: Implement All 8 Pinia Stores**
- **Description:** Complete state management for all features
- **Stores to create:**
  1. `customerStore.js` - Customers state & actions
  2. `addressStore.js` - Addresses state & actions
  3. `bankStore.js` - Bank accounts state & actions
  4. `educationStore.js` - Education state & actions
  5. `documentStore.js` - Documents state & actions
  6. `settingsStore.js` - Settings state & actions
  7. `timelineStore.js` - Activity timeline state & actions
  8. `auditStore.js` - Audit logs state & actions

- **Each store includes:**
  ```javascript
  state: { data array }
  getters: { filter, search functions }
  actions: { 
    fetchData()
    createRecord()
    updateRecord()
    deleteRecord()
  }
  ```
- **Deliverable:** All stores implemented and working
- **Testing:** Stores update correctly, components render

---

#### **Task 12.2: Connect Components to Stores**
- **Description:** Integrate Pinia stores with Vue components
- **Process:**
  1. Each component imports relevant store
  2. Component calls store actions
  3. Store updates state
  4. Components re-render with new data
- **Example:**
  ```javascript
  import { useCustomerStore } from '@/stores/customerStore'
  
  export default {
    setup() {
      const customerStore = useCustomerStore()
      
      const createCustomer = async (data) => {
        await customerStore.createCustomer(data)
      }
      
      return { customers: customerStore.customers, createCustomer }
    }
  }
  ```
- **Deliverable:** All components connected to stores
- **Testing:** Components sync with stores

---

### **Sprint 13: Build & Polish (Days 26-28)**

#### **Task 13.1: Vite Production Build**
- **Description:** Build Vue app for production
- **Command:** `npm run build`
- **Output:** `dist/` folder with optimized app
- **Testing:** Build succeeds without errors

---

#### **Task 13.2: Create README & Documentation**
- **Description:** User guide and setup instructions
- **File:** `README.md`
- **Content:**
  ```markdown
  # Customer Data Hub v2.1
  
  ## Setup
  1. npm install
  2. npm run dev (in one terminal)
  3. npm run server (in another terminal)
  4. Open http://localhost:5173
  
  ## Features
  - Full customer management
  - OCR document extraction
  - Bio-data generation
  - Activity tracking
  - Local data storage
  
  ## Data Location
  All data stored in ./data/ folder
  All files are JSON format
  Portable - can copy entire folder
  ```
- **Deliverable:** Documentation complete
- **Testing:** Follow README to run app

---

#### **Task 13.3: Test All Features End-to-End**
- **Description:** Complete testing of all v2.1 features
- **Test Checklist:**
  - [ ] Create customer with multiple addresses/banks
  - [ ] Upload document and process OCR
  - [ ] Generate bio-data with selected sections
  - [ ] Change customer status
  - [ ] View activity timeline
  - [ ] Configure websites in settings
  - [ ] Enable/disable OCR
  - [ ] Backup and restore data
  - [ ] Export to CSV/Excel
  - [ ] Import from CSV
  - [ ] Search by name/phone/email
  - [ ] Toggle theme (light/dark)
  - [ ] View audit logs
  - [ ] All data in ./data/ folder (local)
  - [ ] No internet errors
- **Deliverable:** All features working
- **Testing:** Complete end-to-end test

---

#### **Task 13.4: Performance Optimization**
- **Description:** Optimize for faster loading and responsiveness
- **Optimizations:**
  - Lazy load components
  - Image compression
  - Code splitting
  - Caching strategies
  - Virtual scrolling for large lists
- **Deliverable:** App performs well
- **Testing:** 
  - Load time < 2 seconds
  - Search response < 100ms
  - List with 1000 items loads smooth

---

---

## ✅ Quality Checklist

Before marking any task complete:

- [ ] Code follows Vue 3 + Express best practices
- [ ] Error handling implemented
- [ ] Logging added (audit trail)
- [ ] Tested with sample data
- [ ] No console errors
- [ ] Follows existing code style
- [ ] Comments added for complex logic
- [ ] All dependencies installed
- [ ] All tests pass
- [ ] Responsive design working
- [ ] Data persisted to JSON files

---

## 🐛 Common Issues & Solutions - v2.1

| Issue | Solution |
|-------|----------|
| CORS error between Vue and Express | Enable CORS in Express, check localhost only |
| JSON files not saving | Ensure data/ folder writable, check file paths |
| OCR taking too long | Process one document at a time, show spinner |
| Tesseract.js not loading | Check internet for first-time download, include in build |
| Data lost after restart | Check JSON files in data/ folder, verify write permissions |
| Search not working | Ensure search route exists, check API endpoint |
| Photo crop not showing | Install vue-cropper, check component imports |

---

## 📊 Progress Tracking - v2.1

| Sprint | Tasks | Estimated Days | Status |
|--------|-------|-----------------|--------|
| 1 | 1.1-1.4 | 2 | ⬜ |
| 2 | 2.1-2.3 | 2 | ⬜ |
| 3 | 3.1-3.3 | 2 | ⬜ |
| 4 | 4.1-4.3 | 3 | ⬜ |
| 5 | 5.1-5.3 | 2 | ⬜ |
| 6 | 6.1-6.3 | 2 | ⬜ |
| 7 | 7.1-7.4 | 2 | ⬜ |
| 8 | 8.1-8.3 | 2 | ⬜ |
| 9 | 9.1-9.2 | 2 | ⬜ |
| 10 | 10.1-10.4 | 2 | ⬜ |
| 11 | 11.1-11.3 | 2 | ⬜ |
| 12 | 12.1-12.2 | 2 | ⬜ |
| 13 | 13.1-13.4 | 3 | ⬜ |

---

## 🚀 Key Advantages v2.1 (Local Web App)

✅ No installation required  
✅ Works in any browser  
✅ No internet needed (offline capable)  
✅ All data on local PC  
✅ Easy to backup (JSON export)  
✅ Easy to portable (copy folder)  
✅ Can run on Windows, Mac, Linux  
✅ No database server needed  
✅ Browser-based UI (responsive)  
✅ Fast development (Vite)  

---

## 🎯 Success Criteria - Phase 1 Complete When

- ✅ Web app runs locally (npm run dev)
- ✅ All data stored in data/ JSON files
- ✅ All v2.1 features working
- ✅ OCR extraction for all document types working
- ✅ Multiple addresses/banks working
- ✅ Activity timeline functional
- ✅ Status tracking working
- ✅ Backup/restore working
- ✅ Import/export CSV/Excel working
- ✅ Search working
- ✅ No errors in console
- ✅ Responsive design working
- ✅ All tests pass
- ✅ Can copy folder to USB/another PC
- ✅ Documentation complete

---

**Status:** Ready for AI Agent to begin v2.1 web app development  
**Version:** 2.1 (Local Web App - Vue.js + Express + JSON)  
**Last Updated:** July 28, 2026  
**Timeline:** 3-4 weeks for MVP Phase 1

