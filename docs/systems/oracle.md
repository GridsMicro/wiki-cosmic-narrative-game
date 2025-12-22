# ระบบคำทำนายพยากรณ์ / Oracle Prophecy System

=== "ภาษาไทย (Thai)"

    ## 🔮 ภาพรวมระบบ
    ระบบคำทำนายพยากรณ์ (Oracle Prophecy System) เป็นกลไกการสุ่มรับ "คำทำนาย" ประจำวันหรือตามอีเวนต์ เพื่อมอบบัฟ (Buff) พิเศษให้กับผู้เล่น โดยอ้างอิงจากไพ่ยิปซี (Tarot) ครบชุดจำนวน 78 ใบ

    ---

    ## 🃏 รายละเอียดไพ่ (Complete Deck - 78 Cards)
    ระบบประกอบด้วยไพ่ทั้งหมด 78 ใบ แบ่งเป็นสองชุดหลัก:

    ### 1. Major Arcana (22 ใบ) - ระดับ: Legendary
    เป็นไพ่ที่มีพลังสูงที่สุด มอบบัฟที่ส่งผลกระทบอย่างมากต่อการเล่น
    - **ตัวอย่างไพ่**: The Fool, The Magician, The Empress, The Sun, The World
    - **บัฟพื้นฐาน**: มักเพิ่มค่า `LUX` หรือค่าสเตตัสสะสมในระดับสูง

    ### 2. Minor Arcana (56 ใบ) - ระดับ: Common
    แบ่งตามชุดสัญลักษณ์ (Suits):
    - **Wands (ไม้เท้า)**: เกี่ยวข้องกับการงานและการเติบโต
    - **Cups (ถ้วย)**: เกี่ยวข้องกับความรู้สึกและความสัมพันธ์
    - **Swords (ดาบ)**: เกี่ยวข้องกับอุปสรรคและการแก้ไขปัญหา
    - **Pentacles (เหรียญ)**: เกี่ยวข้องกับการเงินและความมั่งคั่ง

    ---

    ## 📊 โครงสร้างข้อมูล (Database)
    ข้อมูลถูกเก็บไว้ในตาราง `oracle_prophecies`:

    | ฟิลด์         | ประเภท    | คำอธิบาย                             |
    | :---------- | :-------- | :--------------------------------- |
    | `id`        | `UUID`    | คีย์หลัก                              |
    | `card_name` | `VARCHAR` | ชื่อไพ่ (ภาษาอังกฤษ)                   |
    | `meaning`   | `TEXT`    | ความหมายและคำทำนาย (ภาษาไทย)         |
    | `buff_stat` | `VARCHAR` | รหัสสเตตัสที่ได้รับบัฟ (เช่น LUX +10)      |
    | `rarity`    | `VARCHAR` | ระดับความหายาก (Legendary / Common) |

    ## 📍 จุดเริ่มต้น (Entry Point)
    ผู้เล่นสามารถเข้าถึงระบบคำทำนายได้โดยการไปพบกับ **"นักพยากรณ์ดวงดาว" (Star Oracle)**:
    - **สถานที่**: เมืองดาราอัสตรา (Astra City)
    - **NPC**: เซราฟีน่า (Seraphina)
    - **เงื่อนไข**: สามารถสุ่มไพ่ได้วันละ 1 ครั้ง โดยบัฟจะคงอยู่จนถึงเที่ยงคืน

    ---

    ## 🛠️ การจัดการผ่าน DevTools
    แอดมินสามารถจัดการไพ่ได้ที่เมนู **Oracle Prophecies**:
    - **CRUD**: เพิ่ม แก้ไข หรือลบคำทำนาย
    - **Images**: สามารถอัปโหลดรูปภาพประจำไพ่ได้ (ผ่าน API/Storage)
    - **Seeding**: ระบบรองรับการรัน SQL เพื่อติดตั้งชุดไพ่มาตรฐาน 78 ใบได้ทันที

=== "English"

    ## 🔮 System Overview
    The Oracle Prophecy System is a mechanism for randomly receiving a "Prophecy" (daily or event-based) that grants special buffs to the player. It is based on a complete set of 78 Tarot cards.

    ---

    ## 🃏 Card Details (Complete Deck - 78 Cards)
    The system consists of 78 cards divided into two main categories:

    ### 1. Major Arcana (22 Cards) - Rarity: Legendary
    The most powerful cards, granting buffs that significantly impact gameplay.
    - **Examples**: The Fool, The Magician, The Empress, The Sun, The World.
    - **Base Buffs**: Usually increases `LUX` or cumulative stats at a high level.

    ### 2. Minor Arcana (56 Cards) - Rarity: Common
    Divided by Suits:
    - **Wands**: Related to work and growth.
    - **Cups**: Related to feelings and relationships.
    - **Swords**: Related to obstacles and problem-solving.
    - **Pentacles**: Related to finance and wealth.

    ---

    ## 📊 Database Schema
    Data is stored in the `oracle_prophecies` table:

    | Field       | Type      | Description                    |
    | :---------- | :-------- | :----------------------------- |
    | `id`        | `UUID`    | Primary Key                    |
    | `card_name` | `VARCHAR` | Card Name (English)            |
    | `meaning`   | `TEXT`    | Meaning and Prophecy (Thai)    |
    | `buff_stat` | `VARCHAR` | Buff Stat Code (e.g., LUX +10) |
    | `rarity`    | `VARCHAR` | Rarity (Legendary / Common)    |

    ## 📍 Entry Point
    Players can access the prophecy system by visiting the **"Star Oracle"**:
    - **Location**: Astra City
    - **NPC**: Seraphina
    - **Condition**: One draw per day. Buffs last until midnight.

    ---

    ## 🛠️ DevTools Management
    Admins can manage cards in the **Oracle Prophecies** menu:
    - **CRUD**: Add, Edit, or Delete prophecies.
    - **Images**: Upload card images (via API/Storage).
    - **Seeding**: The system supports running SQL to install the standard 78-card deck immediately.

*Last Updated: 2025-12-22*
