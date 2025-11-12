# Hacking Challenge Submission: SQL Injection + Broken Access Control

## Objective
Gain administrative access and access the hidden administration panel by chaining a SQL Injection with direct URL access.

## Procedure

### Step 1: SQL Injection Login
I logged in as the "Admin" user by entering the following payload into the login form:

```
' OR 1=1 --
```

#### Payload Explanation
- The input sets the username to `admin' OR 1=1`.
- `--` is an SQL comment that ignores the rest of the query.
- This bypasses authentication by making the WHERE clause always true.

**Resulting Query Example:**
```sql
SELECT * FROM users WHERE email = 'admin' OR 1=1 -- ' AND password = '...';
```

This allowed me to log in without knowing the actual password.

### Step 2: Brute-Forcing the Admin Panel URL
After logging in, I manually tested common admin-related routes and discovered that the following URL loads the administration panel:

```
http://localhost:3000/#/administration
```

No role-based access control was enforced — the route was simply hidden from the UI.

## Result
By chaining SQL Injection with direct URL access, I was able to:
- Log in as the administrator
- Access the administration panel
- Complete both challenges: **SQL Injection** and **Broken Access Control**

## Takeaways
- Authentication bypasses must be mitigated with input validation and parameterized queries.
- Sensitive routes must be protected by server-side access control, not just hidden from the frontend.
- Security through obscurity is not a valid defense strategy.
