# 🔧 Environment Variables Setup Guide

## 📝 ภาพรวม

โปรเจกต์ Cosmic Narrative Game ใช้ environment variables สำหรับการตั้งค่าต่างๆ เช่น:
- การเชื่อมต่อ Supabase
- URL ของเกมจริง (สำหรับ DevTools)
- API Keys อื่นๆ

---

## 🏗️ โครงสร้างโปรเจกต์

เรามี 2 โปรเจกต์แยกกัน:

### 1. `engins-cosmic-narrative-game` (DevTools)
- **Port:** 3000
- **จุดประสงค์:** เครื่องมือสำหรับ admin จัดการข้อมูลเกม
- **URL:** http://localhost:3000/dev-tools

### 2. `cosmic-narrative-game` (Game)
- **Port:** 3002
- **จุดประสงค์:** เกมจริงที่ผู้เล่นใช้งาน
- **URL:** http://localhost:3002/game

---

## ⚙️ การตั้งค่า Environment Variables

### สำหรับ DevTools (`engins-cosmic-narrative-game`)

สร้างไฟล์ `.env.local` ในโฟลเดอร์ `engins-cosmic-narrative-game`:

```env
# Supabase Connection
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here

# URL ของโปรเจกต์เกมจริง (cosmic-narrative-game)
# Development: ใช้ localhost
NEXT_PUBLIC_GAME_URL=http://localhost:3002

# Production: ใช้โดเมนจริง
# NEXT_PUBLIC_GAME_URL=https://yourgame.com

# Gemini API (ถ้ามี)
GEMINI_API_KEY=your-gemini-api-key-here
```

### สำหรับ Game (`cosmic-narrative-game`)

สร้างไฟล์ `.env.local` ในโฟลเดอร์ `cosmic-narrative-game`:

```env
# Supabase Connection
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here

# Gemini API (ถ้ามี)
GEMINI_API_KEY=your-gemini-api-key-here
```

---

## 🚀 การรัน Development

### 1. รัน DevTools (Port 3000)
```bash
cd engins-cosmic-narrative-game
npm run dev
```

### 2. รัน Game (Port 3002)
```bash
cd cosmic-narrative-game
npm run dev -- -p 3002
```

หรือแก้ไข `package.json` ของ `cosmic-narrative-game`:
```json
{
  "scripts": {
    "dev": "next dev -p 3002"
  }
}
```

---

## 🌐 Production Deployment

### Vercel / Netlify

เมื่อ deploy ให้ตั้งค่า environment variables ใน dashboard:

**สำหรับ DevTools:**
```
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
NEXT_PUBLIC_GAME_URL=https://yourgame.com
GEMINI_API_KEY=your-api-key
```

**สำหรับ Game:**
```
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
GEMINI_API_KEY=your-api-key
```

### ตัวอย่าง URLs ใน Production:
- **DevTools:** https://admin.yourgame.com
- **Game:** https://yourgame.com
- **Environment Variable:** `NEXT_PUBLIC_GAME_URL=https://yourgame.com`

---

## 🔍 การตรวจสอบ

### ตรวจสอบว่า Environment Variables โหลดถูกต้อง:

```tsx
// ใน component ใดก็ได้
console.log('Game URL:', process.env.NEXT_PUBLIC_GAME_URL);
console.log('Supabase URL:', process.env.NEXT_PUBLIC_SUPABASE_URL);
```

### ตรวจสอบปุ่ม "Visit" ใน DevTools:

1. เปิด DevTools (http://localhost:3000/dev-tools)
2. ไปที่เมนู "Maps" หรือ "Regions"
3. คลิกปุ่ม "Visit" (รูปตา 👁️)
4. ควร redirect ไปที่ `http://localhost:3001/game/world/xxx`

---

## ⚠️ ข้อควรระวัง

### 1. Restart Server หลังเปลี่ยน `.env.local`
Environment variables จะโหลดตอน build time เท่านั้น ต้อง restart:
```bash
# กด Ctrl+C แล้วรันใหม่
npm run dev
```

### 2. ห้ามเผยแพร่ `.env.local`
ไฟล์นี้มี sensitive data (API keys) อยู่:
- ✅ เพิ่ม `.env.local` ใน `.gitignore`
- ❌ ห้าม commit ขึ้น Git

### 3. ใช้ `NEXT_PUBLIC_` สำหรับ Client-Side
- ตัวแปรที่ขึ้นต้นด้วย `NEXT_PUBLIC_` จะถูกส่งไปยัง browser
- ตัวแปรอื่นๆ (เช่น `GEMINI_API_KEY`) จะใช้ได้แค่ server-side

---

## 📚 เอกสารเพิ่มเติม

- [Next.js Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)
- [Supabase Setup](https://supabase.com/docs/guides/getting-started)
- [DevTools Documentation](./dev-tools.md)

---

**สร้างโดย:** Antigravity AI  
**วันที่:** 2025-12-27  
**เวอร์ชัน:** 1.0
