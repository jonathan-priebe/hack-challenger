# Challenge: Login Jim (Injection – 3 Stars)

## Objective
Log in as user **Jim** without knowing his password by exploiting a SQL Injection vulnerability in the login form.

## Background
The Juice Shop login function is vulnerable to SQL Injection. This occurs when user input is directly embedded into a SQL query without proper validation or escaping, allowing attackers to manipulate the query logic.

Typical SQL query:
```sql
SELECT * FROM Users WHERE email = '[INPUT]' AND password = '[INPUT]';
```

By injecting crafted input, the password check can be bypassed entirely.

## My Approach
Before attempting this challenge, I had already logged in as the administrator using SQL Injection. From the administration panel, I was able to view Jim’s email address (`jim@juice-sh.op`). With that information, I returned to the login form and used SQL Injection to log in as Jim.

This demonstrates a chained attack: using one vulnerability [Brute-Forcing the Admin Panel URL](../../2-Star/Admin-Section/README.md#step-2-brute-forcing-the-admin-panel-url) to discover sensitive data, and another (SQL Injection) to escalate access.

## Solution Steps

1. Navigate to the login page: `/#/login`
2. Enter the following credentials:
   - **Email**:  
     ```
     jim@juice-sh.op'--
     ```
   - **Password**:  
     Any value (e.g., `123`)
3. Click “Login”

The resulting SQL query becomes:
```sql
SELECT * FROM Users WHERE email = 'jim@juice-sh.op'--' AND password = '123';
```

The `--` sequence comments out the rest of the query, effectively skipping the password check.

4. You will be logged in as user **Jim**
5. The challenge “Login Jim” will be marked as solved

## Techniques & Tools

- SQL Injection: Manipulating SQL queries via crafted input
- SQL comment sequence (`--`): Terminates the query early
- Reconnaissance via admin panel: Used to discover Jim’s email address

## Takeaways

- SQL Injection remains one of the most critical vulnerabilities in web applications.
- Even simple login forms can be exploited if inputs are not properly sanitized.
- Always validate and escape user input on the server side – client-side filters are not sufficient.
- Chaining vulnerabilities can lead to full system compromise.

---

## Related Documentation

See my previous write-up on logging in as the administrator and accessing the admin panel:  
[Login as Administrator – SQL Injection & Admin Panel Access](../../2-Star/Admin-Section/README.md#hacking-challenge-submission-sql-injection--broken-access-control)
