# Gmail Email Setup Guide for Mindify

## ✅ **What You Already Have**

Based on your Vercel screenshot, you already have:
- ✅ MySQL variables (MYSQL_HOST, MYSQL_USER, MYSQL_PASSWORD, MYSQL_DATABASE, MYSQL_PORT)
- ✅ JWT_SECRET
- ✅ AES_ENCRYPTION_KEY
- ✅ PORT, NODE_ENV, FRONTEND_URL

## 📧 **What You Need to Add: Gmail Email Variables**

You need to add **2 more variables** to Vercel:

### **1. EMAIL_USER**
Your Gmail address

### **2. EMAIL_PASS**
Gmail App Password (NOT your regular Gmail password!)

---

## 🔐 **Step-by-Step: Create Gmail App Password**

### **Step 1: Enable 2-Step Verification**

1. Go to [Google Account Settings](https://myaccount.google.com/)
2. Click **Security** in the left sidebar
3. Under "Signing in to Google", find **2-Step Verification**
4. Click **Get started** or **Turn on**
5. Follow the prompts to enable 2-Step Verification
   - You'll need to verify your phone number
   - Google will send you a verification code

### **Step 2: Create App Password**

1. Go back to [Google Account Settings](https://myaccount.google.com/)
2. Click **Security** again
3. Under "Signing in to Google", find **App passwords**
   - If you don't see "App passwords", make sure 2-Step Verification is enabled first
4. Click **App passwords**
5. You might need to sign in again
6. Select:
   - **App**: Choose "Mail"
   - **Device**: Choose "Other (Custom name)"
   - Type: **Mindify**
   - Click **Generate**
7. Google will show you a **16-character password**
   - It looks like: `abcd efgh ijkl mnop`
   - **Copy this password** (copy it exactly as shown, or remove spaces - either works)

### **Step 3: Add Variables to Vercel**

1. Go to your Vercel project: **Settings → Environment Variables**
2. Click **"Add New"** button
3. Add **EMAIL_USER**:
   - **Key**: `EMAIL_USER`
   - **Value**: Your Gmail address (e.g., `youremail@gmail.com`)
   - Select all environments: ✅ Production, ✅ Preview, ✅ Development
   - Click **Save**
4. Click **"Add New"** again
5. Add **EMAIL_PASS**:
   - **Key**: `EMAIL_PASS`
   - **Value**: The 16-character App Password you just copied
     - You can paste it with or without spaces: `abcdefghijklmnop` or `abcd efgh ijkl mnop`
   - Select all environments: ✅ Production, ✅ Preview, ✅ Development
   - Click **Save**

### **Step 4: Add MYSQL_SSL (If Not Already Added)**

Since you're using Railway MySQL, make sure you have:

- **Key**: `MYSQL_SSL`
- **Value**: `false`
- Select all environments: ✅ Production, ✅ Preview, ✅ Development

---

## ✅ **Final Checklist**

Add these 3 variables to Vercel:

1. ✅ **EMAIL_USER** = `yourname@gmail.com`
2. ✅ **EMAIL_PASS** = `[16-character Gmail App Password]`
3. ✅ **MYSQL_SSL** = `false` (if not already added)

---

## 🔄 **After Adding Variables**

1. **Redeploy your site**:
   - Go to **Deployments** tab in Vercel
   - Click the **"..."** menu on your latest deployment
   - Click **"Redeploy"**

2. **Test it**:
   - Try to register a new account
   - You should receive an email verification code
   - If you get an error, check Vercel logs

---

## 🆘 **Troubleshooting**

### **"App passwords" option not showing?**
- Make sure 2-Step Verification is **enabled** first
- It may take a few minutes to appear after enabling 2-Step Verification

### **"Email service is not configured" error?**
- Check that both `EMAIL_USER` and `EMAIL_PASS` are added
- Make sure you used the **App Password**, not your regular Gmail password
- Make sure you **redeployed** after adding variables

### **"Invalid login" error?**
- Double-check the App Password (copy it exactly)
- Make sure there are no extra spaces
- Try generating a new App Password

### **Not receiving emails?**
- Check your spam folder
- Verify the email address in `EMAIL_USER` is correct
- Check Vercel function logs for email errors

---

## 📝 **Quick Summary**

1. Enable 2-Step Verification in Google Account
2. Generate Gmail App Password for "Mail" → "Mindify"
3. Copy the 16-character password
4. Add `EMAIL_USER` = your Gmail address
5. Add `EMAIL_PASS` = the App Password
6. Add `MYSQL_SSL` = `false` (if missing)
7. Redeploy your site
8. Test registration!

---

**That's it!** Once you add these 2-3 variables and redeploy, email functionality should work perfectly. 🎉

