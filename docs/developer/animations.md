# Animation System Guide

## 📖 ภาพรวม

เอกสารนี้อธิบายระบบ Animation ที่ใช้ใน Cosmic Narrative Game รวมถึงรูปแบบไฟล์ที่แนะนำ วิธีการใช้งาน และ best practices

---

## 🎬 รูปแบบ Animation ที่รองรับ

### 1. **WebP Animation** ⭐ (แนะนำสุด)

#### ข้อดี
- ✅ ขนาดไฟล์เล็กกว่า GIF **25-35%**
- ✅ คุณภาพดีกว่า GIF
- ✅ รองรับ transparency แบบ alpha channel
- ✅ รองรับใน browser สมัยใหม่ทั้งหมด (Chrome, Firefox, Edge, Safari 14+)
- ✅ สร้างง่ายจาก GIF หรือ video

#### วิธีสร้างไฟล์ WebP

**จาก GIF:**
```bash
ffmpeg -i input.gif -c:v libwebp -quality 80 -loop 0 output.webp
```

**จาก Video (MP4):**
```bash
ffmpeg -i input.mp4 -vcodec libwebp -loop 0 -quality 80 -preset default output.webp
```

**จาก PNG Sequence:**
```bash
ffmpeg -framerate 24 -i frame_%04d.png -c:v libwebp -quality 80 -loop 0 output.webp
```

#### การใช้งานในโค้ด

**HTML/React:**
```tsx
<img src="/animations/character-walk.webp" alt="Character Walking" />
```

**Next.js Image Component:**
```tsx
import Image from 'next/image'

<Image 
  src="/animations/character-walk.webp" 
  alt="Character Walking"
  width={128}
  height={128}
  unoptimized // สำหรับ animated WebP
/>
```

#### แนะนำสำหรับ
- Character sprites
- Skill effects
- UI animations
- Icon animations

---

### 2. **Lottie (JSON Animation)** 🎨

#### ข้อดี
- ✅ ขนาดไฟล์**เล็กมาก** (เป็น JSON)
- ✅ Vector-based - ปรับขนาดได้ไม่เสียคุณภาพ
- ✅ ควบคุม animation ได้ (play, pause, speed, direction)
- ✅ Interactive - ตอบสนองต่อ user events
- ✅ สร้างจาก After Effects ได้

#### การติดตั้ง

```bash
npm install lottie-react
```

#### การใช้งานในโค้ด

**Basic Usage:**
```tsx
import Lottie from 'lottie-react'
import animationData from './animations/skill-effect.json'

export function SkillEffect() {
  return (
    <Lottie 
      animationData={animationData} 
      loop={true}
      autoplay={true}
      style={{ width: 200, height: 200 }}
    />
  )
}
```

**Advanced Control:**
```tsx
import Lottie from 'lottie-react'
import { useRef } from 'react'
import animationData from './animations/skill-effect.json'

export function ControlledAnimation() {
  const lottieRef = useRef()

  const handlePlay = () => {
    lottieRef.current?.play()
  }

  const handlePause = () => {
    lottieRef.current?.pause()
  }

  return (
    <div>
      <Lottie 
        lottieRef={lottieRef}
        animationData={animationData} 
        loop={false}
        autoplay={false}
      />
      <button onClick={handlePlay}>Play</button>
      <button onClick={handlePause}>Pause</button>
    </div>
  )
}
```

#### วิธีสร้างไฟล์ Lottie

1. **จาก After Effects:**
   - ติดตั้ง [Bodymovin plugin](https://aescripts.com/bodymovin/)
   - Export animation เป็น JSON

2. **จาก LottieFiles:**
   - ดาวน์โหลดจาก [LottieFiles.com](https://lottiefiles.com/)
   - แก้ไขด้วย [Lottie Editor](https://lottiefiles.com/editor)

3. **จาก SVG:**
   - ใช้ [SVGator](https://www.svgator.com/) แล้ว export เป็น Lottie

#### แนะนำสำหรับ
- UI effects (loading, success, error)
- Skill/Magic effects (vector-based)
- Icon animations
- Decorative elements

---

### 3. **CSS Sprite Sheet** 🎞️

#### ข้อดี
- ✅ Performance ดีมาก (ใช้ CSS animation)
- ✅ ควบคุมได้ง่าย
- ✅ เหมาะกับ pixel art และ game sprites
- ✅ ไม่ต้องใช้ library เพิ่มเติม

#### โครงสร้างไฟล์

Sprite sheet คือรูปภาพเดียวที่มี frames ทั้งหมดเรียงกัน:

```
[Frame 1][Frame 2][Frame 3][Frame 4][Frame 5][Frame 6][Frame 7][Frame 8]
```

#### การใช้งานในโค้ด

**CSS:**
```css
.character-walk {
  width: 64px;
  height: 64px;
  background-image: url('/sprites/character-walk.png');
  background-repeat: no-repeat;
  animation: walk 0.8s steps(8) infinite;
}

@keyframes walk {
  from { background-position: 0 0; }
  to { background-position: -512px 0; } /* 64px * 8 frames */
}
```

**React Component:**
```tsx
export function CharacterSprite({ animation = 'idle' }) {
  return (
    <div 
      className={`sprite sprite-${animation}`}
      style={{
        width: 64,
        height: 64,
        backgroundImage: `url(/sprites/character-${animation}.png)`,
      }}
    />
  )
}
```

**Advanced with Framer Motion:**
```tsx
import { motion } from 'framer-motion'

export function AnimatedSprite({ frames = 8, duration = 0.8 }) {
  return (
    <motion.div
      className="sprite"
      animate={{
        backgroundPosition: ['0px 0px', `-${64 * frames}px 0px`],
      }}
      transition={{
        duration,
        repeat: Infinity,
        ease: 'steps(' + frames + ')',
      }}
    />
  )
}
```

#### วิธีสร้าง Sprite Sheet

**จาก PNG Sequence:**
```bash
# ใช้ ImageMagick
convert frame_*.png +append sprite-sheet.png
```

**จาก Video:**
```bash
# Extract frames
ffmpeg -i input.mp4 -vf fps=24 frame_%04d.png

# Combine to sprite sheet (ใช้ tool เช่น TexturePacker)
```

#### แนะนำสำหรับ
- Character movement (walk, run, attack)
- Pixel art animations
- Retro-style effects

---

### 4. **APNG (Animated PNG)** 📸

#### ข้อดี
- ✅ รองรับ transparency เต็มรูปแบบ (alpha channel)
- ✅ คุณภาพดีกว่า GIF
- ✅ ไม่ต้องใช้ library (ใช้ `<img>` tag ธรรมดา)

#### ข้อเสีย
- ⚠️ ขนาดไฟล์ใหญ่กว่า WebP
- ⚠️ รองรับน้อยกว่า WebP (Safari, Firefox, Chrome 59+)

#### วิธีสร้างไฟล์ APNG

```bash
# จาก PNG sequence
apngasm output.png frame_*.png 1 24 # 24 fps
```

#### การใช้งาน

```tsx
<img src="/animations/effect.apng" alt="Effect" />
```

#### แนะนำสำหรับ
- Effects ที่ต้องการ transparency สูง
- กรณีที่ไม่สามารถใช้ WebP ได้

---

### 5. **Video (MP4/WebM)** 🎥

#### ข้อดี
- ✅ คุณภาพสูงสุด
- ✅ ขนาดไฟล์เล็ก (ด้วย modern codecs)
- ✅ รองรับ transparency (WebM with VP9)
- ✅ เหมาะกับ animation ซับซ้อน

#### ข้อเสีย
- ⚠️ ใช้ทรัพยากรมากกว่า
- ⚠️ ไม่เหมาะกับ small sprites

#### วิธีสร้างไฟล์

**WebM with transparency:**
```bash
ffmpeg -i input.mov -c:v libvpx-vp9 -pix_fmt yuva420p -auto-alt-ref 0 output.webm
```

**MP4 (fallback):**
```bash
ffmpeg -i input.mov -c:v libx264 -pix_fmt yuv420p -crf 23 output.mp4
```

#### การใช้งานในโค้ด

```tsx
export function VideoAnimation({ src, className = '' }) {
  return (
    <video 
      autoPlay 
      loop 
      muted 
      playsInline
      className={className}
    >
      <source src={`${src}.webm`} type="video/webm" />
      <source src={`${src}.mp4`} type="video/mp4" />
    </video>
  )
}
```

**With React state control:**
```tsx
import { useRef } from 'react'

export function ControlledVideo({ src }) {
  const videoRef = useRef<HTMLVideoElement>(null)

  const play = () => videoRef.current?.play()
  const pause = () => videoRef.current?.pause()

  return (
    <div>
      <video ref={videoRef} loop muted playsInline>
        <source src={src} type="video/webm" />
      </video>
      <button onClick={play}>Play</button>
      <button onClick={pause}>Pause</button>
    </div>
  )
}
```

#### แนะนำสำหรับ
- Background animations
- Cinematic effects
- Full-screen cutscenes

---

## 🎯 คำแนะนำตามกรณีใช้งาน

| ประเภท Animation         | รูปแบบที่แนะนำ          | เหตุผล                   |
| ------------------------ | ------------------- | ----------------------- |
| **Character Sprites**    | WebP / Sprite Sheet | เล็ก, เร็ว, performance ดี |
| **Skill Effects**        | Lottie / WebP       | ปรับขนาดได้, สวยงาม       |
| **UI Elements**          | Lottie              | Vector, ควบคุมได้ง่าย      |
| **Background Animation** | Video (WebM)        | คุณภาพสูง, smooth         |
| **Icon Animation**       | Lottie / WebP       | เล็ก, responsive         |
| **Pixel Art**            | Sprite Sheet        | Performance ดีสุด         |
| **Loading Indicators**   | Lottie              | เล็ก, สวยงาม             |
| **Particle Effects**     | WebP / Lottie       | ขึ้นกับความซับซ้อน           |

---

## 📁 โครงสร้างไฟล์แนะนำ

```
public/
├── animations/
│   ├── characters/
│   │   ├── hero-walk.webp
│   │   ├── hero-attack.webp
│   │   └── hero-idle.webp
│   ├── skills/
│   │   ├── fireball.json (Lottie)
│   │   ├── heal.json
│   │   └── shield.webp
│   ├── ui/
│   │   ├── loading.json
│   │   ├── success.json
│   │   └── error.json
│   └── backgrounds/
│       ├── stars.webm
│       └── clouds.webm
├── sprites/
│   ├── character-walk.png (sprite sheet)
│   ├── character-attack.png
│   └── enemies.png
```

---

## ⚡ Performance Best Practices

### 1. **ขนาดไฟล์**
- WebP: ใช้ quality 70-85 (balance ระหว่างขนาดและคุณภาพ)
- Lottie: ลด complexity ของ shapes และ layers
- Video: ใช้ CRF 23-28 สำหรับ MP4

### 2. **Lazy Loading**
```tsx
import dynamic from 'next/dynamic'

const HeavyAnimation = dynamic(() => import('./HeavyAnimation'), {
  loading: () => <div>Loading...</div>,
  ssr: false
})
```

### 3. **Preloading**
```tsx
// สำหรับ animation ที่ต้องใช้ทันที
<link rel="preload" as="image" href="/animations/critical.webp" />
```

### 4. **Conditional Loading**
```tsx
// โหลดเฉพาะเมื่อจำเป็น
const [showAnimation, setShowAnimation] = useState(false)

{showAnimation && <Lottie animationData={data} />}
```

---

## 🛠️ Tools แนะนำ

### สร้าง/แปลงไฟล์
- **FFmpeg**: แปลง video/GIF เป็น WebP, MP4, WebM
- **ImageMagick**: สร้าง sprite sheets
- **apngasm**: สร้าง APNG
- **TexturePacker**: สร้าง sprite sheets แบบ professional

### สร้าง Animation
- **After Effects + Bodymovin**: สร้าง Lottie
- **LottieFiles**: แก้ไขและดาวน์โหลด Lottie
- **Aseprite**: สร้าง pixel art animations
- **Spine**: สร้าง 2D skeletal animations

### Optimization
- **Squoosh**: optimize รูปภาพ (รองรับ WebP)
- **HandBrake**: compress video
- **TinyPNG**: compress PNG

---

## 📊 ตารางเปรียบเทียบ

| Format     | ขนาดไฟล์ | คุณภาพ | Transparency | Browser Support | Use Case     |
| ---------- | ------- | ----- | ------------ | --------------- | ------------ |
| **GIF**    | ⭐⭐      | ⭐⭐    | ⭐⭐           | ⭐⭐⭐⭐⭐           | Legacy       |
| **WebP**   | ⭐⭐⭐⭐⭐   | ⭐⭐⭐⭐  | ⭐⭐⭐⭐⭐        | ⭐⭐⭐⭐            | **แนะนำสุด**   |
| **Lottie** | ⭐⭐⭐⭐⭐   | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐        | ⭐⭐⭐⭐            | Vector/UI    |
| **Sprite** | ⭐⭐⭐⭐    | ⭐⭐⭐   | ⭐⭐⭐⭐         | ⭐⭐⭐⭐⭐           | Pixel Art    |
| **APNG**   | ⭐⭐⭐     | ⭐⭐⭐⭐  | ⭐⭐⭐⭐⭐        | ⭐⭐⭐             | High Quality |
| **Video**  | ⭐⭐⭐⭐    | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐         | ⭐⭐⭐⭐⭐           | Complex      |

---

## 🔗 Resources

- [WebP Documentation](https://developers.google.com/speed/webp)
- [Lottie Documentation](https://airbnb.io/lottie/)
- [LottieFiles](https://lottiefiles.com/)
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)
- [CSS Sprites Guide](https://css-tricks.com/css-sprites/)

---

## 📝 สรุป

สำหรับ **Cosmic Narrative Game** แนะนำใช้:

1. **WebP** - สำหรับ character sprites, skill effects, icons
2. **Lottie** - สำหรับ UI animations, loading indicators
3. **Sprite Sheet** - สำหรับ pixel art characters
4. **Video** - สำหรับ background animations, cutscenes

**หลีกเลี่ยง GIF** เพราะมีขนาดใหญ่และคุณภาพต่ำกว่าทางเลือกอื่นๆ
