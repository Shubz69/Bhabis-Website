# Update Existing User to Super Admin

## 🔧 **Update shubzfx@gmail.com to SUPER_ADMIN Role**

If you already have an account with `shubzfx@gmail.com`, you need to update it to SUPER_ADMIN role in the database.

---

## **Method 1: Using MySQL Workbench (Easiest)**

1. **Connect to Railway MySQL:**
   - Open MySQL Workbench
   - Connect using your Railway MySQL credentials

2. **Run This SQL Query:**
   ```sql
   UPDATE users 
   SET role = 'SUPER_ADMIN' 
   WHERE email = 'shubzfx@gmail.com';
   ```

3. **Verify the Update:**
   ```sql
   SELECT id, username, email, role 
   FROM users 
   WHERE email = 'shubzfx@gmail.com';
   ```
   
   You should see `role = 'SUPER_ADMIN'`

4. **Done!** Log out and log back in to see admin features.

---

## **Method 2: Using Railway MySQL CLI (Alternative)**

If you have access to Railway CLI:

1. Connect to Railway MySQL
2. Run the UPDATE query above

---

## **Method 3: Create New Account (If Account Doesn't Exist)**

If you don't have an account yet:

1. Register with `shubzfx@gmail.com`
2. The new registration code will **automatically** assign SUPER_ADMIN role
3. Complete email verification
4. You'll have full admin access!

---

## ✅ **What You'll Get as Super Admin**

Once your account has SUPER_ADMIN role:

- ✅ Full access to Admin Panel
- ✅ Can manage all users
- ✅ Can create/edit/delete courses
- ✅ Can manage all channels and messages
- ✅ Can assign admin roles to other users
- ✅ Can access all admin features
- ✅ Complete system control

---

## 🔍 **Verify Super Admin Access**

After updating:

1. **Log out** of your account
2. **Log back in** with `shubzfx@gmail.com`
3. You should see **"Admin Panel"** link in navigation
4. Click it to access admin features

---

## 🆘 **Troubleshooting**

### **Still seeing "USER" role after update?**
- Make sure you updated the database correctly
- Clear browser cache and localStorage
- Log out and log back in

### **Don't have MySQL Workbench access?**
- Use Railway's MySQL service interface
- Or wait until database connection is fixed, then use the admin panel

---

**Note:** Once database connection is fixed (see `FIX_DATABASE_CONNECTION.md`), you can also use the Admin Panel to update user roles if needed.

