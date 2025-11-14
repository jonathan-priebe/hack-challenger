# Challenge: SQL Injection + Broken Access Control

## Objective
Gain administrative access and access the hidden administration panel by chaining a SQL Injection vulnerability with direct URL access.

## How I Solved It

### Step 1: Discovering and Exploiting SQL Injection

To test for SQL Injection, I entered the following payload into the login form:

```
admin' OR 1=1 --
```

This is a classic injection string used to bypass authentication by manipulating the SQL query logic. I placed it in the **email** field and submitted the form with any arbitrary password. The application logged me in as the administrator, confirming that user input was directly embedded into the backend SQL query without proper sanitization or parameterization.

**Payload Breakdown:**
- `admin' OR 1=1` sets the condition to always true.
- `--` is an SQL comment that ignores the rest of the query, including the password check.

**Resulting Query Example:**
```sql
SELECT * FROM users WHERE email = 'admin' OR 1=1 -- ' AND password = '...';
```

### Step 2: Accessing the Admin Panel

After logging in as admin, I manually tested common admin-related routes. By entering the following URL directly into the browser:

```
http://localhost:3000/#/administration
```

I was able to access the administration panel. No role-based access control was enforced — the route was simply hidden from the UI.

## Result

By chaining SQL Injection with direct URL access, I successfully:
- Logged in as the administrator
- Accessed the hidden administration panel
- Solved both challenges: **SQL Injection** and **Broken Access Control**

## Takeaways

- SQL Injection must be mitigated using parameterized queries and strict input validation.
- Sensitive routes must be protected by server-side access control, not just hidden from the frontend.
- Chaining vulnerabilities can lead to full system compromise and privilege escalation.
