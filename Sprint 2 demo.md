### Agile Sprint 2 Demo Script

#### Introduction
Welcome everyone! Today, we'll demonstrate the functionality we've developed for Sprint 2, focusing on the **Career History Management** module.

#### Backend API Demonstration

**1. Upload Resume (Core Requirement)**
- Demonstrate uploading a DOCX file through the `POST /api/resumes/upload` endpoint.
- Show response containing the `resumeId` and `status: processing`.

**Stretch:**
- Demonstrate support for uploading and processing a PDF file.

**2. Submit Free-Form Career History (Core Requirement)**
- Demonstrate submitting free-form career history text via `POST /api/resumes/history`.
- Show response confirming storage with a `historyId` and status "saved".

**3. Retrieve Stored Career History (Core Requirement)**
- Fetch the stored career history with a `GET /api/resumes/history` request.
- Clearly show the returned structured job experiences.

**Stretch:**
- Highlight the inclusion of an "accomplishments" list in the response.

**4. Retrieve User's Education Information (Core Requirement)**
- Fetch stored education details via `GET /api/resumes/education`.
- Demonstrate the structured data response with degrees, institutions, dates, and GPA.

**Stretch APIs Demonstration (Optional for Bonus Points)**
- Demonstrate updating career information using your designed endpoint: `POST /api/resumes/career/{id}`.
- Demonstrate updating education information using your designed endpoint: `POST /api/resumes/education/{id}`.

#### Frontend Demonstration

**1. Basic Application Layout (Core Requirement)**
- Display the standard page layout including:
  - Banner with application name
  - User's name clearly displayed
  - Functional logout button/link
  - Navigation system (dropdown or side panel)

**Stretch:**
- Showcase custom-designed logo
- User avatar displayed
- Show/hide functionality for navigation panel
- Settings/preferences page
- Demonstrate collection of name/contact information
- Theme toggle (light/dark), respecting system preference

**2. Resume Upload Interface (Core Requirement)**
- Show file upload interface accepting DOCX files.
- Demonstrate progress indicator and upload notifications.

**Stretch:**
- Demonstrate PDF file upload capability.

**3. Free-form Career History Submission and Display (Core Requirement)**
- Enter career details manually and submit.
- Display a formatted, scrollable timeline view clearly showing:
  - Job titles
  - Company names
  - Employment dates
  - Key responsibilities

**Stretch:**
- Demonstrate editable career history forms, showing successful updates and error handling.

**4. Education Information Display (Core Requirement)**
- Display structured education information:
  - Degrees earned
  - Institutions
  - Attendance dates
  - GPA

**Stretch:**
- Showcase editable education update forms with add/remove functionality.
- Demonstrate immediate feedback upon submission or cancellation.

#### Wrap-Up

- Summarize the key functionalities demonstrated.
- Clearly mention any stretch goals you've completed.
- Conclude by highlighting readiness for the next sprint, "Job Description Processing & AI Resume Generation".

Thank you!

