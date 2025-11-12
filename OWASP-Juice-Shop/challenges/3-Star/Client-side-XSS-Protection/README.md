# Challenge: Client-side XSS Protection (Cross-Site Scripting – 3 Stars)

## Objective
Trigger a persisted XSS attack that bypasses client-side input validation by injecting the payload directly via a backend API call.

## Background
The Juice Shop frontend filters out common XSS payloads like `<script>` or `alert()` during form submission. However, the backend still accepts and stores raw input if sent directly via the API. This challenge demonstrates how client-side protection alone is insufficient.

Typical frontend behavior:
- Filters known XSS patterns during form submission
- Prevents payloads like `<script>` or `alert()` from being sent via the UI

However, the backend does not enforce the same validation, allowing direct API manipulation.

## My Approach
I solved this challenge using **Burp Suite** to intercept and modify the registration request:

1. Started Burp Suite and configured my browser to use its proxy
2. Navigated to the Juice Shop registration page: `/#/register`
3. Filled out the form with dummy data for a test user
4. Enabled "Intercept" in Burp Suite to capture the **POST request** to `/api/Users`
5. Replaced the `email` field in the JSON body with the following payload:
   ```json
   {
     "email": "<iframe src=\"javascript:alert(`xss`)\">"
   }
   ```
6. Forwarded the modified request to the server
7. Navigated to the **User Profile** page where the email is rendered
8. The payload executed successfully, triggering an alert popup

This bypassed the client-side filters and demonstrated a persisted XSS vulnerability.

## Tools & Techniques

- Burp Suite: Intercept and manipulate HTTP requests
- Client-side filter bypass: Injecting payloads directly via API
- Persisted XSS: Payload stored in the database and rendered later

## What is Burp Suite?

Burp Suite is a powerful web security testing tool used by penetration testers and security researchers. It acts as an intercepting proxy between the browser and the target application, allowing users to:

- Inspect and modify HTTP/S requests and responses
- Replay and fuzz requests
- Scan for vulnerabilities (e.g., XSS, SQL Injection)
- Automate attacks with extensions and built-in modules

**Most common use cases:**
- Intercepting and modifying form submissions
- Testing API endpoints for security flaws
- Discovering hidden parameters and logic
- Performing manual and automated vulnerability scans

## Takeaways

- Client-side validation is not sufficient to protect against injection attacks
- All user input must be validated and sanitized on the server side
- APIs must enforce the same security rules as the frontend
- Tools like Burp Suite are essential for identifying and exploiting backend weaknesses
