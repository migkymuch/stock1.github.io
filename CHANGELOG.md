# 📝 Changelog

## Version 1.1.0 - รหัสพนักงานเปลี่ยนเป็น 9999

**วันที่**: 20 ตุลาคม 2025

### 🔄 การเปลี่ยนแปลง

#### 1. เปลี่ยนรหัสพนักงาน
- ❌ เดิม: `0000`
- ✅ ใหม่: `9999`
- เหตุผล: ความปลอดภัยและความชัดเจน

#### 2. ไฟล์ที่แก้ไข
- ✅ `src/pages/LoginPage.tsx`
- ✅ `src/lib/firebaseAuth.ts`
- ✅ `src/lib/firebasePersistence.ts`
- ✅ `src/lib/persistence.ts`
- ✅ `firestore.rules`
- ✅ `README.md`
- ✅ `QUICK_START.md`
- ✅ `SHARED_DATA_SETUP.md`

#### 3. Firebase Console ที่ต้องอัปเดต
- ⚠️ **Firestore Security Rules** - ต้อง Deploy!
- Collection structure เปลี่ยนจาก `0000` → `9999`

---

## Version 1.0.0 - Initial Release

**วันที่**: 20 ตุลาคม 2025

### ✨ ฟีเจอร์หลัก

#### Authentication
- Login ด้วยรหัส: Employee (0000) และ Super-Manager (552499)
- Role-based access control

#### Inventory Management
- 47 pre-seeded items
- 7 categories with color coding
- CRUD operations (Super-Manager only)

#### Stock Counting
- Numeric keypad for mobile
- Bulk save functionality
- Real-time updates

#### Purchase Lists
- Auto-calculation based on min levels
- Export to WhatsApp/LINE/CSV
- Grouped by category

#### Firebase Integration
- ✅ Firestore database
- ✅ Anonymous authentication
- ✅ Online-only (no localStorage)
- ✅ Shared data across devices

#### Additional Features
- Reports and analytics
- Audit log (all actions tracked)
- Import/Export JSON
- PWA support
- Settings management

---

## 🔮 Upcoming Features

- [ ] Real-time sync (no refresh needed)
- [ ] Push notifications for low stock
- [ ] Barcode scanner integration
- [ ] Multi-language support (EN/TH)
- [ ] Advanced analytics dashboard
- [ ] Supplier management
- [ ] Recipe costing calculator

---

## 🐛 Bug Fixes

### Version 1.1.0
- Fixed: Anonymous auth error handling
- Fixed: Async function calls in all stores
- Updated: Security rules for new employee code

### Version 1.0.0
- Initial stable release

---

## 📚 Documentation

- `README.md` - Complete documentation
- `QUICK_START.md` - Quick setup guide
- `FIREBASE_SETUP.md` - Firebase configuration
- `SHARED_DATA_SETUP.md` - Multi-device data sharing
- `DEPLOY_FIREBASE_RULES.md` - How to deploy rules

---

**Last Updated**: 20 ตุลาคม 2025

