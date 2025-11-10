# 🧩 Challenge: Client-side XSS Protection (Cross-Site Scripting – 3 Stars)

## 🎯 Goal
Trigger a **persisted XSS attack** that bypasses the **client-side input validation**, using a direct API call.

## 🧠 Background
The Juice Shop frontend filters out common XSS payloads like `<script>` or `alert()` during form submission. However, the backend still accepts and stores raw input if sent directly via the API. This challenge demonstrates how client-side protection alone is insufficient.

## 🧪 Solution Steps

1. Launch **Burp Suite** and configure your browser to use its proxy
2. Navigate to the Juice Shop registration page: `/#/register`
3. Fill out the form with dummy data (e.g. username, password)
4. Intercept the **POST request** to `/api/Users` in Burp
5. Modify the `email` field in the JSON body to inject your payload:
   ```json
   {
     "email": "<iframe src=\"javascript:alert(`xss`)\">",
   }
   ```
6. Forward the modified request to the server
7. Go to the **User Profile** page or any area where the email is rendered
8. ✅ If the payload executes (e.g. an alert pops up), the challenge is marked as solved

## 🛠️ Tools & Techniques

- **Burp Suite**: Intercept and modify HTTP requests
- **Client-side filter bypass**: Inject payload directly via API
- **Persisted XSS**: Payload is stored and rendered later

## 📚 Takeaways

- Client-side validation can be bypassed easily
- Always sanitize and escape user input on the **server side**
- APIs must enforce the same security rules as the frontend

---
