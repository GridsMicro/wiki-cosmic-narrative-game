# ระบบคำนวณสถิติ / Stat Calculation Formulas (Objective C)

=== "ภาษาไทย (Thai)"

    ## 🎯 เป้าหมายของ Objective C: สูตรการคำนวณสถิติ
    เอกสารฉบับนี้อธิบายเกี่ยวกับ **สูตรคณิตศาสตร์หลัก** ที่ใช้ในเกมเพื่อคำนวณสถิติของผู้เล่น, การเลื่อนระดับ (Level Progression), และฟังก์ชันช่วยเหลือต่างๆ

    ---

    ### 1️⃣ สูตรคำนวณสถิติหลัก (Core Stat Formula)
    ```
    FinalStat = Base + (ClassGrowth * Level) + Equipment + Buffs
    ```
    - **Base** – ค่าพื้นฐานที่กำหนดใน `characters_master` (หรือค่าเริ่มต้นสำหรับผู้เล่นใหม่)
    - **ClassGrowth** – ตัวคูณการเติบโตตามสายอาชีพ (เช่น `growth_stk`, `growth_vit`, …) ซึ่งเก็บไว้ในตารางเดียวกัน
    - **Level** – เลเวลปัจจุบันของผู้เล่น (เริ่มต้นที่ 1)
    - **Equipment** – ผลรวมของโบนัสจากอุปกรณ์สวมใส่ทั้งหมดที่มีผลต่อค่านั้นๆ
    - **Buffs** – ผลรวมของบัฟชั่วคราว (เช่น จากไอเทม, สกิล, หรือประกาศพิเศษ)

    ### 2️⃣ ฟังก์ชันช่วยเหลือ (Implemented in `utils/game-formulas.ts`)
    | ฟังก์ชัน                                                                                            | คำอธิบาย                                                                               |
    | :----------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------- |
    | `calculateFinalStat(base, classGrowth, level, equipment = 0, buffs = 0)`                         | คืนค่าสถิติเดี่ยวโดยใช้สูตรหลัก                                                               |
    | `calculateAllStats({ baseStats, classGrowths, level, equipmentBonuses = {}, buffBonuses = {} })` | คำนวณ **ค่าสถิติหลักทั้ง 7** (`STK`, `VIT`, `NIT`, `TAPA`, `MED`, `SOUL`, `HOLY`) ในครั้งเดียว |
    | `calculateExpForNextLevel(currentLevel)`                                                         | คืนค่าจำนวน EXP ที่ต้องใช้เพื่อเลื่อนระดับถัดไป (เส้นโค้งเอกซ์โพเนนเชียล)                             |

    ### 3️⃣ ระบบการเลื่อนระดับ (Leveling System)
    - **เส้นโค้ง EXP** – `EXP_next = floor(100 * (Level ^ 1.5))`
    - เมื่อผู้เล่นได้รับ EXP ให้เปรียบเทียบยอดรวมกับ `EXP_next` หากเกินขีดจำกัด ให้เพิ่ม `level` ขึ้น 1, หัก EXP ที่ใช้ไป, และคำนวณเกณฑ์ใหม่สำหรับระดับถัดไป
    - UI (หน้าโปรไฟล์) สามารถแสดงความต้องการสำหรับระดับถัดไปโดยใช้ helper function

    ### 4️⃣ ตัวอย่างการใช้งาน (Pseudo-code)
    ```ts
    import { calculateAllStats, calculateExpForNextLevel } from '@/utils/game-formulas';

    // ดึงข้อมูลผู้เล่นและข้อมูลคลาสจาก Supabase
    const player = await supabase.from('player_save_data').select('*').single();
    const classInfo = await supabase.from('characters_master').select('*').eq('id', player.class_id).single();

    const finalStats = calculateAllStats({
      baseStats: {
        STK: player.base_stk,
        VIT: player.base_vit,
        NIT: player.base_nit,
        TAPA: player.base_tapa,
        MED: player.base_med,
        SOUL: player.base_soul,
        HOLY: player.base_holy,
      },
      classGrowths: {
        STK: classInfo.growth_stk,
        VIT: classInfo.growth_vit,
        NIT: classInfo.growth_nit,
        TAPA: classInfo.growth_tapa,
        MED: classInfo.growth_med,
        SOUL: classInfo.growth_soul,
        HOLY: classInfo.growth_holy,
      },
      level: player.level,
      equipmentBonuses: player.equipment_bonuses, // ตัวเลือกเสริม
      buffBonuses: player.active_buffs,          // ตัวเลือกเสริม
    });

    // EXP สำหรับเลเวลถัดไป
    const expNeeded = calculateExpForNextLevel(player.level);
    console.log('เลเวลถัดไปที่', expNeeded, 'EXP');
    ```

    ### 5️⃣ จุดที่ต้องเชื่อมต่อ (Integration Points)
    - **หน้าโปรไฟล์ (Profile Page)** – แทนที่ค่าสถิติดิบด้วย `finalStats` จาก helper เพื่อให้แน่ใจว่าค่าที่แสดงสะท้อนผลจากอุปกรณ์และบัฟ
    - **ระบบต่อสู้ (Combat System)** – ใช้ `calculatePhysicalAttack`, `calculateMagicalAttack` และอื่นๆ ร่วมกับค่าสถิติหลัก
    - **เลเวลอัพ UI** – แสดงแถบความคืบหน้าตาม `player.exp / expNeeded`

    ---

    **ขั้นตอนถัดไป**
    1. อัปเดต **Profile UI** เพื่อเรียก `calculateAllStats` และแสดงค่าเหล่านั้น
    2. เพิ่ม **Level-Up handler** ที่ตรวจสอบ EXP หลังการต่อสู้หรือเควสต์ทุกครั้งและเพิ่มค่า `player.level` ตามความเหมาะสม

=== "English"

    ## 🎯 Objective C: Stat Calculation Formulas
    The goal of this document is to describe the **core mathematical formulas** used throughout the game to calculate a player’s stats, level progression, and related utilities.

    ---

    ### 1️⃣ Core Stat Formula
    ```
    FinalStat = Base + (ClassGrowth * Level) + Equipment + Buffs
    ```
    - **Base** – The base value defined in `characters_master` (or default values for a new player).
    - **ClassGrowth** – Growth multiplier for the selected archetype (e.g., `growth_stk`, `growth_vit`, …). Stored in the same table.
    - **Level** – Player’s current level (starts at 1).
    - **Equipment** – Sum of all equipment bonuses that affect the given attribute.
    - **Buffs** – Sum of temporary buffs (e.g., from items, skills, announcements).

    ### 2️⃣ Helper Functions (Implemented in `utils/game-formulas.ts`)
    | Function                                                                                         | Description                                                                                           |
    | :----------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------- |
    | `calculateFinalStat(base, classGrowth, level, equipment = 0, buffs = 0)`                         | Returns a single stat using the core formula.                                                         |
    | `calculateAllStats({ baseStats, classGrowths, level, equipmentBonuses = {}, buffBonuses = {} })` | Calculates **all seven core stats** (`STK`, `VIT`, `NIT`, `TAPA`, `MED`, `SOUL`, `HOLY`) in one call. |
    | `calculateExpForNextLevel(currentLevel)`                                                         | Returns the amount of EXP required to reach the next level (exponential curve).                       |

    ### 3️⃣ Leveling System
    - **EXP Curve** – `EXP_next = floor(100 * (Level ^ 1.5))`
    - When a player gains EXP, compare the total with `EXP_next`. If the total exceeds the threshold, increase `level` by 1, subtract the required EXP, and recalculate the next threshold.
    - The UI (Profile page) can display the next‑level requirement using the helper.

    ### 4️⃣ Example Usage (Pseudo‑code)
    ```ts
    import { calculateAllStats, calculateExpForNextLevel } from '@/utils/game-formulas';

    // Fetch player data & class info from Supabase
    const player = await supabase.from('player_save_data').select('*').single();
    const classInfo = await supabase.from('characters_master').select('*').eq('id', player.class_id).single();

    const finalStats = calculateAllStats({
      baseStats: {
        STK: player.base_stk,
        VIT: player.base_vit,
        NIT: player.base_nit,
        TAPA: player.base_tapa,
        MED: player.base_med,
        SOUL: player.base_soul,
        HOLY: player.base_holy,
      },
      classGrowths: {
        STK: classInfo.growth_stk,
        VIT: classInfo.growth_vit,
        NIT: classInfo.growth_nit,
        TAPA: classInfo.growth_tapa,
        MED: classInfo.growth_med,
        SOUL: classInfo.growth_soul,
        HOLY: classInfo.growth_holy,
      },
      level: player.level,
      equipmentBonuses: player.equipment_bonuses, // optional
      buffBonuses: player.active_buffs,          // optional
    });

    // EXP for next level
    const expNeeded = calculateExpForNextLevel(player.level);
    console.log('Next level at', expNeeded, 'EXP');
    ```

    ### 5️⃣ Integration Points
    - **Profile Page** – Replace the raw attribute values with `finalStats` from the helper to ensure the displayed numbers reflect equipment and buffs.
    - **Combat System** – Use `calculatePhysicalAttack`, `calculateMagicalAttack`, etc., together with the core stat values.
    - **Level‑Up UI** – Show a progress bar based on `player.exp / expNeeded`.

    ---

    **Next Steps**
    1. Update the **Profile UI** to call `calculateAllStats` and render those values.
    2. Add a **Level‑Up handler** that checks EXP after each battle or quest and increments `player.level` accordingly.
    3. Document any additional formulas (damage, crit, drop rates) in the wiki as needed.

*Document last updated:* 2025‑12‑22
