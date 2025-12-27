# โครงสร้างฐานข้อมูล / Database Schema (Master Reference)

=== "ภาษาไทย (Thai)"

    หน้านี้คือโครงสร้างฐานข้อมูล (Single Source of Truth) ของ Cosmic Narrative Game เพื่อใช้ในการพัฒนาระบบ Sync และ AI Tools

    ---

    ## 🎒 ระบบไอเทม (Inventory & Items)

    ### `items` (Master Data)
    ตารางเก็บข้อมูลไอเทมต้นแบบที่ห้ามผู้เล่นแก้ไขทั่วไป
    - **คอลัมน์**: `id` (UUID), `name`, `slug`, `type` (Weapon, Consumable, Quest), `base_stats` (JSONB), `rarity`, `image_url`

    ---

    ## 👾 ระบบมอนสเตอร์ (Monster System)

    ### `monsters_master`
    ตารางเก็บข้อมูลมอนสเตอร์ที่เป็นศัตรูในเกมและเป้าหมายเควสต์
    - **คอลัมน์สำคัญ**: `name`, `slug`, `level`, `hp`, `atk`, `def`, `exp_reward`, `money_reward`, `location_id`

    ### `player_items` (User Instances)
    ตารางเก็บไอเทมที่ผู้เล่นแต่ละคนเป็นเจ้าของ
    - **คอลัมน์**: `user_id` (FK), `item_id` (FK), `enhancement_level` (Int), `is_equipped` (Bool), `slot` (Head, Body, Weapon)

    ---

    ## 👤 ข้อมูลผู้เล่น (Player Save Data)

    ตารางหลักที่เก็บสถานะและความคืบหน้าของผู้เล่น

    | คอลัมน์                 | คำอธิบาย                                      |
    | :-------------------- | :------------------------------------------ |
    | `user_id`             | PK เชื่อมต่อกับ auth.users                      |
    | `nickname`            | ชื่อที่ผู้เล่นใช้ในเกม                              |
    | `level`               | ระดับปัจจุบัน                                   |
    | `hp_current / hp_max` | ค่าพลังชีวิต                                    |
    | `money`               | สกุลเงิน Astra                                |
    | `stk, vit, nit`       | ค่าพลังหลัก (Strength, Vitality, Intelligence) |
    | `tapa, soul, holy`    | ค่าพลังมหาจักรวาล (Energy, Spirit, Divinity)   |
    | `meditation`          | ค่าพลังสมาธิ (Luck/Concentration)              |
    | `zodiac_json`         | ข้อมูลราศีและคุณสมบัติเริ่มต้น                       |

    ---

    ## 🐾 ระบบสัตว์เลี้ยง (Pet System)

    ### `pets_master`
    ข้อมูลต้นแบบสัตว์เลี้ยง เช่น "เมฆา (Aries)", "นันทิ (Taurus)"
    - **ฟิลด์**: `name`, `element`, `base_buffs` (JSONB)

    ### `player_pets`
    Instance ของสัตว์เลี้ยงที่ผู้เล่นครอบครอง
    - **ฟิลด์**: `is_active` (ตัวที่ติดตามอยู่), `friendship_level`, `memory_json` (ความจำจาก AI)

    ---

    ## 🃏 ระบบการ์ด (Card System)

    - **`cards_master`**: แม่แบบพลังจักรวาล
    - **`player_cards`**: การ์ดที่สะสมและสวมใส่ (Equipped)

    ---

    ## 🎭 ระบบเนื้อเรื่อง (Narrative System)

    ### `narrative_scenes`
    ฐานข้อมูลสำหรับคัทซีนและบทสนทนาแบบก้าวหน้า
    - **คอลัมน์สำคัญ**: `scene_slug`, `content_json` (บทพูด), `choices_json` (ทางเลือก), `action_type`, `conditions_json` (เงื่อนไขเควสต์), `rewards_json` (รางวัล), `speaker_avatar`

    ### `npcs_master`
    ตารางเก็บข้อมูล NPC ทั้งหมดในจักรวาล
    - **คอลัมน์สำคัญ**: `name`, `title`, `map_id`, `dialogue_json`, `position_x`, `position_y` (พิกัดการวางตัวละคร 0-100%)

    ---

    !!! danger "คำเตือนสำหรับการพัฒนา"
        การอัพเดทตารางที่มีคำว่า `player_` นำหน้า ต้องเช็ค `user_id` เสมอและมีการตรวจสอบผ่าน RLS เพื่อป้องกันข้อมูลรั่วไหลระหว่างผู้เล่น

=== "English"

    This page serves as the Database Structure (Single Source of Truth) for the Cosmic Narrative Game, used for developing synchronization systems and AI Tools.

    ---

    ## 🎒 Inventory & Items System

    ### `items` (Master Data)
    Table for storing item templates that players cannot generally modify.
    - **Columns**: `id` (UUID), `name` (String), `type` (Weapon, Consumable, etc.), `base_stats` (JSONB), `rarity` (Common-Legendary), `image_url` (Text)

    ### `player_items` (User Instances)
    Table for items owned by each player.
    - **Columns**: `user_id` (FK), `item_id` (FK), `enhancement_level` (Int), `is_equipped` (Bool), `slot` (Head, Body, Weapon)

    ---

    ## 👤 Player Save Data

    The main table storing player status and progress.

    | Column                | Description                                   |
    | :-------------------- | :-------------------------------------------- |
    | `user_id`             | PK linked to auth.users                       |
    | `nickname`            | The name the player uses in-game              |
    | `level`               | Current level                                 |
    | `hp_current / hp_max` | Health points                                 |
    | `money`               | Astra currency                                |
    | `stk, vit, nit`       | core stats (Strength, Vitality, Intelligence) |
    | `tapa, soul, holy`    | Cosmic powers (Energy, Spirit, Divinity)      |
    | `meditation`          | Meditation power (Luck/Concentration)         |
    | `zodiac_json`         | Zodiac information and starting traits        |

    ---

    ## 🐾 Pet System

    ### `pets_master`
    Pet templates like "Megha (Aries)", "Nandhi (Taurus)".
    - **Fields**: `name`, `element`, `base_buffs` (JSONB)

    ### `player_pets`
    Instances of pets owned by players.
    - **Fields**: `is_active` (currently following), `friendship_level`, `memory_json` (memories from AI)

    ---

    ## 🃏 Card System

    - **`cards_master`**: Cosmic power templates.
    - **`player_cards`**: Collected and equipped cards.

    ---

    ## 🎭 Narrative System

    ### `narrative_scenes`
    Database for cutscenes and progressive dialogue.
    - **Key Columns**: `scene_slug`, `content_json` (dialogue), `choices_json` (choices), `action_type`, `next_scene_slug`

    ---

    !!! danger "Development Warning"
        When updating tables prefixed with `player_`, you must always check the `user_id` and ensure RLS policies are in place to prevent data leakage between players.

*Last Updated: 2025-12-22*
