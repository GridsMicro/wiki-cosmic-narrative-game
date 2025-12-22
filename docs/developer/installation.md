# การติดตั้งและเริ่มต้นโปรเจกต์ / Installation & Getting Started

=== "ภาษาไทย (Thai)"

    ## 📋 ข้อกำหนดเบื้องต้น

    ### ข้อกำหนดด้านซอฟต์แวร์ (Software Requirements)
    - **Node.js**: 18.x หรือสูงกว่า
    - **npm** หรือ **pnpm**: ตัวจัดการแพ็คเกจ (Package manager)
    - **Git**: สำหรับการควบคุมเวอร์ชัน (Version control)
    - **Supabase Account**: สำหรับฐานข้อมูลและการยืนยันตัวตน (Database และ Authentication)

    ### ข้อกำหนดด้านความรู้ (Knowledge Requirements)
    - TypeScript / JavaScript
    - React และ Next.js (App Router)
    - Tailwind CSS
    - Supabase (PostgreSQL, Row Level Security)

    ---

    ## 🚀 การติดตั้ง

    ### 1. Clone Repository
    ```bash
    git clone https://github.com/GridsMicro/cosmic-narrative-game.git
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
        **ห้าม** commit ไฟล์ `.env.local` ขึ้น Git! ตรวจสอบให้แน่ใจว่าได้ระบุไว้ใน `.gitignore`

    ---

    ## 🗄️ ตั้งค่า Database (Supabase)

    ### 1. สร้าง Supabase Project
    1. ไปที่ [supabase.com](https://supabase.com)
    2. สร้าง Project ใหม่
    3. คัดลอก URL และ Anon Key มาใส่ใน `.env.local`

    ### 2. รัน SQL Schema
    ไปที่ **SQL Editor** ใน Supabase Dashboard และรันไฟล์ SQL ตามลำดับ (ดูในโฟลเดอร์ `docs` ของโปรเจกต์)

    ---

    ## 🎮 รันโปรเจกต์

    ### โหมดพัฒนา (Development Mode)
    ```bash
    npm run dev
    ```
    เปิดเบราว์เซอร์ที่ `http://localhost:3000`

    ### โหมด Production
    ```bash
    npm run build
    npm start
    ```

=== "English"

    ## 📋 Prerequisites

    ### Software Requirements
    - **Node.js**: 18.x or higher
    - **npm** or **pnpm**: Package manager
    - **Git**: For version control
    - **Supabase Account**: For database and authentication

    ### Knowledge Requirements
    - TypeScript / JavaScript
    - React and Next.js (App Router)
    - Tailwind CSS
    - Supabase (PostgreSQL, Row Level Security)

    ---

    ## 🚀 Installation

    ### 1. Clone Repository
    ```bash
    git clone https://github.com/GridsMicro/cosmic-narrative-game.git
    cd cosmic-narrative-game
    ```

    ### 2. Install Dependencies
    ```bash
    npm install
    # or
    pnpm install
    ```

    ### 3. Set Environment Variables
    Create a `.env.local` file in the root folder:
    ```env
    # Supabase
    NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
    NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

    # Google Gemini AI (For Chat System)
    GOOGLE_GENERATIVE_AI_API_KEY=your_gemini_api_key

    # Optional: Stripe (For Payment System - if any)
    NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your_stripe_key
    STRIPE_SECRET_KEY=your_stripe_secret
    ```

    !!! warning "Security"
        **Do not** commit the `.env.local` file to Git! Ensure it is included in your `.gitignore`.

    ---

    ## 🗄️ Database Setup (Supabase)

    ### 1. Create Supabase Project
    1. Go to [supabase.com](https://supabase.com)
    2. Create a new project.
    3. Copy the URL and Anon Key into your `.env.local` file.

    ### 2. Run SQL Schema
    Go to the **SQL Editor** in the Supabase Dashboard and run the SQL files in order (refer to the `docs` folder in the project).

    ---

    ## 🎮 Running the Project

    ### Development Mode
    ```bash
    npm run dev
    ```
    Open your browser at `http://localhost:3000`.

    ### Production Mode
    ```bash
    npm run build
    npm start
    ```

*Last Updated: 2025-12-22*
