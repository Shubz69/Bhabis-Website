# Fix Database Connection Error - Railway MySQL

## 🔴 **The Problem**

You're getting "Database connection error" because `MYSQL_HOST` is set to `mysql.railway.internal`, which only works **inside Railway's internal network**. 

**Vercel (your frontend) is external**, so it can't reach the internal hostname. You need the **public Railway MySQL hostname**.

---

## ✅ **Solution: Get the Public Railway MySQL Hostname**

### **Step 1: Get Railway Connection String**

1. Go to [Railway Dashboard](https://railway.app)
2. Click on your **MySQL service**
3. Click the **"Variables"** tab
4. Look for these variables:
   - `MYSQLHOST` - This is the **internal** hostname (don't use this for Vercel)
   - `MYSQLUSER`
   - `MYSQLPASSWORD`
   - `MYSQLDATABASE`
   - `MYSQLPORT`

### **Step 2: Get Public Hostname from Railway**

**Option A: From Railway Dashboard**
1. In your MySQL service, click the **"Connect"** tab
2. You should see connection details
3. Look for a **public hostname** or **connection string**
4. It should look like: `containers-us-west-xxx.railway.app` or `mysql-production.up.railway.app`

**Option B: From Railway Connection Info**
1. In your MySQL service, click **"Settings"**
2. Look for **"Public Networking"** or **"Connection Info"**
3. Find the **public hostname** (not the internal one)

**Option C: Use Railway's Generated Public URL**
1. Railway may provide a **public connection URL**
2. Extract the hostname from it (everything before the `:` port number)

### **Step 3: Update MYSQL_HOST in Vercel**

1. Go to **Vercel Dashboard** → Your Project → **Settings** → **Environment Variables**
2. Find `MYSQL_HOST` in your variables
3. Click the **"..."** menu next to it → **Edit**
4. **Change the value** from `mysql.railway.internal` to the **public hostname** you found
   - Example: `containers-us-west-xxx.railway.app`
5. Make sure `MYSQL_SSL` is set to `false`
6. Click **Save**

### **Step 4: Verify Other MySQL Variables**

Make sure these match exactly what you see in Railway:
- ✅ `MYSQL_HOST` = Public hostname (not internal)
- ✅ `MYSQL_USER` = From Railway: `MYSQLUSER`
- ✅ `MYSQL_PASSWORD` = From Railway: `MYSQLPASSWORD`
- ✅ `MYSQL_DATABASE` = From Railway: `MYSQLDATABASE`
- ✅ `MYSQL_PORT` = From Railway: `MYSQLPORT` (usually `3306`)
- ✅ `MYSQL_SSL` = `false`

### **Step 5: Redeploy**

After updating `MYSQL_HOST`:
1. Go to **Deployments** tab
2. Click **"..."** on latest deployment → **"Redeploy"**
3. Wait 1-2 minutes for deployment to complete

---

## 🔍 **How to Find Your Public Railway MySQL Hostname**

If you can't find it in Railway dashboard, try this:

1. **Check Railway Connection Info:**
   - Railway usually shows connection info like: `mysql://root:password@hostname:3306/railway`
   - The `hostname` part is what you need (the part between `@` and `:`)

2. **Check Railway Service Settings:**
   - Go to MySQL service → Settings
   - Look for "Public URL" or "Connection String"

3. **Common Railway MySQL Public Hostnames:**
   - `containers-us-west-xxx.railway.app`
   - `containers-us-east-xxx.railway.app`
   - `mysql-production.up.railway.app`
   - `xxx-production.up.railway.app`

---

## ⚠️ **Important Notes**

- **Internal hostname** (`mysql.railway.internal`) only works from within Railway services
- **Vercel is external**, so it needs the **public hostname**
- Make sure Railway MySQL service has **public networking enabled** (most Railway MySQL services have this by default)

---

## 🆘 **Still Having Issues?**

If you still get connection errors:

1. **Check Railway MySQL is Running:**
   - Railway Dashboard → MySQL service → Make sure it's "Active"

2. **Verify Railway MySQL Allows External Connections:**
   - Some Railway MySQL services only allow internal connections
   - Check Railway MySQL service settings for "Public Networking"

3. **Check Firewall/Network Settings:**
   - Railway MySQL should accept connections from anywhere (0.0.0.0/0)
   - Check Railway service settings

4. **Test Connection:**
   - Try connecting from MySQL Workbench using the public hostname
   - If that works, Vercel should work too

---

## ✅ **After Fixing**

Once you update `MYSQL_HOST` to the public hostname and redeploy:
- ✅ Database connection errors should be gone
- ✅ Email verification should work
- ✅ User registration should work
- ✅ All database operations should work

**Remember to redeploy after changing environment variables!**

