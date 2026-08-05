# Bug Note 1: Cropper Modal Blocked by ReelUp

**Issue:** 
The Zepto cropper modal (crop box/upload) fails to initialize and crashes when opened.

**Culprit:** 
**ReelUp App** (Analytics script) - https://apps.shopify.com/reelup

**Script to Block/Identify:** 
`reelup.io` (specifically `webPixelAnalytics...` from `cdn-v2.reelup.io`)

**Console Error Signature:**
`Uncaught TypeError: can't access property "length", XMLHttpRequest.callbacks is undefined`

**Why it happens:** 
ReelUp's analytics script intercepts network requests (`XMLHttpRequest`) and crashes during the cropper's zoom/crop events, which kills the Zepto `cropper.js` process.

**Quick Test / Proof (No Admin Needed):**
1. Open DevTools -> Network -> Blocking.
2. Block `reelup.io`.
3. Refresh and open the cropper (it will work perfectly).

**Solution for Merchant:** 
Disable the ReelUp app or contact ReelUp support to fix their `XMLHttpRequest.callbacks` conflict.

---

