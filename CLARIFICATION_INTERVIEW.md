# Customer Data Hub - Clarification Interview Session
**Date:** July 27, 2026  
**Status:** In Progress (7/21 questions answered)
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
- **Decision:** Display list of 50 duplicates found, let user review and decide to import anyway or skip

---

## Repository Change Protocol
**User Preference:** Full permission granted - make all changes directly to patrasuva123/CUSTOMER-DATA-HUB

---

