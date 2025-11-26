# Quick Steps: Add Gmail Variables to Vercel

## ✅ **Your Gmail App Password**

You've successfully generated: `hhbq lets dhoy eixu`

You can use this password **with or without spaces**:
- With spaces: `hhbq lets dhoy eixu`
- Without spaces: `hhbqletsdhoyeixu`

Both will work! 

---

## 📝 **Step-by-Step: Add to Vercel**

### **Step 1: Go to Vercel Environment Variables**

1. Open your Vercel project: https://vercel.com/shobhit-singhs-projects-c3f665ca/bhabis-website-1r9x/settings/environment-variables
2. You should already be on the Environment Variables page (where you see all your MySQL variables)

### **Step 2: Add EMAIL_USER**

1. Click the **"Add New"** button at the top right
2. Enter:
   - **Key**: `EMAIL_USER`
   - **Value**: Your Gmail address (the one you used to generate the app password)
     - Example: `youremail@gmail.com`
   - **Environments**: Select all three ✅
     - ✅ Production
     - ✅ Preview  
     - ✅ Development
3. Click **"Save"**

### **Step 3: Add EMAIL_PASS**

1. Click **"Add New"** button again
2. Enter:
   - **Key**: `EMAIL_PASS`
   - **Value**: `hhbq lets dhoy eixu`
     - Or use without spaces: `hhbqletsdhoyeixu`
     - Either way works!
   - **Environments**: Select all three ✅
     - ✅ Production
     - ✅ Preview
     - ✅ Development
3. Click **"Save"**

### **Step 4: Verify MYSQL_SSL (Check if it exists)**

1. Look through your existing variables
2. If you see `MYSQL_SSL`, make sure its value is `false`
3. If you DON'T see `MYSQL_SSL`, add it:
   - Click **"Add New"**
   - **Key**: `MYSQL_SSL`
   - **Value**: `false`
   - **Environments**: Select all three ✅
   - Click **"Save"**

---

## 🔄 **Step 5: Redeploy Your Site**

**Important!** After adding variables, you MUST redeploy:

1. Go to the **"Deployments"** tab (top navigation)
2. Find your latest deployment
3. Click the **"..."** (three dots) menu button
4. Click **"Redeploy"**
5. Wait for deployment to complete (1-2 minutes)

---

## ✅ **Final Checklist**

After redeploy, you should have these variables:

- ✅ `MYSQL_HOST` (already have)
- ✅ `MYSQL_USER` (already have)
- ✅ `MYSQL_PASSWORD` (already have)
- ✅ `MYSQL_DATABASE` (already have)
- ✅ `MYSQL_PORT` (already have)
- ✅ `MYSQL_SSL` = `false` (check or add)
- ✅ `EMAIL_USER` = `your-gmail@gmail.com` (add now)
- ✅ `EMAIL_PASS` = `hhbq lets dhoy eixu` (add now)
- ✅ `JWT_SECRET` (already have)
- ✅ `AES_ENCRYPTION_KEY` (already have)

---

## 🧪 **Test It!**

After redeploying:

1. Go to your website
2. Try to **register a new account**
3. You should receive an **email verification code**
4. Check your email (and spam folder if needed)

If you get an email, it's working! 🎉

---

## 🆘 **Troubleshooting**

### **"Email service is not configured" error?**
- Make sure you added BOTH `EMAIL_USER` AND `EMAIL_PASS`
- Make sure you **redeployed** after adding variables
- Check for typos in variable names (case-sensitive!)

### **"Invalid login" error?**
- Make sure you used the App Password, not your regular Gmail password
- Copy the password exactly: `hhbq lets dhoy eixu`

### **Not receiving emails?**
- Check spam folder
- Wait a minute or two (emails can be delayed)
- Check Vercel function logs for errors

---

**That's it!** Once you add these two variables and redeploy, email functionality will work. 🚀

