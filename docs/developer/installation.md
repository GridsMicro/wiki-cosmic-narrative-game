# การติดตั้งและเริ่มต้นโปรเจค

## 📋 ข้อกำหนดเบื้องต้น

### Software Requirements
- **Node.js**: 18.x หรือสูงกว่า
- **npm** หรือ **pnpm**: Package manager
- **Git**: สำหรับ version control
- **Supabase Account**: สำหรับ database และ authentication

### Knowledge Requirements
- TypeScript / JavaScript
- React และ Next.js (App Router)
- Tailwind CSS
- Supabase (PostgreSQL, Row Level Security)

---

## 🚀 การติดตั้ง

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/cosmic-narrative-game.git
cd cosmic-narrative-game
```

### 2. ติดตั้ง Dependencies

```bash
npm install
# หรือ
pnpm install
```

### 3. ตั้งค่า Environment Variables

สร้างไฟล์ `.env.local` ในโฟลเดอร์ root:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

# Google Gemini AI (สำหรับระบบ Chat)
GOOGLE_GENERATIVE_AI_API_KEY=your_gemini_api_key

# Optional: Stripe (สำหรับระบบชำระเงิน - ถ้ามี)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your_stripe_key
STRIPE_SECRET_KEY=your_stripe_secret
```

!!! warning "ความปลอดภัย"
    **ห้าม** commit ไฟล์ `.env.local` ขึ้น Git! ตรวจสอบให้แน่ใจว่ามีใน `.gitignore`

---

## 🗄️ ตั้งค่า Database (Supabase)

### 1. สร้าง Supabase Project

1. ไปที่ [supabase.com](https://supabase.com)
2. สร้าง Project ใหม่
3. คัดลอก URL และ Anon Key มาใส่ใน `.env.local`

### 2. รัน SQL Schema

ไปที่ **SQL Editor** ใน Supabase Dashboard และรันไฟล์ SQL ตามลำดับ:

#### 2.1 Core Tables
```bash
# ในโปรเจค ดูไฟล์ที่:
docs/database_master_schema.md
```

รัน SQL สำหรับตารางหลัก:
- `player_save_data` - ข้อมูลผู้เล่น
- `cards_master` - ข้อมูลการ์ด
- `items` - ไอเทมในเกม
- `player_items` - ไอเทมของผู้เล่น
- `maps` - แผนที่และสถานที่
- `npcs_master` - ตัวละคร NPC

#### 2.2 Row Level Security (RLS)

!!! danger "สำคัญมาก"
    ต้องเปิด RLS และตั้งค่า Policies เพื่อความปลอดภัย!

```sql
-- ตัวอย่าง RLS Policy สำหรับ player_save_data
ALTER TABLE player_save_data ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Users can view own data"
ON player_save_data FOR SELECT
USING (auth.uid() = user_id);

CREATE POLICY "Users can update own data"
ON player_save_data FOR UPDATE
USING (auth.uid() = user_id);
```

### 3. Seed Data (ข้อมูลเริ่มต้น)

รันคำสั่ง SQL เพื่อใส่ข้อมูลเริ่มต้น:

```sql
-- ดูตัวอย่างใน:
-- docs/card_system.md
-- docs/equipment_system.md
```

หรือใช้ **Dev Tools** ในเกม:
1. รันเกม: `npm run dev`
2. ไปที่ `/game/dev-tools`
3. กดปุ่ม "Seed Data" ในแต่ละแท็บ

---

## 🎮 รันโปรเจค

### Development Mode

```bash
npm run dev
```

เปิดเบราว์เซอร์ที่ `http://localhost:3000`

### Production Build

```bash
npm run build
npm start
```

---

## 📁 โครงสร้างโปรเจค

```
cosmic-narrative-game/
├── app/                        # Next.js App Router
│   ├── ai/                    # ระบบ AI Chat
│   ├── game/                  # ระบบเกม RPG
│   │   ├── layout.tsx         # Game Layout + Modals
│   │   ├── astra-city/        # เมืองหลัก
│   │   ├── battle/            # ระบบการต่อสู้
│   │   ├── cards/             # จัดการการ์ด
│   │   └── dev-tools/         # เครื่องมือสำหรับ Dev
│   └── api/                   # API Routes
│       └── chat/              # Gemini AI Integration
├── components/                 # React Components
│   ├── game/                  # Game-specific components
│   │   ├── modals/            # Modal components
│   │   ├── PlayerHUD.tsx      # HUD หลัก
│   │   └── PetCompanion.tsx   # ระบบสัตว์เลี้ยง
│   └── CosmicChatComponent.tsx
├── context/
│   └── GameContext.tsx        # Global State Management
├── hooks/
│   └── useGameData.ts         # Custom Hooks
├── lib/
│   └── supabase.ts            # Supabase Client
├── types/
│   ├── game.ts                # Game Types
│   └── database.ts            # Database Types
└── docs/                      # เอกสาร
    ├── roadmap.md
    ├── changelog.md
    └── ...
```

---

## 🔧 เครื่องมือสำหรับนักพัฒนา

### Dev Tools Panel

เข้าถึงได้ที่: `/game/dev-tools`

**ฟีเจอร์**:
- 📊 **Dashboard**: ภาพรวมข้อมูลทั้งหมด
- 🃏 **Cards**: จัดการการ์ด (CRUD)
- 🎒 **Items**: จัดการไอเทม
- 👥 **Players**: ดูและแก้ไขข้อมูลผู้เล่น
- 🗺️ **Maps**: จัดการแผนที่
- 🧑‍🤝‍🧑 **NPCs**: จัดการตัวละคร NPC
- 🐾 **Pets**: จัดการสัตว์เลี้ยง
- 🎵 **Music**: อัพโหลดเพลง BGM

### Database Viewer

ใช้ Supabase Dashboard:
- **Table Editor**: แก้ไขข้อมูลโดยตรง
- **SQL Editor**: รัน SQL queries
- **Storage**: จัดการไฟล์ (รูปภาพ, เสียง)

---

## 🐛 การ Debug

### React DevTools
```bash
npm install -g react-devtools
react-devtools
```

### Supabase Logs
ดู Real-time logs ใน Supabase Dashboard > Logs

### Console Logging
```typescript
// ใช้ใน development เท่านั้น
if (process.env.NODE_ENV === 'development') {
  console.log('Debug:', data)
}
```

---

## 📦 การ Deploy

### Vercel (แนะนำ)

1. Push โค้ดขึ้น GitHub
2. Import project ใน [Vercel](https://vercel.com)
3. เพิ่ม Environment Variables
4. Deploy!

### Manual Build

```bash
npm run build
npm start
```

---

## 🔗 ลิงก์ที่เป็นประโยชน์

- [Next.js Documentation](https://nextjs.org/docs)
- [Supabase Documentation](https://supabase.com/docs)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Framer Motion](https://www.framer.com/motion/)
- [Google Gemini AI](https://ai.google.dev/)

---

## 💡 เคล็ดลับ

!!! tip "Hot Reload"
    Next.js รองรับ Hot Module Replacement (HMR) - บันทึกไฟล์แล้วเห็นผลทันที!

!!! tip "TypeScript"
    ใช้ TypeScript เต็มที่ - จะช่วยจับ bugs ก่อน runtime

!!! tip "Supabase Types"
    Generate TypeScript types จาก Supabase:
    ```bash
    npx supabase gen types typescript --project-id your-project-id > types/database.ts
    ```
