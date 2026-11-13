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

# Sign Letter "S" – Cart Transform Price Security

**Purpose:**
The Sign Letter "S" is used to encrypt/sign the cart transform price, preventing anyone from manually changing the price through the storefront.

**Important Notes:**
- This feature must be enabled manually. (Rony bhai can do this) 
- If a customer adds a product to the cart while this feature is disabled, and we enable it afterward, the previously added item's price will show as **Invalid**.
- This happens because the cart item was added before price signing was enabled.

**How to Check:**

Open the product page and run this command in the browser console:

`window.pplr_ct_sign`

**Results:**
- `0` = Disabled (False)

**Important:** Be aware of existing cart items before enabling this feature, as previously added items may show an invalid price.

--- 

# Duplicate Meta Pixel AddToCart Events – Troubleshooting

**Issue:** Multiple Meta Pixel `AddToCart` events appear after clicking Add to Cart once.

**Store:** `voroam.com`

**Extension to Use:** Meta Ads Data Advisor (Chrome / Microsoft Edge)

**How to Test:**

1. Install the **Meta Ads Data Advisor** extension.
2. Open the product page and click **Add to Cart** once.
3. Check the number of `AddToCart` events.
4. Open DevTools → Network and verify `/cart/add.js` requests.
5. Block Zepto scripts through DevTools → Network Request Blocking.
6. Refresh and repeat the test.

**Test Results:**

- Zepto enabled: **2 AddToCart events**
- Zepto blocked: **2 AddToCart events**
- Shopify cart requests: **1**

**Conclusion:** Duplicate events occurred even with Zepto blocked, indicating the issue was not caused solely by our app.

**Possible Causes:** Shopify theme, Meta Pixel configuration, or third-party tracking scripts.

**Important:** Always test with Zepto enabled and blocked before determining the source of duplicate ATC events.
