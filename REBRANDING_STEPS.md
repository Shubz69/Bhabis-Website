# Complete Rebranding Guide: TheGlitch → Mindify

## 📋 Overview
This guide will walk you through completing the rebranding from "TheGlitch" to "Mindify" and setting up new infrastructure (Railway + MySQL).

---

## 🎨 PHASE 3: Complete UI Branding Updates

### Step 3.1: I'll Update Remaining Brand References
I'll search and replace all remaining "Glitch", "Infinity", "TheGlitch" references in:
- All page components
- All component files  
- CSS files with brand names
- Any remaining service files

**Status**: I'll do this automatically for you.

---

## 🚀 PHASE 4: Set Up New Railway Project & MySQL Database

### Step 4.1: Create New Railway Account/Project

1. **Go to Railway**: https://railway.app/
2. **Sign up/Login**: Use your GitHub account (recommended)
3. **Create New Project**:
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repo: `Shubz69/Bhabis-Website`
   - Name it: `mindify-website` or `mindify-production`

### Step 4.2: Add MySQL Database Service

1. **In your Railway project dashboard**:
   - Click "+ New"
   - Select "Database"
   - Choose "MySQL"

2. **Configure MySQL**:
   - Railway will automatically create a MySQL database
   - Wait 1-2 minutes for it to provision

3. **Get Database Credentials**:
   - Click on the MySQL service in your project
   - Go to the "Variables" tab
   - You'll see these variables (SAVE THESE!):
     - `MYSQL_HOST` (e.g., `containers-us-west-xxx.railway.app`)
     - `MYSQL_PORT` (usually `3306`)
     - `MYSQLDATABASE` (database name)
     - `MYSQLUSER` (username)
     - `MYSQLPASSWORD` (password)
     - `MYSQL_ROOT_PASSWORD` (root password)

4. **Alternative: Use FreeSQLDatabase.com** (Free option):
   - Go to https://freesqldatabase.com/
   - Sign up for free account
   - Create new database
   - Save connection details:
     - Host
     - Database name
     - Username
     - Password
     - Port (usually 3306)

### Step 4.3: Connect MySQL Workbench to New Database

1. **Open MySQL Workbench**
2. **Create New Connection**:
   - Click the "+" icon next to "MySQL Connections"
   - Connection Name: `Mindify Production`
   - Hostname: (Your Railway MYSQL_HOST or FreeSQL host)
   - Port: `3306` (or the port provided)
   - Username: (Your MySQL username)
   - Password: (Click "Store in Keychain" and enter password)
   - Default Schema: (Your database name)

3. **Test Connection**:
   - Click "Test Connection"
   - Should see "Successfully made the MySQL connection"

4. **Connect**:
   - Double-click the new connection
   - You're now connected to your new Mindify database

---

## 💾 PHASE 5: Import Database Schema

### Step 5.1: Export Schema from Old Database (if you have access)

**Option A: Export from Old MySQL Workbench Connection**
1. Connect to old database
2. Go to: `Server` → `Data Export`
3. Select your old database
4. Choose "Export to Self-Contained File"
5. Save as: `mindify_schema_backup.sql`
6. Click "Start Export"

**Option B: Use SQLite Database (if you have the old one locally)**
- We have `data.sqlite3` in the project
- We can convert it to MySQL format

### Step 5.2: Import Schema to New Database

1. **In MySQL Workbench** (connected to new Mindify database):
2. Go to: `Server` → `Data Import`
3. Select "Import from Self-Contained File"
4. Choose your exported SQL file
5. Select "New" under "Default Target Schema" and name it (same as your database name)
6. Click "Start Import"

### Step 5.3: Create Database Tables (Alternative: Manual Creation)

If you don't have an export, we'll need to create tables. I can help generate the SQL schema based on your API files.

---

## 🔧 PHASE 6: Update Code Configuration

### Step 6.1: Update Environment Variables in Railway

1. **In Railway Dashboard**:
   - Go to your project
   - Click on your deployed service (or create one)
   - Go to "Variables" tab
   - Add these environment variables:

```env
# Database Configuration
DB_HOST=your_mysql_host_from_railway
DB_PORT=3306
DB_NAME=your_database_name
DB_USER=your_mysql_username
DB_PASSWORD=your_mysql_password

# Server Configuration  
PORT=8080
NODE_ENV=production

# Email Configuration (Update with your email)
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password

# Stripe (Update with your Stripe keys)
STRIPE_SECRET_KEY=sk_live_your_stripe_key
STRIPE_PUBLISHABLE_KEY=pk_live_your_stripe_key

# JWT Secret (Generate new one)
JWT_SECRET=your_new_jwt_secret_here

# AES Encryption Key (Generate new one)
AES_ENCRYPTION_KEY=your_new_aes_key_here

# OpenAI API Key (if using)
OPENAI_API_KEY=your_openai_key
```

### Step 6.2: Generate New Secrets

**Generate JWT Secret** (in terminal):
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
```

**Generate AES Encryption Key** (in terminal):
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

Save these values to your Railway environment variables.

---

## 📝 PHASE 7: Update Code Files

### Files I'll Update Once You Provide Database Credentials:

1. **API Files** (will need database connection strings):
   - `api/auth/login.js`
   - `api/auth/register.js`
   - `api/community/channels.js`
   - `api/courses.js`
   - `api/leaderboard.js`
   - All other API files

2. **Server Configuration**:
   - `server.js` - Update database connection

3. **Environment Configuration Files**:
   - Create `.env.example` file
   - Update any hardcoded database references

---

## 🚀 PHASE 8: Deploy to Railway

### Step 8.1: Configure Railway Deployment

1. **In Railway Dashboard**:
   - Make sure your GitHub repo is connected
   - Railway will auto-detect your `package.json`
   - Set Root Directory: `/` (root of repo)
   - Build Command: `npm install && npm run build`
   - Start Command: `node server.js`
   - Environment: `production`

### Step 8.2: Set Up Custom Domain (Optional)

1. **In Railway Dashboard**:
   - Go to your service
   - Click "Settings" → "Networking"
   - Click "Generate Domain" to get a Railway domain
   - Or add custom domain (you'll need to configure DNS)

### Step 8.3: Deploy

1. Railway will auto-deploy when you push to GitHub
2. Or click "Deploy" button manually
3. Watch the build logs for any errors

---

## ✅ PHASE 9: Testing Checklist

### Step 9.1: Test Database Connection
- [ ] Can connect to database via MySQL Workbench
- [ ] Can see tables in database
- [ ] Can run basic queries

### Step 9.2: Test API Endpoints
- [ ] `/api/auth/register` - User registration works
- [ ] `/api/auth/login` - Login works
- [ ] `/api/courses` - Courses load
- [ ] Database writes/reads work

### Step 9.3: Test Frontend
- [ ] Homepage loads with "Mindify" branding
- [ ] Can register new account
- [ ] Can login
- [ ] Can access courses
- [ ] All pages show "Mindify" (not "Glitch")

---

## 📋 Quick Reference: What You Need to Provide Me

Once you complete Railway setup, provide me:

```
Database Host: _______________
Database Name: _______________
Database User: _______________
Database Password: _______________
Database Port: _______________
Railway Domain/URL: _______________
```

Then I'll update all the code files for you!

---

## 🔄 Current Status

- ✅ Phase 1: Foundation files updated
- ✅ Phase 2: API base URL placeholder added
- 🔄 Phase 3: UI branding (in progress)
- ⏳ Phase 4: Railway + MySQL setup (your turn)
- ⏳ Phase 5-9: Waiting for your database credentials

---

## 💡 Tips

1. **Keep old database running** until new one is fully tested
2. **Test locally first** before deploying to production
3. **Use environment variables** - never hardcode secrets
4. **Backup everything** before making changes
5. **Document your credentials** in a secure password manager

---

Need help with any step? Let me know where you're stuck!

