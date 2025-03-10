# Shopify FBCLID Tracking

This repository provides a guide and code snippets for capturing **Facebook Click ID (FBCLID)** in Shopify orders and using it for **Facebook Offline Conversion Tracking**.

---

## 📌 How It Works
1. **Capture FBCLID from URL** when a user visits your Shopify store via Facebook Ads.
2. **Store FBCLID in Shopify Cart Attributes**.
3. **Automatically transfer it to Order Note Attributes** after purchase.
4. **Export FBCLID from Shopify Orders** for Facebook Offline Conversion Upload.

---

## 🛠️ Setup Instructions

### **1️⃣ Add FBCLID Tracking to theme.liquid**

Insert the following script inside `<head>` in `theme.liquid`:

```html
<!-- FBCLID Capture: Store in Cart Attributes -->
<script>
function storeFbclidInCart() {
    let urlParams = new URLSearchParams(window.location.search);
    let fbclid = urlParams.get('fbclid');
    if (fbclid) {
        fetch('/cart/update.js', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ attributes: { fbclid: fbclid } })
        }).then(response => console.log("FBCLID Stored in Cart:", fbclid));
    }
}
storeFbclidInCart();
</script>
<!-- End FBCLID Capture -->
```

### **2️⃣ Verify FBCLID in Shopify Orders**
- After placing a test order, check **Shopify Admin → Orders**.
- In the order details, scroll to **Note Attributes** and confirm that FBCLID is stored.

### **3️⃣ Export Orders with FBCLID**
- Go to **Shopify Admin → Orders → Export Orders**.
- Ensure the **Note Attributes** column contains FBCLID.
- Save as CSV and prepare for **Facebook Offline Conversion Upload**.

---

## 🔄 Facebook Offline Conversion Upload

### **1️⃣ Format Your CSV for Facebook**
Create a CSV file with the following columns:

| FBCLID | Conversion Name | Conversion Time | Conversion Value | Currency |
|--------|----------------|-----------------|------------------|----------|
| ABC123... | Purchase | 2025-02-20 14:30:00 | 50.00 | USD |

### **2️⃣ Upload to Facebook**
1. **Go to** [Facebook Events Manager → Offline Events](https://www.facebook.com/events_manager/offline-events/).
2. Click **Create Offline Event Set**.
3. Upload the formatted CSV.
4. Facebook will match FBCLIDs and attribute conversions.

---

## ✅ Notes & Best Practices
- FBCLID tracking **does NOT require cookie consent**, as it's stored in **cart attributes**.
- Shopify **automatically moves cart attributes to Note Attributes**, so no extra checkout script is needed.
- If using **Google Tag Manager**, push FBCLID to `dataLayer` for analytics tracking.

---

## 📂 Repository Structure
```
/ shopify-fbclid-tracking
│── /docs                  # Documentation
│── theme.liquid           # Shopify Theme Script for FBCLID
│── facebook_upload.csv    # Sample CSV for Facebook Offline Conversion Upload
│── README.md              # Setup Guide
```

---

## 🚀 You're All Set!
Now you can accurately track Facebook Ads conversions even if purchases happen **offline** or outside the standard tracking window.

💡 Need help? Open an issue or reach out!

---
