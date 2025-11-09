# 🧩 Challenge: Login Jim (Injection – 3 Stars)

## 🎯 Goal
Log in as user **Jim** without knowing his password by exploiting a **SQL Injection** vulnerability in the login form.

## 🧠 Background
The Juice Shop login function is vulnerable to SQL Injection. This means that user input is directly embedded into a SQL query without proper validation or escaping, allowing attackers to manipulate the query logic.

Typical SQL query:
SELECT * FROM Users WHERE email = '[INPUT]' AND password = '[INPUT]'

By injecting crafted input, we can bypass the password check entirely.

## 🧪 Solution Steps

1. Navigate to the login page: /#/login
2. Enter the following credentials:

   - **Email**:
     jim@juice-sh.op'--
   - **Password**: (any value, e.g. 123)

3. Click “Login”

The resulting SQL query becomes:
SELECT * FROM Users WHERE email = 'jim@juice-sh.op'--' AND password = '123'
→ The -- sequence comments out the rest of the query, effectively skipping the password check.

4. You will be logged in as user **Jim**
5. The challenge “Login Jim” will be marked as solved

## 🛠️ Techniques & Tools

- SQL Injection: Manipulating SQL queries via crafted input
- Comment sequence --: Terminates the query early
- Known user: jim@juice-sh.op is a predefined user in Juice Shop

## 📚 Takeaways

- SQL Injection is one of the most critical vulnerabilities in web applications
- Even simple login forms can be exploited if inputs are not properly sanitized
- Always validate and escape user input on the **server side** – client-side filters are not enough

---
