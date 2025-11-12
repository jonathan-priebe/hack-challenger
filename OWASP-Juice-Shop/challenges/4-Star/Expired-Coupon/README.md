# Challenge: Expired Coupon (Improper Input Validation – 4 Stars)

## Objective
Redeem a campaign coupon code that is technically expired by bypassing client-side time validation.

## Background
Juice Shop uses client-side JavaScript to check whether a coupon is expired. This validation relies on the system time of the user's device. Since this logic is not enforced on the server, it can be bypassed by manipulating the local system clock.

This challenge demonstrates the insecurity of relying solely on client-side validation for time-based restrictions.

## My Approach
I solved this challenge by analyzing the frontend JavaScript and manipulating my system time:

1. Opened the browser’s developer tools and inspected the `main.js` file.
2. Searched for keywords like `coupon`, `campaign`, or `validOn`.
3. Found a hardcoded coupon entry:
   ```json
   {
     "coupon": "WMNSDY2019",
     "validOn": 1551999600000
   }
   ```
4. Converted the Unix timestamp `1551999600000` using [epochconverter.com](https://www.epochconverter.com/) → Result: **8 March 2019**
5. Changed my host system time to **8 March 2019**.
6. Navigated to `/#/wallet` and entered the coupon code:
   ```
   WMNSDY2019
   ```
7. Clicked “Apply Coupon” – the frontend accepted the coupon as valid.
8. The challenge “Expired Coupon” was marked as solved.

## Techniques & Tools

- JavaScript inspection: Analyzing `main.js` for coupon logic and timestamps
- Epoch conversion: Translating Unix timestamps to readable dates
- System time manipulation: Adjusting local time to bypass frontend checks
- Frontend-only bypass: No backend or API tampering required

## Takeaways

- Client-side time validation is inherently insecure and can be bypassed easily
- All validation logic, especially for time-sensitive features, must be enforced server-side
- Attackers can manipulate system time to exploit logic flaws in the 