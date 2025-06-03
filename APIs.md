## 📚 Sprint 1: Personal History Collection & Structuring

### 🎯 Purpose:

Collect and consolidate the user’s full professional and academic history. Users can submit this history via resumes, biographical documents (e.g., LinkedIn), or freeform text. These sources are combined into a single corpus and parsed with AI to extract structured information across five categories:

1. Name and Contact Information
2. Career Objectives
3. Skills
4. Job History
5. Education

The goal is to produce an editable, structured profile that forms the basis for future resume generation.

### 📄 Sprint 1 API Specifications

---

### **1. POST /api/history/upload**

**Purpose:** Accepts file uploads (PDF or DOCX resumes, LinkedIn exports) and extracts raw text.

**Business Logic:**

* Stores uploaded file under the authenticated user.
* Extracts text content using file parser.
* Appends extracted text to user's history corpus.
* Automatically triggers AI parsing pipeline.

**Request Specification:**

| Field | Type                       | Required | Description                      |
| ----- | -------------------------- | -------- | -------------------------------- |
| file  | File (multipart/form-data) | Yes      | Resume or bio document to upload |

**Request Example:** (Form-encoded)

* `Content-Type: multipart/form-data`

**Response Specification:**

| Field  | Type   | Description           |
| ------ | ------ | --------------------- |
| status | String | Upload status message |
| fileId | String | ID of uploaded file   |

**Response Example:**

```json
{
  "status": "processing",
  "fileId": "abc123"
}
```

---

### **2. POST /api/history/freeform**

**Purpose:** Accepts unstructured biographical text submitted directly by the user.

**Business Logic:**

* Stores the freeform text input.
* Appends to user history corpus.
* Automatically triggers AI parsing.

**Request Specification:**

| Field | Type   | Required | Description                 |
| ----- | ------ | -------- | --------------------------- |
| text  | String | Yes      | User-entered biography text |

**Request Example:**

```json
{
  "text": "I've worked as a data scientist at three different companies since 2017..."
}
```

**Response Specification:**

| Field  | Type   | Description    |
| ------ | ------ | -------------- |
| status | String | Parsing status |

**Response Example:**

```json
{
  "status": "processing"
}
```

---

### **3. GET /api/history/structured**

**Purpose:** Returns the user’s parsed and structured personal history.

**Business Logic:**

* Returns a unified JSON representation of five sections parsed from user data: contact, objectives, skills, jobs, education.

**Response Specification:**

| Field      | Type   | Description            |
| ---------- | ------ | ---------------------- |
| contact    | Object | User contact info      |
| objectives | String | User's career goals    |
| skills     | Array  | List of skills         |
| jobs       | Array  | Job history records    |
| education  | Array  | Educational background |

**Response Example:**

```json
{
  "contact": {
    "fullName": "Jane Doe",
    "email": "jane@example.com",
    "phone": "(123) 456-7890"
  },
  "objectives": "To apply my data science expertise to solve real-world problems...",
  "skills": ["Python", "TensorFlow", "SQL"],
  "jobs": [ ... ],
  "education": [ ... ]
}
```

---

### **4. PUT /api/history/\:section**

**Purpose:** Updates a specific section of the user’s structured personal history.

**Business Logic:**

* `:section` must be one of: `contact`, `objectives`, `skills`, `jobs`, `education`.
* Validates section structure.
* Replaces or merges the new content into existing structured data.

**Request Specification:**

| Parameter      | Type   | Required | Description                        |
| -------------- | ------ | -------- | ---------------------------------- |
| section (path) | String | Yes      | Section to update                  |
| body           | Varies | Yes      | JSON matching structure of section |

**Request Example:**

```
PUT /api/history/skills
```

```json
{
  "skills": ["JavaScript", "SQL", "TensorFlow"]
}
```

**Response Specification:**

| Field  | Type   | Description   |
| ------ | ------ | ------------- |
| status | String | Update result |

**Response Example:**

```json
{
  "status": "updated"
}
```

---

### **5. POST /api/history/merge** *(Optional)*

**Purpose:** Re-process the full corpus of user-submitted text using the latest AI parsing logic.

**Business Logic:**

* Combines uploaded documents and freeform text.
* Runs fresh AI parsing pass.
* Overwrites existing structured history with new results.

**Request Specification:**
*No body.*

**Response Specification:**

| Field  | Type   | Description                    |
| ------ | ------ | ------------------------------ |
| status | String | Status of re-parsing operation |

**Response Example:**

```json
{
  "status": "re-parsed"
}
```
