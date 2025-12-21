# 🌌 Cosmic Narrative Game Wiki

คู่มือสมบูรณ์สำหรับเกม Cosmic Narrative Game - สร้างด้วย MkDocs และ Material Theme

## 📖 เกี่ยวกับ

Wiki นี้เป็นคู่มือครบวงจรสำหรับผู้เล่นและนักพัฒนาของเกม Cosmic Narrative Game ครอบคลุมทุกระบบในเกม ตั้งแต่การสร้างตัวละคร, ระบบการต่อสู้, ระบบการ์ด, ไปจนถึงข้อมูลโลกเกมและ API สำหรับนักพัฒนา

## 🚀 การติดตั้งและรัน

### ข้อกำหนดเบื้องต้น
- Python 3.8 ขึ้นไป
- pip

### ติดตั้ง

1. **Clone repository**
```bash
git clone https://github.com/GridsMicro/wiki-cosmic-narrative-game.git
cd wiki-cosmic-narrative-game
```

2. **สร้าง Virtual Environment**
```bash
python3 -m venv venv
```

3. **ติดตั้ง Dependencies**
```bash
./venv/bin/pip install -r requirements.txt
```

### รัน Development Server

```bash
./venv/bin/mkdocs serve
```

เปิดเบราว์เซอร์ที่ `http://127.0.0.1:8000`

## 📝 การเขียนเอกสาร

### โครงสร้างไฟล์

```
wiki-cosmic-narrative-game/
├── docs/                    # เอกสารทั้งหมด
│   ├── index.md            # หน้าแรก
│   ├── getting-started/    # คู่มือเริ่มต้น
│   ├── systems/            # ระบบเกม
│   ├── world/              # โลกเกม
│   ├── guides/             # คู่มือต่างๆ
│   └── developer/          # เอกสารสำหรับนักพัฒนา
├── mkdocs.yml              # ไฟล์ config
├── requirements.txt        # Python dependencies
└── README.md               # ไฟล์นี้
```

### การเพิ่มหน้าใหม่

1. สร้างไฟล์ `.md` ใน `docs/` หรือในโฟลเดอร์ย่อย
2. เพิ่มลิงก์ใน `mkdocs.yml` ในส่วน `nav:`

ตัวอย่าง:
```yaml
nav:
  - หน้าแรก: index.md
  - หน้าใหม่: new-page.md
```

### Markdown Extensions ที่รองรับ

Wiki นี้รองรับ Markdown extensions มากมาย:

#### Admonitions (กล่องข้อความพิเศษ)
```markdown
!!! note "หมายเหตุ"
    นี่คือข้อความในกล่อง note

!!! warning "คำเตือน"
    นี่คือข้อความเตือน

!!! tip "เคล็ดลับ"
    นี่คือเคล็ดลับ
```

#### Tabs (แท็บ)
```markdown
=== "Tab 1"
    เนื้อหาของ Tab 1

=== "Tab 2"
    เนื้อหาของ Tab 2
```

#### Code Blocks พร้อม Syntax Highlighting
```markdown
\`\`\`python
def hello():
    print("Hello, World!")
\`\`\`
```

#### Icons
```markdown
:material-heart:
:fontawesome-brands-github:
```

## 🎨 การปรับแต่ง Theme

แก้ไขไฟล์ `mkdocs.yml` ในส่วน `theme:` เพื่อปรับแต่งสี, ฟอนต์, และฟีเจอร์ต่างๆ

## 🚢 การ Deploy

### GitHub Pages

1. **สร้าง GitHub Actions Workflow**

สร้างไฟล์ `.github/workflows/deploy.yml`:

```yaml
name: Deploy MkDocs

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.x
      
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
      
      - name: Deploy to GitHub Pages
        run: |
          mkdocs gh-deploy --force
```

2. **Push ขึ้น GitHub**
```bash
git add .
git commit -m "Initial wiki setup"
git push origin main
```

3. **เปิดใช้งาน GitHub Pages**
   - ไปที่ Settings > Pages
   - เลือก Branch: `gh-pages`
   - บันทึก

Wiki จะพร้อมใช้งานที่ `https://gridsmicro.github.io/wiki-cosmic-narrative-game/`

### Manual Build

```bash
./venv/bin/mkdocs build
```

ไฟล์ที่ build แล้วจะอยู่ในโฟลเดอร์ `site/`

## 🤝 การมีส่วนร่วม

เรายินดีรับการมีส่วนร่วมจากทุกคน!

1. Fork repository
2. สร้าง branch ใหม่ (`git checkout -b feature/amazing-feature`)
3. Commit การเปลี่ยนแปลง (`git commit -m 'Add some amazing feature'`)
4. Push ไปยัง branch (`git push origin feature/amazing-feature`)
5. เปิด Pull Request

## 📄 License

โปรเจคนี้เป็น open source ภายใต้ MIT License

## 🔗 Links

- **เกมหลัก**: [cosmic-narrative-game](https://github.com/GridsMicro/cosmic-narrative-game)
- **Wiki**: [wiki-cosmic-narrative-game](https://github.com/GridsMicro/wiki-cosmic-narrative-game)
- **MkDocs**: [mkdocs.org](https://www.mkdocs.org)
- **Material for MkDocs**: [squidfunk.github.io/mkdocs-material](https://squidfunk.github.io/mkdocs-material/)

---

<div align="center">
  <p>สร้างด้วย ❤️ โดย Cosmic Narrative Game Team</p>
</div>
