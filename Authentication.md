### **User Authentication & Management: Technical Requirements**

The authentication system will be built using a third-party authentication provider such as **Firebase, Auth0, or Clerk**. Students are **not** expected to implement authentication from scratch but must integrate and configure the authentication provider to meet the feature requirements.

---

## **Base Requirements (Must be completed to pass)**

### **1. Email and Password Login**
#### **Use Case: User Authentication with Email & Password**
- **Actors:** Job Seeker (End User), Authentication Service
- **Preconditions:**
  - The user must have an account registered in the system.
  - The authentication provider must be correctly configured to allow email/password sign-in.

- **Flow of Events:**
  1. User navigates to the login page.
  2. User enters their email and password.
  3. The frontend application sends the credentials to the authentication provider.
  4. If authentication is successful, the user receives a session token.
  5. The frontend stores the token securely and redirects the user to the dashboard.

- **Error Handling:**
  - If the email is not registered, an appropriate error message is shown.
  - If the password is incorrect, an error message is displayed.
  - If the authentication provider is unavailable, the system shows a maintenance message.

- **Acceptance Criteria:**
  - Users can successfully log in with a valid email and password.
  - Invalid credentials produce an error message without exposing security details.
  - The system stores the authentication token securely (e.g., HTTP-only cookie or secure local storage).

---

### **2. Single OAuth Provider Login**
#### **Use Case: Authentication via a Single OAuth Provider (e.g., Google)**
- **Actors:** Job Seeker (End User), OAuth Provider (Google, GitHub, etc.), Authentication Service
- **Preconditions:**
  - The authentication provider must be configured to support OAuth login.
  - The user must have a valid account with the selected OAuth provider.

- **Flow of Events:**
  1. User clicks the "Sign in with Google" button.
  2. The frontend redirects the user to the OAuth provider’s login page.
  3. The user authenticates with their Google (or other provider) credentials.
  4. The authentication provider returns a token to the frontend.
  5. The frontend sends the token to the authentication provider to verify the user's identity.
  6. If verification succeeds, the user is granted access.

- **Error Handling:**
  - If OAuth authentication fails, the system displays an error message.
  - If the user cancels the OAuth login, they are returned to the login page.

- **Acceptance Criteria:**
  - Users can successfully log in using a single OAuth provider (e.g., Google).
  - The authentication provider securely handles OAuth token exchange.
  - Users are redirected to the appropriate dashboard after authentication.

---

## **Optional Requirements (Needed for an A or B Grade)**

### **3. Account Verification (Optional)**
#### **Use Case: Email Verification for New Accounts**
- **Actors:** Job Seeker (End User), Authentication Service, Email Provider
- **Preconditions:**
  - The authentication provider must support email verification.
  - The user must register with an email address.

- **Flow of Events:**
  1. User registers an account with an email and password.
  2. The authentication provider sends a verification email with a confirmation link.
  3. The user clicks the verification link.
  4. The authentication provider marks the account as verified.
  5. The user can now log in to the system.

- **Error Handling:**
  - If the email is not delivered, the system allows resending the verification email.
  - If the verification link is expired, the system prompts the user to request a new one.

- **Acceptance Criteria:**
  - Users receive a verification email upon registration.
  - Users cannot log in until their email is verified.
  - A user-friendly message is displayed when a user attempts to log in without verifying their email.

---

### **4. Multiple OAuth Providers (Optional)**
#### **Use Case: Authentication via Multiple OAuth Providers**
- **Actors:** Job Seeker (End User), OAuth Providers (Google, GitHub, Microsoft, etc.), Authentication Service
- **Preconditions:**
  - The authentication provider must support multiple OAuth configurations.
  - Users must have an account with at least one of the configured OAuth providers.

- **Flow of Events:**
  1. User clicks the "Sign in with [Provider]" button for their preferred OAuth provider.
  2. The frontend redirects the user to the selected provider's login page.
  3. The user authenticates with their credentials.
  4. The provider returns an authentication token.
  5. The frontend verifies the token with the authentication service.
  6. If successful, the user is granted access.

- **Error Handling:**
  - If authentication with one provider fails, users can attempt login with another provider.
  - If OAuth configuration changes (e.g., a provider is removed), users should be notified.

- **Acceptance Criteria:**
  - Users can authenticate using multiple OAuth providers.
  - Each provider’s authentication flow works as expected.
  - Users logging in via different OAuth providers (but with the same email) are treated as the same user.

---

### **5. Multi-Factor Authentication (Optional)**
#### **Use Case: Enhanced Security with Multi-Factor Authentication (MFA)**
- **Actors:** Job Seeker (End User), Authentication Service, MFA Provider (e.g., Authenticator App, SMS, Email)
- **Preconditions:**
  - The authentication provider must support MFA.
  - The user must enable MFA in their account settings.

- **Flow of Events:**
  1. User logs in with their email/password or OAuth provider.
  2. The authentication provider prompts the user for an additional authentication factor (e.g., a one-time code).
  3. The user retrieves the code from their authentication method (app, SMS, email).
  4. The user enters the code.
  5. If the code is valid, access is granted.

- **Error Handling:**
  - If the user enters the wrong MFA code, they must be given another attempt.
  - If the MFA method is unavailable (e.g., lost device), a recovery option should be provided.

- **Acceptance Criteria:**
  - Users can enable/disable MFA in their account settings.
  - Users must complete an additional authentication step when MFA is enabled.
  - Recovery options are available for users who lose access to their MFA device.

---

### **6. Forgot Password (Base Requirement)**
#### **Use Case: Password Recovery via Email**
- **Actors:** Job Seeker (End User), Authentication Service, Email Provider
- **Preconditions:**
  - The user must have an existing account registered in the system.
  - The authentication provider must support password reset via email.

- **Flow of Events:**
  1. The user navigates to the login page and clicks "Forgot Password."
  2. The system prompts the user to enter their registered email.
  3. The authentication provider sends a password reset email containing a secure link.
  4. The user clicks the link, which redirects them to a password reset page.
  5. The user enters and confirms a new password.
  6. The authentication provider validates and updates the password.
  7. The user receives a confirmation message and can log in with the new password.

- **Error Handling:**
  - If the email does not exist, the system should not indicate whether an account exists (to prevent enumeration attacks).
  - If the reset link is expired or invalid, the system prompts the user to request a new reset email.
  - If the user tries to reuse an old password, the system should enforce password policies if applicable.

- **Acceptance Criteria:**
  - Users can request a password reset using their registered email.
  - A secure password reset email is sent with a time-limited link.
  - Users can successfully update their password using the reset link.
  - The system provides appropriate feedback without exposing security vulnerabilities.

---
