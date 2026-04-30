# 📦 TrackBox
### **ระบบกล่องรับพัสดุอัจฉริยะสำหรับที่พักอาศัย (Smart Parcel Box IoT System)**

---

## 📝 **ภาพรวมระบบ (System Overview)**
<small>
**ระบบ TrackBox** เป็นเครื่องมือที่ช่วยให้ผู้อยู่อาศัยในหอพักสามารถจัดการการรับพัสดุได้อย่างมีประสิทธิภาพ โดยการรวมเทคโนโลยีการตรวจจับด้วยเซนเซอร์ การแจ้งเตือนผ่านหน้าเว็บ และการจัดเก็บข้อมูลประวัติไว้ในระบบเดียว เพื่อลดความกังวลเรื่องความปลอดภัยและเพิ่มความสะดวกสบายในการใช้ชีวิตประจำวัน
</small>

---

## 🛠️ **เทคโนโลยีที่ใช้ (Tech Stack & Tools)**
| ส่วนของระบบ | เทคโนโลยีและการนำไปใช้งาน |
| :--- | :--- |
| **Hardware & IoT** | **Raspberry Pi 4/5** ใช้ร่วมกับเซนเซอร์ตรวจจับวัตถุภายในกล่อง และเชื่อมต่อ Wi-Fi |
| **Database** | **MariaDB (MySQL)** ใช้จัดเก็บข้อมูล Users, ประวัติการรับของ (Logs) และรหัส OTP |
| **Back-end Logic** | **Node-RED** เป็นตัวควบคุมการประมวลผล Logic และจัดการ Flow ข้อมูลระหว่างอุปกรณ์ |
| **Front-end Design** | **Node-RED Dashboard** (HTML5 & CSS) สำหรับแสดงผลสถานะแบบ Real-time |
| **Connectivity** | **TCP/IP & MQTT** ใช้สำหรับการรับส่งข้อมูลระหว่างกล่องพัสดุและตัว Server |

---

## ✨ **เค้าโครงสีหลักของระบบ (Brand Theme)**
เพื่อให้หน้า Dashboard อ่านง่ายและทันสมัย เราจึงเลือกใช้กลุ่มสีดังนี้:

* **Royal Blue (`#435ebe`):** สีหลักสำหรับ Header และแถบเมนู ให้ความรู้สึกมั่นคง
* **Sky Blue (`#31a8ff`):** สีสำหรับปุ่มแอคชั่นหลัก (เช่น ปุ่ม Start หรือปุ่ม Verify)
* **Soft Cyan (`#e0f7fa`):** สีพื้นหลังส่วน Content เพื่อช่วยให้สบายตา
* **Success Green (`#28a745`):** ใช้สำหรับแสดงสถานะ "กล่องว่าง" หรือสถานะแบตเตอรี่ที่ปกติ
* **Charcoal Grey (`#333333`):** สีตัวอักษรหลักที่เน้นความคมชัดสูง อ่านง่าย

---

## 📖 **คู่มือการใช้งานระบบ (User Manual)**

### **1. หน้าจอหลักและสถานะพัสดุ**
* **Real-time Monitoring:** แสดงสถานะปัจจุบันของกล่องพัสดุ (🟢 สีเขียว: ไม่มีพัสดุ / 🔴 สีแดง: มีพัสดุ)
* **Battery Status:** ตรวจสอบระดับพลังงานคงเหลือของเซนเซอร์ในกล่องได้โดยตรงจากหน้าจอ

### **2. การจัดการข้อมูลและประวัติ**
* **History Table:** ตารางแสดงประวัติการรับพัสดุย้อนหลัง (วัน/เวลา/เลขพัสดุ/บริษัทขนส่ง)

### **3. ระบบความปลอดภัย (Verify OTP)**
* **OTP Request:** ต้องใส่เบอร์โทรศัพท์ก่อนเข้าใช้งาน ระบบจะส่งรหัส 6 หลักเพื่อยืนยันตัวตน
* **Time Limit:** รหัส OTP มีอายุการใช้งานจำกัด 60 วินาที เพื่อความปลอดภัยสูงสุด

---

## 🔑 **บัญชีสำหรับทดสอบระบบ (Test Credentials)**
สำหรับการเข้าสู่ระบบเพื่อทดสอบการทำงาน สามารถใช้บัญชีจำลองดังนี้:

| ระดับผู้ใช้งาน | ชื่อผู้ใช้ (Username) | รหัสผ่าน (Password) |
| :--- | :--- | :--- |
| **Administrator** | `admin_test` | `password123` |
| **General User** | `user_test` | `user123` |

---
### **🗂️ รายละเอียดโครงสร้างฐานข้อมูล (Data Dictionary)**
รายละเอียดฟิลด์ข้อมูลของแต่ละตารางที่ใช้ในระบบ **TrackBox**:

#### **1. ตาราง: USERS (ข้อมูลผู้ใช้งาน)**
| Name | Data Type | Data Format | Field Size | Description | Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **user_id** | Integer | - | - | รหัสผู้ใช้งาน | 1 |
| **username** | Text | - | 50 | ชื่อบัญชีผู้ใช้ | boonyapat99 |
| **password** | Text | - | 255 | รหัสผ่าน | hash_pwd_123 |
| **full_name** | Text | - | 200 | ชื่อและนามสกุล | บุญยพัต จ้อยเจริญ |
| **phone_number** | Text | 0xxxxxxxxx | 15 | เบอร์โทรศัพท์ | 0812345678 |
| **email** | Text | - | 100 | อีเมล | test@gmail.com |

#### **2. ตาราง: SMARTBOXES (ข้อมูลลงทะเบียนกล่องพัสดุ)**
| Name | Data Type | Data Format | Field Size | Description | Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **box_id** | Integer | - | - | รหัสกล่องพัสดุ | 101 |
| **user_id** | Integer | - | - | รหัสเจ้าของกล่อง | 1 |
| **location_name** | Text | - | 100 | ชื่อเรียกจุดติดตั้ง | หน้าประตูรั้ว |
| **connection_status** | Text | - | 10 | สถานะการเชื่อมต่อ | Online |

#### **3. ตาราง: ACTIVITYLOGS (ข้อมูลประวัติการทำงานและสถานะ)**
| Name | Data Type | Data Format | Field Size | Description | Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **log_id** | Integer | - | - | รหัสบันทึก | 5001 |
| **box_id** | Integer | - | - | รหัสกล่องพัสดุ | 101 |
| **timestamp** | DateTime | DD/MM/YYYY | - | วัน-เวลาที่บันทึก | 22/04/2026 |
| **action_event** | Text | - | 50 | เหตุการณ์ที่เกิดขึ้น | Delivery |
| **box_status** | Text | - | 50 | สถานะของกล่อง | Occupied |

#### **4. ตาราง: TEMPORARYPASSWORDS (ข้อมูลรหัสผ่านชั่วคราว)**
| Name | Data Type | Data Format | Field Size | Description | Example |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **otp_id** | Integer | - | - | รหัสรายการ | 901 |
| **box_id** | Integer | - | - | รหัสกล่องพัสดุ | 101 |
| **otp_code** | Text | - | 10 | รหัสผ่านชั่วคราว | 552914 |
| **created_at** | DateTime | DD/MM/YYYY | - | เวลาที่สร้าง | 22/04/2026 |
| **expired_at** | DateTime | DD/MM/YYYY | - | เวลาหมดอายุ | 22/04/2026 |
| **usage_status** | Text | - | 10 | สถานะการใช้งาน | Unused |

---

## ⚙️ **ขั้นตอนการติดตั้ง (Installation Guide)**

### **1. สิ่งที่ต้องเตรียม (Prerequisites)**
1. **Raspberry Pi OS** (64-bit)
2. **Node-RED** และ **Thingsboard** ติดตั้งบน Raspberry Pi
3. **MariaDB Server** สำหรับจัดการฐานข้อมูล
4. **Network:** การเชื่อมต่อ Wi-Fi ในวงแลนเดียวกัน

---

## 🛠️ **ขั้นตอนการติดตั้งและเริ่มใช้งาน (Installation & Setup)**

#### **Step 1: การเตรียมฐานข้อมูล (Database Setup)**
ทำการสร้างตารางข้อมูลใน **MariaDB** เพื่อรองรับการจัดเก็บข้อมูล:
1. เข้าใช้งาน MariaDB ผ่าน Terminal:
```bash
sudo mysql -u root -p
```
2.สร้าง Database และสร้างตารางหลักด้วยคำสั่ง SQL:
```bash
CREATE DATABASE TrackBoxDB;
USE TrackBoxDB;

CREATE TABLE ActivityLogs (
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    action_event VARCHAR(50), 
    log_timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    box_status VARCHAR(50)
);
```

#### **Step 2: การนำเข้า Flow ใน Node-RED (Import Flow)**
เปิดหน้า Node-RED Dashboard และเลือกเมนู Import ที่มุมขวาบน
เลือกไฟล์ .json ที่อยู่ในโฟลเดอร์ /src ของโปรเจกต์นี้มาวาง
ตรวจสอบโหนด MySQL ให้เชื่อมต่อกับ IP, Username และ Password ให้ถูกต้อง

#### **Step 3: การรันระบบและทดสอบ (Run & Test)**
กดปุ่ม Deploy สีแดงที่มุมขวาบนของ Node-RED เพื่อเริ่มการทำงาน
เข้าสู่หน้า Dashboard ผ่าน URL:
```bash
http://<IP_ADDRESS_RPI>:1880/ui
```

ทดสอบระบบโดยการวางวัตถุในกล่องเพื่อดูการอัปเดตสถานะแบบ Real-time
 ### **ขั้นตอนการใช้งานสำหรับผู้ใช้ (User Workflow)**
* **เข้าสู่ระบบ (Identity): ทำการ Login เข้าสู่ระบบเพื่อความปลอดภัย**
* **กรอกรายละเอียด (Entry): เมื่อพัสดุมาถึง ให้ระบุชื่อบริษัทขนส่งและชื่อพัสดุผ่านหน้าจอ**
* **ตรวจสอบประวัติ (Monitoring): ดูรายการพัสดุทั้งหมดได้ที่หน้า Record**
* **ความปลอดภัย (Verify): กดขอรหัส OTP และกรอกรหัส 6 หลักภายใน 60 วินาทีเพื่อเปิดกล่อง**

###👥 **สมาชิกกลุ่ม (Team Members)**

* **นายพิรชัช กลิ่นทอง - รหัสนักศึกษา 67173537**
* **นายบุญยพัต จ้อยเจริญ - รหัสนักศึกษา 67160881**
* **นายภูรินท์ แซ่ภู่ - รหัสนักศึกษา 67154983**
