# 🧩 Challenge: Admin Section (Broken Access Control – 2 Stars)

## 🎯 Goal
Access the **administration section** of the Juice Shop without proper authorization, exploiting a **Broken Access Control** vulnerability.

## 🧠 Background
Broken Access Control occurs when an application fails to properly restrict access to sensitive areas or functions. In this challenge, the admin section is not protected by authentication or role checks – it’s simply hidden from the UI.

## 🧪 Solution Steps

1. Open your browser’s developer tools (F12) and go to the **Console** or **Network** tab
2. Manually navigate to the admin section by entering the following URL:
   ```
   /#/administration
   ```
   or directly in the address bar:
   ```
   http://localhost:3000/#/administration
   ```
3. Press Enter – the page will load without requiring admin credentials
4. ✅ The challenge “Admin Section” will be marked as solved

## 🛠️ Techniques & Tools

- **Broken Access Control**: Accessing hidden or restricted areas without proper authorization
- **Direct URL Access**: Navigating to a route that’s not linked in the UI
- **Developer Tools**: Useful for inspecting routes, hidden elements, and application behavior

## 📚 Takeaways

- Sensitive routes must be protected by **server-side access control**, not just hidden from the UI
- Relying on obscurity (e.g. hiding links) is **not a security measure**
- Always enforce role-based access checks on the backend

---
