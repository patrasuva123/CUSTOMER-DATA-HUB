This conversation was generated with Duck.ai (https://duck.ai) using Anthropic's Claude Haiku 4.5 Model. AI chats may display inaccurate or offensive information (see https://duckduckgo.com/duckai/privacy-terms for more info).

====================

User prompt 1 of 8 - 7/25/2026, 1:11:13 PM:
 i want to build a Customer Data Hub for my bussiness. It contains Dashboard, Add New Customer, Customer Directory, System Settings and Bio-Data Generator options. i am giving you 5 images of each Sections. I want to store all the documents in my personal PC Drive. Look into the images and Interview me for my choices and give a proper PRD of the Project. I will build with the help of AI agent. 
[Attached image 1][Attached image 2][Attached image 3]

Claude Haiku 4.5:
I appreciate you sharing these detailed mockups! Before I create a comprehensive PRD, I need to understand your vision better. Let me ask you some clarifying questions:

## Essential Information

**1. Language & Environment**
- What programming language/framework do you prefer to build this with? (React, Vue, Angular, .NET, Python Flask, etc.)
- Should this be a web application, desktop app, or mobile-responsive web?
- Will you need backend infrastructure (database), or is local PC storage truly sufficient for your scale?

**2. Current Proficiency**
- Are you familiar with full-stack development, or will you primarily guide an AI agent with detailed requirements?
- Do you have experience with databases (SQL, NoSQL)?

**3. Data & Scale**
- **How many customers** do you expect to manage? (I see 1,568 in the dashboard—is this your target?)
- **File storage**: You mentioned "personal PC Drive"—do you mean:
  - Local file system (JSON, CSV files)?
  - SQLite or another embedded database?
  - Cloud sync (OneDrive, Google Drive) with local backup?

**4. Feature Clarifications**

From your images, I can see:

| Feature | Questions |
|---------|-----------|
| **Dashboard** | Do you need real-time analytics? Charts/graphs library preference? Export functionality? |
| **Add New Customer** | Auto-validation rules? Duplicate detection? Required vs. optional fields? |
| **Customer Directory** | Advanced filtering/search? Batch operations? Export to Excel? |
| **System Settings** | User roles/permissions? Backup scheduling? Data privacy/encryption? |
| **Bio-Data Generator** | Does this auto-populate fields, generate reports, or create documents? PDF export? |

**5. Business Rules**
- Do customers have hierarchies (primary contact, linked accounts)?
- Is there audit logging needed (who changed what, when)?
- Data validation—any specific formats or constraints? (e.g., phone number format, email validation)

Once you answer these, I'll deliver a **detailed PRD with user stories, technical specs, and a phased roadmap** ready for your AI agent.

--------------------

User prompt 2 of 8 - 7/25/2026, 1:11:49 PM:

[Attached image 1][Attached image 2]

Claude Haiku 4.5:
Thank you for the additional images! These are very helpful. I can now see the **System Settings** and **Bio-Data Generator** modules more clearly. Let me refine my questions based on what I'm observing:

## Refined Interview Questions

**1. Technology Stack & Deployment**
- **Primary language/framework preference?** (I notice a professional UI—are you thinking React/Vue web app, or something else?)
- **Local PC storage approach**: 
  - SQLite database stored on your PC?
  - JSON/CSV files in a folder structure?
  - Hybrid (cloud-backed local cache)?

**2. Bio-Data Generator (Image 5)**
- Is this feature meant to:
  - **Generate a formatted profile document** (PDF/Word) from selected customer data?
  - **Auto-populate missing fields** based on existing data?
  - **Create bulk documents** (certificates, ID cards, reports)?
- Should users be able to **customize the template** for the bio-data profile?
- Output format: **PDF, Word, or both?**

**3. System Settings (Image 4) – Clarifications**
- **Application Users**: Should this support **multiple users** with different access levels (Admin, Manager, Viewer)?
- **Module Resources**: Are these toggles to **enable/disable features** for different user roles?
- **OCR Document Rule Config**: Do you need to:
  - Scan and extract data from uploaded documents (like ID cards, passports)?
  - Auto-populate customer fields from document scans?
- **System Integrity & Logs**: Should this track:
  - Login history?
  - Data change audit trail (who modified what, when)?
  - Backup status & restore points?

**4. Customer Data & Relationships**
- From Image 2: I see **linked important websites** (Gmail, LinkedIn, Aadhaar Bharat)—are these custom links per customer, or predefined integrations?
- **Document Vault**: Can customers have **multiple documents attached** (PDFs, images, certificates)?
- Should there be **bulk import** capability (CSV to add 100+ customers at once)?

**5. Business Rules & Validation**
- **Duplicate detection**: Should the system warn if a phone number or email already exists?
- **Status values**: I see "Active," "Inactive," "Pending"—any other statuses?
- **Required fields**: Which fields in the form **must always be filled**?

**6. Scope & Phasing**
- Do you want **all features in v1**, or would you prefer a **phased rollout** (e.g., Dashboard + Directory first, then Bio-Data Generator)?
- **Timeline**: When do you need this operational?

---

Once you answer these, I'll create a **professional PRD with**:
- ✅ Feature specifications
- ✅ Data schema design
- ✅ UI/UX flow diagrams
- ✅ Technical architecture
- ✅ Phased development roadmap

**Please respond to the questions you feel are most important—I'll fill in reasonable defaults for the rest.**

--------------------

User prompt 3 of 8 - 7/25/2026, 9:35:59 PM:
1. Technology Stack & Deployment
 i. Vue web as an app desktop app. 
 ii. I will use my local PC storage which is truly sufficient for my scale. 
 iii. I primarily guide an AI agent with detailed requirements. 
 iv. I am not experience enough with databases .
 v. I expect more than 1000 customer to manage .
vi. Personal PC drive - Local file system CSV files in folder structure.
2. Bio-Data Generator - YES for all .
3. System Settings (Image 4) – Clarifications - YES for all except Application Users, Module Resources . I will use it only myself. 
4. Customer Data & Relationships -websites are predefined integrations. They can have Multiple Doc attached. There should be Bulk import capability.
5. Business Rules & Validation— The system warn if a phone number or email already exists. Status values is for the customer status who are vising, not vising or Complt data not given. Name & Mobile fields in the form must always be filled.
6. Scope & Phasing - I want your recomandation . A perfect work of my project. As close as possible to my pictures given.
I want my app further to be run on another PC also.

Claude Haiku 4.5:
Perfect! Now I have all the information I need. Let me create a **comprehensive PRD** tailored to your requirements.

---

## **CUSTOMER DATA HUB – PROJECT REQUIREMENTS DOCUMENT (PRD)**

**Version:** 1.0  
**Date:** July 25, 2026  
**Status:** Ready for AI Agent Development  
**Platform:** Vue.js Desktop Application (Electron)  
**Storage:** Local File System (CSV + JSON)  
**Target Users:** 1,000+ customers  
**Scalability:** Cross-PC Compatible

---

## **1. PROJECT OVERVIEW**

The **Customer Data Hub** is a desktop application designed to centralize customer management with intuitive dashboards, bulk import capabilities, document storage, and automated bio-data profile generation. The system prioritizes ease of use, data validation, and local file-based persistence for privacy and portability.

---

## **2. CORE FEATURES & SPECIFICATIONS**

| Feature | Status | Priority | Description |
|---------|--------|----------|-------------|
| **Dashboard** | MVP | High | Real-time customer metrics, activity timeline, quick actions |
| **Add New Customer** | MVP | High | Form-based customer registration with validation & duplicate detection |
| **Customer Directory** | MVP | High | Searchable, filterable customer list with bulk operations & Excel export |
| **System Settings** | MVP | Medium | Backup/restore, OCR document config, audit logs, system health monitoring |
| **Bio-Data Generator** | MVP | High | Template-based PDF/Word profile generation with customizable templates |
| **Bulk Import** | MVP | High | CSV-based bulk customer upload with validation & error reporting |
| **Document Vault** | MVP | Medium | Multiple document attachment & storage per customer |

---

## **3. FEATURE SPECIFICATIONS**

### **3.1 Dashboard**
**Concept Brief:**  
Single-screen overview of customer base health, recent activities, and quick navigation to core functions.

**Key Components:**
- **Total Customers Widget** – Display count + weekly growth percentage (📈 metric)
- **Recently Added Customers** – Last 5 entries with join date
- **Recent Activity Timeline** – Sidebar log of recent actions (add, edit, export)
- **Quick Action Buttons:**
  - ➕ ADD NEW CUSTOMER (large primary CTA)
  - 👁️ VIEW CUSTOMER DIRECTORY
  - ⚙️ SYSTEM SETTINGS
  - 📄 BIO-DATA GENERATOR

**Data Source:** CSV files + metadata JSON  
**Refresh Rate:** Real-time (on app load, after actions)

---

### **3.2 Add New Customer**

**Concept Brief:**  
Multi-section form capturing personal, financial, educational, and document data with real-time validation.

**Form Sections:**

#### **A. Customer Personal Profile**
| Field | Type | Required | Validation | Notes |
|-------|------|----------|-----------|-------|
| First Name | Text | ✅ Yes | Non-empty, max 50 chars | |
| Last Name | Text | ❌ No | Max 50 chars | |
| Father's Name | Text | ❌ No | Max 50 chars | |
| Mother's Name | Text | ❌ No | Max 50 chars | |
| Date of Birth | Date | ❌ No | Valid date, age ≥ 18 (optional check) | |
| Gender | Dropdown | ❌ No | Male / Female / Other | |
| Marital Status | Dropdown | ❌ No | Single / Married / Divorced / Widowed | |
| Religion | Dropdown | ❌ No | Predefined list | |
| Blood Group | Dropdown | ❌ No | A+, A-, B+, B-, O+, O-, AB+, AB- | |
| Mobile Number | Phone | ✅ Yes | **10 digits** (India format), **must be unique** | ⚠️ Warn if duplicate |
| Email ID | Email | ❌ No | Valid email format, **must be unique if provided** | ⚠️ Warn if duplicate |
| Ration Card No. | Text | ❌ No | Max 20 chars | |
| Pan Number | Text | ❌ No | Valid PAN format (10 chars) | |

#### **B. Bank & Financial Details**
| Field | Type | Required | Validation | Notes |
|-------|------|----------|-----------|-------|
| Bank Name | Text | ❌ No | Predefined dropdown or free text | |
| Account Number | Text | ❌ No | Valid format check | |
| IFSC Code | Text | ❌ No | 11 chars, valid IFSC format | |
| Is Primary Account? | Checkbox | ❌ No | Boolean | |

#### **C. Education & Qualifications**
| Field | Type | Required | Validation | Notes |
|-------|------|----------|-----------|-------|
| Qualification Level | Dropdown | ❌ No | 8th Pass / 10th / 12th / Diploma / Graduate / Post-Graduate | |
| Highest Qualification | Text | ❌ No | e.g., B.Sc., M.A. | |
| Board/University | Text | ❌ No | Max 100 chars | |
| Year of Completion | Year | ❌ No | Valid year ≤ current year | |

#### **D. Address Details**
| Field | Type | Required | Validation | Notes |
|-------|------|----------|-----------|-------|
| Address Type | Dropdown | ❌ No | Select Type (Residential, Commercial) | |
| Street Address | Text | ❌ No | Max 200 chars | |
| Village/Town | Text | ❌ No | Max 50 chars | |
| Post Office | Text | ❌ No | Max 50 chars | |
| District | Text | ❌ No | Max 50 chars | |
| State | Text | ❌ No | Max 50 chars | |
| Pin Code | Text | ❌ No | 6 digits (India) | |

#### **E. Important Websites**
**Predefined Links** (read-only, customer clicks to visit):
- 🔗 Gmail
- 🔗 LinkedIn
- 🔗 Aadhaar Bharat
- ➕ Add custom links (optional)

#### **F. Document Vault**
- **File upload zone** (drag & drop or file picker)
- Allowed formats: PDF, JPG, PNG, DOCX
- Multiple files per customer
- Document metadata: upload date, file size, document type

#### **G. Other Data**
| Field | Type | Required | Notes |
|-------|------|----------|-------|
| Occupation/Job Title | Text | ❌ No | Max 50 chars |
| Company Name | Text | ❌ No | Max 100 chars |
| Work Experience (years) | Number | ❌ No | 0-70 |
| Computer Certificate | Checkbox | ❌ No | Has basic IT skills? |
| Year of Completion | Year | ❌ No | When cert was obtained |

**Form Behaviors:**
- ✅ **Real-time validation** on field blur
- ⚠️ **Duplicate warnings** for Mobile & Email (highlight if exists)
- 💾 **Auto-save to draft** every 5 seconds (warn before discard)
- 🔄 **Reset form** button
- ✅ **Submit button** (disabled until Name + Mobile filled)

**On Submit:**
- Save as CSV row + attachments in folder structure
- Generate unique Customer ID (e.g., `CUST_001568`)
- Show success toast + redirect to Directory

---

### **3.3 Customer Directory**

**Concept Brief:**  
Comprehensive searchable table with filtering, sorting, bulk operations, and export capabilities.

**Table Columns:**
| Column | Sortable | Filterable | Width | Notes |
|--------|----------|-----------|-------|-------|
| ☑️ Checkbox | - | - | 40px | For bulk select |
| Customer ID | ✅ | ❌ | 100px | Auto-generated |
| Name | ✅ | ✅ | 150px | First + Last Name |
| Address (Village) | ✅ | ✅ | 200px | Village/Town name |
| Phone | ✅ | ✅ | 120px | Mobile number |
| Join Date | ✅ | ✅ (date range) | 100px | YYYY-MM-DD |
| Status | ✅ | ✅ | 100px | Visiting / Not Visiting / Incomplete Data |
| Documents | ✅ | ❌ | 80px | Count badge |
| Actions | - | - | 150px | Edit / View / Delete / Generate Bio |

**Toolbar Features:**
- 🔍 **Search box** (searches Name, Phone, Email, ID)
- 📊 **Sort dropdown** (by Name, Date, Status, Phone)
- 🔽 **Filter panel:**
  - Status (multi-select)
  - Date range (from/to)
  - Location (Village/District)
  - Has Documents (Yes/No)
- 💾 **Export to Excel** (selected or all)
- 📥 **Bulk Import** (CSV file upload)
- 📋 **Save Changes** button
- 📄 **Export Selected** button

**Row Actions:**
- ✏️ **Edit** – Opens Add New Customer form in edit mode
- 👁️ **View** – Read-only detailed profile modal
- 🗑️ **Delete** – Confirm dialog + remove from CSV
- 📄 **Generate Bio** – Opens Bio-Data Generator with pre-filled data
- 📎 **View Docs** – Modal showing attached documents

**Pagination:**
- Show 25/50/100 rows per page
- Display "1-25 of 1,568" counter

**Status Filter Values:**
- 🟢 **Visiting** – Active customer, regularly engaged
- 🔴 **Not Visiting** – Inactive customer
- 🟡 **Incomplete Data** – Missing required fields (email, address)

---

### **3.4 Bio-Data Generator**

**Concept Brief:**  
Two-step wizard to customize and generate professional PDF/Word bio-data profiles from customer data.

**Step 1: Select Customer Profile**
- Search/filter customers by name or ID
- Display customer avatar + key details
- Show "Selected Customer Info" panel with profile snapshot

**Step 2: Customize Bio-Data Content**
- **Toggleable sections** (checkboxes to include/exclude):
  - ✅ Personal Details
  - ✅ Bank & Financial Details
  - ✅ Education & Qualifications
  - ✅ Important Websites (as links)
  - ✅ Address Details
  - ✅ Work Experience
  - ✅ Document References (list attached docs)
  - ✅ Other Data

- **Template Selector:**
  - Standard (professional one-page format)
  - Detailed (multi-page with sections)
  - Custom (user-defined layout)

- **Customization Options:**
  - Document Title (e.g., "Bio-Data Profile – Rajesh Sen")
  - Include/exclude sections
  - Add custom footer/notes
  - Select output format: **PDF** or **Word (.docx)**

**Output Features:**
- 📄 Generate PDF with:
  - Professional formatting
  - Customer photo/avatar (if available)
  - All selected sections
  - Generated timestamp
  - Custom footer (optional)
- 📝 Generate Word document (editable)
- 💾 Save to local folder: `Documents/BioDatas/{CUST_ID}_{Date}.pdf`
- 🖨️ Print-ready
- 📧 (Future) Email as attachment

**Actions:**
- ✅ **Generate PDF & Save**
- ✅ **Generate Word & Save**
- 📥 **Finalize and Send/Profile**
- 🏠 **Edit Selection (Previous Step)**

---

### **3.5 System Settings**

**Concept Brief:**  
Administrative control panel for backups, OCR configuration, audit logging, and system health monitoring.

#### **A. Application Settings**
| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| App Name | Text | Customer Data Hub | Display name |
| Version | Read-only | 1.0 | Current app version |
| Data Location | Path | C:\Users\[User]\CustomerHub | CSV storage folder path |
| Auto-Backup | Toggle | ON | Enable auto-backup (daily) |
| Backup Frequency | Dropdown | Daily | Hourly / Daily / Weekly |
| Backup Location | Path | C:\Users\[User]\CustomerHub\Backups | Backup folder |

#### **B. Module Resources**
**Status toggles** (informational, all modules enabled by default):
- ✅ CSV Processing
- ✅ Search & Filtering
- ✅ Blank Activity Tracking

#### **C. OCR Document Rule Config**
- 📄 **Enable Document Scanning** – Toggle to activate OCR
- 🔍 **OCR Engine** – Tesseract (local, no cloud)
- 📋 **Auto-Extract Fields** – Toggle to auto-populate customer fields from uploaded docs:
  - Extract Name from document
  - Extract Phone from document
  - Extract Address from document
  - Extract Document Type (Passport, Aadhaar, etc.)
- ⚙️ **Extraction Confidence Threshold** – Slider (0-100%, default 85%)
- 🧪 **Test OCR** – Upload sample document to test extraction

#### **D. System Integrity & Logs**
- 📊 **Login History** – Table showing:
  - Timestamp
  - User (currently: Admin)
  - Action (Login/Logout)
- 📝 **Audit Trail** – Table showing:
  - Timestamp
  - Action (Create/Edit/Delete/Export/Backup)
  - Entity (Customer ID, File name)
  - Details (field changed from X to Y)
- 🔍 **System Health** – Status indicators:
  - Database (CSV files) – ✅ Connected
  - Storage Space – ✅ 50 GB free
  - Last Backup – ✅ 2 hours ago
  - Errors – 0 Errors

#### **E. Backup & Restore**
- 💾 **Create Manual Backup** – Button to trigger immediate backup
- 📦 **Backup History** – Table:
  - Backup Date/Time
  - File Size
  - Location
  - Restore button
- 🔄 **Restore from Backup** – Select backup file → confirm → restore all CSV + documents
- ⚠️ **Restore Warning** – "This will replace current data. Are you sure?"

---

### **3.6 Bulk Import**

**Concept Brief:**  
CSV-based import with validation, error reporting, and dry-run preview.

**File Format:**
```
FirstName,LastName,MobileNumber,Email,Address,Village,Gender,Status
Rajesh,Sen,9876543210,rajesh@email.com,123 Street,Shampur Village,Male,Visiting
Aarti,Das,9123456789,aarti@email.com,456 Lane,Ranpur Village,Female,Not Visiting
```

**Import Workflow:**
1. **Select CSV file** (drag & drop or file picker)
2. **Map columns** – Auto-detect or manual column mapping
3. **Validate data** – Check for:
   - Required fields (Name, Mobile)
   - Duplicate mobiles/emails (warn, don't import duplicates)
   - Valid phone format (10 digits)
   - Valid email format
   - Date format validation
4. **Preview** – Show first 10 rows with validation status:
   - ✅ Valid row – green
   - ⚠️ Warning (duplicate) – yellow
   - ❌ Invalid row – red (skip)
5. **Dry Run Report** – "X rows will be imported, Y rows will be skipped"
6. **Confirm & Import** – Create CSV rows + assign Customer IDs
7. **Success Report** – "1,500 customers imported. 10 skipped due to errors."

---

### **3.7 Document Vault**

**Concept Brief:**  
Per-customer document storage with metadata and retrieval.

**Storage Structure:**
```
CustomerHub/
├── Data/
│   ├── customers.csv
│   └── metadata.json
└── Documents/
    ├── CUST_001/
    │   ├── resume.pdf
    │   ├── aadhaar.jpg
    │   └── cert.pdf
    ├── CUST_002/
    │   └── id_card.jpg
```

**Document Management:**
- ✅ Upload multiple files (PDF, JPG, PNG, DOCX)
- 📋 Document type tagging (Resume, Certificate, ID, etc.)
- 📅 Upload date auto-captured
- 🔍 Search documents by customer or type
- 🗑️ Delete individual documents
- 💾 Auto-organized folder structure per customer

---

## **4. DATA SCHEMA**

### **4.1 Main CSV Structure: `customers.csv`**

```csv
CustomerID,FirstName,LastName,FathersName,MothersName,DOB,Gender,MaritalStatus,Religion,BloodGroup,MobileNumber,EmailID,RationCardNo,PANNumber,BankName,AccountNumber,IFSCCode,IsPrimaryAccount,QualificationLevel,HighestQual,Board,YearCompletion,AddressType,StreetAddress,Village,PostOffice,

--------------------

User prompt 4 of 8 - 7/25/2026, 10:05:08 PM:
3.2 Add New Customer -  A. Customer Personal Profile - Add " Field - Aadhaar Number	Type - Text	Required - No	Validation - Max 12 digits 	Notes "
 C. Education & Qualifications - Add " Field - Roll Number, Reg Number, Full Marks, Obtained Marks , auto calculated % of marks.''
The rest is perfect. I have some questions. As per my Picture given in Add New Customer - Customer Personal Profile there are PIC & Signature , will it be available? In Education & Qualifications - As it is a multi level education so for Madhyamik the uploaded doc should be Admit for MP, for HS it should be Admit for HS, as they are different documents. Lastly How should I hand over it to my AI agent for Perfect work as per my Pictures ?

Claude Haiku 4.5:
Excellent clarifications! Let me update the PRD with your additions and address your questions comprehensively.

---

## **UPDATED SECTION 3.2 – Add New Customer**

### **3.2A Customer Personal Profile (UPDATED)**

| Field | Type | Required | Validation | Notes |
|-------|------|----------|-----------|-------|
| First Name | Text | ✅ Yes | Non-empty, max 50 chars | |
| Last Name | Text | ❌ No | Max 50 chars | |
| Father's Name | Text | ❌ No | Max 50 chars | |
| Mother's Name | Text | ❌ No | Max 50 chars | |
| Date of Birth | Date | ❌ No | Valid date, age ≥ 18 (optional check) | |
| Gender | Dropdown | ❌ No | Male / Female / Other | |
| Marital Status | Dropdown | ❌ No | Single / Married / Divorced / Widowed | |
| Religion | Dropdown | ❌ No | Predefined list | |
| Blood Group | Dropdown | ❌ No | A+, A-, B+, B-, O+, O-, AB+, AB- | |
| Mobile Number | Phone | ✅ Yes | **10 digits (India format), must be unique** | ⚠️ Warn if duplicate |
| Email ID | Email | ❌ No | Valid email format, must be unique if provided | ⚠️ Warn if duplicate |
| **Aadhaar Number** | **Text** | **❌ No** | **Max 12 digits, numeric only** | **⚠️ Validate format** |
| Ration Card No. | Text | ❌ No | Max 20 chars | |
| Pan Number | Text | ❌ No | Valid PAN format (10 chars) | |
| **Customer Photo** | **File Upload** | **❌ No** | **JPG/PNG only, max 5 MB, 400x400px recommended** | **Profile picture display** |
| **Signature** | **File Upload** | **❌ No** | **JPG/PNG only, max 2 MB, 200x100px recommended** | **Document signing** |

**Photo & Signature Upload Behavior:**
- Drag & drop or click to upload
- Live preview after upload
- Crop tool (optional) to resize/adjust
- Display in form and bio-data documents
- Store in `Documents/CUST_[ID]/photos/` folder
- File naming: `photo.jpg`, `signature.png`

---

### **3.2C Education & Qualifications (UPDATED)**

**Multi-Level Education Support** – Each customer can have multiple education records (8th, 10th, 12th, Diploma, Graduate, Post-Graduate, etc.)

**Add repeating section:** "➕ Add Another Qualification"

| Field | Type | Required | Validation | Notes |
|-------|------|----------|-----------|-------|
| **Qualification Level** | **Dropdown** | **✅ Yes** | **8th / 10th (Madhyamik) / 12th (HS) / Diploma / Graduate / Post-Graduate** | **Determines doc type** |
| Highest Qualification | Text | ❌ No | e.g., B.Sc., M.A., B.Tech | |
| Board/University | Text | ❌ No | Max 100 chars | |
| Roll Number | **Text** | **❌ No** | **Max 20 chars, alphanumeric** | **Exam roll no.** |
| Registration Number | **Text** | **❌ No** | **Max 20 chars, alphanumeric** | **Certificate reg no.** |
| Full Marks | **Number** | **❌ No** | **0-10,000** | **Total marks** |
| Obtained Marks | **Number** | **❌ No** | **≤ Full Marks** | **Marks scored** |
| **Percentage (%)** | **Auto-calculated** | **Read-only** | **(Obtained / Full) × 100** | **Auto-compute on blur** |
| Year of Completion | Year | ❌ No | Valid year ≤ current year | |
| **Required Document Type** | **Dropdown (Dynamic)** | **✅ Yes** | **Based on Qualification Level** | **⚠️ Enforced validation** |

#### **Dynamic Document Validation by Qualification Level:**

| Qualification Level | Required Document Type(s) | Accepted File Extensions | Notes |
|-------------------|---------------------------|-------------------------|-------|
| **8th** | Admit Card (8th) / Marksheet (8th) | PDF, JPG, PNG | Madhyamik stage docs |
| **10th (Madhyamik)** | Admit Card (Madhyamik) / Marksheet (Madhyamik) / Certificate (10th) | PDF, JPG, PNG | Board exam documents |
| **12th (HS)** | Admit Card (HS) / Marksheet (HS) / Certificate (12th) | PDF, JPG, PNG | Higher Secondary docs |
| **Diploma** | Admit Card (Diploma) / Marksheet (Diploma) / Certificate (Diploma) | PDF, JPG, PNG | Polytechnic/Technical docs |
| **Graduate** | Admit Card (Graduate) / Marksheet (Graduate) / Degree Certificate | PDF, JPG, PNG | Bachelor's degree docs |
| **Post-Graduate** | Admit Card (PG) / Marksheet (PG) / Degree Certificate | PDF, JPG, PNG | Master's degree docs |

**Example Workflow:**
1. User selects **"10th (Madhyamik)"** from Qualification Level dropdown
2. **Required Document Type** dropdown automatically shows:
   - ☐ Admit Card (Madhyamik)
   - ☐ Marksheet (Madhyamik)
   - ☐ Certificate (10th)
3. User must upload **at least one** of these document types
4. File upload validator checks:
   - File extension matches accepted types
   - Document labeled correctly (e.g., "Admit_Card_Madhyamik.pdf")
5. ⚠️ **Validation Error** if wrong document uploaded (e.g., "Admit Card HS" for "10th level")

**Education Section Storage:**
```
Documents/
├── CUST_001/
│   ├── education/
│   │   ├── 10th_madhyamik_admit.pdf
│   │   ├── 10th_madhyamik_marksheet.jpg
│   │   ├── 12th_hs_admit.pdf
│   │   └── 12th_hs_certificate.pdf
```

---

## **5. ANSWERING YOUR QUESTIONS**

### **Question 1: Will Photo & Signature be available in the form?**

**YES, absolutely!** ✅

**Implementation Details:**

#### **A. Photo Upload**
- **Placement:** Right side of "Customer Personal Profile" section (as shown in your Image 2)
- **Display:** Circular avatar placeholder (200x200px)
- **Upload:** Click or drag-drop
- **Format:** JPG/PNG, max 5 MB
- **Auto-crop:** Optional crop tool with 1:1 aspect ratio lock
- **Used in:**
  - Customer Directory (small thumbnail next to name)
  - Bio-Data profile document (centered at top)
  - Customer detail view

#### **B. Signature Upload**
- **Placement:** Below photo or in "Other Data" section
- **Display:** Rectangular preview (300x150px)
- **Upload:** Click or drag-drop
- **Format:** JPG/PNG, max 2 MB
- **Used in:**
  - Bio-Data PDF (bottom right, above date)
  - Can be overlaid on exported certificates
  - Document signing purposes

#### **C. Storage Structure**
```
Documents/
├── CUST_001/
│   └── photos/
│       ├── photo.jpg (main profile picture)
│       └── signature.png (digital signature)
```

#### **D. Metadata Tracking**
In `metadata.json`:
```json
{
  "CUST_001": {
    "photo": {
      "filename": "photo.jpg",
      "upload_date": "2026-07-25",
      "size_bytes": 245000,
      "dimensions": "400x400"
    },
    "signature": {
      "filename": "signature.png",
      "upload_date": "2026-07-25",
      "size_bytes": 15000,
      "dimensions": "300x150"
    }
  }
}
```

---

### **Question 2: Education Level-Based Document Validation – How does this work?**

**CRITICAL REQUIREMENT:** ⚠️ **Enforce document type matching**

**Your Use Case:**
- Student completes **10th (Madhyamik)** → Must upload **Madhyamik Admit Card** or **Madhyamik Marksheet**
- Student completes **12th (HS)** → Must upload **HS Admit Card** or **HS Certificate** (NOT Madhyamik docs)

**Implementation Strategy:**

#### **Step 1: Dynamic Dropdown Based on Selection**
```
User selects "10th (Madhyamik)" 
    ↓
"Required Document Type" dropdown shows:
  • Admit Card (Madhyamik)
  • Marksheet (Madhyamik)  
  • Certificate (10th)
    ↓
User selects "Admit Card (Madhyamik)"
    ↓
File upload validator expects filename pattern:
  "Admit_Card_Madhyamik_*" or "madhyamik_admit_*"
```

#### **Step 2: File Naming Convention**
Users should name files descriptively:
- ✅ `Admit_Card_Madhyamik.pdf`
- ✅ `10th_Madhyamik_Marksheet.jpg`
- ✅ `Certificate_10th.pdf`
- ❌ `admit.pdf` (too vague)
- ❌ `doc1.jpg` (non-descriptive)

#### **Step 3: Validation Logic**
When user uploads file:
```
1. Get selected Qualification Level (e.g., "10th")
2. Get selected Document Type (e.g., "Admit Card Madhyamik")
3. Check if filename contains:
   - Qualification keyword (e.g., "10th" or "madhyamik")
   - Document type keyword (e.g., "admit" or "marksheet")
4. Validate extension (.pdf, .jpg, .png)

❌ REJECT if:
   - File named "HS_Admit.pdf" but qualification is "10th"
   - Extension is .docx or .txt
   
✅ ACCEPT if:
   - File named "Madhyamik_Admit_Card.pdf" and qualification is "10th"
```

#### **Step 4: Error Messages for Wrong Document**
```
⚠️ ERROR: "You selected '10th (Madhyamik)' but uploaded an HS document.
Please upload the correct Madhyamik Admit Card or Marksheet."

✅ SUCCESS: "Document verified! Admit Card (Madhyamik) uploaded for 10th."
```

#### **Step 5: Education Section UI Layout**

```
┌─────────────────────────────────────────────┐
│ 📚 EDUCATION & QUALIFICATIONS               │
├─────────────────────────────────────────────┤
│                                             │
│ 🎓 Qualification 1: 10th (Madhyamik)        │
│ ├─ Roll Number: [______]                    │
│ ├─ Reg Number: [______]                     │
│ ├─ Full Marks: [____] | Obtained: [____]    │
│ ├─ Percentage: 78.5% (auto-calculated)      │
│ ├─ Year: [2020]                             │
│ │                                           │
│ └─ 📄 Document Type (required):              │
│    ☑ Admit Card (Madhyamik)                │
│    ☐ Marksheet (Madhyamik)                 │
│    ☐ Certificate (10th)                    │
│                                             │
│    📎 Upload File: [Drag or Click]          │
│    📋 madhyamik_admit_card.pdf (✅ Valid)   │
│                                             │
│                                             │
│ 🎓 Qualification 2: 12th (HS)               │
│ ├─ Roll Number: [______]                    │
│ ├─ Full Marks: [____] | Obtained: [____]    │
│ ├─ Percentage: 82.0% (auto-calculated)      │
│ ├─ Year: [2022]                             │
│ │                                           │
│ └─ 📄 Document Type (required):              │
│    ☑ Admit Card (HS)                        │
│    ☐ Marksheet (HS)                         │
│    ☐ Certificate (12th)                     │
│                                             │
│    📎 Upload File: [Drag or Click]          │
│    📋 HS_Admit_2022.pdf (✅ Valid)          │
│                                             │
│                                             │
│ [➕ Add Another Qualification]  [Save]      │
│                                             │
└─────────────────────────────────────────────┘
```

#### **CSV Storage for Education:**
```csv
CustomerID,..
,QualLevel_1,DocType_1,RollNo_1,RegNo_1,FullMarks_1,ObtainedMarks_1,Percentage_1,YearCompl_1,DocFilename_1,
CUST_001,10th,Admit_Madhyamik,12345,MD2020001,500,390,78.0,2020,madhyamik_admit_card.pdf,
CUST_001,12th,Admit_HS,54321,HS2022001,600,492,82.0,2022,hs_admit_card.pdf,
CUST_001,Graduate,Degree_Cert,G001,GR2024001,,,85.5,2024,graduation_certificate.pdf,
```

---

### **Question 3: How to Hand Over to AI Agent for Perfect Work?**

**This is CRITICAL!** 🎯 Here's a structured handover checklist:

---

## **6. AI AGENT HANDOVER PACKAGE**

### **6.1 What to Provide to the AI Agent**

#### **A. Complete Deliverables Package**

**Create a folder on your PC:**
```
CustomerHub_Project/
├── 📋 PRD_Complete.md (this entire document)
├── 📸 UI_Mockups/
│   ├── 1_Dashboard.png
│   ├── 2_AddNewCustomer.png
│   ├── 3_CustomerDirectory.png
│   ├── 4_SystemSettings.png
│   └── 5_BioDataGenerator.png
├── 📊 Data_Schema/
│   ├── customers_csv_structure.txt
│   ├── metadata_json_structure.txt
│   └── folder_structure_example.txt
├── 🎨 Design_Guidelines/
│   ├── color_palette.txt
│   ├── font_specs.txt
│   └── component_sizes.txt
└── 🔧 Technical_Specs/
    ├── tech_stack.md
    ├── validation_rules.md
    └── feature_checklist.md
```

#### **B. Create a Detailed Technical Brief**

Save this as `HANDOVER_BRIEF.md`:

```markdown
# CUSTOMER DATA HUB – AI AGENT DEVELOPMENT BRIEF
**Date:** July 25, 2026
**Developer:** [Your Name]
**Status:** Ready for Implementation

## PROJECT CONSTRAINTS
- **Language:** Vue.js 3.x
- **Format:** Desktop App (Electron wrapper)
- **Storage:** Local file system (CSV + JSON, NO database)
- **Scale:** 1,000+ customers
- **Portability:** Must run on any Windows/Mac PC with Node.js

## CRITICAL FEATURES (In Priority Order)

### PHASE 1 (MVP - Weeks 1-3)
1. ✅ Project setup (Vue 3 + Electron)
2. ✅ Dashboard (static + real metrics)
3. ✅ Add New Customer (form + validation)
4. ✅ Customer Directory (table + search)
5. ✅ CSV read/write functionality

### PHASE 2 (Weeks 4-5)
6. ✅ Photo & Signature upload
7. ✅ Education with dynamic doc validation
8. ✅ Document Vault (file storage)
9. ✅ Bulk Import (CSV upload)

### PHASE 3 (Week 6)
10. ✅ Bio-Data Generator (PDF + Word)
11. ✅ System Settings (backup/restore)

## KEY VALIDATION RULES (DO NOT SKIP)

### Mobile Number
- Exactly 10 digits
- Unique (warn if duplicate exists)
- Number only (no spaces, dashes)
- Validation: `^[0-9]{10}$`

### Email
-

--------------------

User prompt 5 of 8 - 7/25/2026, 10:10:34 PM:
Give Proper copy paste instruction with Compleate PRD to handover it to my AI agent

Claude Haiku 4.5:
Perfect! Let me create a **complete, copy-paste ready PRD** with detailed AI agent handover instructions.

---

# **CUSTOMER DATA HUB – COMPLETE PROJECT REQUIREMENTS DOCUMENT (PRD)**

**Version:** 1.0  
**Date:** July 25, 2026  
**Status:** Ready for AI Agent Development  
**Platform:** Vue.js 3.x Desktop Application (Electron)  
**Storage:** Local File System (CSV + JSON, NO Database)  
**Target Users:** 1,000+ customers  
**Scalability:** Cross-PC Compatible (Windows/Mac/Linux)

---

## **TABLE OF CONTENTS**

1. [Project Overview](#project-overview)
2. [Core Features & Specifications](#core-features--specifications)
3. [Detailed Feature Specifications](#detailed-feature-specifications)
4. [Data Schema & Storage](#data-schema--storage)
5. [Validation Rules & Business Logic](#validation-rules--business-logic)
6. [UI Component Specifications](#ui-component-specifications)
7. [Development Phases & Timeline](#development-phases--timeline)
8. [Technical Stack & Setup](#technical-stack--setup)
9. [AI Agent Handover Checklist](#ai-agent-handover-checklist)

---

## **PROJECT OVERVIEW**

The **Customer Data Hub** is a desktop application designed to centralize customer management with intuitive dashboards, bulk import capabilities, document storage, and automated bio-data profile generation. The system prioritizes:

- ✅ **Ease of Use** – Intuitive UI matching provided mockups
- ✅ **Data Validation** – Real-time validation on all fields
- ✅ **Privacy** – Local file storage (no cloud dependency)
- ✅ **Portability** – Run on any PC with Node.js
- ✅ **Scalability** – Handle 1,000+ customer records efficiently

---

## **CORE FEATURES & SPECIFICATIONS**

| Feature | Status | Priority | Phase | Description |
|---------|--------|----------|-------|-------------|
| **Dashboard** | MVP | High | 1 | Real-time customer metrics, activity timeline, quick navigation |
| **Add New Customer** | MVP | High | 1 | Multi-section form with validation & duplicate detection |
| **Customer Directory** | MVP | High | 1 | Searchable, filterable table with bulk operations & export |
| **Photo & Signature Upload** | MVP | High | 2 | Profile picture & digital signature file handling |
| **Education with Doc Validation** | MVP | High | 2 | Multi-level education with dynamic document type enforcement |
| **Document Vault** | MVP | Medium | 2 | Multiple file attachment & organized storage per customer |
| **Bulk Import** | MVP | High | 2 | CSV-based bulk customer upload with validation & error reporting |
| **Bio-Data Generator** | MVP | High | 3 | Template-based PDF/Word profile generation |
| **System Settings** | MVP | Medium | 3 | Backup/restore, OCR config, audit logs, system health |

---

## **DETAILED FEATURE SPECIFICATIONS**

### **FEATURE 1: DASHBOARD**

**Concept Brief:**  
Single-screen overview of customer base health, recent activities, and quick navigation to core functions.

**Layout Structure:**
```
┌──────────────────────────────────────────────────────┐
│ Customer Data Hub          [Search] [Sort By] [Admin] │
├──────────────────────────────────────────────────────┤
│ [Dashboard] [Add New Customer] [Customer Directory]  │
│ [System Settings] [Bio-Data Generator]               │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌─────────────────┐  ┌──────────────────────────┐  │
│  │ Total Customers │  │ Recently Added Customers │  │
│  │     1,568       │  │ • Rahul Sen - Dec 21,22 │  │
│  │  +32 this week  │  │ • Aarti Das - Jun 11,22 │  │
│  └─────────────────┘  │ • Aarti Das - Oct 21,23 │  │
│                       │ • Sumit Roy - Oct 13,23 │  │
│                       └──────────────────────────┘  │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │ Direct Access & Quick Actions                │   │
│  │                                              │   │
│  │ ┌──────────────┐  ┌─────────────────────┐   │   │
│  │ │      ➕      │  │ View Customer       │   │   │
│  │ │  ADD NEW     │  │ Directory           │   │   │
│  │ │  CUSTOMER    │  │                     │   │   │
│  │ └──────────────┘  └─────────────────────┘   │   │
│  │                                              │   │
│  │ ┌────────────────────┐ ┌──────────────────┐ │   │
│  │ │ System Settings    │ │ Bio-Data         │ │   │
│  │ │ ⚙️                 │ │ Generator        │ │   │
│  │ └────────────────────┘ └──────────────────┘ │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│ Recent Activity Timeline:                            │
│ • Rahul Sen - Added - Dec 21, 2022                  │
│ • Aarti Das - Edited - Oct 21, 2023                 │
│ • Sumit Roy - Generated Bio - Oct 13, 2023          │
│                                                      │
└──────────────────────────────────────────────────────┘
```

**Components:**

#### **A. Header Section**
- App Title: "Customer Data Hub"
- Search Box (searches across all customers)
- Sort By Dropdown: Name / Date / Status
- Admin label (top right)

#### **B. Metrics Widgets**

**Total Customers Widget:**
- Large number display: "1,568"
- Growth indicator: "+32 this week" (green, with up arrow)
- Click → View all customers
- Updates: Real-time on app load and after customer added

**Recently Added Customers Widget:**
- List format (max 4-5 entries)
- Display: Name + Join Date
- Format: "Rahul Sen - Dec 21, 2022"
- Clickable: Click name → View customer detail
- Updates: Real-time

#### **C. Quick Action Panel**

Large buttons for core features:
1. **ADD NEW CUSTOMER** (primary blue color, large)
   - Icon: ➕
   - Action: Navigate to "Add New Customer" page
   
2. **VIEW CUSTOMER DIRECTORY** 
   - Icon: 👁️
   - Action: Navigate to "Customer Directory" page
   
3. **SYSTEM SETTINGS**
   - Icon: ⚙️
   - Action: Navigate to "System Settings" page
   
4. **BIO-DATA GENERATOR**
   - Icon: 📄
   - Action: Navigate to "Bio-Data Generator" page

#### **D. Recent Activity Timeline (Sidebar)**
- Vertical timeline
- Last 5 actions logged
- Format: "[Name] - [Action] - [Date]"
- Actions: Added / Edited / Deleted / Generated / Imported

#### **Data Sources:**
- Customer count: Count of rows in `customers.csv`
- Weekly growth: Calculate new customers added in past 7 days
- Recently added: Sort `customers.csv` by DOJ (date of joining), descending, take top 5
- Activity: Read from `activity.json`

**Refresh Logic:**
- Load on app startup
- Refresh after each major action (add, edit, delete, import)
- Real-time updates (no polling needed)

---

### **FEATURE 2: ADD NEW CUSTOMER**

**Concept Brief:**  
Multi-section form capturing personal, financial, educational, and document data with real-time validation and duplicate detection.

**Form Structure:**
```
┌─ ADD NEW CUSTOMER ──────────────────────────────────┐
│ [← Back]                                             │
├─────────────────────────────────────────────────────┤
│                                                     │
│ 📋 CUSTOMER PERSONAL PROFILE                        │
│ ├─ First Name * [_____________]  Last Name [____]  │
│ ├─ Father's Name [___________]  Mother's Name [...] │
│ ├─ Date of Birth [________]  Gender [Dropdown ▼]  │
│ ├─ Marital Status [Dropdown ▼]  Religion [......]  │
│ ├─ Blood Group [O+▼]                               │
│ ├─ Mobile Number * [_________] ⚠️ (duplicate warn) │
│ ├─ Email ID [________________]  ⚠️ (duplicate warn)│
│ ├─ Aadhaar Number [____________] (12 digits max)  │
│ ├─ Ration Card No. [___________]  PAN [_________] │
│ │                                                  │
│ ├─ 📸 [Upload Photo]  🖊️ [Upload Signature]       │
│ │    [Photo Preview]      [Signature Preview]      │
│ │                                                  │
│ │ ──────────────────────────────────────────────  │
│ │                                                  │
│ 💰 BANK & FINANCIAL DETAILS                        │
│ ├─ Bank Name [____________]                        │
│ ├─ Account Number [______________]                 │
│ ├─ IFSC Code [__________]  ☑ Is Primary Account?  │
│ │                                                  │
│ │ ──────────────────────────────────────────────  │
│ │                                                  │
│ 📚 EDUCATION & QUALIFICATIONS                      │
│ │ 🎓 Qualification 1: [10th ▼]                     │
│ │ ├─ Roll Number [____]  Reg Number [______]      │
│ │ ├─ Full Marks [____]  Obtained [____]           │
│ │ ├─ Percentage [___%] (auto)  Year [2020]        │
│ │ ├─ Document Type: [Dropdown ▼]                  │
│ │ ├─ 📎 [Upload Doc]                              │
│ │ │                                                │
│ │ [➕ Add Another Qualification]                    │
│ │                                                  │
│ │ ──────────────────────────────────────────────  │
│ │                                                  │
│ 📍 ADDRESS DETAILS                                 │
│ ├─ Address Type [Select Type ▼]                    │
│ ├─ Street Address [_______________________________] │
│ ├─ Village/Town [___________]  Post Office [____]  │
│ ├─ District [___________]  State [_________]       │
│ ├─ Pin Code [______]                               │
│ │                                                  │
│ │ ──────────────────────────────────────────────  │
│ │                                                  │
│ 🔗 IMPORTANT WEBSITES                              │
│ ├─ 🌐 Gmail  🌐 LinkedIn  🌐 Aadhaar Bharat      │
│ │ (Click links to open in browser)                 │
│ │                                                  │
│ │ ──────────────────────────────────────────────  │
│ │                                                  │
│ 📦 DOCUMENT VAULT                                  │
│ ├─ 📎 Drag files or [Click to Upload]              │
│ │ Supported: PDF, JPG, PNG, DOCX (max 10 MB each) │
│ │                                                  │
│ │ Uploaded:                                        │
│ │ • resume.pdf (250 KB) [Delete]                   │
│ │ • aadhaar.jpg (1.2 MB) [Delete]                  │
│ │                                                  │
│ │ ──────────────────────────────────────────────  │
│ │                                                  │
│ 💼 OTHER DATA                                      │
│ ├─ Job Title [____________]  Company [_________]   │
│ ├─ Work Experience (years) [__]                    │
│ ├─ ☑ Computer Certificate?  Year [____]            │
│ │                                                  │
│ [Reset Form]  [← Previous]  [Save Customer] ✓     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### **A. CUSTOMER PERSONAL PROFILE SECTION**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **First Name** | Text Input | ✅ Yes | Non-empty, max 50 chars, letters only | "First name is required" | Primary identifier |
| **Last Name** | Text Input | ❌ No | Max 50 chars, letters only | N/A | Optional |
| **Father's Name** | Text Input | ❌ No | Max 50 chars, letters only | N/A | Optional |
| **Mother's Name** | Text Input | ❌ No | Max 50 chars, letters only | N/A | Optional |
| **Date of Birth** | Date Picker | ❌ No | Valid date, YYYY-MM-DD format | "Invalid date format" | Optional age check |
| **Gender** | Dropdown | ❌ No | Male / Female / Other / Prefer Not to Say | N/A | Optional |
| **Marital Status** | Dropdown | ❌ No | Single / Married / Divorced / Widowed / Prefer Not to Say | N/A | Optional |
| **Religion** | Dropdown | ❌ No | Hindu / Muslim / Christian / Sikh / Buddhist / Jain / Other | N/A | Predefined list |
| **Blood Group** | Dropdown | ❌ No | A+ / A- / B+ / B- / O+ / O- / AB+ / AB- / Unknown | N/A | Medical info |
| **Mobile Number** | Phone Input | ✅ Yes | Exactly 10 digits, numeric only, unique | "Mobile must be 10 digits" / "This mobile already exists (ID: CUST_XXX)" | **⚠️ Warn if duplicate** |
| **Email ID** | Email Input | ❌ No | Valid email format (user@domain.com), unique if provided | "Invalid email format" / "This email already exists (ID: CUST_XXX)" | **⚠️ Warn if duplicate** |
| **Aadhaar Number** | Text Input | ❌ No | Max 12 digits, numeric only, optional format check | "Aadhaar must be max 12 digits" | Unique ID proof |
| **Ration Card No.** | Text Input | ❌ No | Max 20 chars, alphanumeric | N/A | Optional ID |
| **PAN Number** | Text Input | ❌ No | 10 chars, format: AAAAA1234A (5 letters, 4 digits, 1 letter) | "Invalid PAN format" | Tax ID |
| **Customer Photo** | File Upload | ❌ No | JPG/PNG only, max 5 MB, recommended 400x400px | "Only JPG/PNG files allowed (max 5 MB)" | Profile picture |
| **Signature** | File Upload | ❌ No | JPG/PNG only, max 2 MB, recommended 300x150px | "Only JPG/PNG files allowed (max 2 MB)" | Digital signature |

**Validation Behavior:**
- Validate on field blur (after user exits field)
- Show error message in red below field
- Disable Save button until all required fields valid
- **Duplicate Check (Mobile & Email):**
  - Trigger AJAX search through `customers.csv`
  - If duplicate found: Show warning toast with Customer ID
  - Format: ⚠️ "Mobile +91-9876543210 already used by Rahul Sen (CUST_001)"
  - Allow user to continue (don't block submission)

---

#### **B. BANK & FINANCIAL DETAILS SECTION**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **Bank Name** | Dropdown/Text | ❌ No | Predefined list or free text, max 100 chars | N/A | Select or type |
| **Account Number** | Text Input | ❌ No | 9-18 digits, alphanumeric | "Invalid account number format" | Bank account |
| **IFSC Code** | Text Input | ❌ No | Exactly 11 chars, pattern: AAAA0AAAAAA | "IFSC must be 11 characters" | Bank branch code |
| **Is Primary Account?** | Checkbox | ❌ No | Boolean | N/A | Single primary account |

---

--------------------

User prompt 6 of 8 - 7/25/2026, 10:55:56 PM:
compleate it

Claude Haiku 4.5:
# **CUSTOMER DATA HUB – COMPLETE PROJECT REQUIREMENTS DOCUMENT (PRD)**

**Version:** 1.0  
**Date:** July 25, 2026  
**Status:** Ready for AI Agent Development  
**Platform:** Vue.js 3.x Desktop Application (Electron)  
**Storage:** Local File System (CSV + JSON, NO Database)  
**Target Users:** 1,000+ customers  
**Scalability:** Cross-PC Compatible (Windows/Mac/Linux)

---

## **TABLE OF CONTENTS**

1. [Project Overview](#project-overview)
2. [Core Features & Specifications](#core-features--specifications)
3. [Detailed Feature Specifications](#detailed-feature-specifications)
4. [Data Schema & Storage](#data-schema--storage)
5. [Validation Rules & Business Logic](#validation-rules--business-logic)
6. [UI Component Specifications](#ui-component-specifications)
7. [Development Phases & Timeline](#development-phases--timeline)
8. [Technical Stack & Setup](#technical-stack--setup)
9. [AI Agent Handover Checklist](#ai-agent-handover-checklist)

---

## **PROJECT OVERVIEW**

The **Customer Data Hub** is a desktop application designed to centralize customer management with intuitive dashboards, bulk import capabilities, document storage, and automated bio-data profile generation. The system prioritizes:

- ✅ **Ease of Use** – Intuitive UI matching provided mockups
- ✅ **Data Validation** – Real-time validation on all fields
- ✅ **Privacy** – Local file storage (no cloud dependency)
- ✅ **Portability** – Run on any PC with Node.js
- ✅ **Scalability** – Handle 1,000+ customer records efficiently

---

## **CORE FEATURES & SPECIFICATIONS**

| Feature | Status | Priority | Phase | Description |
|---------|--------|----------|-------|-------------|
| **Dashboard** | MVP | High | 1 | Real-time customer metrics, activity timeline, quick navigation |
| **Add New Customer** | MVP | High | 1 | Multi-section form with validation & duplicate detection |
| **Customer Directory** | MVP | High | 1 | Searchable, filterable table with bulk operations & export |
| **Photo & Signature Upload** | MVP | High | 2 | Profile picture & digital signature file handling |
| **Education with Doc Validation** | MVP | High | 2 | Multi-level education with dynamic document type enforcement |
| **Document Vault** | MVP | Medium | 2 | Multiple file attachment & organized storage per customer |
| **Bulk Import** | MVP | High | 2 | CSV-based bulk customer upload with validation & error reporting |
| **Bio-Data Generator** | MVP | High | 3 | Template-based PDF/Word profile generation |
| **System Settings** | MVP | Medium | 3 | Backup/restore, OCR config, audit logs, system health |

---

## **DETAILED FEATURE SPECIFICATIONS**

### **FEATURE 1: DASHBOARD**

**Concept Brief:**  
Single-screen overview of customer base health, recent activities, and quick navigation to core functions.

**Layout Structure:**
```
┌──────────────────────────────────────────────────────┐
│ Customer Data Hub          [Search] [Sort By] [Admin] │
├──────────────────────────────────────────────────────┤
│ [Dashboard] [Add New Customer] [Customer Directory]  │
│ [System Settings] [Bio-Data Generator]               │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌─────────────────┐  ┌──────────────────────────┐  │
│  │ Total Customers │  │ Recently Added Customers │  │
│  │     1,568       │  │ • Rahul Sen - Dec 21,22 │  │
│  │  +32 this week  │  │ • Aarti Das - Jun 11,22 │  │
│  └─────────────────┘  │ • Aarti Das - Oct 21,23 │  │
│                       │ • Sumit Roy - Oct 13,23 │  │
│                       └──────────────────────────┘  │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │ Direct Access & Quick Actions                │   │
│  │                                              │   │
│  │ ┌──────────────┐  ┌─────────────────────┐   │   │
│  │ │      ➕      │  │ View Customer       │   │   │
│  │ │  ADD NEW     │  │ Directory           │   │   │
│  │ │  CUSTOMER    │  │                     │   │   │
│  │ └──────────────┘  └─────────────────────┘   │   │
│  │                                              │   │
│  │ ┌────────────────────┐ ┌──────────────────┐ │   │
│  │ │ System Settings    │ │ Bio-Data         │ │   │
│  │ │ ⚙️                 │ │ Generator        │ │   │
│  │ └────────────────────┘ └──────────────────┘ │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│ Recent Activity Timeline:                            │
│ • Rahul Sen - Added - Dec 21, 2022                  │
│ • Aarti Das - Edited - Oct 21, 2023                 │
│ • Sumit Roy - Generated Bio - Oct 13, 2023          │
│                                                      │
└──────────────────────────────────────────────────────┘
```

**Components:**

#### **A. Header Section**
- App Title: "Customer Data Hub"
- Search Box (searches across all customers)
- Sort By Dropdown: Name / Date / Status
- Admin label (top right)

#### **B. Metrics Widgets**

**Total Customers Widget:**
- Large number display: "1,568"
- Growth indicator: "+32 this week" (green, with up arrow)
- Click → View all customers
- Updates: Real-time on app load and after customer added

**Recently Added Customers Widget:**
- List format (max 4-5 entries)
- Display: Name + Join Date
- Format: "Rahul Sen - Dec 21, 2022"
- Clickable: Click name → View customer detail
- Updates: Real-time

#### **C. Quick Action Panel**

Large buttons for core features:
1. **ADD NEW CUSTOMER** (primary blue color, large)
   - Icon: ➕
   - Action: Navigate to "Add New Customer" page
   
2. **VIEW CUSTOMER DIRECTORY** 
   - Icon: 👁️
   - Action: Navigate to "Customer Directory" page
   
3. **SYSTEM SETTINGS**
   - Icon: ⚙️
   - Action: Navigate to "System Settings" page
   
4. **BIO-DATA GENERATOR**
   - Icon: 📄
   - Action: Navigate to "Bio-Data Generator" page

#### **D. Recent Activity Timeline (Sidebar)**
- Vertical timeline
- Last 5 actions logged
- Format: "[Name] - [Action] - [Date]"
- Actions: Added / Edited / Deleted / Generated / Imported

#### **Data Sources:**
- Customer count: Count of rows in `customers.csv`
- Weekly growth: Calculate new customers added in past 7 days
- Recently added: Sort `customers.csv` by DOJ (date of joining), descending, take top 5
- Activity: Read from `activity.json`

**Refresh Logic:**
- Load on app startup
- Refresh after each major action (add, edit, delete, import)
- Real-time updates (no polling needed)

---

### **FEATURE 2: ADD NEW CUSTOMER**

**Concept Brief:**  
Multi-section form capturing personal, financial, educational, and document data with real-time validation and duplicate detection.

#### **A. CUSTOMER PERSONAL PROFILE SECTION**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **First Name** | Text Input | ✅ Yes | Non-empty, max 50 chars, letters only | "First name is required" | Primary identifier |
| **Last Name** | Text Input | ❌ No | Max 50 chars, letters only | N/A | Optional |
| **Father's Name** | Text Input | ❌ No | Max 50 chars, letters only | N/A | Optional |
| **Mother's Name** | Text Input | ❌ No | Max 50 chars, letters only | N/A | Optional |
| **Date of Birth** | Date Picker | ❌ No | Valid date, YYYY-MM-DD format | "Invalid date format" | Optional age check |
| **Gender** | Dropdown | ❌ No | Male / Female / Other / Prefer Not to Say | N/A | Optional |
| **Marital Status** | Dropdown | ❌ No | Single / Married / Divorced / Widowed / Prefer Not to Say | N/A | Optional |
| **Religion** | Dropdown | ❌ No | Hindu / Muslim / Christian / Sikh / Buddhist / Jain / Other | N/A | Predefined list |
| **Blood Group** | Dropdown | ❌ No | A+ / A- / B+ / B- / O+ / O- / AB+ / AB- / Unknown | N/A | Medical info |
| **Mobile Number** | Phone Input | ✅ Yes | Exactly 10 digits, numeric only, unique | "Mobile must be 10 digits" / "This mobile already exists (ID: CUST_XXX)" | **⚠️ Warn if duplicate** |
| **Email ID** | Email Input | ❌ No | Valid email format (user@domain.com), unique if provided | "Invalid email format" / "This email already exists (ID: CUST_XXX)" | **⚠️ Warn if duplicate** |
| **Aadhaar Number** | Text Input | ❌ No | Max 12 digits, numeric only, optional format check | "Aadhaar must be max 12 digits" | Unique ID proof |
| **Ration Card No.** | Text Input | ❌ No | Max 20 chars, alphanumeric | N/A | Optional ID |
| **PAN Number** | Text Input | ❌ No | 10 chars, format: AAAAA1234A (5 letters, 4 digits, 1 letter) | "Invalid PAN format" | Tax ID |
| **Customer Photo** | File Upload | ❌ No | JPG/PNG only, max 5 MB, recommended 400x400px | "Only JPG/PNG files allowed (max 5 MB)" | Profile picture |
| **Signature** | File Upload | ❌ No | JPG/PNG only, max 2 MB, recommended 300x150px | "Only JPG/PNG files allowed (max 2 MB)" | Digital signature |

**Validation Behavior:**
- Validate on field blur (after user exits field)
- Show error message in red below field
- Disable Save button until all required fields valid
- **Duplicate Check (Mobile & Email):**
  - Trigger search through `customers.csv`
  - If duplicate found: Show warning toast with Customer ID
  - Format: ⚠️ "Mobile +91-9876543210 already used by Rahul Sen (CUST_001)"
  - Allow user to continue (don't block submission)

---

#### **B. BANK & FINANCIAL DETAILS SECTION**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **Bank Name** | Dropdown/Text | ❌ No | Predefined list or free text, max 100 chars | N/A | Select or type |
| **Account Number** | Text Input | ❌ No | 9-18 digits, alphanumeric | "Invalid account number format" | Bank account |
| **IFSC Code** | Text Input | ❌ No | Exactly 11 chars, pattern: AAAA0AAAAAA | "IFSC must be 11 characters" | Bank branch code |
| **Is Primary Account?** | Checkbox | ❌ No | Boolean | N/A | Single primary account |

**Predefined Bank Names:**
- HDFC Bank
- ICICI Bank
- Axis Bank
- State Bank of India (SBI)
- IDBI Bank
- PUNJAB NATIONAL BANK
- Bank of India
- Union Bank
- Canara Bank
- Indian Overseas Bank
- Other (free text)

---

#### **C. EDUCATION & QUALIFICATIONS SECTION**

**Concept:** Repeating sections for each education level with dynamic document validation.

**Education Levels Available:**
1. **8th Standard** – Primary qualification
2. **10th/Madhyamik** – Secondary
3. **12th/HS (Higher Secondary)** – Senior secondary
4. **Diploma** – Vocational
5. **Graduate** – Bachelor's degree
6. **Post-Graduate** – Master's degree

**Education Entry Structure:**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **Qualification Level** | Dropdown | ✅ Yes (per entry) | 8th / 10th / 12th / Diploma / Graduate / Post-Graduate | "Select a level" | Can add multiple |
| **Roll Number** | Text Input | ❌ No | Max 30 chars, alphanumeric | N/A | Student ID |
| **Registration Number** | Text Input | ❌ No | Max 30 chars, alphanumeric | N/A | Official reg ID |
| **Full Marks** | Number Input | ❌ No | Positive integer | "Must be a positive number" | Total marks |
| **Obtained Marks** | Number Input | ❌ No | Positive integer, ≤ Full Marks | "Must be ≤ Full Marks" | Achieved marks |
| **Percentage** | Number Display | ❌ No | Auto-calculated: (Obtained / Full) × 100 | N/A | Read-only, 2 decimals |
| **Year of Completion** | Year Picker | ❌ No | Valid year (1980–2026) | "Invalid year" | Graduation year |
| **Document Type (Dynamic)** | Dropdown | ✅ YES (required if upload) | Depends on level (see table below) | "Select document type" | Dynamic based on level |
| **Document Upload** | File Upload | ❌ No | PDF, JPG, PNG, DOCX; max 10 MB | "File too large or unsupported format" | Admit / Marksheet / Certificate |

**Dynamic Document Type Validation Table:**

| Education Level | Allowed Document Types | Required? | Notes |
|-----------------|------------------------|-----------|-------|
| **8th Standard** | Admit Card, Marksheet, Passing Certificate | ❌ No | Flexible |
| **10th/Madhyamik** | Madhyamik Admit Card, Madhyamik Marksheet, Madhyamik Pass Certificate | ✅ YES if uploading | Level-specific docs |
| **12th/HS** | HS Admit Card, HS Marksheet, HS Certificate | ✅ YES if uploading | Level-specific docs |
| **Diploma** | Diploma Admit, Diploma Marksheet, Diploma Certificate | ✅ YES if uploading | Vocational/technical |
| **Graduate** | Bachelor Admit, Bachelor Marksheet, Degree Certificate | ✅ YES if uploading | University degree |
| **Post-Graduate** | Master Admit, Master Marksheet, Degree Certificate | ✅ YES if uploading | Advanced degree |

**Behavior:**
- Each education level can be added once (no duplicates)
- When user selects "10th/Madhyamik", document dropdown auto-filters to show only Madhyamik documents
- Document upload validation checks file type against selected document type
- Calculate percentage in real-time as user types
- Show "➕ Add Another Qualification" button after each entry (max 6 entries)
- Allow delete of individual education entries

---

#### **D. ADDRESS DETAILS SECTION**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **Address Type** | Dropdown | ❌ No | Current / Permanent / Both | N/A | Location category |
| **Street Address** | Text Area | ❌ No | Max 200 chars | N/A | Full address |
| **Village/Town** | Text Input | ❌ No | Max 50 chars | N/A | Town name |
| **Post Office** | Text Input | ❌ No | Max 50 chars | N/A | Postal area |
| **District** | Dropdown/Text | ❌ No | Indian districts or free text | N/A | Administrative division |
| **State** | Dropdown | ❌ No | Indian states (28 states) | N/A | Predefined list |
| **Pin Code** | Text Input | ❌ No | Exactly 6 digits | "Pin code must be 6 digits" | Postal code |

**Predefined States (India):**
Andhra Pradesh, Arunachal Pradesh, Assam, Bihar, Chhattisgarh, Goa, Gujarat, Haryana, Himachal Pradesh,

--------------------

User prompt 7 of 8 - 7/27/2026, 9:42:06 AM:
give the rest of it

Claude Haiku 4.5:
# **CUSTOMER DATA HUB – COMPLETE PRD (CONTINUED)**

**Predefined States (India):**
Andhra Pradesh, Arunachal Pradesh, Assam, Bihar, Chhattisgarh, Goa, Gujarat, Haryana, Himachal Pradesh, Jharkhand, Karnataka, Kerala, Madhya Pradesh, Maharashtra, Manipur, Meghalaya, Mizoram, Nagaland, Odisha, Punjab, Rajasthan, Sikkim, Tamil Nadu, Telangana, Tripura, Uttar Pradesh, Uttarakhand, West Bengal, Jammu & Kashmir, Ladakh

---

#### **E. IMPORTANT WEBSITES SECTION**

Quick access links to predefined websites (opens in default browser):

| Website | URL | Icon | Action |
|---------|-----|------|--------|
| **Gmail** | https://mail.google.com | 📧 | Click → Open Gmail in browser |
| **LinkedIn** | https://www.linkedin.com | 💼 | Click → Open LinkedIn in browser |
| **Aadhaar Bharat** | https://uidai.gov.in | 🆔 | Click → Open Aadhaar official portal |

**Implementation:**
- Display as three clickable buttons/links
- Use `electron.shell.openExternal(url)` for Electron
- Add hover effect to indicate clickable

---

#### **F. DOCUMENT VAULT SECTION**

**Concept Brief:**  
Drag-and-drop file upload area for storing multiple documents per customer.

| Feature | Specification | Notes |
|---------|---------------|-------|
| **Upload Method** | Drag-and-drop + Click to browse | Intuitive UX |
| **Supported Formats** | PDF, JPG, PNG, DOCX | Common business files |
| **File Size Limit** | 10 MB per file | Prevents large files |
| **Total Files Per Customer** | Unlimited | Scalable |
| **Storage Path** | `CustomerHub/Documents/CUST_[ID]/` | Organized by customer ID |
| **File Naming** | Original filename preserved | User can rename after upload |

**Display:**
- Drag-and-drop zone with clear label
- Shows list of uploaded files
- Each file displays: Name, Size (in KB/MB), Upload Date
- Delete button per file
- Progress bar during upload

**Validation:**
- Check file extension (.pdf, .jpg, .jpeg, .png, .docx)
- Check file size (max 10 MB)
- Show error toast if invalid: "File 'resume.exe' not supported. Only PDF, JPG, PNG, DOCX allowed."

---

#### **G. OTHER DATA SECTION**

| Field | Type | Required | Validation | Error Message | Notes |
|-------|------|----------|-----------|---------------|-------|
| **Job Title** | Text Input | ❌ No | Max 100 chars | N/A | Current profession |
| **Company Name** | Text Input | ❌ No | Max 100 chars | N/A | Employer |
| **Work Experience (Years)** | Number Input | ❌ No | 0-70, integer | "Enter valid years" | Years in profession |
| **Computer Certificate?** | Checkbox | ❌ No | Boolean | N/A | Has certificate |
| **Certificate Year** | Year Picker | ❌ No | Valid year (1980–2026) | "Invalid year" | When obtained |

---

#### **H. FORM FOOTER & ACTIONS**

| Button | Action | Validation | Notes |
|--------|--------|-----------|-------|
| **[← Back]** | Return to Dashboard | No validation | Warn if unsaved changes |
| **[Reset Form]** | Clear all fields | Confirm action | Reload blank form |
| **[Save Customer]** | Submit form and create customer | Required fields valid | Generate CUST_ID, save to CSV, create Documents folder, log activity |

**Save Logic:**
1. Validate all required fields (First Name, Mobile)
2. Check for duplicates (Mobile, Email, Aadhaar)
3. Generate unique Customer ID: `CUST_[TIMESTAMP]_[RANDOM_4_DIGITS]` (e.g., CUST_20260725_1847_8392)
4. Create folder: `CustomerHub/Documents/CUST_[ID]/`
5. Save uploaded files to folder
6. Add new row to `customers.csv`
7. Update `metadata.json` (last modified, total count)
8. Log activity in `activity.json`: "Customer [Name] added"
9. Show success toast: "Customer Rahul Sen (CUST_[ID]) saved successfully!"
10. Navigate to Customer Directory
11. Highlight newly added customer in list

---

### **FEATURE 3: CUSTOMER DIRECTORY**

**Concept Brief:**  
Searchable, sortable, filterable table of all customers with bulk operations, export, and inline editing.

**Layout:**
```
┌─ CUSTOMER DIRECTORY ────────────────────────────────┐
│ [← Back]                                             │
├─────────────────────────────────────────────────────┤
│ 📋 All Customers (1,568)                             │
│                                                     │
│ [🔍 Search by Name/Mobile] [Filter ▼] [Sort ▼]    │
│ [Export to Excel] [Bulk Delete] [Bulk Status]      │
│                                                     │
│ ┌──────────────────────────────────────────────┐   │
│ │ ☑ │ ID      │ Name        │ Mobile  │ Email  │   │
│ ├────┼─────────┼─────────────┼─────────┼────────┤   │
│ │ ☑ │ CUST001 │ Rahul Sen   │ 98765.. │ rahul@ │   │
│ │ ☐ │ CUST002 │ Aarti Das   │ 98765.. │ aarti@ │   │
│ │ ☐ │ CUST003 │ Sumit Roy   │ 98765.. │ sumit@ │   │
│ │ ☐ │ CUST004 │ Priya Nath  │ 98765.. │ priya@ │   │
│ │ ☑ │ CUST005 │ Amit Kumar  │ 98765.. │ amit@  │   │
│ │... │ ...     │ ...         │ ...     │ ...    │   │
│ └──────────────────────────────────────────────┘   │
│                                                     │
│ [< Prev] [1] [2] [3] [4] [5] ... [Next >]          │
│ Showing 1–50 of 1,568 records                       │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### **A. TABLE COLUMNS**

| Column | Width | Sortable | Filterable | Content | Actions |
|--------|-------|----------|-----------|---------|---------|
| **Checkbox** | 5% | ❌ No | ❌ No | Select row | Multi-select for bulk ops |
| **ID** | 12% | ✅ Yes | ✅ Yes | CUST_001 | Click → View detail |
| **Name** | 20% | ✅ Yes | ✅ Yes | Rahul Sen | Click → View detail |
| **Mobile** | 15% | ✅ Yes | ✅ Yes | 9876543210 (masked as 98765**) | Click → View detail |
| **Email** | 20% | ✅ Yes | ✅ Yes | rahul@gmail.com (masked as rahul@*) | Click → View detail |
| **Status** | 10% | ✅ Yes | ✅ Yes | Visiting / Not Visiting / Incomplete Data | Dropdown to change |
| **Last Updated** | 12% | ✅ Yes | ✅ Yes | Dec 21, 2022 | N/A |
| **Actions** | 6% | ❌ No | ❌ No | 👁️ View / ✎ Edit / 🗑️ Delete | Inline buttons |

#### **B. SEARCH & FILTER CONTROLS**

**Search Box:**
- Real-time search across Name + Mobile + Email + ID
- Highlights matching results
- Shows "0 results" if no match
- Case-insensitive

**Filter Dropdown:**

| Filter Type | Options | Behavior |
|-------------|---------|----------|
| **Status** | Visiting / Not Visiting / Incomplete Data / All | Filter rows by status |
| **Has Documents** | Yes / No / All | Show only customers with/without docs |
| **Has Email** | Yes / No / All | Filter by email presence |
| **Date Range** | Last 7 days / Last 30 days / Last 90 days / All | Filter by creation date |

**Sort Dropdown:**

| Sort Option | Default | Behavior |
|-------------|---------|----------|
| **Name (A-Z)** | ❌ No | Alphabetical ascending |
| **Name (Z-A)** | ❌ No | Alphabetical descending |
| **Date Added (Newest)** | ✅ YES | Newest first |
| **Date Added (Oldest)** | ❌ No | Oldest first |
| **Mobile** | ❌ No | Numeric ascending |
| **Status** | ❌ No | Custom order |

#### **C. BULK OPERATIONS**

**When rows selected:**
- Show "X rows selected" indicator
- Enable bulk action buttons

| Button | Action | Confirmation | Result |
|--------|--------|--------------|--------|
| **[Export to Excel]** | Download selected rows as .xlsx | No confirmation | Generate Excel file with all customer data, formatted nicely |
| **[Bulk Delete]** | Delete selected customers | "Delete 5 customers? This cannot be undone." | Remove from CSV, delete Documents folders, log activity |
| **[Bulk Change Status]** | Change status of all selected | Select new status → Confirm | Update Status column for each selected row |

**Export Format:**
- Filename: `CustomerHub_Export_[DATE]_[TIME].xlsx`
- Sheets: Customers, Education, Bank Details, Addresses
- Columns: All captured data
- Formatting: Headers bolded, alternating row colors

#### **D. ROW ACTIONS**

**View Customer (👁️ Button):**
- Open read-only view of customer profile
- Display all sections: Personal, Bank, Education, Address, Documents
- Show document preview (thumbnails)
- Allow download of documents
- Back button to directory

**Edit Customer (✎ Button):**
- Open form pre-filled with existing data
- Allow modification of all fields
- Same validation as Add New Customer
- Save changes to CSV
- Log activity: "Customer [Name] edited"

**Delete Customer (🗑️ Button):**
- Show confirmation: "Delete Rahul Sen? This cannot be undone."
- Delete from CSV
- Delete Documents folder
- Log activity: "Customer [Name] deleted"
- Refresh table

#### **E. PAGINATION**

- **Default:** 50 records per page
- Options: 25 / 50 / 100 records per page
- Show: "Showing 1–50 of 1,568 records"
- Navigation: [< Prev] [Page Numbers] [Next >]
- Keyboard support: Arrow keys to navigate

#### **F. STATUS MANAGEMENT**

**Status Options:**
1. **Visiting** – Active customer
2. **Not Visiting** – Inactive / dormant
3. **Incomplete Data** – Missing required information

**Change Status:**
- Click on status cell → dropdown appears
- Select new status
- Auto-save to CSV
- Log activity

---

### **FEATURE 4: BULK IMPORT**

**Concept Brief:**  
Upload CSV file with multiple customers, validate data, preview, and import with error reporting.

**Layout:**
```
┌─ BULK IMPORT ──────────────────────────────────────┐
│ [← Back]                                            │
├────────────────────────────────────────────────────┤
│ 📥 UPLOAD CSV FILE                                 │
│                                                    │
│ ┌──────────────────────────────────────────────┐  │
│ │ 📄 Drag CSV file here or [Click to upload]   │  │
│ │                                              │  │
│ │ Format: customers.csv with columns:          │  │
│ │ FirstName, LastName, Mobile, Email,          │  │
│ │ BankName, AccountNo, etc.                    │  │
│ └──────────────────────────────────────────────┘  │
│                                                    │
│ [Upload Example Template] [View Format Guide]    │
│                                                    │
│ ──────────────────────────────────────────────    │
│                                                    │
│ 🔍 VALIDATION RESULTS                             │
│ File: customers_bulk.csv (245 KB)                 │
│ Rows: 150 total                                   │
│ ✅ Valid: 148 rows                                │
│ ⚠️ Warnings: 2 rows (duplicates)                  │
│ ❌ Errors: 0 rows                                 │
│                                                    │
│ ──────────────────────────────────────────────    │
│                                                    │
│ 📋 PREVIEW (Valid Records)                        │
│ ┌──────────────────────────────────────────────┐  │
│ │ FirstName │ Mobile │ Email │ Bank │ Status   │  │
│ ├───────────┼────────┼───────┼──────┼──────────┤  │
│ │ Rahul     │ 98765.. │ r...  │ HDFC │ ✅ OK    │  │
│ │ Aarti     │ 98765.. │ a...  │ ICICI│ ✅ OK    │  │
│ │ Sumit     │ 98765.. │ s...  │ SBI  │ ⚠️ DUP   │  │
│ │ ...       │ ...     │ ...   │ ...  │ ...      │  │
│ └──────────────────────────────────────────────┘  │
│                                                    │
│ ⚠️ WARNINGS & ERRORS                              │
│ • Row 15: Mobile "1234567890" already exists     │
│   (CUST_001 - Rahul Sen)                         │
│ • Row 42: Email "aarti@gmail.com" already exists │
│   (CUST_002 - Aarti Das)                         │
│                                                    │
│ ──────────────────────────────────────────────    │
│                                                    │
│ 🎯 IMPORT OPTIONS                                 │
│ ☑ Import Valid Records Only (148 rows)           │
│ ☑ Skip Duplicates (2 rows will be skipped)       │
│ ☑ Create Activity Log for this import            │
│                                                    │
│ [Cancel] [← Back] [Import 148 Records] ✓         │
│                                                    │
└────────────────────────────────────────────────────┘
```

#### **A. UPLOAD & VALIDATION**

**Supported Format:**
- File: `.csv` (comma-separated values)
- Encoding: UTF-8
- Max size: 50 MB

**Required CSV Columns:**
```
FirstName, LastName, FatherName, MotherName, DOB, Gender, MaritalStatus, 
Religion, BloodGroup, Mobile, Email, AadhaarNumber, RationCardNo, PAN,
BankName, AccountNumber, IFSC, IsPrimaryAccount,
JobTitle, Company, WorkExperience, ComputerCert, CertYear,
AddressType, StreetAddress, Village, PostOffice, District, State, PinCode,
EducationLevel, RollNumber, RegNumber, FullMarks, ObtainedMarks, 
YearOfCompletion, DocumentType
```

**CSV Template Download:**
- Provide downloadable template with column headers
- Include example rows
- Show validation rules as comments

#### **B. VALIDATION LOGIC**

**Per-Row Validation:**

| Field | Rule | Error Type | Message |
|-------|------|-----------|---------|
| **FirstName** | Non-empty, ≤50 chars | Error | "First name missing or too long" |
| **Mobile** | Exactly 10 digits, numeric, unique | Error/Warning | "Invalid mobile" / "Duplicate mobile (CUST_001)" |
| **Email** | Valid format if provided, unique | Warning | "Duplicate email (CUST_002)" |
| **AadhaarNumber** | ≤12 digits, numeric | Warning | "Invalid Aadhaar format" |
| **BankName** | Max 100 chars | Warning | "Bank name too long" |
| **EducationLevel** | Must be in predefined list | Error | "Invalid education level" |
| **State** | Must be valid Indian state | Error | "Invalid state" |
| **PinCode** | 6 digits if provided | Warning | "Pin code must be 6 digits" |

--------------------

User prompt 8 of 8 - 7/27/2026, 9:46:42 AM:
is it complete ?

Claude Haiku 4.5:
No, it's **not complete yet**. Let me continue from where it stopped. I'll provide the remaining sections:
Here is the **COMPLETE PRD** — all remaining sections:

---

## **FEATURE 4: BULK IMPORT (CONTINUED)**

#### **C. IMPORT WORKFLOW**

**Step 1: File Upload**
- Accept `.csv` file via drag-and-drop or file picker
- Show file name and size

**Step 2: Parse & Validate**
- Read CSV file row by row
- Validate against rules
- Count: Valid rows, Warnings, Errors
- Display summary

**Step 3: Duplicate Detection**
- Check Mobile against existing `customers.csv`
- Check Email against existing records
- Flag as warning with matching Customer ID
- Allow user to skip or force-import

**Step 4: Preview**
- Show table of valid records
- Highlight warning rows in yellow
- Show error rows in red (disabled for import)
- Scrollable preview

**Step 5: Confirmation & Import**
- Checkbox: "Import Valid Records Only"
- Checkbox: "Skip Duplicates"
- Show count: "Import 148 of 150 records"
- Click [Import] → Process all valid rows
- Create customer folders for each
- Log activity: "Bulk import: 148 customers added"
- Show success toast: "Successfully imported 148 customers"

#### **D. IMPORT OUTPUT**

**For Each Valid Row:**
1. Generate unique Customer ID: `CUST_[TIMESTAMP]_[RANDOM]`
2. Create folder: `CustomerHub/Documents/CUST_[ID]/`
3. Add row to `customers.csv`
4. Update `metadata.json` (count, last modified)
5. Log in `activity.json`: action type "bulk_import"

**Activity Log Entry:**
```
{
  "type": "bulk_import",
  "date": "2026-07-25",
  "time": "14:32:15",
  "filename": "customers_bulk.csv",
  "recordsImported": 148,
  "recordsSkipped": 2,
  "duration": "3.5 seconds"
}
```

---

### **FEATURE 5: BIO-DATA GENERATOR**

**Concept Brief:**  
Generate professional PDF/Word documents with customer profile data from customizable templates.

**Layout:**
```
┌─ BIO-DATA GENERATOR ───────────────────────────────┐
│ [← Back]                                            │
├────────────────────────────────────────────────────┤
│ 📄 SELECT CUSTOMER                                 │
│                                                    │
│ [Search/Select Customer: ________▼]                │
│ (Shows: Rahul Sen - CUST_001)                      │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 🎨 CHOOSE TEMPLATE                                │
│                                                    │
│ ┌──────────────┐  ┌──────────────┐  ┌──────────┐  │
│ │  Template 1  │  │  Template 2  │  │ Template │  │
│ │   Standard   │  │   Academic   │  │    3     │  │
│ │   Profile    │  │   Focus      │  │ Minimal  │  │
│ │   [Preview]  │  │   [Preview]  │  │[Preview] │  │
│ │   ☑ Select   │  │   ☐ Select   │  │ ☐ Select │  │
│ └──────────────┘  └──────────────┘  └──────────┘  │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ ⚙️ CUSTOMIZE SECTIONS                             │
│ ☑ Personal Information      ☑ Bank Details        │
│ ☑ Education Qualifications  ☑ Address             │
│ ☑ Work Experience           ☑ Documents           │
│ ☑ Photo & Signature         ☑ Family Details      │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 💾 OUTPUT FORMAT                                  │
│ ☑ PDF Document    ☐ Word Document (.docx)        │
│                                                    │
│ Filename: Bio_Rahul_Sen_CUST_001_[DATE].pdf       │
│                                                    │
│ [Preview Document] [Cancel] [Generate & Download] │
│                                                    │
└────────────────────────────────────────────────────┘
```

#### **A. CUSTOMER SELECTION**

- Dropdown/autocomplete search
- Show customer name + ID
- Display selected customer details (optional preview card)
- Required to proceed

#### **B. TEMPLATE SELECTION**

**Template 1: Standard Profile (Default)**
- Professional bio-data layout
- All sections included
- Standard fonts and styling
- Photo on left, details on right

**Template 2: Academic Focus**
- Emphasizes education qualifications
- Detailed education section with grades
- Work experience highlighted
- Certificates section prominent

**Template 3: Minimal**
- Compact, one-page format
- Essential info only
- Fits on single sheet
- Clean, minimal design

**Template Preview:**
- Show thumbnail preview of each template
- Click [Preview] to open full mock document
- Displays sample data

#### **C. SECTION CUSTOMIZATION**

Allow user to toggle sections on/off:

| Section | Default | Include in All Templates |
|---------|---------|--------------------------|
| Personal Information | ✅ On | Yes |
| Education Qualifications | ✅ On | Yes |
| Bank Details | ✅ On | Yes |
| Address | ✅ On | Yes |
| Work Experience | ✅ On | Yes |
| Documents | ✅ On | Yes |
| Photo & Signature | ✅ On | Yes |
| Family Details (Parent names) | ❌ Off | Optional |

#### **D. OUTPUT FORMAT**

| Format | Extension | Notes | Behavior |
|--------|-----------|-------|----------|
| **PDF** | .pdf | Professional, read-only | Default, recommended |
| **Word** | .docx | Editable document | Allow user customization |

**Libraries:**
- PDF: `pdfkit` or `html2pdf.js`
- Word: `docx` library

#### **E. FILE NAMING & STORAGE**

**Filename Format:**
```
Bio_[FirstName]_[LastName]_[CUST_ID]_[DATE].pdf
Example: Bio_Rahul_Sen_CUST_001_20260725.pdf
```

**Storage Path:**
```
CustomerHub/BioDatas/[CUST_ID]/
CustomerHub/BioDatas/CUST_001/Bio_Rahul_Sen_CUST_001_20260725.pdf
```

#### **F. GENERATION PROCESS**

1. User selects customer + template + sections
2. Click [Generate & Download]
3. App fetches customer data from CSV
4. Render selected sections into template
5. Generate PDF/Word file
6. Save to `CustomerHub/BioDatas/[CUST_ID]/`
7. Download file to user's Downloads folder
8. Show success toast: "Bio-data for Rahul Sen generated successfully!"
9. Log activity: "Bio-data generated for [Name]"

**Document Content per Section:**

**Personal Information Section:**
- Full Name, Date of Birth, Age, Gender
- Marital Status, Religion, Blood Group
- Contact: Mobile, Email
- Government IDs: Aadhaar, PAN, Ration Card

**Education Section:**
- Table format with columns:
  - Level | Roll No | Reg No | Full Marks | Obtained | Percentage | Year
- One row per qualification

**Bank Details Section:**
- Bank Name, Account Number, IFSC Code
- Primary Account: Yes/No

**Address Section:**
- Complete address with state, pin code

**Work Experience Section:**
- Job Title, Company, Years of Experience
- Computer Certificate: Yes/No (Year)

**Photo & Signature:**
- Embedded images (if available)
- Small size, top-right corner

---

### **FEATURE 6: SYSTEM SETTINGS**

**Concept Brief:**  
Administrative controls for backup, restore, OCR configuration, audit logs, and system health.

**Layout:**
```
┌─ SYSTEM SETTINGS ──────────────────────────────────┐
│ [← Back]                                            │
├────────────────────────────────────────────────────┤
│                                                    │
│ [Backup & Restore] [OCR Config] [Audit Logs]     │
│ [System Health] [Data Management]                 │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 💾 BACKUP & RESTORE                               │
│                                                    │
│ Last Backup: Dec 21, 2022 at 14:32 (6 months ago) │
│ Backup Size: 125 MB                               │
│ Location: /Documents/CustomerHub_Backups/         │
│                                                    │
│ ┌────────────────────────────────────────────┐   │
│ │ ☑ Auto-backup enabled (Daily at 02:00 AM) │   │
│ └────────────────────────────────────────────┘   │
│                                                    │
│ [Create Backup Now] [View Backups] [Restore]     │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 🔍 OCR CONFIGURATION (Tesseract)                  │
│                                                    │
│ Status: ✅ Installed (v5.2.0)                      │
│ Path: C:\Program Files\Tesseract-OCR\             │
│                                                    │
│ ☑ Enable OCR for document scanning                │
│ Language: [English ▼]  [Add Language]             │
│                                                    │
│ [Test OCR] [Reconfigure] [Reinstall]              │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 📋 AUDIT LOGS                                     │
│                                                    │
│ Total Events: 15,847                              │
│ Date Range: Dec 20, 2022 – Jul 25, 2026           │
│                                                    │
│ [Export All Logs] [View Recent 100] [Clear Logs]  │
│                                                    │
│ Last 10 Events:                                    │
│ • Jul 25, 2026 14:32 - Customer CUST_001 edited   │
│ • Jul 25, 2026 14:15 - Bulk import: 148 rows      │
│ • Jul 24, 2026 23:45 - Customer CUST_005 deleted  │
│ • Jul 24, 2026 18:22 - Backup created (125 MB)    │
│ ...                                                │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 🏥 SYSTEM HEALTH                                  │
│                                                    │
│ Total Customers: 1,568                            │
│ Total Documents: 3,245                            │
│ Total Size: 2.3 GB                                │
│ Database (CSV) Size: 12 MB                        │
│ Memory Usage: 245 MB / 8 GB                       │
│ Disk Free Space: 150 GB                           │
│                                                    │
│ Status: ✅ All systems operational                │
│                                                    │
│ [Generate Report] [Cleanup Orphaned Files]        │
│                                                    │
│ ──────────────────────────────────────────────────  │
│                                                    │
│ 🗂️ DATA MANAGEMENT                                │
│                                                    │
│ [Export All Data] [Import Data] [Reset Application]
│                                                    │
└────────────────────────────────────────────────────┘
```

#### **A. BACKUP & RESTORE**

**Backup Details:**
- Last backup date/time
- Backup size
- Auto-backup enabled (default: Daily at 2:00 AM)
- Manual backup option

**Backup Contents:**
```
CustomerHub_Backup_[DATE]_[TIME].zip
├── Data/
│   ├── customers.csv
│   ├── metadata.json
│   └── activity.json
├── Documents/
│   ├── CUST_001/
│   ├── CUST_002/
│   └── ...
└── BioDatas/
    ├── CUST_001/
    └── ...
```

**Backup Location:**
- Default: `~/Documents/CustomerHub_Backups/`
- User can change location in settings
- Store up to 10 backups (auto-rotate old ones)

**Restore Process:**
1. Click [Restore]
2. Select backup file from list
3. Confirm: "This will replace all current data. Continue?"
4. Restore all files to original locations
5. Show success: "Data restored from backup [DATE]"

#### **B. OCR CONFIGURATION**

**Purpose:**
- Enable document scanning and text extraction
- Support for uploaded documents

**Configuration:**
- **Tesseract-OCR Status:** Installed / Not Installed
- **Version:** Display current version
- **Path:** Show installation path
- **Toggle:** Enable/Disable OCR
- **Language:** English (default), add more languages
- **Test Button:** Run OCR on sample document

**Behavior:**
- Check Tesseract installation on app startup
- If not found, show prompt: "Tesseract-OCR not installed. [Download] [Manual Install]"
- Log OCR operations in activity log

#### **C. AUDIT LOGS**

**Log Entry Format:**
```json
{
  "timestamp": "2026-07-25T14:32:15Z",
  "action": "customer_added",
  "userId": "admin",
  "details": {
    "customerId": "CUST_001",
    "customerName": "Rahul Sen",
    "fieldsModified": ["name", "mobile", "email"]
  },
  "ipAddress": "local",
  "systemVersion": "1.0.0"
}
```

**Logged Actions:**
- Customer Added
- Customer Edited
- Customer Deleted
- Customer Status Changed
- Bulk Import
- Bio-Data Generated
- Document Uploaded
- Document Deleted
- Backup Created
- Data Restored
- Settings Changed
- File Exported

**Display:**
- Table with columns: Date | Time | Action | User | Details
- Searchable by date, action type, customer
- Export to CSV
- Retention: Keep all logs (no deletion, only manual clear)

#### **D. SYSTEM HEALTH**

**Metrics:**
- Total customers: Count from CSV
- Total documents: Count files in Documents/ folder
- Total size: Sum of all files
- Database size: Size of customers.csv
- Memory usage: Current process memory
- Disk free space: System disk space available
- Backup status: Last backup date

**Health Indicators:**
- ✅ Green: All systems normal
- ⚠️ Yellow: Warning (e.g., low disk space < 10GB)
- ❌ Red: Critical (e.g., no disk space, CSV corrupted)

**Actions:**
- [Generate Report] → Export system health summary as PDF
- [Cleanup Orphaned Files] → Remove documents with no matching customer

#### **E. DATA MANAGEMENT**

| Action | Description | Confirmation | Result |
|--------|-------------|--------------|--------|
| **Export All Data** | Download entire database as ZIP | No | Create ZIP with all customers, docs, metadata |
| **Import Data** | Upload exported ZIP to restore | Overwrite existing? | Restore all data from ZIP |
| **Reset Application** | Delete all data and restart | "Delete ALL data? This cannot be undone." | Clear all folders, reset to fresh state |

---

## **DATA SCHEMA & STORAGE**

### **Directory Structure**

```
CustomerHub/
├── Data/
│   ├── customers.csv
│   ├── metadata.json
│   └── activity.json
├── Documents/
│   ├── CUST_001/
│   │   ├── resume.pdf
│   │   ├── photo.jpg
│   │   ├── signature.png
│   │   └── aadhaar.jpg
│   ├── CUST_002/
│   └── CUST_XXX/
├── BioDatas/
│   ├── CUST_001/
│   │   └── Bio_Rahul_Sen_CUST_001_20260725.pdf
│   └── CUST_XXX/
├── Backups/
│   ├── CustomerHub_Backup_20260715_140000.zip
│   └── CustomerHub_Backup_20260720_020000.zip
└── Logs/
    └── activity.json
```

### **CSV Schema: customers.csv**

```csv
ID,FirstName,LastName,FatherName,MotherName,DOB,Gender,MaritalStatus,Religion,
