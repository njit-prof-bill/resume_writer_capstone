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

---

### **Detailed RESTful API Specifications for AI-Powered Resume Writer**

Below are **detailed API specifications** based on the **APIs.md** document, ensuring clarity and coverage for both frontend and backend teams. Each API is broken down by **resource, HTTP verb, parameters, request/response body, and business logic**.

---

## API Specifications ##

### **1. Career History Management APIs**
These APIs allow users to manage their **career history**, which serves as the basis for AI-generated resumes.

#### **1.1 Upload Resume (Text Parsing & Storage)**
- **Endpoint:** `POST /api/resumes/upload`
- **Purpose:** Allows users to upload an existing resume (PDF or DOCX). The system extracts structured career history.
- **Business Logic:**
  - The file is processed asynchronously.
  - A resume parsing service extracts text and formats it.
  - The parsed data is stored in a structured format.

##### **Request**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| file | File (PDF/DOCX) | Yes | Resume file to be parsed and stored |

##### **Example Request**
```http
POST /api/resumes/upload
Content-Type: multipart/form-data

{
  "file": "resume.pdf"
}
```

##### **Response**
| Field | Type | Description |
|-------|------|-------------|
| resumeId | String | Unique ID for the uploaded resume |
| status | String | Processing status (`processing`, `completed`, `failed`) |

```json
{
  "resumeId": "456",
  "status": "processing"
}
```

---

#### **1.2 Submit Free-Form Career History**
- **Endpoint:** `POST /api/resumes/history`
- **Purpose:** Allows users to manually enter their career history as free-form text.
- **Business Logic:**
  - The system stores the raw text as unstructured data.
  - AI processing refines and formats the text upon resume generation.

##### **Request**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| text | String | Yes | Raw text of career history |

##### **Example Request**
```json
{
  "text": "Software Engineer at TechCorp from 2020-2023. Developed AI-based applications."
}
```

##### **Response**
| Field | Type | Description |
|-------|------|-------------|
| historyId | String | Unique ID for the stored career history |
| status | String | Processing status (`saved`) |

```json
{
  "historyId": "789",
  "status": "saved"
}
```

---

#### **1.3 Submit Career History via Structured Form**
- **Endpoint:** `POST /api/resumes/form`
- **Purpose:** Enables users to input structured career history through a form.
- **Business Logic:**
  - Stores structured work experience details.
  - Supports multiple job entries.

##### **Request**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| jobs | Array | Yes | List of job history entries |

```json
{
  "jobs": [
    {
      "title": "Software Engineer",
      "company": "Tech Corp",
      "startDate": "2022-01-01",
      "endDate": "2023-06-01",
      "responsibilities": "Developed backend systems."
    }
  ]
}
```

##### **Response**
| Field | Type | Description |
|-------|------|-------------|
| historyId | String | Unique ID for the stored history |
| status | String | Processing status (`saved`) |

```json
{
  "historyId": "101",
  "status": "saved"
}
```

---

#### **1.4 Retrieve Stored Career History**
- **Endpoint:** `GET /api/resumes/history`
- **Purpose:** Fetch stored career history for a user.
- **Business Logic:**
  - Returns all stored job experiences for the authenticated user.

##### **Response**
```json
{
  "jobs": [
    {
      "title": "Software Engineer",
      "company": "Tech Corp",
      "startDate": "2022-01-01",
      "endDate": "2023-06-01",
      "responsibilities": "Developed backend systems."
    }
  ]
}
```

---

### **2. Job Description Processing APIs**
These APIs allow users to submit and retrieve job descriptions to tailor their resumes accordingly.

#### **2.1 Submit Job Description**
- **Endpoint:** `POST /api/jobs/submit`
- **Purpose:** Users submit job descriptions for resume customization.
- **Business Logic:**
  - Stores job descriptions.
  - The system later matches job descriptions with the user’s history.

##### **Request**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| text | String | Yes | Job description text |

##### **Response**
```json
{
  "jobId": "234",
  "status": "saved"
}
```

---

#### **2.2 Retrieve Job Descriptions**
- **Endpoint:** `GET /api/jobs/history`
- **Purpose:** Retrieves past job descriptions submitted by the user.
- **Business Logic:**
  - Allows users to review previous job postings.

##### **Response**
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

### **3. AI Resume Generation APIs**
These APIs manage AI-powered resume creation.

#### **3.1 Generate Resume**
- **Endpoint:** `POST /api/resumes/generate`
- **Purpose:** Generates a resume based on job descriptions and career history.
- **Business Logic:**
  - Uses AI to create a tailored resume.

##### **Request**
```json
{
  "jobId": "234",
  "historyId": "101"
}
```

##### **Response**
```json
{
  "resumeId": "567",
  "status": "processing"
}
```

---

#### **3.2 Check Resume Status**
- **Endpoint:** `GET /api/resumes/status/{resumeId}`
- **Purpose:** Returns the status of resume generation.
- **Business Logic:**
  - Monitors processing progress.

##### **Response**
```json
{
  "resumeId": "567",
  "status": "completed"
}
```

---

### **4. Resume Formatting & Download APIs**
#### **4.1 Get Available Resume Templates**
- **Endpoint:** `GET /api/templates`
- **Purpose:** Returns available LaTeX templates.

##### **Response**
```json
{
  "templates": [
    { "templateId": "default", "name": "Standard Resume" },
    { "templateId": "modern", "name": "Modern Style Resume" }
  ]
}
```

---

#### **4.2 Format Resume**
- **Endpoint:** `POST /api/resumes/format`
- **Purpose:** Formats an AI-generated resume using LaTeX.
- **Business Logic:**
  - Converts text into a downloadable PDF.

##### **Request**
```json
{
  "resumeId": "567",
  "templateId": "default"
}
```

##### **Response**
```json
{
  "formattedResumeId": "789",
  "downloadUrl": "/api/resumes/download/789"
}
```

---

#### **4.3 Download Formatted Resume**
- **Endpoint:** `GET /api/resumes/download/{formattedResumeId}`
- **Purpose:** Allows users to download formatted resumes.
- **Response:** Binary PDF file.

---
