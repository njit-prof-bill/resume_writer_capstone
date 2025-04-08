## 🖨️ **Sprint 4: Resume Formatting & Tracking**

The final sprint will handle transforming AI-generated resume content into professionally formatted resumes and optionally track resume/job application history.

### **Sprint 4 APIs:**

**Resume Formatting (LaTeX Service):**
- `GET /api/templates`
  - Retrieve available LaTeX templates for formatting resumes.
- `POST /api/resumes/format`
  - Format AI-generated resume content using selected LaTeX template.
- `GET /api/resumes/download/{formattedResumeId}`
  - Download the finalized resume as a PDF.

**Resume & Job Application Tracking (Optional):**
- `POST /api/user/job-applications` *(Optional)*
  - Store records of resume/job application submissions.
- `GET /api/user/job-applications` *(Optional)*
  - Retrieve records of past resume/job applications.

### **Sprint 4 UX features:**
- Selection interface for resume formatting templates.
- Preview or download interface for formatted resumes.
- UI for tracking and reviewing past job applications (optional).

---

## **Updated Sprint Schedule:**

| Sprint | Theme                                 | APIs Included |
|--------|---------------------------------------|---------------|
| 1      | User Authentication                   | *(Completed)* |
| 2      | Career & Education Management         | *(Completed)* |
| 3      | Job Description & AI Resume Generation | *(Completed))* |
| 4      | Resume Formatting & Tracking          | Resume formatting and optional application tracking |
