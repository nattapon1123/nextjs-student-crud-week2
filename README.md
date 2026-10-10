# Student Management (Next.js)

ระบบจัดการข้อมูลนักศึกษา สร้างด้วย Next.js, Prisma และ SQLite
พร้อมตัวอย่างการตรวจสอบข้อมูล (Zod) และการจัดการหน้า Loading/Error

## เทคโนโลยีที่ใช้

- Node.js
- Next.js (App Router) + TypeScript
- Tailwind CSS
- Prisma 7.10.0
- SQLite (better-sqlite3)
- Zod

## วิธีการติดตั้ง

ต้องติดตั้ง Node.js (แนะนำเวอร์ชัน LTS) และ Git ก่อน

1. ดาวน์โหลดโปรเจกต์

```bash
git clone <URL ของ repository นี้>
cd <ชื่อโฟลเดอร์โปรเจกต์>
```

2. ติดตั้งแพ็กเกจ

```bash
npm install
```

3. สร้างไฟล์ `.env` ไว้ที่โฟลเดอร์นอกสุด (ระดับเดียวกับ package.json) แล้วใส่

```
DATABASE_URL="file:./dev.db"
```

4. สร้างฐานข้อมูลและ Prisma Client

```bash
npx prisma migrate dev
npx prisma generate
```

5. เปิดเซิร์ฟเวอร์

```bash
npm run dev
```

## วิธีการใช้งาน

### สัปดาห์ที่ 1: ระบบ CRUD นักศึกษา

เปิด http://localhost:3000/students

- ดูรายการ: หน้า /students แสดงตารางนักศึกษาทั้งหมด
- เพิ่ม: กดปุ่ม "เพิ่มนักศึกษา" กรอกข้อมูลแล้วกด "บันทึก"
- แก้ไข: กดปุ่ม "แก้ไข" ที่แถวของนักศึกษา แล้วกด "บันทึกการแก้ไข"
- ลบ: กดปุ่ม "ลบ" แล้วกดยืนยันในกล่องข้อความ

### สัปดาห์ที่ 2: Validation, Loading และ Error

1. การตรวจสอบข้อมูลด้วย Zod
   ที่หน้า http://localhost:3000/students/create ถ้ากรอกข้อมูลไม่ถูกต้อง
   (เช่น เว้นช่องว่าง, ชั้นปีเกิน 8, รหัสนักศึกษาซ้ำ) จะแสดงข้อความ error ใต้ช่องนั้น

2. Loading, Suspense และ Skeleton
   เปิด http://localhost:3000/blogs จะเห็นรายการบทความจาก API ภายนอก
   ระหว่างโหลดจะแสดง Skeleton (ต้องต่ออินเทอร์เน็ต)

3. หน้า Not Found
   เปิด http://localhost:3000/blogs/1 เพื่อดูบทความ
   ถ้าเปิดรหัสที่ไม่มี เช่น http://localhost:3000/blogs/999 จะแสดงหน้า 404

4. หน้า Error
   มี error.tsx สำหรับส่วน /blogs และ global-error.tsx สำหรับทั้งเว็บ

หน้าตัวอย่าง Skeleton ดูได้ที่ http://localhost:3000/skeleton