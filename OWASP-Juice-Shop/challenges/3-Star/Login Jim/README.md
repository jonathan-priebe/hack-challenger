# Challenge: Login Jim (Injection – 3 Stars)

## Objective
Log in as user **Jim** without knowing his password by exploiting a SQL Injection vulnerability in the login form.

## Background

In the previous challenge ([SQL Injection + Broken Access Control](../../2-Star/Admin-Section/README.md)), I discovered a SQL Injection vulnerability in the login form by entering the following payload:

```
admin' OR 1=1 --
```

This allowed me to log in as the administrator without knowing the password. After gaining access to the administration panel, I was able to view Jim’s email address (`jim@juice-sh.op`). This confirmed that user input was directly embedded into a SQL query without proper validation or escaping.

Typical vulnerable query:
```sql
SELECT * FROM Users WHERE email = '[INPUT]' AND password = '[INPUT]';
```

By injecting crafted input, the password check can be bypassed entirely.

## My Approach

I reused the SQL Injection technique from the previous challenge, this time targeting Jim’s account. Since I had already retrieved his email address from the admin panel, I crafted a new injection payload using his known email to bypass authentication.

This demonstrates a chained attack: using one vulnerability ([Brute-Forcing the Admin Panel URL](../../2-Star/Admin-Section/README.md#how-i-solved-it)) to discover sensitive data, and another (SQL Injection) to escalate access.

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

**Resulting Query:**
```sql
SELECT * FROM Users WHERE email = 'jim@juice-sh.op'--' AND password = '123';
```

The `--` sequence comments out the password check, allowing login without credentials.

4. You will be logged in as user **Jim**
5. The challenge “Login Jim” will be marked as solved

## Takeaways

- SQL Injection remains one of the most critical vulnerabilities in web applications.
- Even simple login forms can be exploited if inputs are not properly sanitized.
- Always validate and escape user input on the server side – client-side filters are not sufficient.
- Chaining vulnerabilities can lead to full system compromise.

---

## Related Documentation

See my previous write-up on logging in as the administrator and accessing the admin panel:  
[Login as Administrator – SQL Injection & Admin Panel Access](../../2-Star/Admin-Section/README.md#challenge-sql-injection--broken-access-control)
