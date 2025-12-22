# การอ้างอิง API / API Reference (System Actions)

=== "ภาษาไทย (Thai)"

    หน้านี้รวบรวมคำอธิบายเกี่ยวกับ `GameAction` ที่ใช้ในการควบคุมสถานะของเกมผ่านระบบ AI Chat และ RPG UI

    ---

    ## 🛠️ รายละเอียด GameAction (GameAction Specs)

    ระบบใช้ `GameAction` ในการรับข้อมูลจาก AI (Tools) หรือ UI เพื่ออัพเดท `GameContext`

    ### 1. ZODIAC_SET
    ใช้เมื่อเริ่มเกมเพื่อระบุราศีและสถานะเริ่มต้น
    - **Payload**: `ZodiacTrait` object
    - **Database**: อัพเดทตาราง `player_save_data` ในคอลัมน์ `zodiac_json`

    ### 2. STATS_UPDATE
    ใช้เมื่อตัวละครเลเวลอัพ หรือได้รับการฝึกฝน
    - **Payload**: `Partial<Stats>` (รองรับทั้งชื่อเก่าชุด str/dex และชื่อใหม่ชุด stk/nit)
    - **Logic**: ระบบมี **Stats Mapping Interpreter** ใน `GameContext` เพื่อแปลงค่าสเตตัสจาก AI (Legacy) ให้ตรงกับคอลัมน์ใน Supabase (New RPG) อัตโนมัติ

    ### 3. ITEM_ADD (Integrated)
    ใช้เมื่อผู้เล่นได้รับไอเทมจากการสำรวจหรือ AI มอบให้
    - **Smart Mapping**: ระบบจะค้นหาไอเทมใน `items` โดยใช้หลักการ Fuzzy Search (คำแรกของชื่อ)
    - **Persistence**: บันทึกจำนวน (Quantity) อัตโนมัติ หากมีไอเทมซ้ำจะทำการบวกจำนวนเพิ่มแทนการสร้างแถวใหม่

    ### 4. HEALTH_UPDATE (Upcoming)
    ใช้ในการคำนวณความเสียหายหรือการรักษา
    - **Payload**: `{ amount: number, type: 'DAMAGE' | 'HEAL' }`

    ---

    ## 🛡️ ระบบความปลอดภัยและเสถียรภาพ (Robustness)

    - **Item Orphan Protection**: ป้องกันการแครชของหน้า Inventory เมื่อพบไอเทมที่ไม่มีชื่อใน Master Data
    - **Sync Latency Handling**: มีการหน่วงเวลา 500ms ก่อน Re-sync เพื่อความแม่นยำของข้อมูลจาก Database
    - **Supabase Realtime Sync**: ระบบจะทำการ Sync ข้อมูลอัตโนมัติเมื่อมีการเรียกใช้ `processGameAction`

=== "English"

    This page compiles descriptions of `GameAction` used to control the game state via the AI Chat system and RPG UI.

    ---

    ## 🛠️ GameAction Specs

    The system uses `GameAction` to receive data from AI (Tools) or UI to update the `GameContext`.

    ### 1. ZODIAC_SET
    Used at the start of the game to specify the zodiac and initial state.
    - **Payload**: `ZodiacTrait` object
    - **Database**: Updates the `player_save_data` table in the `zodiac_json` column.

    ### 2. STATS_UPDATE
    Used when a character levels up or is trained.
    - **Payload**: `Partial<Stats>` (supports both the old set str/dex and the new set stk/nit).
    - **Logic**: The system has a **Stats Mapping Interpreter** in `GameContext` to automatically convert status values from AI (Legacy) to match columns in Supabase (New RPG).

    ### 3. ITEM_ADD (Integrated)
    Used when a player receives an item from exploration or given by AI.
    - **Smart Mapping**: The system searches for items in `items` using Fuzzy Search (first word of the name).
    - **Persistence**: Automatically records quantity. If there are duplicate items, it will add to the quantity instead of creating a new row.

    ### 4. HEALTH_UPDATE (Upcoming)
    Used for calculating damage or healing.
    - **Payload**: `{ amount: number, type: 'DAMAGE' | 'HEAL' }`

    ---

    ## 🛡️ Robustness

    - **Item Orphan Protection**: Prevents the Inventory page from crashing when an item without a name is found in Master Data.
    - **Sync Latency Handling**: There is a 500ms delay before Re-sync for data accuracy from the Database.
    - **Supabase Realtime Sync**: The system automatically syncs data when `processGameAction` is called.

*Last Updated: 2025-12-22*
