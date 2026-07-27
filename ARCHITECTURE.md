# Customer Data Hub - Architecture Document

**Version:** 1.0  
**Date:** July 27, 2026  
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
│         CSV Storage Layer + JSON Config              │
│  (customers.csv, education.csv, audit_logs.json)    │
└──────────────────────────────────────────────────────┘
           ↓                              ↓
┌──────────────────────────┐  ┌──────────────────────────┐
│   File System            │  │   External Libraries     │
│   (Photos, Documents)    │  │   (Puppeteer, xlsx)      │
└──────────────────────────┘  └──────────────────────────┘
```

---

## 📂 Project Folder Structure

```
customer-data-hub/
├── public/
│   ├── icon.png (App icon - customize with your org name)
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
│   │   │   ├── Dashboard.jsx
│   │   │   ├── CustomerList.jsx
│   │   │   ├── CustomerForm.jsx
│   │   │   ├── PhotoUploader.jsx (with crop tool)
│   │   │   ├── BioDataGenerator.jsx
│   │   │   ├── ImportExport.jsx
│   │   │   ├── Settings.jsx
│   │   │   └── SearchBar.jsx
│   │   ├── pages/
│   │   │   ├── HomePage.jsx
│   │   │   ├── CustomersPage.jsx
│   │   │   ├── CustomerDetailPage.jsx
│   │   │   └── SettingsPage.jsx
│   │   ├── styles/
│   │   │   ├── App.css (Light theme)
│   │   │   ├── dark.css (Dark theme)
│   │   │   └── components.css
│   │   └── utils/
│   │       ├── validators.js (Email, phone validation)
│   │       └── formatters.js (Date, currency formatting)
│   │
│   ├── backend/
│   │   ├── index.js (Express server entry - runs in Electron)
│   │   ├── routes/
│   │   │   ├── customers.js (Customer CRUD endpoints)
│   │   │   ├── education.js (Education endpoints)
│   │   │   ├── biodata.js (Bio-data generator endpoints)
│   │   │   ├── import.js (Bulk import endpoints)
│   │   │   ├── export.js (Export endpoints)
│   │   │   ├── backup.js (Backup/restore endpoints)
│   │   │   └── audit.js (Audit log endpoints)
│   │   ├── services/
│   │   │   ├── CustomerService.js (Business logic)
│   │   │   ├── CSVService.js (CSV read/write)
│   │   │   ├── BioDataService.js (PDF/Word generation)
│   │   │   ├── ImportService.js (Import logic)
│   │   │   ├── AuditService.js (Audit logging)
│   │   │   └── BackupService.js (Backup operations)
│   │   ├── models/
│   │   │   ├── Customer.js (Data model)
│   │   │   ├── Education.js (Data model)
│   │   │   └── AuditLog.js (Data model)
│   │   ├── templates/
│   │   │   ├── default-biodata.html (Default HTML template)
│   │   │   └── custom-templates.json (User templates)
│   │   └── utils/
│   │       ├── logger.js (Logging utility)
│   │       ├── database.js (CSV database wrapper)
│   │       └── constants.js (App constants)
│   │
│   └── shared/
│       └── constants.js (Shared constants between main & renderer)
│
├── data/ (User data storage - created at runtime)
│   ├── customers.csv
│   ├── education.csv
│   ├── documents.csv
│   ├── addresses.csv
│   ├── metadata.json
│   ├── audit_logs.json
│   ├── audit_logs.csv
│   ├── photos/ (Customer photos)
│   ├── documents/ (Uploaded documents)
│   ├── biodata_templates/ (Custom templates)
│   └── backups/ (Backup files)
│
├── package.json (Dependencies)
├── electron-builder.json (Build configuration)
├── webpack.config.js (Build configuration)
├── REQUIREMENTS.md (PRD)
├── CLARIFICATION_INTERVIEW.md (Interview responses)
├── DEVELOPMENT_PLAN.md (Step-by-step build plan)
└── README.md (Quick start guide)
```

---

## 🔄 Data Flow Architecture

### 1. **Customer Creation Flow:**
```
User Input Form
    ↓
React Component (CustomerForm.jsx)
    ↓
IPC Call → Main Process
    ↓
Express Route (POST /api/customers)
    ↓
CustomerService.js (Validation, duplicate check)
    ↓
CSVService.js (Write to customers.csv)
    ↓
AuditService.js (Log: "Customer created")
    ↓
Response → UI Update
```

### 2. **Photo Upload Flow:**
```
User Selects Photo
    ↓
PhotoUploader.jsx (Crop tool)
    ↓
Cropped Image → Temp Buffer
    ↓
IPC Call → Main Process
    ↓
File System (Save to data/photos/CUST_ID.jpg)
    ↓
Update customers.csv (photo_path)
    ↓
AuditService.js (Log: "Photo updated")
    ↓
UI Refreshes
```

### 3. **Bio-Data Generation Flow:**
```
User Clicks "Generate Bio-Data"
    ↓
BioDataGenerator.jsx (Select customer + format)
    ↓
API Call → Express Route (POST /api/biodata/generate)
    ↓
BioDataService.js (Load template)
    ↓
Merge Data (Customer info + Education + Photo)
    ↓
Puppeteer (Render HTML to PDF) OR
DocxService (Generate .docx)
    ↓
Save As Dialog (User chooses location)
    ↓
File saved to user location
    ↓
AuditService.js (Log: "Bio-data generated")
```

### 4. **Bulk Import Flow:**
```
User Selects CSV File
    ↓
ImportExport.jsx (File selection dialog)
    ↓
IPC Call → Main Process
    ↓
CSVService.js (Parse CSV file)
    ↓
ImportService.js (Validate + Detect duplicates)
    ↓
Show Dialog:
  - Valid rows: 450
  - Duplicates: 30
  - Errors: 20
    ↓
User Chooses Action:
  - Import all valid + skip duplicates
  - Cancel
    ↓
CSVService.js (Append valid rows)
    ↓
AuditService.js (Log: "450 customers imported")
    ↓
Show Success Message
```

---

## 🗃️ Database Schema (CSV-Based)

### **customers.csv**
```
customer_id,name,age,gender,phone,email,address,bank_name,account_number,ifsc,photo_path,notes,created_date,last_modified

CUST_001,Rajesh Kumar,35,Male,9876543210,rajesh@email.com,"123 Main St, Delhi",HDFC Bank,123456789012,HDFC0001234,"data/photos/CUST_001.jpg","Senior executive",2026-01-15,2026-07-27
```

### **education.csv**
```
customer_id,qualification,institution,year_completed,stream,score,document_path,created_date

CUST_001,B.Tech,IIT Delhi,2012,Computer Science,8.5,"data/documents/CUST_001_BTech_Cert.pdf",2026-01-15
CUST_001,12th,Delhi Public School,2008,Science,92,"data/documents/CUST_001_12th_Cert.pdf",2026-01-15
```

### **documents.csv**
```
doc_id,customer_id,document_type,file_name,file_path,upload_date,created_date

DOC_001,CUST_001,certificate,"B.Tech Certificate.pdf","data/documents/CUST_001_BTech_Cert.pdf",2026-01-15,2026-01-15
DOC_002,CUST_001,admit_card,"Admission Letter.jpg","data/documents/CUST_001_AdmitCard.jpg",2026-01-15,2026-01-15
```

### **addresses.csv**
```
customer_id,street_address,city,state,postal_code,country

CUST_001,"123 Main St","Delhi","Delhi","110001","India"
```

### **metadata.json**
```json
{
  "app_version": "1.0.0",
  "last_backup": "2026-07-27T14:30:22Z",
  "theme": "dark",
  "total_customers": 150,
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

### **audit_logs.json**
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
  },
  {
    "timestamp": "2026-07-27T14:36:15Z",
    "customer_id": "CUST_001",
    "action": "photo_uploaded",
    "field": "photo",
    "old_value": null,
    "new_value": "data/photos/CUST_001.jpg",
    "user": "default_user"
  }
]
```

---

## 🔌 IPC (Inter-Process Communication) Bridge

### **Main → Renderer Communication:**
```javascript
// main/index.js
ipcMain.handle('get-customers', async (event) => {
  return await CustomerService.getAll();
});

ipcMain.handle('save-photo', async (event, customerId, photoBuffer) => {
  return await FileService.savePhoto(customerId, photoBuffer);
});
```

### **Renderer → Main Communication:**
```javascript
// renderer/components/CustomerList.jsx
const customers = await window.ipcRenderer.invoke('get-customers');

await window.ipcRenderer.invoke('save-photo', customerId, photoBuffer);
```

---

## 🔐 Security Architecture

### **Preload Script (preload.js):**
```javascript
// Only expose safe IPC methods
const { contextBridge, ipcRenderer } = require('electron');

contextBridge.exposeInMainWorld('ipcRenderer', {
  invoke: (channel, ...args) => {
    const validChannels = [
      'get-customers',
      'create-customer',
      'update-customer',
      'save-photo',
      'generate-biodata'
    ];
    if (validChannels.includes(channel)) {
      return ipcRenderer.invoke(channel, ...args);
    }
  }
});
```

### **No Authentication Needed:**
- Single-user desktop app
- Local file storage only
- No network calls (except Puppeteer for PDF)

---

## 📦 Build & Packaging

### **Build Process:**
```
1. npm run build:frontend   → Bundle React/Vue
2. npm run build:backend    → Bundle Express API
3. electron-builder         → Create .exe installer
   └── Output: CustomerDataHub-1.0.0-Setup.exe (~200MB)
```

### **Distribution:**
- .exe installer (signed with org certificate)
- Installs to `Program Files/CustomerDataHub/`
- Desktop shortcut + Start Menu entry
- Auto-update capable (future feature)

---

## 🚀 Technology Decisions & Rationale

| Technology | Choice | Reason |
|-----------|--------|--------|
| **Desktop Framework** | Electron | Cross-platform, .exe packaging, built-in Node.js |
| **Frontend** | React | Rich component ecosystem, easy state management |
| **Backend** | Express | Lightweight, runs in Electron, perfect for desktop APIs |
| **Storage** | CSV | Simple, no database setup, human-readable, up to 5,000 rows |
| **PDF Generation** | Puppeteer | Professional output, HTML-to-PDF, customizable templates |
| **Excel Export** | xlsx | Popular library, reliable formatting |
| **Image Crop** | react-easy-crop | Lightweight, good UX for photo editing |
| **UI Components** | Material-UI | Professional look, dark mode support built-in |
| **Build Tool** | electron-builder | Simplified .exe creation, auto-updates support |

---

## 🔄 Component Interaction Diagram

```
┌──────────────────┐
│   Electron Main  │
│   (index.js)     │
└────────┬─────────┘
         │
    ┌────┴────────────────────┐
    ↓                         ↓
┌─────────┐          ┌──────────────┐
│ IPC     │          │ File System  │
│ Routes  │          │ (photos,     │
└────┬────┘          │  documents)  │
     │               └──────────────┘
     ↓
┌─────────────────┐
│ React Frontend  │
│ (Components)    │
└────┬────────────┘
     │
     └────→ API Calls (localhost:3000)
     
     ↓
┌────────────────┐
│ Express Routes │
│ (API Layer)    │
└────┬───────────┘
     │
     ↓
┌────────────────┐
│ Services       │
│ (Business      │
│  Logic)        │
└────┬───────────┘
     │
     ├────→ CSVService (Read/Write CSV)
     ├────→ AuditService (Logging)
     ├────→ BioDataService (Puppeteer)
     └────→ FileService (Photos/Documents)
```

---

## 🧪 Testing Architecture

### **Unit Tests:**
- Services (CustomerService, CSVService, etc.)
- Validators (Email, phone format)
- Formatters (Date, currency)

### **Integration Tests:**
- API routes + Services
- CSV read/write operations
- Photo upload flow

### **E2E Tests:**
- Full customer creation → bio-data generation
- Import/export workflows

---

## 📈 Performance Considerations

### **Optimization for 5,000 Customers:**

1. **CSV Indexing:** Create in-memory index for fast lookup
   ```javascript
   // Load CSV once at app start, maintain index in RAM
   const customerIndex = new Map();
   customers.forEach(c => customerIndex.set(c.customer_id, c));
   ```

2. **Pagination:** List view shows 50 customers per page
   ```javascript
   // Renderer only loads next 50 on demand
   GET /api/customers?page=1&limit=50
   ```

3. **Search Optimization:** Index on Name, Phone, Email
   ```javascript
   // Trie or simple Map for fast prefix search
   const phoneIndex = new Map();
   customers.forEach(c => phoneIndex.set(c.phone, c));
   ```

4. **Lazy Loading:** Photos loaded on demand, not all at once

---

## 🔧 Configuration Files

### **package.json**
```json
{
  "name": "customer-data-hub",
  "version": "1.0.0",
  "main": "src/main/index.js",
  "scripts": {
    "start": "electron .",
    "dev": "concurrently \"npm run backend\" \"npm run frontend\"",
    "backend": "node src/backend/index.js",
    "frontend": "react-scripts start",
    "build": "electron-builder",
    "build:exe": "npm run build -- --win nsis"
  },
  "dependencies": {
    "electron": "^latest",
    "express": "^4.18.0",
    "puppeteer": "^latest",
    "xlsx": "^latest",
    "csv-parser": "^latest"
  }
}
```

### **electron-builder.json**
```json
{
  "appId": "com.customerdata.hub",
  "productName": "Customer Data Hub",
  "files": ["src/", "node_modules/"],
  "directories": {
    "buildResources": "public"
  },
  "win": {
    "target": ["nsis"],
    "icon": "public/icon.ico"
  },
  "nsis": {
    "oneClick": false,
    "allowToChangeInstallationDirectory": true,
    "createDesktopShortcut": true,
    "createStartMenuShortcut": true
  }
}
```

---

## 📝 Development Workflow

### **Phase 1: Foundation (Week 1)**
1. Project setup (Electron + React + Express)
2. CSV storage layer (Read/Write)
3. Customer CRUD API
4. Basic UI (List, Create, Update)

### **Phase 2: Features (Week 2)**
1. Photo upload with crop tool
2. Bio-data PDF generation (Puppeteer)
3. Bulk import with validation
4. CSV/Excel export

### **Phase 3: Polish (Week 3)**
1. Theme toggle (Light/Dark)
2. Audit logging
3. Backup/restore
4. Settings page
5. Build .exe installer

---

## ✅ Implementation Checklist for AI Agent

- [ ] Set up Electron + React + Express project structure
- [ ] Create CSVService (read/write CSV files)
- [ ] Implement Customer routes (CRUD)
- [ ] Build Customer UI components
- [ ] Add photo upload with crop tool
- [ ] Integrate Puppeteer for PDF generation
- [ ] Add bulk import logic
- [ ] Implement CSV/Excel export
- [ ] Add audit logging system
- [ ] Create settings page with theme toggle
- [ ] Implement backup/restore
- [ ] Build and test .exe installer
- [ ] Document deployment process

---

## 📞 Key Integration Points

1. **CSV Operations:** CSVService handles all file I/O
2. **IPC Communication:** Preload.js exposes safe methods
3. **Business Logic:** Services layer (no logic in routes)
4. **Error Handling:** Consistent error format across all APIs
5. **Logging:** AuditService logs all important actions

---

**This architecture supports:**
- ✅ Single-user desktop app
- ✅ CSV-based storage (up to 5,000 records)
- ✅ Electron .exe packaging
- ✅ Offline operation (no internet required)
- ✅ Professional bio-data generation
- ✅ Audit trail for compliance
- ✅ Light/Dark theme support

