# 🧪 ทดสอบ Firebase Integration

## ✅ Checklist การทดสอบ

### 1️⃣ ตรวจสอบ Firebase Rules ใน Console

1. เปิด [Firebase Console](https://console.firebase.google.com)
2. เลือก Project: **pos-mick-an-petch**
3. ไปที่ **Firestore Database** → **Rules**
4. ตรวจสอบว่ามีคำว่า `"9999"` และ `"552499"` ✅
5. ต้องไม่มี `"0000"` อีกแล้ว ❌

**ควรเห็นแบบนี้:**
```javascript
match /inventory/{code} {
  allow read, write: if request.auth != null && 
                        (code == "9999" || code == "552499");
}
```

---

### 2️⃣ ทดสอบ Login (Basic Test)

#### Test 1: Login ด้วยรหัสพนักงาน
```
✅ ขั้นตอน:
1. เปิด http://localhost:5177
2. กรอกรหัส: 9999
3. กด "เข้าสู่ระบบ"

✅ ผลลัพธ์ที่ต้องการ:
- แสดงข้อความ "กำลังโหลด..." 
- แสดง "เข้าสู่ระบบสำเร็จ (พนักงาน)"
- เข้าสู่ Dashboard
- Auto seed 47 รายการ (ถ้าเป็นครั้งแรก)

❌ ถ้า Error:
- Permission Denied → Rules ยังไม่ Deploy หรือ Deploy ผิด
- Configuration Error → Anonymous Auth ยังไม่เปิด
```

#### Test 2: Login ด้วยรหัสผู้จัดการ
```
✅ ขั้นตอน:
1. Logout (ถ้า Login อยู่)
2. กรอกรหัส: 552499
3. กด "เข้าสู่ระบบ"

✅ ผลลัพธ์ที่ต้องการ:
- Login สำเร็จ
- เข้าสู่ Dashboard
- เห็นเมนูเพิ่มเติม (จัดการสินค้า, รายงาน, ตั้งค่า, ประวัติ)
```

#### Test 3: Login ด้วยรหัสเก่า (ต้องไม่ผ่าน)
```
✅ ขั้นตอน:
1. Logout
2. กรอกรหัส: 0000 (รหัสเก่า)
3. กด "เข้าสู่ระบบ"

✅ ผลลัพธ์ที่ต้องการ:
- ❌ แสดง "รหัสไม่ถูกต้อง กรุณาลองใหม่อีกครั้ง"
- ไม่ให้ Login
```

---

### 3️⃣ ทดสอบ Firestore Operations

#### Test 1: เพิ่มสินค้า (Super-Manager)
```
✅ ขั้นตอน:
1. Login: 552499
2. ไปหน้า "จัดการสินค้า"
3. กด "เพิ่มสินค้า"
4. กรอก:
   - ชื่อ: "ทดสอบ Firebase"
   - หมวดหมู่: ของสด
   - หน่วย: ชิ้น
   - คงเหลือ: 10
5. กด "เพิ่ม"

✅ ผลลัพธ์ที่ต้องการ:
- แสดง "เพิ่มสินค้าสำเร็จ"
- เห็นสินค้าใหม่ในตาราง
- กด F12 → Console → ต้องเห็น "💾 Inventory saved to Firebase"

❌ ถ้า Error:
- Permission Denied → Rules ไม่ถูกต้อง
- Document not found → Firebase ไม่พร้อม
```

#### Test 2: นับสต็อก (Employee)
```
✅ ขั้นตอน:
1. Login: 9999
2. ไปหน้า "นับสต็อก"
3. เลือกสินค้า "ต้นผักชี"
4. กรอกจำนวน: 200
5. กด "บันทึก"

✅ ผลลัพธ์ที่ต้องการ:
- แสดง "บันทึกสำเร็จ"
- จำนวนอัพเดทเป็น 200
- Console เห็น "💾 Inventory saved to Firebase"
```

---

### 4️⃣ ทดสอบ Shared Data (สำคัญที่สุด!)

#### Test: สองเบราว์เซอร์เห็นข้อมูลเดียวกัน

**Browser 1 (Chrome):**
```
1. Login: 9999
2. ไปหน้า "จัดการสินค้า" (ถ้าเป็น Super) หรือ "นับสต็อก"
3. เพิ่มสินค้า "ABC TEST"
4. บันทึก
5. ✅ เห็นสินค้าในรายการ
```

**Browser 2 (Edge/Firefox/Incognito Chrome):**
```
1. เปิด http://localhost:5177
2. Login: 9999 (รหัสเดียวกัน)
3. ไปหน้า "จัดการสินค้า" หรือ "นับสต็อก"
4. รีเฟรชหน้า (F5)
5. ✅ ต้องเห็น "ABC TEST" ด้วย!
```

**ถ้าไม่เห็น:**
- รีเฟรชอีกครั้ง (Ctrl+Shift+R)
- เช็ค Console มี Error ไหม
- ตรวจสอบว่า Login Code เหมือนกันจริงๆ

---

### 5️⃣ ตรวจสอบข้อมูลใน Firebase Console

#### ดูข้อมูลจริงๆ ใน Firestore

1. ไปที่ **Firestore Database** → **Data** (แท็บ)
2. ควรเห็น Collections:
   - `inventory`
   - `settings`
   - `audit`
   - `counts`
3. คลิกเข้า Collection `inventory`
4. ควรเห็น Documents:
   - ✅ `9999` (ถ้า Login ด้วย 9999 แล้ว)
   - ✅ `552499` (ถ้า Login ด้วย 552499 แล้ว)
5. คลิกเข้าไปใน Document `9999`
6. ควรเห็น:
   ```json
   {
     "items": [ ... 47 รายการ ... ],
     "updatedAt": "2025-10-20T..."
   }
   ```

---

## 🔍 ตรวจสอบ Console Logs

เปิด Browser DevTools (F12) → Console

### ✅ Logs ที่ควรเห็น (ปกติ)

```
🚀 Initializing Firebase...
🔥 Firebase initialized successfully
🔐 Firebase anonymous sign-in initiated
✅ Firebase authenticated (Token ready)
🔐 Firebase ready - waiting for login

[หลัง Login ด้วย 9999]
🔑 Login Code set: 9999
📦 Inventory loaded from Firebase
📊 Counts loaded from Firebase
⚙️ Settings loaded from Firebase
📝 Audit log loaded from Firebase
📦 All data loaded from Firebase
```

### ❌ Error Logs ที่อาจเจอ

**Error 1: Permission Denied**
```
FirebaseError: Missing or insufficient permissions
```
**สาเหตุ**: Rules ยังไม่ Deploy หรือ Deploy ผิด
**วิธีแก้**: Deploy Rules อีกครั้งตาม `DEPLOY_FIREBASE_RULES.md`

**Error 2: Configuration Not Found**
```
Firebase: Error (auth/configuration-not-found)
```
**สาเหตุ**: Anonymous Auth ยังไม่เปิด
**วิธีแก้**: เปิด Anonymous Auth ใน Firebase Console

**Error 3: Document Not Found**
```
Document not found
```
**สาเหตุ**: ปกติ - ครั้งแรกยังไม่มีข้อมูล
**ผลลัพธ์**: ระบบจะ Auto Seed 47 รายการให้

---

## 🎯 Test Scenarios

### Scenario 1: First Time Login (9999)
```
Expected Flow:
1. Login: 9999
2. System checks: Document "9999" → Not found
3. Auto seed: 47 items
4. Save to: inventory/9999
5. ✅ Dashboard shows 47 items
```

### Scenario 2: Second Login (9999)
```
Expected Flow:
1. Login: 9999
2. System checks: Document "9999" → Found!
3. Load: 47 items from Firebase
4. ✅ Dashboard shows existing data
```

### Scenario 3: Multi-Device (Same Code)
```
Device A:
1. Login: 9999
2. Add item: "น้ำอัดลม"
3. Save → Firestore

Device B:
1. Login: 9999
2. Refresh page
3. ✅ See "น้ำอัดลม" in list
```

### Scenario 4: Different Codes (Isolated Data)
```
Device A:
1. Login: 9999 (Employee)
2. See Document: inventory/9999

Device B:
1. Login: 552499 (Manager)
2. See Document: inventory/552499
3. ❌ ไม่เห็นข้อมูลของ 9999 (ถูกต้อง - แยกกัน)
```

---

## 📊 Firebase Console Checks

### Check 1: Authentication
```
Firebase Console → Authentication → Users

ควรเห็น:
- Anonymous users: 1 หรือมากกว่า
- Last sign-in: เวลาที่ Login ล่าสุด
- ✅ มี user = Firebase Auth ทำงาน
```

### Check 2: Firestore Data
```
Firebase Console → Firestore Database → Data

ควรเห็น:
└── inventory
    ├── 9999       ← มี! (ถ้า Login ด้วย 9999)
    └── 552499     ← มี! (ถ้า Login ด้วย 552499)

คลิกเข้าไปใน Document:
- มี field: items (array)
- มี field: updatedAt (timestamp)
- ใน items มี 47 objects
```

### Check 3: Rules Status
```
Firebase Console → Firestore Database → Rules

ควรเห็น:
- Published: [เวลาที่ Deploy]
- Contains: "9999" และ "552499"
- ✅ No "0000" anymore
```

---

## 🐛 Troubleshooting Guide

### ปัญหา 1: Login ได้แต่ไม่มีข้อมูล
```
อาการ: Dashboard แสดง 0 รายการ

ตรวจสอบ:
1. เปิด Console (F12)
2. ดู Error messages
3. ถ้าเห็น "Permission Denied" → Rules ผิด
4. ถ้าไม่มี Error → Auto seed ไม่ทำงาน

วิธีแก้:
- ไปหน้า "จัดการสินค้า" (Super Manager)
- กด "โหลดข้อมูลตัวอย่าง"
- ยืนยัน
```

### ปัญหา 2: บันทึกไม่ได้
```
อาการ: กดบันทึกแล้วไม่มีอะไรเกิดขึ้น

ตรวจสอบ:
1. Console มี Error: "Permission Denied"
2. → Rules ไม่ถูกต้อง

วิธีแก้:
- Deploy Rules อีกครั้ง
- ตรวจสอบว่ามี "9999" ใน Rules
```

### ปัญหา 3: เบราว์เซอร์ที่ 2 ไม่เห็นข้อมูล
```
อาการ: เพิ่มข้อมูลเครื่อง A แต่เครื่อง B ไม่เห็น

ตรวจสอบ:
1. Login Code เหมือนกันหรือไม่? (9999 vs 9999)
2. รีเฟรชหรือยัง? (F5)
3. Console มี Error ไหม?

วิธีแก้:
- ตรวจสอบ Login Code ให้แน่ใจว่าเหมือนกัน
- Hard refresh: Ctrl+Shift+R
- Clear cache แล้ว Login ใหม่
```

---

## 🔍 Live Testing Script

### คำสั่งทดสอบแบบครอบคลุม

```bash
# 1. เช็ค Dev Server
เปิด: http://localhost:5177

# 2. เปิด Console (F12)
คลิก Console tab

# 3. Login Test
รหัส: 9999
Result: ✅ เข้าได้ / ❌ Error

# 4. ดู Console Logs
ต้องเห็น:
- 🔑 Login Code set: 9999
- 💾 Inventory saved to Firebase
- 📦 Inventory loaded from Firebase

# 5. เช็ค Network (F12 → Network tab)
กรอง: firestore
Result: ✅ เห็น Request ไป Firestore / ❌ ไม่มี Request
```

---

## 📸 Screenshot Checklist

### หน้าจอที่ควรเห็น:

#### 1. Login Screen
```
┌─────────────────────────────────┐
│  🔒 ร้านข้าวมันไก่              │
│  ระบบจัดการสต็อก               │
│                                 │
│  [_____9999_____] (input)      │
│                                 │
│  [ เข้าสู่ระบบ ]               │
│                                 │
│  รหัสพนักงาน: 9999 ✅          │
│  รหัสผู้จัดการ: 552499         │
└─────────────────────────────────┘
```

#### 2. Dashboard (หลัง Login 9999)
```
┌─────────────────────────────────┐
│  แดชบอร์ด                       │
│  ยินดีต้อนรับ พนักงาน            │
│                                 │
│  [47] [0] [0] [X]              │
│  รายการ ต่ำกว่า ใกล้ รายการสั่ง │
│                                 │
│  📋 เมนูหลัก                    │
│  [นับสต็อก] [รายการสั่งซื้อ]    │
│  [รับสินค้า]                    │
└─────────────────────────────────┘
```

#### 3. Firestore Console
```
Firestore Database > Data

inventory
├── 9999 ✅ (ถ้า Login ด้วย 9999)
│   └── items: Array[47]
│   └── updatedAt: October 20, 2025...
└── 552499 (ถ้า Login ด้วย 552499)
```

---

## ✅ Success Indicators

### ระบบทำงานถูกต้องถ้า:

1. ✅ Login ด้วย 9999 ได้
2. ✅ Login ด้วย 552499 ได้
3. ✅ Login ด้วย 0000 ไม่ได้ (รหัสเก่า)
4. ✅ เห็น 47 รายการสินค้า (Auto seed)
5. ✅ เพิ่ม/แก้ไข/ลบสินค้าได้
6. ✅ นับสต็อกได้
7. ✅ Console ไม่มี Error สีแดง
8. ✅ Firebase Console เห็น Document 9999 และ 552499
9. ✅ สองเบราว์เซอร์เห็นข้อมูลเดียวกัน (Login Code เดียวกัน)
10. ✅ Network tab เห็น Request ไป Firestore

---

## 🎬 Quick Test Commands

### คัดลอกคำสั่งนี้ไปทดสอบ:

1. **Open App**
   ```
   http://localhost:5177
   ```

2. **Login as Employee**
   ```
   Code: 9999
   ```

3. **Login as Manager**
   ```
   Code: 552499
   ```

4. **Check Console** (F12)
   ```javascript
   // Should see:
   🔑 Login Code set: 9999
   💾 Inventory saved to Firebase
   📦 Inventory loaded from Firebase
   ```

5. **Check Firestore** (Firebase Console)
   ```
   Firestore Database > Data > inventory > 9999
   Should exist with 47 items
   ```

---

## 📞 Report Results

### ถ้าสำเร็จ ✅
บอกฉันว่า:
- "Login 9999 สำเร็จ เห็น 47 รายการ"
- "Firebase Console เห็น Document 9999"

### ถ้ามีปัญหา ❌
บอกฉันพร้อม:
- Error message (จาก Console)
- Screenshot (ถ้าได้)
- ขั้นตอนที่ทำไปแล้ว

---

## 🎉 Expected Success Message

หลังทำตาม Test ทั้งหมด ควรได้:

```
✅ Firebase Rules: Deployed
✅ Anonymous Auth: Enabled  
✅ Login 9999: Success
✅ Login 552499: Success
✅ Login 0000: Failed (ถูกต้อง)
✅ Data Seeded: 47 items
✅ Firestore Saved: Document 9999 & 552499
✅ Multi-Device: Shared data works
✅ Console: No errors
```

**ถ้าได้แบบนี้ = 🎉 สำเร็จ 100%!**

---

**พร้อมทดสอบแล้ว! ลองตาม Checklist นี้แล้วบอกผลครับ!** 🚀

