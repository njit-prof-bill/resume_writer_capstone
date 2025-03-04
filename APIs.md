Below is a structured list of **RESTful API endpoints** required to support the **AI-Powered Resume Writer** project. Optional features are marked as **(Optional)**.

---

### **User Authentication & Management**
1. **User Registration**
   - `POST /api/auth/register`
   - **Request:** `{ "email": "user@example.com", "password": "securepassword" }`
   - **Response:** `{ "userId": "123", "email": "user@example.com", "token": "jwt_token" }`

2. **User Login**
   - `POST /api/auth/login`
   - **Request:** `{ "email": "user@example.com", "password": "securepassword" }`
   - **Response:** `{ "userId": "123", "email": "user@example.com", "token": "jwt_token" }`

3. **OAuth Login (Optional)**
   - `POST /api/auth/oauth`
   - **Request:** `{ "provider": "google", "token": "oauth_access_token" }`
   - **Response:** `{ "userId": "123", "email": "user@example.com", "token": "jwt_token" }`

4. **User Profile Management**
   - `GET /api/user/profile`
   - `PUT /api/user/profile`
   - **Allows users to retrieve and update their profile details (e.g., name, email, preferences).**

---

### **Career History Management**
5. **Upload Resume (Text Parsing & Storage)**
   - `POST /api/resumes/upload`
   - **Request:** `{ "file": "resume.pdf" }`
   - **Response:** `{ "resumeId": "456", "status": "processing" }`

6. **Submit Free-Form Career History**
   - `POST /api/resumes/history`
   - **Request:** `{ "text": "Work history in free-form text..." }`
   - **Response:** `{ "historyId": "789", "status": "saved" }`

7. **Submit Career History via Form**
   - `POST /api/resumes/form`
   - **Request:**
     ```json
     {
       "jobs": [
         {
           "title": "Software Engineer",
           "company": "Tech Corp",
           "startDate": "2022-01-01",
           "endDate": "2023-06-01",
           "responsibilities": "Developed backend systems..."
         }
       ]
     }
     ```
   - **Response:** `{ "historyId": "101", "status": "saved" }`

8. **Retrieve Stored Career History**
   - `GET /api/resumes/history`
   - **Response:**
     ```json
     {
       "jobs": [
         {
           "title": "Software Engineer",
           "company": "Tech Corp",
           "startDate": "2022-01-01",
           "endDate": "2023-06-01",
           "responsibilities": "Developed backend systems..."
         }
       ]
     }
     ```

---

### **Job Description Processing**
9. **Submit Job Description for Resume Matching**
   - `POST /api/jobs/submit`
   - **Request:** `{ "text": "Job description text..." }`
   - **Response:** `{ "jobId": "234", "status": "saved" }`

10. **Retrieve Previously Submitted Job Descriptions (Optional)**
   - `GET /api/jobs/history`
   - **Response:**
     ```json
     {
       "jobs": [
         {
           "jobId": "234",
           "text": "Job description text...",
           "submittedAt": "2025-03-02T10:00:00Z"
         }
       ]
     }
     ```

---

### **AI-Powered Resume Generation**
11. **Generate Resume Based on Career History & Job Description**
   - `POST /api/resumes/generate`
   - **Request:**
     ```json
     {
       "jobId": "234",
       "historyId": "101"
     }
     ```
   - **Response:** `{ "resumeId": "567", "status": "processing" }`

12. **Check Resume Generation Status**
   - `GET /api/resumes/status/{resumeId}`
   - **Response:** `{ "resumeId": "567", "status": "completed" }`

---

### **LaTeX-Based Resume Formatting**
13. **Get Available Resume Templates**
   - `GET /api/templates`
   - **Response:**
     ```json
     {
       "templates": [
         { "templateId": "default", "name": "Standard Resume" },
         { "templateId": "modern", "name": "Modern Style Resume" }
       ]
     }
     ```

14. **Format Resume Using Selected Template**
   - `POST /api/resumes/format`
   - **Request:**
     ```json
     {
       "resumeId": "567",
       "templateId": "default"
     }
     ```
   - **Response:** `{ "formattedResumeId": "789", "downloadUrl": "/api/resumes/download/789" }`

15. **Download Formatted Resume**
   - `GET /api/resumes/download/{formattedResumeId}`
   - **Response:** Binary PDF file

---

### **Resume & Job Tracking (Optional)**
16. **Store Resume and Job Application History (Optional)**
   - `POST /api/user/job-applications`
   - **Request:**
     ```json
     {
       "jobId": "234",
       "resumeId": "567",
       "status": "submitted"
     }
     ```
   - **Response:** `{ "applicationId": "901", "status": "saved" }`

17. **Retrieve Past Resume Applications (Optional)**
   - `GET /api/user/job-applications`
   - **Response:**
     ```json
     {
       "applications": [
         {
           "jobId": "234",
           "resumeId": "567",
           "status": "submitted",
           "appliedAt": "2025-03-02T12:00:00Z"
         }
       ]
     }
     ```

---

### **Summary of API Categories**
- **Authentication & User Management**
  - `/api/auth/register`, `/api/auth/login`, `/api/auth/oauth` (Optional), `/api/user/profile`

- **Career History Management**
  - `/api/resumes/upload`, `/api/resumes/history`, `/api/resumes/form`, `/api/resumes/history`

- **Job Description Processing**
  - `/api/jobs/submit`, `/api/jobs/history` (Optional)

- **AI Resume Generation**
  - `/api/resumes/generate`, `/api/resumes/status/{resumeId}`

- **Resume Formatting (LaTeX Service)**
  - `/api/templates`, `/api/resumes/format`, `/api/resumes/download/{formattedResumeId}`

- **Job Application & Resume Tracking (Optional)**
  - `/api/user/job-applications`

---

### **Next Steps**
- Define **API request/response schemas** in detail (e.g., OpenAPI/Swagger spec).
- Provide **error handling & authentication mechanisms** (e.g., JWT-based authentication).
- Define rate limits or access restrictions for AI API calls.

Let me know if you'd like any refinements! 🚀