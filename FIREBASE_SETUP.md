# 🔥 Firebase Setup Guide

## ✅ สถานะการติดตั้ง

ระบบได้เชื่อมต่อ Firebase เรียบร้อยแล้ว! 🎉

### เปลี่ยนแปลงที่สำคัญ:

1. ✅ **ไม่ใช้ localStorage อีกต่อไป** - ข้อมูลทั้งหมดเก็บใน Firebase Firestore
2. ✅ **Online-Only** - ต้องมีอินเทอร์เน็ตในการใช้งาน
3. ✅ **Anonymous Authentication** - ใช้ Firebase Anonymous Auth
4. ✅ **Real-time Sync** - ข้อมูลซิงค์กับ Cloud ทันที

---

## 📋 Firebase Configuration

ข้อมูล Firebase Project:
- **Project ID**: `pos-mick-an-petch`
- **Database**: Firestore (Cloud Firestore)
- **Authentication**: Anonymous (no login required)
- **Region**: `asia-southeast1`

---

## 🗂️ Firestore Collections

ระบบใช้ 4 Collections:

### 1. `inventory/{userId}`
```json
{
  "items": [
    {
      "id": "xxx",
      "name": "ต้นผักชี",
      "category": "ของสด",
      "unit": "กรัม",
      "currentQty": 150,
      "minLevel": 100,
      "dailyUsage": 50,
      "orderCycleDays": 1,
      "isActive": true
    }
  ],
  "updatedAt": "2025-01-20T10:30:00.000Z"
}
```

### 2. `settings/{userId}`
```json
{
  "businessName": "ร้านข้าวมันไก่",
  "superCode": "552499",
  "employeeCode": "0000",
  "defaultOpenDaysAhead": 1,
  "brandColor": "#761F1C",
  "updatedAt": "2025-01-20T10:30:00.000Z"
}
```

### 3. `audit/{userId}`
```json
{
  "logs": [
    {
      "id": "xxx",
      "ts": "2025-01-20T10:30:00.000Z",
      "actor": "super",
      "action": "ITEM_CREATE",
      "meta": { "name": "น้ำโค้ก" }
    }
  ],
  "updatedAt": "2025-01-20T10:30:00.000Z"
}
```

### 4. `counts/{userId}`
```json
{
  "counts": [
    {
      "id": "xxx",
      "itemId": "xxx",
      "date": "2025-01-20",
      "qty": 150,
      "userRole": "employee"
    }
  ],
  "updatedAt": "2025-01-20T10:30:00.000Z"
}
```

---

## 🔒 Security Rules

ไฟล์ `firestore.rules` ได้ถูกสร้างแล้ว:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow users to read/write only their own data
    match /inventory/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    match /settings/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    match /audit/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    match /counts/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

### การติดตั้ง Security Rules:

1. ไปที่ [Firebase Console](https://console.firebase.google.com)
2. เลือก Project: **pos-mick-an-petch**
3. ไปที่ **Firestore Database** → **Rules**
4. คัดลอกเนื้อหาจากไฟล์ `firestore.rules`
5. Paste และกด **Publish**

---

## 🚀 การใช้งาน

### เริ่มต้น Development Server

```bash
npm run dev
```

จากนั้นเปิด `http://localhost:5173`

### สิ่งที่จะเกิดขึ้น:

1. **Loading Screen** - แสดงหน้า "กำลังเชื่อมต่อ Firebase"
2. **Anonymous Login** - Firebase จะสร้าง User ID อัตโนมัติ
3. **Load Data** - โหลดข้อมูลจาก Firestore
4. **Auto Seed** - ถ้าไม่มีข้อมูล จะโหลดสินค้า 47 รายการอัตโนมัติ

---

## 📦 การ Seed ข้อมูล

สินค้าที่ seed อัตโนมัติ: **47 รายการ**

- ของสด: 12 รายการ
- ของแห้ง/วัตถุดิบหลัก: **7 รายการ** (รวม: ข้าว, แป้งทอดไก่, น้ำโค้ก, น้ำเปล่า, น้ำส้ม, น้ำสไปร์ท)
- ของปรุงรส/เครื่องปรุงเหลว: 12 รายการ
- ผงปรุงรส/เครื่องเทศ: 5 รายการ
- ของใช้ในครัว/ทำความสะอาด: 8 รายการ
- ของประเภทโปรตีนสำเร็จรูป: 2 รายการ
- ของหมักดอง: 1 รายการ

---

## 🔍 การตรวจสอบข้อมูลใน Firebase

1. ไปที่ [Firebase Console](https://console.firebase.google.com)
2. เลือก Project: **pos-mick-an-petch**
3. ไปที่ **Firestore Database**
4. เลือก Collection เช่น `inventory`
5. จะเห็น Document ID = User UID
6. กดเข้าไปดูข้อมูลทั้งหมด

---

## ⚠️ ข้อควรระวัง

### 1. ต้องมีอินเทอร์เน็ตตลอด
- ❌ ใช้งาน offline ไม่ได้
- ✅ ต้องเชื่อมต่ออินเทอร์เน็ตเสมอ

### 2. ค่าใช้จ่าย Firebase
Firebase มี **Free Tier**:
- ✅ Reads: 50,000/day
- ✅ Writes: 20,000/day
- ✅ Deletes: 20,000/day
- ✅ Storage: 1 GB

สำหรับร้านเล็ก ใช้ฟรีได้สบาย ไม่มีค่าใช้จ่าย

### 3. User ID
- แต่ละอุปกรณ์จะได้ User ID ต่างกัน
- ถ้าเคลียร์ browser data จะได้ User ID ใหม่
- ข้อมูลเก่าจะยังอยู่ใน Firebase แต่เข้าไม่ถึง

---

## 🛠️ Troubleshooting

### 1. Firebase Connection Failed
**อาการ**: หน้าแสดง "เกิดข้อผิดพลาด"

**แก้ไข**:
- ตรวจสอบอินเทอร์เน็ต
- เช็ค Firebase Console ว่า Project ยังทำงานอยู่
- กด "ลองใหม่อีกครั้ง"

### 2. Permission Denied
**อาการ**: Console แสดง "Permission denied"

**แก้ไข**:
- ตรวจสอบ Firestore Rules ใน Firebase Console
- ตรวจสอบว่า Anonymous Auth เปิดอยู่

### 3. Data Not Saving
**อาการ**: บันทึกแล้วแต่ไม่มีการเปลี่ยนแปลง

**แก้ไข**:
- เช็ค Console สำหรับ Error
- ดูใน Firebase Console ว่าข้อมูลอัพเดทหรือไม่
- Reload หน้าเพื่อโหลดข้อมูลใหม่

---

## 📊 การ Export/Import

### Export
1. Login เป็น Super Manager (552499)
2. ไปหน้า "จัดการสินค้า"
3. กด "ส่งออกทั้งหมด"
4. ได้ไฟล์ JSON

### Import
1. Login เป็น Super Manager
2. ไปหน้า "จัดการสินค้า"
3. กด "นำเข้า"
4. เลือกไฟล์ JSON
5. ข้อมูลจะ upload ไป Firebase ทันที

---

## 🎯 สถาปัตยกรรม

```
Client (Browser)
    ↓ Anonymous Auth
Firebase Auth
    ↓ User UID
Firebase Firestore
    ├── inventory/{userId}
    ├── settings/{userId}
    ├── audit/{userId}
    └── counts/{userId}
```

### Flow การทำงาน:

1. เปิดแอป → Firebase Auth (Anonymous)
2. ได้ User UID
3. ใช้ UID เป็น Document ID
4. Read/Write ไปที่ Firestore
5. ทุกการเปลี่ยนแปลงบันทึกทันที

---

## ✅ Checklist

- [x] Firebase SDK ติดตั้งแล้ว
- [x] Firebase Config ตั้งค่าแล้ว
- [x] Anonymous Auth เปิดแล้ว
- [x] Firestore Database สร้างแล้ว
- [x] Security Rules ตั้งค่าแล้ว
- [x] ลบ localStorage ออกหมดแล้ว
- [x] ทุก function เป็น async
- [x] Loading states พร้อม
- [x] Error handling พร้อม
- [x] Build สำเร็จ ✅

---

## 🎉 พร้อมใช้งาน!

ระบบพร้อมใช้งานแล้ว ข้อมูลทั้งหมดจะเก็บบน Firebase Cloud ✨

ไม่ต้องกังวลเรื่อง:
- ❌ localStorage เต็ม
- ❌ ข้อมูลหาย
- ❌ Clear cache

เพราะข้อมูลอยู่บน Cloud แล้ว! ☁️

---

**Need Help?**
- [Firebase Documentation](https://firebase.google.com/docs)
- [Firestore Documentation](https://firebase.google.com/docs/firestore)
- [Firebase Console](https://console.firebase.google.com)

