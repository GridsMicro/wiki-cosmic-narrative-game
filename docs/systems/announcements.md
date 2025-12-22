# ระบบประกาศ / Announcement System

=== "ภาษาไทย (Thai)"

    ## 🌎 ภาพรวม
    ระบบประกาศ (Announcement System) ถูกออกแบบมาเพื่อสื่อสารกับผู้เล่นในเกม โดยสามารถกำหนดความสำคัญ วันเวลาที่จะแสดงผล และรูปแบบการแสดงผล (เช่น Popup หรือ Banner) ได้ผ่าน DevTools

    ---

    ## 🏗️ โครงสร้างฐานข้อมูล (Database Schema)

    ระบบใช้ตาราง `announcements` ในการเก็บข้อมูล:

    | ฟิลด์                     | ประเภท        | คำอธิบาย                                         |
    | :---------------------- | :------------ | :--------------------------------------------- |
    | `id`                    | `UUID`        | คีย์หลัก (Primary Key)                            |
    | `title`                 | `TEXT`        | หัวข้อข่าว                                        |
    | `message`               | `TEXT`        | เนื้อหาข่าว                                       |
    | `type`                  | `TEXT`        | ประเภท (`info`, `warning`, `success`, `event`) |
    | `priority`              | `INTEGER`     | ความสำคัญ (0=ปกติ, 1=สำคัญ, 2=เร่งด่วน)               |
    | `start_time`            | `TIMESTAMPTZ` | เริ่มแสดงผล                                      |
    | `end_time`              | `TIMESTAMPTZ` | สิ้นสุดการแสดงผล (null = ตลอดไป)                  |
    | `is_recurring`          | `BOOLEAN`     | แสดงซ้ำหรือไม่                                     |
    | `repeat_interval_hours` | `INTEGER`     | ระยะเวลาในการแสดงซ้ำ (ชม.)                       |
    | `is_active`             | `BOOLEAN`     | สถานะการใช้งาน                                  |
    | `show_on_login`         | `BOOLEAN`     | แสดงทันทีเมื่อเข้าสู่ระบบ                             |
    | `show_as_popup`         | `BOOLEAN`     | แสดงผลเป็น Popup                                |

    ---

    ## 🛠️ การใช้งานผ่าน DevTools

    คุณสามารถจัดการประกาศได้ที่เมนู **Announcements** ใน DevTools:

    1. **Create Entity**: คลิกปุ่มเพื่อสร้างประกาศใหม่
    2. **Form Fields**:
       - **Scheduling**: กำหนดวันเวลาที่ต้องการให้ข่าวเริ่มและจบ
       - **Recurring**: หากต้องการให้แสดงซ้ำ (เช่น ข่าว Maintenance รายสัปดาห์) ให้ติ๊ก `Is Recurring` และใส่จำนวนชั่วโมง
       - **Display Settings**: เลือก `Show as Popup` หากต้องการให้เด้งขึ้นมากลางจอ
    3. **Save**: คลิก "Commit Changes" เพื่อบันทึกลง Database

    ---

    ## 💻 การเชื่อมต่อกับ Frontend

    ใช้ฟังก์ชัน `get_active_announcements()` ใน Supabase เพื่อดึงข้อมูลข่าวสารปัจจุบัน:

    ```sql
    -- ตัวอย่างการดึงข้อมูลจาก SQL Editor
    SELECT * FROM get_active_announcements();
    ```

    ใน React Component สามารถดึงข้อมูลได้ผ่าน:

    ```typescript
    const { data, error } = await supabase
      .from('announcements')
      .select('*')
      .eq('is_active', true)
      .lte('start_time', new Date().toISOString())
      .or(`end_time.is.null,end_time.gte.${new Date().toISOString()}`);
    ```

=== "English"

    ## 🌎 Overview
    The Announcement System is designed to communicate with players in-game. You can define priority, display timing, and display formats (e.g., Popup or Banner) via DevTools.

    ---

    ## 🏗️ Database Schema

    The system uses the `announcements` table to store information:

    | Field                   | Type          | Description                                  |
    | :---------------------- | :------------ | :------------------------------------------- |
    | `id`                    | `UUID`        | Primary Key                                  |
    | `title`                 | `TEXT`        | Announcement title                           |
    | `message`               | `TEXT`        | Announcement content                         |
    | `type`                  | `TEXT`        | Type (`info`, `warning`, `success`, `event`) |
    | `priority`              | `INTEGER`     | Priority (0=normal, 1=important, 2=urgent)   |
    | `start_time`            | `TIMESTAMPTZ` | Display start time                           |
    | `end_time`              | `TIMESTAMPTZ` | Display end time (null = forever)            |
    | `is_recurring`          | `BOOLEAN`     | Whether to repeat the announcement           |
    | `repeat_interval_hours` | `INTEGER`     | Repeat interval (in hours)                   |
    | `is_active`             | `BOOLEAN`     | Usage status                                 |
    | `show_on_login`         | `BOOLEAN`     | Show immediately on login                    |
    | `show_as_popup`         | `BOOLEAN`     | Show as a Popup                              |

    ---

    ## 🛠️ DevTools Usage

    You can manage announcements in the **Announcements** menu in DevTools:

    1. **Create Entity**: Click the button to create a new announcement
    2. **Form Fields**:
       - **Scheduling**: Define the start and end times for the news
       - **Recurring**: If you want it to repeat (e.g., weekly maintenance news), check `Is Recurring` and enter the number of hours
       - **Display Settings**: Select `Show as Popup` if you want it to pop up in the middle of the screen
    3. **Save**: Click "Commit Changes" to save to the database

    ---

    ## 💻 Frontend Integration

    Use the `get_active_announcements()` function in Supabase to fetch current active announcements:

    ```sql
    -- Example of fetching data from SQL Editor
    SELECT * FROM get_active_announcements();
    ```

    In a React Component, you can fetch data via:

    ```typescript
    const { data, error } = await supabase
      .from('announcements')
      .select('*')
      .eq('is_active', true)
      .lte('start_time', new Date().toISOString())
      .or(`end_time.is.null,end_time.gte.${new Date().toISOString()}`);
    ```

*Last Updated: 2025-12-22*
