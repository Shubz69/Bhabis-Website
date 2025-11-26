# Environment Variables Quick Reference

## 🚨 **REQUIRED VARIABLES (Add to Vercel)**

### **MySQL Database (Get from Railway Dashboard → MySQL Service → Variables Tab)**

```
MYSQL_HOST = [from Railway: MYSQLHOST]
MYSQL_USER = [from Railway: MYSQLUSER]
MYSQL_PASSWORD = [from Railway: MYSQLPASSWORD]
MYSQL_DATABASE = [from Railway: MYSQLDATABASE]
MYSQL_PORT = [from Railway: MYSQLPORT] (usually 3306)
MYSQL_SSL = false
```

### **Email (Gmail Example)**

```
EMAIL_USER = youremail@gmail.com
EMAIL_PASS = [Gmail App Password - 16 characters, no spaces]
```

**To get Gmail App Password:**
1. Google Account → Security → 2-Step Verification → App passwords
2. Generate for "Mail" → Copy 16-character password

### **Security Keys**

```
JWT_SECRET = [Generate: node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"]
AES_ENCRYPTION_KEY = v8y/B?E(H+KbPeShVmYq3t6w9z$C&F)J
```

---

## ⚙️ **OPTIONAL VARIABLES (Add Later if Needed)**

### **Stripe (For Payments)**

```
STRIPE_SECRET_KEY = sk_live_...
REACT_APP_STRIPE_PUBLIC_KEY = pk_live_...
```

### **OpenAI (For Chatbot)**

```
OPENAI_API_KEY = sk-proj-...
```

### **Custom Email Provider (Instead of Gmail)**

```
EMAIL_HOST = smtp.sendgrid.net
EMAIL_PORT = 587
EMAIL_SECURE = false
```

---

## 📝 **HOW TO ADD TO VERCEL**

1. Vercel Dashboard → Your Project → Settings → Environment Variables
2. Click "Add New"
3. Enter Key and Value
4. Select: Production ✅ Preview ✅ Development ✅
5. Save
6. **Redeploy** your site

---

## ✅ **CHECKLIST**

- [ ] MySQL variables (6 total)
- [ ] Email variables (2 total)
- [ ] JWT_SECRET
- [ ] AES_ENCRYPTION_KEY
- [ ] Optional: Stripe keys
- [ ] Optional: OpenAI key

---

**Total Required**: 10 variables
**Total Optional**: 3-5 variables

