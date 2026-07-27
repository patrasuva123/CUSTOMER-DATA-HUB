# Customer Data Hub - Clarification Interview Session
**Date:** July 27, 2026  
**Status:** In Progress (17/21 questions answered)
**Purpose:** Gather detailed requirements before AI agent development begins

---

## Interview Questions & Answers

### Round 1: Technology & Deployment

**Q1. Operating System Support** ✅
- **Answer:** A) Windows only
- **Decision:** Build as Windows desktop app (.exe installer)

**Q2. Data Storage Structure** ✅
- **Answer:** B) Multiple CSV files (split by category)
- **Decision:** customers.csv, education.csv, documents.csv, addresses.csv, metadata.json

**Q3. Backup Strategy** ✅
- **Answer:** D) Manual backup only
- **Decision:** User clicks "Backup Now" button in System Settings

**Q4. Photo Upload & Cropping Tool** ✅
- **Answer:** A) Show a built-in crop tool
- **Decision:** User can drag, resize, and rotate photos before saving

**Q5. Education Document Validation - Upload Timing** ✅
- **Answer:** C) Optional BUT with warning
- **Decision:** User can save education record without document, app shows yellow warning badge

**Q6. Document Naming Convention - Enforcement** ✅
- **Answer:** B) Suggest naming pattern
- **Decision:** App shows hint but accepts any PDF/JPG/PNG name

**Q7. Bulk Import - Duplicate Handling** ✅
- **Answer:** B) Show warning before import
- **Decision:** Display list of duplicates found, let user review and decide

**Q8. Bulk Import - Partial Success Handling** ✅
- **Answer:** B) Show error preview and ask confirmation
- **Decision:** Display error summary and let user decide to import anyway

**Q9. Bio-Data Generator - PDF Library** ✅
- **Answer:** B) puppeteer
- **Decision:** Use Puppeteer for HTML-to-PDF rendering with professional formatting

**Q10. Bio-Data Generator - Word Document Output** ✅
- **Answer:** A) Fully editable
- **Decision:** User can open in Microsoft Word and modify text, formatting, add notes freely

**Q11. Bio-Data Generator - Template Customization** ✅
- **Answer:** C) Fully custom template builder
- **Decision:** User can drag-drop fields, choose colors, add logo, customize layout

**Q12. Bio-Data Save Location** ✅
- **Answer:** B) Let user choose location each time
- **Decision:** Show "Save As" dialog every time for maximum user control

**Q13. System Settings - Audit Logging Detail** ✅
- **Answer:** A) High detail
- **Decision:** Log "Field changed from X to Y" for every modification with timestamp

**Q14. System Settings - Audit Log Storage Format** ✅
- **Answer:** C) Both JSON and CSV
- **Decision:** JSON for app use, CSV export for manual review

**Q15. Maximum Customer Capacity** ✅
- **Answer:** A) Up to 5,000 customers
- **Decision:** Optimize for 5,000 limit. CSV-based storage sufficient, no database needed.

**Q16. Multi-user Support** ✅
- **Answer:** A) Single user only
- **Decision:** Just you using it on one PC. No login/authentication needed.

**Q17. Search Functionality - Search Scope** ✅
- **Question:** Search in which fields: 3 core, 5 core+extended, or all fields?
- **Answer:** A) Name, Phone, Email only
- **Decision:** Fast searches limited to 3 primary fields. Simplest and fastest.

---

## Repository Change Protocol
**User Preference:** Full permission granted - make all changes directly to patrasuva123/CUSTOMER-DATA-HUB

---

