# 🎨 3D Prompt Explorer

คู่มือการใช้ AI เจนเนอเรตภาพแผนที่และสถานที่ในมุมมอง 3D Isometric (45 องศา) สำหรับโปรเจค Cosmic Narrative Game

---

## 🏛️ ชุดคำสั่งสำหรับเมืองหลัก (City Prompts)

ด้านล่างนี้คือ Prompts ที่ออกแบบมาเพื่อสร้างภาพแผนที่ที่มีความสม่ำเสมอในเชิงศิลปะ (Artistic Consistency)

### 1. เอเธลเรีย (Atheleria)
**แนวคิด**: มหานครสีขาวมุกเน้นความบริสุทธิ์และสติ

> **Prompt**: `Isometric 3D game map tile, 45-degree tilted perspective, Atheleria sky temple, tiered white marble courtyards with visible vertical walls, golden Thai-style gables, central celestial fountain with flowing star water, floating in a white sea of clouds, star-shaped floor tiles, soft cinematic lighting, high-angle 3D orthographic render, clean white and gold palette.`

---

### 2. ธัมมิกนารา (Dhammik-Nara)
**แนวคิด**: เมืองโบราณลอยฟ้าที่มีหอสมุดศิลาเป็นศูนย์กลาง

> **Prompt**: `Isometric 3D game asset, 45-degree perspective, ancient Sukhothai ruins on floating stone platforms, visible vertical stone layers, central golden library pavilion with detailed side columns, surrounded by layered lotus ponds, glowing Thai Pali scripts floating in 3D space, warm golden sunbeams, high-angle miniature style, detailed mossy stone textures.`

---

### 3. วิริยันตรา (Viriyantra)
**แนวคิด**: ปราสาทหินทรายบนยอดภูเขาไฟ

> **Prompt**: `Isometric 3D map tile, 45-degree perspective, red sandstone Khmer-style fortress on a dormant volcano crater, visible high stairs and steep walls, lava channels flowing through rock crevices with depth, obsidian stone foundations, intense solar flare particles, rugged rocky terrain, dramatic side-lighting, high-angle fantasy RTS map style.`

---

### 4. ปีติสวรรค์ (Pitis-Vana)
**แนวคิด**: เมืองท่าเหนือน้ำและป่าหิมพานต์ที่มีพืชเรืองแสง

> **Prompt**: `Isometric 3D game environment, 45-degree tilted view, tropical coastal paradise, multi-level Thai wooden pavilions built on cliffside and water stilts, visible coral reefs deep below transparent emerald water, glowing Himmapan trees with 3D fruits, vibrant cyan and purple bioluminescence, luxury resort aesthetic, high-angle clean render.`

---

### 5. ปัสสัทธานนท์ (Passadhon)
**แนวคิด**: วิหารกลางป่าสนและม่านหมอก สไตล์ล้านนา

> **Prompt**: `Isometric 3D map tile, 45-degree tilted perspective, Lanna-style temple complex inside a dense 3D pine forest, layered misty valleys with visible depth, golden teakwood roofs, floating lanterns at different heights, soft blue cosmic moonlight, forest paths forming a grid, miniature diorama style, high-angle orthographic view.`

---

### 6. สมาธินทร์ (Samadhindra)
**แนวคิด**: เจดีย์ทองคำยักษ์กลางอวกาศและวงแหวนพลังงาน

> **Prompt**: `Isometric 3D celestial object, 45-degree perspective, giant golden stupa (Phra Pathom Chedi style) floating in deep cosmos, concentric rings of golden aura with visible thickness, radiating white energy lines forming a geometric grid, dark cosmic void background, perfect 3D symmetry, high-angle spiritual game map, glowing metallic gold texture.`

---

### 7. อุเบกขามณฑล (Ubekkha-Mandala)
**แนวคิด**: วิหารกระจกบนจุดสูงสุด สะท้อนแสงรุ่งอรุณแห่งจักรวาล

> **Prompt**: `Isometric 3D final stage map, 45-degree tilted view, highest mountain sanctuary, infinite mirror floor reflecting a radiant amber and gold cosmic dawn, symmetric crystal stairs with height depth leading to a central altar, above cloud layers, glowing atmosphere, cosmic surrealism, divine high-angle 3D perspective.`

---

## 🛠️ เทคนิคการเขียน Prompt (Best Practices)

เพื่อให้ได้ผลลัพธ์ที่เป็นสไตล์ 3D Isometric ที่สมบูรณ์แบบ ควรมีองค์ประกอบดังนี้:

1.  **Perspective**: ต้องระบุ `Isometric`, `45-degree`, หรือ `Orthographic perspective` เสมอ
2.  **Angle**: ใช้ `High-angle view` เพื่อให้เห็นมิติความลึก (Depth)
3.  **Lighting**: ระบุทิศทางแสง เช่น `Side-lighting` หรือ `Cinematic lighting` เพื่อเพิ่มเงา (Shadow) ให้กับวัตถุ 3D
4.  **Keywords สำหรับสไตล์**:
    -   `Miniature diorama style` (ทำให้ดูเหมือนของจำลอง)
    -   `Clean render` (ลดนอยซ์ของภาพ)
    -   `Game asset container` (ถ้าต้องการให้พื้นหลังโปร่งใส)

---

## 📊 องค์ประกอบทางภาพ (Visual Analysis)

ในการเจนเนอเรตภาพพยายามบาลานซ์ 5 องค์ประกอบนี้:

- **ความสูง (Height)**: เลเยอร์ของวัตถุ
- **แสงสว่าง (Lighting)**: แสงที่สื่อถึงพลังงาน (Solar/Lunar)
- **ความซับซ้อน (Complexity)**: รายละเอียดของสถาปัตยกรรมไทย
- **ออร่า (Aura)**: เอฟเฟกต์แสงรอบๆ วัตถุ
- **พื้นผิว (Texture)**: วัสดุ เช่น ไม้สัก, หินทราย, ทองคำ

!!! info "AI ที่แนะนำ"
    ชุดคำสั่งเหล่านี้ทดสอบแล้วว่าทำงานได้ดีเยี่ยมกับ **Midjourney v6**, **DALL-E 3**, และ **Stable Diffusion (SDXL)**
