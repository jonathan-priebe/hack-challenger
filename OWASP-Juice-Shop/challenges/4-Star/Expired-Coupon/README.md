# Challenge: Expired Coupon (Improper Input Validation – 4 Stars)

## Objective
Redeem a campaign coupon code that is technically expired by bypassing client-side time validation.

## Background

While exploring the Juice Shop frontend, I inspected the `main.js` file using browser developer tools and noticed hardcoded coupon entries containing Unix timestamps under the `validOn` field. One of them was:

### JSON
```json
{
  "coupon": "WMNSDY2019",
  "validOn": 1551999600000
}
```

I converted the timestamp using [epochconverter.com](https://www.epochconverter.com/) and saw that it corresponded to **8 March 2019**, which was clearly in the past. This led me to suspect that the coupon validation was based solely on the client-side system time.

To confirm this, I changed my host system time to match the coupon’s valid date and attempted to redeem it. The frontend accepted the coupon, proving that the expiration check was performed entirely on the client side and not enforced by the backend.

## My Approach

1. Opened the browser’s developer tools and inspected the `main.js` file.
2. Searched for keywords like `coupon`, `campaign`, or `validOn`.
3. Found a hardcoded coupon entry like [this](#json)
4. Converted the Unix timestamp using [epochconverter.com](https://www.epochconverter.com/) → Result: **8 March 2019**
5. Changed my host system time to **8 March 2019**
6. Navigated to `/#/wallet` and entered the coupon code:
   ```
   WMNSDY2019
   ```
7. Clicked “Apply Coupon” – the frontend accepted the coupon as valid
8. The challenge “Expired Coupon” was marked as solved

## Techniques & Tools

- JavaScript inspection: Analyzing `main.js` for coupon logic and timestamps
- Epoch conversion: Translating Unix timestamps to readable dates
- System time manipulation: Adjusting local time to bypass frontend checks
- Frontend-only bypass: No backend or API tampering required

## Takeaways

- Client-side time validation is inherently insecure and can be bypassed easily
- All validation logic, especially for time-sensitive features, must be enforced server-side
- Attackers can manipulate system time to exploit logic flaws in the frontend
