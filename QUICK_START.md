# 🚀 Quick Start Guide

## ✅ Installation Complete!

Your Hainanese Chicken Rice Inventory Management PWA is ready to use!

## 🎯 Running the Application

The development server should now be running. If not, run:

```bash
npm run dev
```

Then open your browser and navigate to:
- **Local**: `http://localhost:5173`
- **Network**: Check the terminal output for your network IP

## 🔐 First Login

Use these default credentials:

### Employee Login
- **Code**: `9999`
- **Access**: Count Stock, View Purchase Lists, Receive Items

### Super-Manager Login
- **Code**: `552499`
- **Access**: Full System Control

⚠️ **IMPORTANT**: Change these codes immediately via Settings!

## 📦 Pre-loaded Data

The system comes with **42 pre-configured items** across 7 categories:
- ของสด (Fresh Items) - 12 items
- ของแห้ง/วัตถุดิบหลัก (Dry Goods) - 2 items
- ของปรุงรส/เครื่องปรุงเหลว (Liquid Seasonings) - 12 items
- ผงปรุงรส/เครื่องเทศ (Powder Seasonings) - 5 items
- ของใช้ในครัว/ทำความสะอาด (Kitchen Supplies) - 8 items
- ของประเภทโปรตีนสำเร็จรูป (Ready-made Protein) - 2 items
- ของหมักดอง (Pickled Items) - 1 item

All items are automatically loaded on first run!

## 🎨 Available Routes

### For Everyone
- `/login` - Login page

### For Employees (9999)
- `/dashboard` - Overview with stats and alerts
- `/count` - Count stock with numeric keypad
- `/purchase-list` - View and export purchase orders
- `/receive` - Mark items as received

### For Super-Manager (552499) - All above plus:
- `/stock` - Manage inventory items (CRUD)
- `/reports` - Advanced analytics and reports
- `/settings` - Configure system settings
- `/audit` - View complete audit trail

## 🔥 Key Features to Try

### 1. Count Stock (Employee)
1. Login with `0000`
2. Go to "นับสต็อก" (Count Stock)
3. Tap any item card
4. Use the numeric keypad to enter quantity
5. Save individual or bulk save all

### 2. Generate Purchase List
1. After counting, go to "รายการสั่งซื้อ" (Purchase List)
2. System automatically calculates what to order
3. Export as text for WhatsApp/LINE
4. Or export as CSV for Excel

### 3. Receive Items
1. Go to "รับสินค้า" (Receive)
2. Review suggested quantities
3. Adjust if needed
4. Confirm receipt - stock automatically updates!

### 4. Manage Inventory (Manager)
1. Login with `552499`
2. Go to "จัดการสินค้า" (Stock)
3. Add/Edit/Delete items
4. Set min levels, daily usage, order cycles
5. Export/Import data as JSON

### 5. View Reports (Manager)
1. Check dashboard for overview
2. Go to "รายงาน" (Reports)
3. See category-wise statistics
4. View items by days until empty
5. Export detailed reports

## 📱 Install as PWA

### On Mobile (iOS/Android)
1. Open the app in your mobile browser
2. Tap browser menu (⋮ or share icon)
3. Select "Add to Home Screen"
4. Icon appears on home screen - works offline!

### On Desktop (Chrome/Edge)
1. Look for install icon (➕) in address bar
2. Click "Install"
3. App opens in standalone window

## 💾 Backup Your Data

**Important**: Always backup before making major changes!

1. Go to Stock Management
2. Click "ส่งออกทั้งหมด" (Export All)
3. Save the JSON file somewhere safe
4. To restore: Click "นำเข้า" (Import) and select the file

## ⚙️ Essential Settings

1. Login as Super-Manager (`552499`)
2. Go to Settings
3. Update:
   - Business name
   - Login codes (change from defaults!)
   - Days ahead coverage (for purchase calculations)
4. Save settings

## 🎯 Daily Workflow Example

### Morning (9 AM)
1. Employee logs in
2. Checks dashboard for alerts
3. Reviews purchase list
4. Sends order to suppliers via WhatsApp

### Throughout Day
1. Counts stock when received
2. Updates quantities in system
3. Checks alerts periodically

### Evening (Closing)
1. Final stock count
2. Review tomorrow's purchase needs
3. Manager reviews reports
4. Export backup (weekly)

## 🐛 Troubleshooting

### App won't load
- Clear browser cache
- Try different browser
- Check JavaScript is enabled

### Data not saving
- Check localStorage is enabled
- Ensure sufficient storage
- Try export then re-import

### Forgot Super-Manager code
- Open browser DevTools (F12)
- Go to Application > Local Storage
- Find `settings.v1`
- Delete entry or edit `superCode`
- Defaults will restore: `552499`

## 📚 Need More Help?

See the complete **README.md** for:
- Detailed feature documentation
- Architecture overview
- Complete acceptance criteria
- Security best practices
- Advanced configuration

## 🎉 You're All Set!

Start by logging in and exploring the Dashboard. The system is designed to be intuitive - just start using it!

**Happy inventory management! 🍗**

---

**Questions or Issues?**
- Check README.md for detailed documentation
- Review the inline help in each page
- Check browser console for errors (F12)

