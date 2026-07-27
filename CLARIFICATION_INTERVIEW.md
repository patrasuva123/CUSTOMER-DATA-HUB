# Customer Data Hub - Clarification Interview Session
**Date:** July 27, 2026  
**Status:** In Progress  
**Purpose:** Gather detailed requirements before AI agent development begins

---

## Interview Questions & Answers

### Round 1: Technology & Deployment

**Q1. Operating System Support** ✅
- **Question:** Should the app run on Windows only, or Windows + Mac + Linux?
- **Answer:** A) Windows only
- **Decision:** Build as Windows desktop app (.exe installer)

**Q2. Data Storage Structure** ✅
- **Question:** Single CSV file or Multiple CSV files?
- **Answer:** B) Multiple CSV files (split by category)
- **Decision:** 
  - `customers.csv` (basic info)
  - `education.csv` (education records)
  - `documents.csv` (document references)
  - `addresses.csv` (address records)
  - `metadata.json` (photo/signature paths, audit logs)

**Q3. Backup Strategy** ✅
- **Question:** How often should backups happen?
- **Answer:** D) Manual backup only
- **Decision:** User clicks "Backup Now" button in System Settings

**Q4. Photo Upload & Cropping Tool** ✅
- **Question:** Should photo upload include cropping?
- **Answer:** A) Show a built-in crop tool
- **Decision:** User can drag, resize, and rotate photos before saving

---

## Repository Change Protocol
**User Preference:** Full permission granted - make all changes directly to patrasuva123/CUSTOMER-DATA-HUB without asking for confirmation

---

