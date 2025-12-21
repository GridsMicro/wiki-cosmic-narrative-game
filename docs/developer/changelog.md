# ประวัติการอัพเดท (Changelog)

เอกสารนี้บันทึกการเปลี่ยนแปลงที่สำคัญทั้งหมดของโปรเจค Cosmic Narrative Game

รูปแบบอ้างอิงจาก [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)

---

## [Unreleased] - 2025-12-21

### Added
- 📚 **Wiki Documentation**: สร้าง wiki แยกต่างหากด้วย MkDocs Material
  - เอกสารสำหรับผู้เล่น (Getting Started, Systems, World, Guides)
  - เอกสารสำหรับนักพัฒนา (Installation, Roadmap, Changelog)
  - รองรับภาษาไทยเต็มรูปแบบ

---

## [Unreleased] - 2025-12-20

### Added
- 🗺️ **NPC & Map Master System**: ระบบจัดการโลกเกมที่สมบูรณ์
  - **Map Registry**: ตาราง `maps` และ Dev Tools สำหรับจัดการสถานที่
  - **NPC Engine**: ตาราง `npcs_master` พร้อมระบบจัดการ sprite ผ่าน Supabase Storage
  - **Dialogue System**: ระบบบทสนทนาแบบ JSON array
  - **Interactive NPCs**: รองรับ `function_type` (Warp, Reward, Shop, Buff, Upgrade)
- 🔍 **Search & Filter System**: ระบบค้นหา real-time ใน Dev Tools
- 🔮 **Oracle Editor**: เพิ่มการอัพโหลดรูปภาพสำหรับ Oracle Prophecies

### Changed
- 🎨 **Dev Tools Layout**: ปรับโครงสร้างให้ Editor Form อยู่ด้านบนและ Registry List อยู่ด้านล่าง
- ⚡ **Player Editor**: เพิ่มการแก้ไข "5 Celestial Powers" (`nit`, `tapa`, `meditation`, `soul`, `holy`)

### Fixed
- 🔧 **SQL Idempotency**: ปรับ SQL schema ให้ใช้ `IF NOT EXISTS` เพื่อรันซ้ำได้อย่างปลอดภัย

---

## [Unreleased] - 2025-12-18

### Added
- 📸 **Design System Snapshot**: สร้าง `/docs/ui_snapshot_v2.md` เพื่อบันทึกสไตล์ Premium Dark Mode
- 🎮 **Enhanced Equipment Slots**: เพิ่มขนาด slot จาก `w-16` เป็น `w-20` เพื่อความรู้สึก "AAA game"
- 📱 **Responsive Body Layout**: ระบบ responsive สำหรับ equipment grid แบบ humanoid
- 🛒 **Marketplace Integration**: เชื่อมต่อ UI กับ Supabase `items` table
- 🗄️ **Equipment Database**: ออกแบบตาราง `items` (master) และ `player_items` (instance)
- 💊 **Consumable Seed Data**: เพิ่มข้อมูล HP/MP potions และ status cleanse items
- 🎯 **Game Overlay Menu**: เพิ่มเมนูลอยสำหรับเข้าถึง Equipment และ Skills

### Changed
- ↩️ **UI/UX Revert**: เปลี่ยนกลับเป็น separate pages แทน scrollable modal
- 🎯 **Skills Tab Revert**: กลับไปใช้ mock version คุณภาพสูง
- 📏 **Modal Refinement**: ปรับ padding และ heading scale สำหรับหน้าจอเล็ก
- 📱 **Mobile UI Optimization**: ปรับ game modals ให้เหมาะกับมือถือ
- 🏛️ **Main Square Header**: ทำให้ compact ขึ้นเพื่อไม่ทับกับ HUD
- 🎨 **Game Buttons**: ปรับปุ่มให้เป็น `rounded-2xl` และ compact

### Fixed
- 🐛 **JSX Structure**: แก้ syntax errors ใน `layout.tsx`
- 📐 **HUD Overlap**: แก้ปัญหา layout shifts
- 🗄️ **Database Schema**: แก้ missing columns (`rarity`, `price`) ในตาราง `items`
- 🎨 **UI Overlap**: แก้ปัญหา UI ทับกันในหลายหน้า

---

## [Unreleased] - 2024-12-17

### Added
- 📝 **Rich Text Rendering**: ใช้ `react-markdown` และ `remark-gfm` สำหรับ AI responses
- 🔧 **Shared Types**: สร้าง `types/chat.ts` สำหรับ type safety

### Changed
- 🧩 **Component Refactoring**: แยก Player Status ออกเป็น `PlayerHUD.tsx`

### Fixed
- 🔒 **AI Response Encoding**: แก้ปัญหา "Code Leaking" ด้วย Base64 encoding
  - เพิ่ม Base64 encoding ใน `app/api/chat/route.ts`
  - เพิ่ม Base64 decoding ใน `CosmicChatComponent.tsx`

---

## [0.3.0] - 2024-12-15

### Added
- 🐾 **Pet System**: ระบบสัตว์เลี้ยงครบวงจร
  - ตาราง `pets_master` และ `player_pets`
  - Pet Companion UI พร้อม animations
  - ระบบ buffs จากสัตว์เลี้ยง
  - Pet personality และ dialogue
- 🎴 **Card System Enhancements**:
  - Card rarity system (Common, Rare, Epic, Legendary)
  - Card upgrade mechanics
  - Visual card collection UI

### Changed
- 🎨 **UI Polish**: ปรับปรุง animations และ transitions
- ⚡ **Performance**: Optimize re-renders ด้วย React.memo

---

## [0.2.0] - 2024-12-10

### Added
- ⚔️ **Equipment System**: ระบบอุปกรณ์และ inventory
  - 8 equipment slots (Weapon, Helmet, Armor, etc.)
  - Humanoid layout UI
  - Item stats และ bonuses
- 🏪 **Marketplace**: ระบบซื้อขายไอเทม
  - Dynamic item listing
  - Gold currency system
  - Buy/Sell mechanics
- 🔨 **Blacksmith**: ระบบอัพเกรดอุปกรณ์

### Changed
- 💾 **Database Schema**: ปรับปรุงโครงสร้างตาราง
- 🎯 **Game Balance**: ปรับ item prices และ stats

---

## [0.1.0] - 2024-12-01

### Added
- 🎮 **Initial Release**: เวอร์ชันแรกของเกม
  - ระบบ Authentication (Supabase)
  - Player Profile System
  - Basic Chat Interface
  - Card Collection System
  - Dark Mode Premium UI
  - Thai Language Support

### Infrastructure
- ⚙️ **Tech Stack**:
  - Next.js 14 (App Router)
  - TypeScript
  - Tailwind CSS
  - Supabase (PostgreSQL + Auth + Storage)
  - Framer Motion
  - Google Gemini AI

---

## 📊 Statistics

### Code Metrics (ล่าสุด)
- **Total Lines of Code**: ~15,000+
- **Components**: 50+
- **Database Tables**: 12
- **API Routes**: 8
- **Pages**: 20+

### Database Records
- **Cards**: 50+ cards
- **Items**: 30+ items
- **NPCs**: 20+ characters
- **Maps**: 7 main hubs
- **Pets**: 10+ companions

---

## 🏷️ Version Naming

เราใช้ [Semantic Versioning](https://semver.org/):
- **MAJOR**: เปลี่ยนแปลงใหญ่ที่ไม่ compatible
- **MINOR**: เพิ่มฟีเจอร์ใหม่แบบ backward compatible
- **PATCH**: Bug fixes และ improvements

---

## 📝 Change Categories

### Added
ฟีเจอร์ใหม่ที่เพิ่มเข้ามา

### Changed
การเปลี่ยนแปลงฟีเจอร์ที่มีอยู่แล้ว

### Deprecated
ฟีเจอร์ที่จะถูกลบในอนาคต

### Removed
ฟีเจอร์ที่ถูกลบออก

### Fixed
Bug fixes

### Security
แก้ไขช่องโหว่ด้านความปลอดภัย

---

## 🔗 Links

- [Roadmap](roadmap.md) - แผนการพัฒนาในอนาคต
- [GitHub Issues](https://github.com/yourusername/cosmic-narrative-game/issues) - รายงานปัญหา
- [GitHub Releases](https://github.com/yourusername/cosmic-narrative-game/releases) - Download versions

---

*เอกสารนี้อัพเดทอัตโนมัติทุกครั้งที่มีการเปลี่ยนแปลงสำคัญ*
