# 🧩 Challenge: Expired Coupon (Improper Input Validation – 4 Stars)

## 🎯 Goal
Redeem a **campaign coupon code** that is technically expired, by bypassing client-side time validation.

## 🧠 Background
Juice Shop uses client-side JavaScript to check whether a coupon is expired. The validation relies on the system time of the user's device. This opens the door for manipulation: if you change your system clock, you can trick the frontend into accepting an expired coupon.

## 🧪 Solution Steps

1. Open browser **developer tools** and inspect `main.js`
   - Search for keywords like `coupon`, `campaign`, or `validOn`
   - You’ll find hardcoded coupon entries with Unix timestamps

2. Identify an expired coupon
   - Example: `WMNSDY2019` with `validOn: 1551999600000`
   - Convert the timestamp using [epochconverter.com](https://www.epochconverter.com/)
   - Result: **8 March 2019**

3. Change your **host system time** to match the coupon’s valid date
   - Set system clock to **8 March 2019**

4. Go to `/#/wallet` and enter the coupon code:
   ```
   WMNSDY2019
   ```

5. Click “Apply Coupon”
   - The frontend now considers the coupon valid
   - ✅ Challenge “Expired Coupon” is marked as solved

## 🛠️ Techniques & Tools

- **JavaScript inspection**: Analyze `main.js` for coupon logic
- **Epoch conversion**: Translate Unix timestamps to human-readable dates
- **System time manipulation**: Trick client-side validation
- **Frontend-only bypass**: No API tampering required

## 📚 Takeaways

- Relying on **client-side time checks** is insecure
- All validation logic should be enforced **server-side**
- Attackers can manipulate system time to bypass date-based restrictions

---
