# Exact Vercel Environment Variables to Fix Database Connection

## 🔴 **The Problem**

Your `MYSQL_HOST` in Vercel is set to `mysql.railway.internal`, which only works inside Railway's network. Vercel is external, so it can't reach it.

## ✅ **The Solution**

Use the **PUBLIC** Railway MySQL hostname from your `MYSQL_PUBLIC_URL`.

---

## 📋 **Exact Values to Use in Vercel**

Based on your Railway MySQL service, here are the **exact values** you need:

### **Update These Variables in Vercel:**

| Variable Name | Current Value (WRONG) | New Value (CORRECT) | Source |
|--------------|----------------------|---------------------|---------|
| `MYSQL_HOST` | `mysql.railway.internal` | `yamanote.proxy.rlwy.net` | From `MYSQL_PUBLIC_URL` |
| `MYSQL_PORT` | `3306` | `15135` | From `MYSQL_PUBLIC_URL` |

### **Keep These Values (Already Correct):**

| Variable Name | Value | Notes |
|--------------|-------|-------|
| `MYSQL_USER` | `root` | Already correct |
| `MYSQL_PASSWORD` | `iQXsKMYyJKGuaEdENhwNBOCTBtDhpsnU` | Already correct |
| `MYSQL_DATABASE` | `railway` | Already correct |
| `MYSQL_SSL` | `false` | Must be `false` for Railway |

---

## 🔧 **Step-by-Step: Update in Vercel**

1. **Go to Vercel Dashboard:**
   - Visit: https://vercel.com/shobhit-singhs-projects-c3f665ca/bhabis-website-1r9x/settings/environment-variables

2. **Update MYSQL_HOST:**
   - Find `MYSQL_HOST` in your variables
   - Click the **"..."** menu → **"Edit"**
   - **Change value to:** `yamanote.proxy.rlwy.net`
   - Make sure all environments are selected ✅
   - Click **"Save"**

3. **Update MYSQL_PORT:**
   - Find `MYSQL_PORT` in your variables (or add it if missing)
   - **Change value to:** `15135`
   - Make sure all environments are selected ✅
   - Click **"Save"**

4. **Verify MYSQL_SSL:**
   - Find `MYSQL_SSL` (or add it if missing)
   - Make sure value is: `false`
   - Make sure all environments are selected ✅
   - Click **"Save"**

5. **Redeploy:**
   - Go to **"Deployments"** tab
   - Click **"..."** on latest deployment
   - Click **"Redeploy"**
   - Wait 1-2 minutes

---

## ✅ **Complete List of MySQL Variables for Vercel**

After updating, you should have these 6 variables:

```
MYSQL_HOST = yamanote.proxy.rlwy.net
MYSQL_PORT = 15135
MYSQL_USER = root
MYSQL_PASSWORD = iQXsKMYyJKGuaEdENhwNBOCTBtDhpsnU
MYSQL_DATABASE = railway
MYSQL_SSL = false
```

---

## 🎯 **Key Points**

- ❌ **DON'T use:** `mysql.railway.internal` (internal only, won't work from Vercel)
- ✅ **USE:** `yamanote.proxy.rlwy.net` (public hostname, works from anywhere)

- ❌ **DON'T use:** Port `3306` (internal port)
- ✅ **USE:** Port `15135` (public port from MYSQL_PUBLIC_URL)

---

## 🔍 **How I Found These Values**

From your Railway dashboard:
- `MYSQL_PUBLIC_URL` shows: `mysql://root:...@yamanote.proxy.rlwy.net:15135/railway`
- The hostname is: `yamanote.proxy.rlwy.net`
- The port is: `15135`

---

## ✅ **After Updating**

Once you update `MYSQL_HOST` to `yamanote.proxy.rlwy.net` and `MYSQL_PORT` to `15135`, then redeploy:

- ✅ Database connection errors will be fixed
- ✅ Email verification will work
- ✅ User registration will work
- ✅ All database operations will work

**Don't forget to redeploy after changing environment variables!**

