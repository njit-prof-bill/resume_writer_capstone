## **AI-Powered Resume Writer: Capstone Project Overview**

### **Project Summary**
This project is an AI-powered resume writer designed to help job seekers tailor their resumes to specific job postings. The system will allow users to input job descriptions and generate customized resumes using a combination of structured career history data and AI-generated content. The application will be developed as a full-stack web application, with a modular backend supporting multiple services.

#### **Core Features and Technical Scope**

1. **User Authentication and Registration**
   - The system will support user accounts with self-registration and sign-in functionality.
   - Initial authentication will use a username and password system, with Stretch OAuth-based login (e.g., Google authentication).

2. **Career History Management**
   - Users will be able to maintain a career history that serves as the foundation for generated resumes.
   - Multiple input methods will be supported, including:
     - Uploading existing resumes (parsing text where possible).
     - Free-form text entry.
     - An Stretch structured online form.

3. **Job Description Processing**
   - The system will allow users to paste job descriptions, which will serve as input for resume customization.

4. **AI-Powered Resume Generation**
   - A Large Language Model (LLM) will generate resume content based on the job description and the user's career history.
   - The AI-generated content will be structured to align with industry best practices for resume writing.

5. **LaTeX-Based Resume Formatting Service**
   - The system will utilize LaTeX templates to format resumes into high-quality, professional documents.
   - A default template will be provided, with support for additional formats.
   - Users may have the option to select from multiple LaTeX templates.

6. **Document Output & Logging**
   - The generated resume will be available for download in a polished format (PDF).
   - Optionally, the system may maintain a log of job applications and generated resumes for users to track their history.

#### **Technical Considerations**
- **Frontend:** The web application frontend will be built using a modern JavaScript framework such as React, Vue, or Angular.
- **Backend:** The backend will consist of multiple services, likely implemented using Node.js, Python, or another appropriate backend technology.
- **Database:** A relational or NoSQL database will be used to store user profiles, career history, and job descriptions.
- **AI Integration:** The system will integrate with an external LLM API (e.g., OpenAI, Anthropic, or a self-hosted model).
- **Resume Formatting:** The LaTeX service will generate resumes from structured resume data, producing high-quality PDF documents.

#### **Development Approach**
The project will be developed using an Agile methodology, consisting of four two-week sprints. Students will incrementally build and test each core feature, ensuring modularity and maintainability.

This project will provide students with experience in full-stack web development, authentication systems, AI integration, and document generation using LaTeX. The result will be a practical tool that helps job seekers create targeted resumes, demonstrating both technical expertise and real-world applicability.

---

## 💼 Project Sprint Specifications: AI-Powered Resume Writer

### 🛠️ Sprint 0: Authentication & Onboarding

#### 🎯 Purpose:

Establish the authentication and access control system that governs user registration, login, and session management. This sprint ensures the platform can securely distinguish users and support account-based workflows in later sprints.

#### 📄 Sprint 0 APIs

* `POST /api/auth/register` — Register a new user with email and password
* `POST /api/auth/login` — Login and receive a session token
* `POST /api/auth/oauth` *(Stretch)* — OAuth login via third-party (e.g., Google)
* `POST /api/auth/forgot-password` *(Stretch)* — Initiate password reset
* `POST /api/auth/verify-email` *(Stretch)* — Verify new user email
* `GET /api/user/profile` / `PUT /api/user/profile` — Retrieve or update user details

#### 🧑‍💻 Sprint 0 Frontend Features

* Landing page with login and registration options
* Registration form with validation (password confirmation, email format)
* Login form with error handling and session management
* Redirect to home page on successful login
* Logout button
* (Stretch) Support for OAuth login
* (Stretch) UI for forgot password and email verification

---

### 📚 Sprint 1: Personal History Collection & Structuring

#### 🎯 Purpose:

Collect and consolidate the user’s full professional and academic history. Users can submit this history via resumes, biographical documents (e.g., LinkedIn), or freeform text. These sources are combined into a single corpus and parsed with AI to extract structured information across five categories:

1. Name and Contact Information
2. Career Objectives
3. Skills
4. Job History
5. Education

The goal is to produce an editable, structured profile that forms the basis for future resume generation.

#### 📄 Sprint  APIs

* `POST /api/history/upload` — Upload resumes or biographical documents
* `POST /api/history/freeform` — Submit unstructured text content
* `GET /api/history/structured` — Retrieve parsed and structured personal history
* `PUT /api/history/:section` — Update one of the five profile sections
* *(Stretch)* `POST /api/history/merge` — Reprocess combined history corpus

#### 🧑‍💻 Sprint 1 Frontend Features

* File upload area for resumes and LinkedIn documents
* Text input area for pasting or typing freeform biographical text
* Submit button to initiate processing
* Notification when parsing is complete
* UI to view and edit:

  * Contact Info
  * Career Objectives
  * Skills
  * Job History
  * Education

* Loading and error states for processing

---

### 🧠 Sprint 2: Job Description & AI Resume Generation

#### 🎯 Purpose:

Enable users to generate tailored resumes based on specific job postings. Users submit job descriptions, and the system uses their personal history (from Sprint 1) to generate structured resume content using AI. Resume generation is asynchronous and requires users to track completion status.

#### 📄 Sprint 2 APIs

* `POST /api/jobs/submit` — Submit a job description for targeting
* `GET /api/jobs/history` *(Stretch)* — Retrieve past submitted job descriptions
* `POST /api/resumes/generate` — Generate structured resume content using AI
* `GET /api/resumes/status/{resumeId}` — Check status of resume generation

#### 🧑‍💻 Sprint 2 Frontend Features

* Job description input form (paste or type)
* (Stretch) Job description history view
* Selection UI for resume generation (select job + history)
* Trigger button for resume generation
* Polling status indicator for generation completion
* Display generated resume content (read-only)
* Error feedback for invalid inputs or failures

---

### 🖨️ Sprint 3: Resume Formatting, Advice & Tracking

#### 🎯 Purpose:

Finalize and download the AI-generated resume by formatting it into a readable file (Markdown, plain text, or HTML). Additionally, provide personalized job-seeking advice based on how well the resume matches the job description. Advanced formatting and job tracking features are encouraged as stretch goals.

#### 📄 Sprint 3 APIs

* `POST /api/resumes/format` — Format resume content into a downloadable file
* `GET /api/resumes/download/{formattedResumeId}` — Download the formatted file
* `POST /api/jobs/advice` — Generate advice based on job description and resume
* *(Stretch)* `POST /api/user/job-applications` — Log job/resume submissions
* *(Stretch)* `GET /api/user/job-applications` — Retrieve submission history
* *(Stretch)* `GET /api/templates` — Retrieve available formatting templates

#### 🧑‍💻 Sprint 3 Frontend Features

* UI to select resume and format type (Markdown, HTML, plain text)
* Button to format resume and generate download link
* Advice panel to request and display job-seeking advice
* (Stretch) UI to track submitted applications (history view)
* (Stretch) UI to select formatting templates and visual styles
* User feedback, loading states, and error handling for all actions
