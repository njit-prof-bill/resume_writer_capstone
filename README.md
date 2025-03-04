### **AI-Powered Resume Writer: Capstone Project Overview**  

#### **Project Summary**  
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
