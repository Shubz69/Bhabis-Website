# Complete Environment Variables Setup Guide for Mindify

## 📋 Overview

This guide lists all environment variables needed for your Mindify website, organized by priority and where they need to be added (Vercel vs Railway).

---

## 🚨 **PRIORITY 1: REQUIRED VARIABLES (Add These First!)**

These are **critical** for basic functionality. Your site won't work properly without them.

### **1. MySQL Database Variables (Railway - Already Connected ✅)**

You've already connected MySQL Workbench to Railway, so you have these values! Add them to **Vercel**.

| Variable Name | Description | Where to Find | Example Value |
|--------------|-------------|---------------|---------------|
| `MYSQL_HOST` | Railway MySQL hostname | Railway Dashboard → MySQL Service → Variables tab → `MYSQLHOST` | `containers-us-west-xxx.railway.app` |
| `MYSQL_USER` | Database username | Railway Dashboard → MySQL Service → Variables tab → `MYSQLUSER` | `root` |
| `MYSQL_PASSWORD` | Database password | Railway Dashboard → MySQL Service → Variables tab → `MYSQLPASSWORD` | `your_password_here` |
| `MYSQL_DATABASE` | Database name | Railway Dashboard → MySQL Service → Variables tab → `MYSQLDATABASE` | `railway` |
| `MYSQL_PORT` | Database port | Railway Dashboard → MySQL Service → Variables tab → `MYSQLPORT` | `3306` |
| `MYSQL_SSL` | SSL connection (usually false for Railway) | Set manually | `false` |

**How to get Railway MySQL credentials:**
1. Go to [Railway Dashboard](https://railway.app)
2. Click on your MySQL service
3. Click the **"Variables"** tab
4. Find these variables:
   - `MYSQLHOST` → Use for `MYSQL_HOST`
   - `MYSQLUSER` → Use for `MYSQL_USER`
   - `MYSQLPASSWORD` → Use for `MYSQL_PASSWORD`
   - `MYSQLDATABASE` → Use for `MYSQL_DATABASE`
   - `MYSQLPORT` → Use for `MYSQL_PORT`

---

### **2. Email Service Variables (Required for User Registration!)**

These are needed for:
- Email verification codes (signup)
- Password reset emails
- MFA (Multi-Factor Authentication) codes
- Contact form submissions

#### **Option A: Gmail (Easiest - Recommended for Quick Setup)**

| Variable Name | Description | How to Get |
|--------------|-------------|------------|
| `EMAIL_USER` | Your Gmail address | Your Gmail address (e.g., `youremail@gmail.com`) |
| `EMAIL_PASS` | Gmail App Password | **NOT your regular password!** See steps below |

**Steps to create Gmail App Password:**
1. Go to [Google Account Settings](https://myaccount.google.com/)
2. Click **Security** → **2-Step Verification** (enable it if not enabled)
3. Scroll down to **App passwords**
4. Select **Mail** and **Other (Custom name)**
5. Type "Mindify" and click **Generate**
6. Copy the 16-character password (no spaces)
7. Use this as your `EMAIL_PASS` value

**Example:**
```
EMAIL_USER = yourname@gmail.com
EMAIL_PASS = abcd efgh ijkl mnop
```

#### **Option B: Custom SMTP Server (Any Email Service)**

If you want to use a different email provider (Outlook, SendGrid, Mailgun, etc.):

| Variable Name | Description | Example |
|--------------|-------------|---------|
| `EMAIL_USER` | Your email address | `noreply@mindify.app` |
| `EMAIL_PASS` | Email password/API key | Your email password |
| `EMAIL_HOST` | SMTP server hostname | `smtp.sendgrid.net` or `smtp.office365.com` |
| `EMAIL_PORT` | SMTP port | `587` (usually) or `465` for SSL |
| `EMAIL_SECURE` | Use SSL/TLS | `false` for port 587, `true` for port 465 |

**Popular Email Services:**
- **SendGrid**: `smtp.sendgrid.net`, port `587`
- **Mailgun**: `smtp.mailgun.org`, port `587`
- **Outlook/Office365**: `smtp.office365.com`, port `587`
- **Zoho**: `smtp.zoho.com`, port `587`

---

### **3. JWT Secret (Required for Authentication)**

Used to sign and verify authentication tokens.

| Variable Name | Description | How to Generate |
|--------------|-------------|-----------------|
| `JWT_SECRET` | Secret key for JWT tokens | Generate a random string (see below) |

**How to generate JWT_SECRET:**
1. **Option 1**: Use Node.js
   ```bash
   node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
   ```
2. **Option 2**: Use online generator: https://randomkeygen.com/
3. **Option 3**: Use a long random string (at least 32 characters)

**Example:**
```
JWT_SECRET = a8f5f167f44f4964e6c998dee827110c8f5f167f44f4964e6c998dee827110c
```

⚠️ **IMPORTANT**: Keep this secret! Don't share it publicly.

---

### **4. AES Encryption Key (Required for Data Encryption)**

Used to encrypt sensitive data in the database.

| Variable Name | Description | Default Value |
|--------------|-------------|---------------|
| `AES_ENCRYPTION_KEY` | 32-character encryption key | Use the default or generate your own |

**Default (you can use this):**
```
AES_ENCRYPTION_KEY = v8y/B?E(H+KbPeShVmYq3t6w9z$C&F)J
```

**Or generate your own (32 characters):**
```bash
node -e "console.log(require('crypto').randomBytes(16).toString('base64'))"
```

---

## ✅ **PRIORITY 2: OPTIONAL VARIABLES (Add Later if Needed)**

These enhance functionality but aren't required for basic operation.

### **5. Stripe Payment Variables (Optional - For Payments)**

Only needed if you want to accept payments.

| Variable Name | Description | Where to Get |
|--------------|-------------|--------------|
| `STRIPE_SECRET_KEY` | Stripe secret key | [Stripe Dashboard](https://dashboard.stripe.com/apikeys) → API Keys |
| `STRIPE_WEBHOOK_SECRET` | Webhook signing secret | Stripe Dashboard → Webhooks → Add endpoint → Copy secret |
| `REACT_APP_STRIPE_PUBLIC_KEY` | Stripe publishable key | Stripe Dashboard → API Keys (Public key) |

**How to get Stripe keys:**
1. Sign up at [Stripe](https://stripe.com)
2. Go to [API Keys](https://dashboard.stripe.com/apikeys)
3. Copy:
   - **Publishable key** → `REACT_APP_STRIPE_PUBLIC_KEY` (add to Vercel with `REACT_APP_` prefix)
   - **Secret key** → `STRIPE_SECRET_KEY`

---

### **6. OpenAI API Key (Optional - For Advanced Chatbot)**

Only needed if your chatbot uses OpenAI GPT.

| Variable Name | Description | Where to Get |
|--------------|-------------|--------------|
| `OPENAI_API_KEY` | OpenAI API key | [OpenAI Platform](https://platform.openai.com/api-keys) |

**How to get OpenAI key:**
1. Go to [OpenAI Platform](https://platform.openai.com)
2. Sign up/login
3. Go to **API Keys**
4. Click **Create new secret key**
5. Copy the key

⚠️ **Note**: The current codebase doesn't seem to use OpenAI in the chatbot, but if you want to add it later, you'll need this.

---

### **7. Frontend URL (Optional - Usually Auto-Detected)**

| Variable Name | Description | Example |
|--------------|-------------|---------|
| `FRONTEND_URL` | Your Vercel deployment URL | `https://bhabis-website-1r9x.vercel.app` |
| `REACT_APP_API_URL` | API base URL (if different from Vercel) | `https://mindify.app` (if using custom domain) |

**Usually you don't need to set these** - Vercel automatically detects your URL.

---

## 📝 **HOW TO ADD VARIABLES TO VERCEL**

### **Step-by-Step Instructions:**

1. **Go to Vercel Dashboard**
   - Visit [vercel.com](https://vercel.com)
   - Log in to your account

2. **Select Your Project**
   - Click on **"Bhabis-Website"** (or your project name)

3. **Go to Settings**
   - Click **"Settings"** tab at the top

4. **Navigate to Environment Variables**
   - Click **"Environment Variables"** in the left sidebar

5. **Add Each Variable**
   - Click **"Add New"**
   - Enter the **Key** (variable name)
   - Enter the **Value** (variable value)
   - Select environments:
     - ✅ **Production**
     - ✅ **Preview**
     - ✅ **Development**
   - Click **"Save"**

6. **Redeploy Your Site**
   - After adding variables, go to **"Deployments"** tab
   - Click the **"..."** menu on your latest deployment
   - Click **"Redeploy"**

---

## 🔄 **HOW TO ADD VARIABLES TO RAILWAY (If Needed)**

If you need to add environment variables to Railway services (not MySQL):

1. **Go to Railway Dashboard**
   - Visit [railway.app](https://railway.app)
   - Log in

2. **Select Your Service**
   - Click on the service (if you have any Node.js services)

3. **Go to Variables**
   - Click the **"Variables"** tab

4. **Add Variables**
   - Click **"New Variable"**
   - Enter key and value
   - Click **"Add"**

⚠️ **Note**: For this project, you typically only need variables in **Vercel**, not Railway. Railway is just for the MySQL database.

---

## 📋 **QUICK CHECKLIST**

### **Must Add Now:**
- [ ] `MYSQL_HOST` (from Railway)
- [ ] `MYSQL_USER` (from Railway)
- [ ] `MYSQL_PASSWORD` (from Railway)
- [ ] `MYSQL_DATABASE` (from Railway)
- [ ] `MYSQL_PORT` (from Railway, usually `3306`)
- [ ] `MYSQL_SSL` (set to `false`)
- [ ] `EMAIL_USER` (your email)
- [ ] `EMAIL_PASS` (Gmail App Password or email password)
- [ ] `JWT_SECRET` (generate random string)
- [ ] `AES_ENCRYPTION_KEY` (use default or generate)

### **Optional (Add Later):**
- [ ] `STRIPE_SECRET_KEY` (if using payments)
- [ ] `REACT_APP_STRIPE_PUBLIC_KEY` (if using payments)
- [ ] `OPENAI_API_KEY` (if using OpenAI)
- [ ] `EMAIL_HOST` (only if not using Gmail)
- [ ] `EMAIL_PORT` (only if not using Gmail)
- [ ] `EMAIL_SECURE` (only if not using Gmail)

---

## 🎯 **RECOMMENDED ORDER TO ADD VARIABLES**

1. **First**: MySQL variables (you already have these from Railway)
2. **Second**: Email variables (to fix registration)
3. **Third**: JWT_SECRET and AES_ENCRYPTION_KEY
4. **Last**: Optional variables (Stripe, OpenAI, etc.)

---

## 🔍 **VERIFYING YOUR VARIABLES**

After adding variables, you can verify they're working:

1. **Check Vercel Logs**
   - Go to Vercel → Your Project → Deployments
   - Click on a deployment → **"Functions"** tab
   - Check logs for errors about missing variables

2. **Test Registration**
   - Try to register a new account
   - If you get "Email service is not configured", email variables are missing
   - If you get database errors, MySQL variables are wrong

3. **Test Login**
   - If login works, JWT_SECRET is configured correctly

---

## 🆘 **TROUBLESHOOTING**

### **"Email service is not configured" error:**
- ✅ Make sure `EMAIL_USER` and `EMAIL_PASS` are set
- ✅ If using Gmail, use App Password (not regular password)
- ✅ Check for typos in variable names

### **Database connection errors:**
- ✅ Verify MySQL variables match Railway exactly
- ✅ Make sure `MYSQL_SSL` is set to `false` for Railway
- ✅ Check Railway MySQL service is running

### **Authentication errors:**
- ✅ Make sure `JWT_SECRET` is set (at least 32 characters)
- ✅ Redeploy after adding variables

---

## 📞 **NEED HELP?**

If you get stuck:
1. Check Vercel deployment logs for specific error messages
2. Verify variable names match exactly (case-sensitive!)
3. Make sure you redeployed after adding variables
4. Double-check Railway MySQL credentials

---

**Last Updated**: December 2024
**Project**: Mindify Website

