## **AI-Powered Resume Writer: Capstone Project Overview**

### **Project Summary**
This project is an AI-powered resume writer designed to help job seekers tailor their resumes to specific job postings. The system will allow users to input job descriptions and generate customized resumes using a combination of structured career history data and AI-generated content. The application will be developed as a full-stack web application, with a modular backend supporting multiple services.

#### **Core Features and Technical Scope**

1. **User Authentication and Registration**
   - The system will support user accounts with self-registration and sign-in functionality.
   - Initial authentication will use a username and password system, with optional OAuth-based login (e.g., Google authentication).

2. **Career History Management**
   - Users will be able to maintain a career history that serves as the foundation for generated resumes.
   - Multiple input methods will be supported, including:
     - Uploading existing resumes (parsing text where possible).
     - Free-form text entry.
     - An optional structured online form.

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

## Project Requirements by Sprint

### Sprint 1: Authentication & Access Control

#### Core Requirements (Backend & Auth Provider)

1. Implement email + password registration and login
2. Implement OAuth login with one provider (e.g., Google)
3. Redirect verified users to the home page
4. Allow users to log out

#### Frontend

5. Build landing page with login/register links
6. Build registration form (username, password, confirm password)
7. Build login form with error feedback
8. Redirect to home page after login
9. Add logout button to home page
10. Show error messages for invalid credentials

#### Stretch

11. Implement multi-provider OAuth login
12. Add account verification (email validation)
13. Implement MFA support
14. Implement “Forgot Password” flow

---

### Sprint 2: Career & Education Management

#### Backend (APIs)

1. `POST /api/resumes/upload` — Upload & parse resume text
2. `POST /api/career/freeform` — Submit career history manually
3. `GET /api/career/history` — Retrieve all stored career entries
4. `PUT /api/career/:id` — Update a specific career item
5. `POST /api/education/freeform` — Submit education history
6. `GET /api/education/history` — Retrieve education data
7. `PUT /api/education/:id` — Update a specific education item
8. De-dupe freeform career and education submissions

#### Frontend

9. UI for uploading and submitting resume text
10. UI form for manually entering career history
11. Table view for displaying saved career items
12. Inline editing or modal update for career items
13. UI for manually entering education history
14. Table view and editing for education records
15. Resume upload progress and success/failure messages

---

### Sprint 3: AI Resume Generation

#### Backend (APIs)

1. `POST /api/jobs/submit` — Paste and store job descriptions
2. `GET /api/jobs/:id` — Retrieve specific job description
3. `GET /api/jobs` — List all user-submitted job descriptions
4. `POST /api/resumes/generate` — Generate resume text using AI
5. De-dupe job descriptions
6. Structure resume content before formatting (for downstream LaTeX use)

#### Frontend

7. UI to paste or input job descriptions
8. (Stretch) View previously submitted job descriptions
9. UI to select job and resume and trigger resume generation
10. Display generated resume text with success message
11. Show generation progress/status indicator

---

### Sprint 4: Resume Formatting, Download & Advice

#### Backend (APIs)

1. `POST /api/resumes/format` — Format resume (Markdown by default)
2. `GET /api/resumes/download/{formattedResumeId}` — Download formatted file
3. `POST /api/jobs/advice` — Generate AI-based advice for improving job success
4. (Stretch) `POST /api/user/job-applications` — Record job/resume application
5. (Stretch) `GET /api/user/job-applications` — View past job applications
6. (Stretch) `GET /api/templates` — View available resume templates
7. (Stretch) Add support for LaTeX and styled formats (templateId in formatting)

#### Frontend

8. Format resume and display download link
9. Display job-seeking advice based on resume and job
10. (Stretch) Display job application tracking history
11. (Stretch) UI for selecting resume templates and styles

---

### Global Stretch Goals (Optional Throughout)

* View and update user contact info parsed from resumes
* Add a dedicated skills section (parse and store skills)
* Manual entry of skills
* Skill de-duping
* Resume viewer for uploaded content
* Viewer/editor for freeform career and education data
* Application dashboard summarizing job interactions

---

### Summary by Sprint

| Sprint   | Category  | Task Count          |
| -------- | --------- | ------------------- |
| Sprint 1 | Auth & UX | 10 core + 4 stretch |
| Sprint 2 | API & UX  | 8 API + 7 UX        |
| Sprint 3 | API & UX  | 6 API + 5 UX        |
| Sprint 4 | API & UX  | 7 API + 4 UX        |
| Stretch  | Global    | 7+ additional ideas |

---
