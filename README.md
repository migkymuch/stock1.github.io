# 🍗 Chicken Rice Inventory - Stock Management System

A production-ready, cloud-based inventory management system designed specifically for Hainanese chicken rice shops to achieve **ZERO stockouts** and **minimal waste**.

## 🎯 Features

- **Two Role System**: Super-Manager (full control) and Employee (count & view only)
- **Cloud-Based Storage**: Real-time data sync with Firebase Firestore
- **47 Pre-seeded Items**: Ready-to-use inventory items for chicken rice shop
- **Smart Purchase Calculation**: Auto-generates purchase lists based on min levels and daily usage
- **Real-time Alerts**: Red/Orange badges for items below or near minimum stock
- **Mobile-Optimized**: Touch-friendly numeric keypad for stock counting
- **Full Audit Trail**: Every action is logged with timestamp and user
- **Import/Export**: JSON backup and restore functionality
- **Thai Language UI**: Full Thai language interface with English dev comments

## 🚀 Quick Start

### Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

The app will be available at `http://localhost:5173`

### Default Login Codes

- **Employee**: `9999` (can count stock, view purchase lists, receive items)
- **Super-Manager**: `552499` (full access to all features)

⚠️ **Important**: Change these codes immediately after installation via Settings page!

## 🌐 Internet Connection Required

This system requires an active internet connection to function properly as all data is stored and synchronized with Firebase Firestore cloud database.

## 🎨 User Roles & Permissions

### Employee Role (9999)
✅ Can access:
- Dashboard (view stats)
- Count Stock (enter current quantities)
- Purchase List (view and export)
- Receive Items (mark items as received)

❌ Cannot access:
- Stock Management (CRUD items)
- Reports
- Settings
- Audit Log

### Super-Manager Role (552499)
✅ Full access to all features:
- All Employee features
- Stock Management (add/edit/delete items)
- Advanced Reports
- Settings (change codes, business info)
- Audit Log (view all actions)

## 📊 System Overview - 7 Steps

The system implements the 7-step stock management methodology:

1. **Categorize Stock**: 7 categories (fresh, dry goods, seasonings, etc.)
2. **Daily Stock Table**: Real-time inventory with current quantities
3. **Usage per Dish/Day**: Track daily usage patterns
4. **End-of-Day Check**: Employee counts and updates stock
5. **Fixed Ordering Cycles**: Configurable reorder cycles per item
6. **Auto Calculation & Alerts**: Smart purchase suggestions and low-stock warnings
7. **Clear Responsibility & Audit Trail**: Every action is logged

## 🗂️ Pre-seeded Inventory (42 Items)

The system comes with 42 pre-configured items across 7 categories:

### ของสด (Fresh Items) - 12 items
- ต้นผักชี, รากผักชี, ขิง (สด), ใบเตย, กระเทียม
- พริกแดงจินดา, พริกชี้ฟ้า (สีส้ม), ต้นหอม, แตงกวา
- ไก่ต้ม, ไก่สด, ไก่ทอด

### ของแห้ง/วัตถุดิบหลัก - 2 items
- ข้าวหอม (ถุงส้ม) กระสอบเต็ม
- ข้าวหอม (ถุงเปิดใช้ วางแยก)

### ของปรุงรส/เครื่องปรุงเหลว - 12 items
- มะขามเปียก, น้ำมะขามเปียก, น้ำส้มสายชู, น้ำตาลปี๊ป
- น้ำตาล, เกลือ, ซอสปรุงรส, ซีอิ๊วหวาน (ในครัว + ลูกค้า)
- ซอสหอยนางรม, น้ำมันพืช, น้ำมันงา

### ผงปรุงรส/เครื่องเทศ - 5 items
- ผงชูรส (อายิโนะฯ), พริกไทยดำ, พริกไทยขาว
- รสดีหมู (ถุงเขียว), รสดีผงไก่ (สีส้ม)

### ของใช้ในครัว/ทำความสะอาด - 8 items
- น้ำยาเช็ดกระจก, น้ำยาล้างจาน, ถุงมือ
- ถุงใส่อาหาร, ถุงใส่น้ำจิ้ม, กระดาษทิชชู
- ม้วนกระดาษเครื่องพิมพ์ใบเสร็จ (POS), น้ำหอม

### ของประเภทโปรตีนสำเร็จรูป - 2 items
- คนอไก่, คนอหมู

### ของหมักดอง - 1 item
- กระปุกกระเทียมดอง

## 💾 Data Management

### Export Data

**Export Inventory Only**:
1. Go to Stock Management page
2. Click "ส่งออกสินค้า" (Export Items)
3. Saves: `inventory-YYYY-MM-DD.json`

**Export All Data** (Full Backup):
1. Go to Stock Management page
2. Click "ส่งออกทั้งหมด" (Export All)
3. Saves: `backup-full-YYYY-MM-DD.json`
4. Includes: inventory, settings, audit logs, count history

### Import Data

1. Go to Stock Management page
2. Click "นำเข้า" (Import)
3. Select JSON file (from previous export)
4. System will restore data automatically

### Reset/Clear Data

⚠️ **Warning**: This action cannot be undone!

1. Go to Settings page
2. Scroll to "โซนอันตราย" (Danger Zone)
3. Click "ลบข้อมูลทั้งหมด" (Delete All Data)
4. Confirm twice
5. Page will reload with empty database

## ⚙️ Settings Configuration

### Change Login Codes

1. Login as Super-Manager
2. Go to Settings page
3. Update:
   - **รหัสผู้จัดการ** (Super-Manager Code)
   - **รหัสพนักงาน** (Employee Code)
4. Click "บันทึกการตั้งค่า" (Save Settings)

### Adjust Purchase Coverage Days

1. Go to Settings page
2. Find "จำนวนวันที่ต้องการครอบคลุม"
3. Set number of days (1-30)
4. This affects purchase quantity calculations
5. Save settings

### Adjust Order Cycles

For individual items:
1. Go to Stock Management page
2. Click Edit (pencil icon) on any item
3. Set "รอบสั่งซื้อ (วัน)" (Order Cycle Days)
4. Common values: 1 (daily), 2, 3, 7 (weekly), 14 (bi-weekly)
5. Save item

## 📋 Daily Workflow

### Morning - Employee Workflow

1. **Login** with employee code (0000)
2. **Dashboard**: Check alerts for low stock items
3. **View Purchase List**: See what needs to be ordered today
4. **Share/Export**: Send purchase list via WhatsApp/LINE to supplier

### Throughout Day - Stock Counting

1. Go to **Count Stock** page
2. Search or filter by category
3. Tap on item card to open numeric keypad
4. Enter current quantity
5. Save individual items or "บันทึกทั้งหมด" (Save All)

### Evening - Receive Items

1. Go to **Receive Items** page
2. View list of items to receive
3. Adjust quantities if needed (tap to edit)
4. Click "ยืนยันรับสินค้า" (Confirm Receipt) for each item
5. Or "รับทั้งหมด" (Receive All)

### Weekly - Manager Review

1. **Reports**: Check category stats and usage trends
2. **Stock Management**: Add/edit items, adjust min levels
3. **Audit Log**: Review employee actions
4. **Export Backup**: Download full backup JSON

## 🧮 Purchase Calculation Logic

The system uses this formula to calculate purchase quantities:

```
purchaseQty = max(0, minLevel - currentQty + dailyUsage × daysToCover)
```

Where:
- `minLevel`: Minimum stock level (set per item)
- `currentQty`: Current quantity on hand
- `dailyUsage`: Average daily usage (set per item)
- `daysToCover`: Days ahead setting (default: 1)

### Alert Levels

- 🔴 **RED (Danger)**: `currentQty < minLevel` - "ต่ำกว่าจุดสั่งซื้อ"
- 🟡 **ORANGE (Warning)**: `currentQty < minLevel × 1.1` - "ใกล้หมด"
- 🟢 **GREEN (OK)**: `currentQty ≥ minLevel × 1.1` - Normal

## 🔐 Security Best Practices

1. **Change default codes immediately** after setup
2. Use codes with **at least 4-6 digits**
3. **Don't share Super-Manager code** with unauthorized personnel
4. **Change codes regularly** (monthly recommended)
5. **Review audit logs** weekly to monitor activity
6. **Backup data regularly** (export JSON weekly)

## 🛠️ Troubleshooting

### App won't load
- Clear browser cache and reload
- Check if JavaScript is enabled
- Try different browser (Chrome/Edge recommended)

### Lost login code
- If you lost Super-Manager code and need to reset:
  1. Open browser DevTools (F12)
  2. Go to Application > Local Storage
  3. Find `settings.v1`
  4. Edit `superCode` or delete to restore defaults
  5. Default codes will be restored

### Data not saving
- Ensure browser has localStorage enabled
- Check available storage space
- Try exporting and re-importing data
- Clear old data if storage is full

### PWA not installing
- Use Chrome/Edge/Safari (not Firefox)
- Ensure HTTPS (required for PWA)
- Check browser PWA support

## 📱 Browser Support

- ✅ Chrome 90+ (Desktop & Mobile)
- ✅ Edge 90+
- ✅ Safari 14+ (iOS & macOS)
- ✅ Samsung Internet 15+
- ⚠️ Firefox (limited PWA support)

## 🏗️ Technical Stack

- **Frontend**: React 18 + TypeScript
- **Build Tool**: Vite 5
- **Styling**: TailwindCSS 3 + shadcn/ui components
- **State Management**: Zustand 4
- **Routing**: React Router 6
- **Icons**: Lucide React
- **Database**: Firebase Firestore (Cloud)
- **Authentication**: Firebase Anonymous Auth
- **Date Handling**: date-fns

## 📂 Project Structure

```
src/
├── components/
│   ├── ui/              # shadcn/ui base components
│   ├── Layout.tsx       # Main layout with sidebar
│   ├── ProtectedRoute.tsx
│   ├── NumericKeypad.tsx
│   ├── CategoryBadge.tsx
│   └── AlertBadge.tsx
├── pages/
│   ├── LoginPage.tsx
│   ├── DashboardPage.tsx
│   ├── StockPage.tsx
│   ├── CountPage.tsx
│   ├── PurchaseListPage.tsx
│   ├── ReceivePage.tsx
│   ├── ReportsPage.tsx
│   ├── SettingsPage.tsx
│   └── AuditPage.tsx
├── store/
│   ├── inventoryStore.ts
│   ├── userStore.ts
│   ├── settingsStore.ts
│   └── auditStore.ts
├── lib/
│   ├── calculators.ts   # Purchase calculation logic
│   ├── validation.ts    # Input validation
│   ├── firebase.ts      # Firebase configuration
│   ├── firebaseAuth.ts  # Firebase authentication
│   ├── firebasePersistence.ts # Firebase Firestore operations
│   ├── date.ts          # Date formatting
│   └── utils.ts         # General utilities
├── types/
│   ├── inventory.ts
│   └── auth.ts
├── data/
│   └── seed.ts          # 47 pre-configured items
├── App.tsx
├── main.tsx
└── index.css
```

## ✅ Acceptance Criteria Checklist

### Authentication & Authorization
- [x] Login with employee code (0000) and super code (552499)
- [x] Employee can only access: Dashboard, Count, Purchase List, Receive
- [x] Super-Manager can access all pages including Stock, Reports, Settings, Audit
- [x] Unauthorized access redirects to login or dashboard
- [x] Ability to change codes in Settings (Super-Manager only)

### Inventory Management
- [x] 42 items seeded from specification with categories
- [x] Items organized into 7 categories with color-coded badges
- [x] CRUD operations for items (Super-Manager only)
- [x] Soft delete (isActive flag)
- [x] Units restricted to: กรัม, ชิ้น, กิโลกรัม

### Stock Counting
- [x] Employee can enter current quantities via numeric keypad
- [x] Mobile-optimized touch-friendly input
- [x] Search and filter by category
- [x] Save individual items or bulk save all changes
- [x] Visual indication of changed items

### Purchase List Generation
- [x] Auto-calculates purchase quantities: `max(0, minLevel - currentQty + dailyUsage × days)`
- [x] Respects minLevel, dailyUsage, and daysToCover settings
- [x] Groups by category
- [x] Distinguishes "below-min" (🔴) vs "cycle-topup" (🟡)
- [x] Export as text for WhatsApp/LINE
- [x] Export as CSV
- [x] Print functionality

### Alerts & Notifications
- [x] RED badge for items below minimum stock level
- [x] ORANGE badge for items within 10% above minimum
- [x] Dashboard shows count of low-stock items
- [x] Toast notifications for user actions (success/error)

### Receive Items
- [x] Employee can mark items as received
- [x] Adjust received quantities with numeric keypad
- [x] Updates current stock quantities
- [x] Records receipt in audit log

### Reports (Super-Manager)
- [x] Summary statistics (total items, below min, near min)
- [x] Category-wise breakdown
- [x] Usage trend analysis (days until empty)
- [x] Export report as JSON

### Settings (Super-Manager)
- [x] Change Super-Manager code
- [x] Change Employee code
- [x] Change business name
- [x] Adjust default days ahead setting
- [x] Reset settings to defaults
- [x] Clear all data with confirmation

### Audit Trail
- [x] Every action logged with timestamp
- [x] Records actor (employee/super)
- [x] Records action type and metadata
- [x] Filter by user, action, date
- [x] Search functionality
- [x] Export audit log
- [x] Clear audit log (Super-Manager only)

### Import/Export
- [x] Export inventory items only (JSON)
- [x] Export full backup (inventory + settings + audit + counts)
- [x] Import from JSON file
- [x] Preserves data integrity on import
- [x] Download with timestamped filename

### Cloud Features
- [x] Firebase Firestore integration
- [x] Real-time data synchronization
- [x] Anonymous authentication
- [x] Cloud-based data storage
- [x] Requires internet connection

### UI/UX
- [x] Thai language labels throughout
- [x] Mobile-first responsive design
- [x] Numeric keypad for quantity input
- [x] Category color coding
- [x] Empty states with helpful messages
- [x] Loading states where appropriate
- [x] Clean, modern design with brand color #761F1C
- [x] Accessible keyboard navigation

### Data Persistence
- [x] Firebase Firestore persistence
- [x] Auto-load on app start
- [x] Auto-seed 47 items if empty
- [x] Real-time data sync
- [x] Backup/restore functionality

## 🎓 Training Tips

### For Employees
1. Practice stock counting during slow hours
2. Always double-check quantities before saving
3. Report any missing or damaged items to manager
4. Save counts at least twice daily (morning & evening)

### For Managers
1. Review audit logs weekly
2. Adjust min levels based on actual usage patterns
3. Update daily usage values monthly
4. Export backup before making bulk changes
5. Train new employees on the Count page only

## 📞 Support & Feedback

This is a cloud-based inventory management system. For questions or issues:
1. Check this README first
2. Review the Troubleshooting section
3. Inspect browser console for errors (F12)
4. Export data before making major changes
5. Ensure stable internet connection

## 📄 License

Copyright © 2025. All rights reserved.

---

**Built with ❤️ for zero-waste, zero-stockout Hainanese chicken rice operations.**

🍗 ข้าวมันไก่ - ไม่มีของหมด ไม่มีของเหลือ

