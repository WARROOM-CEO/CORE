# สกิล: frontend-design

**สร้างอินเทอร์เฟซ Frontend ที่โดดเด่นและพร้อม production ด้วยคุณภาพการออกแบบสูง**

---

## สกิลนี้ทำอะไร?

สกิล `frontend-design` ช่วยให้ Claude สร้างโค้ด Frontend ที่:

- **โดดเด่นและน่าจดจำ** — หลีกเลี่ยงรูปแบบ "AI ทั่วไป" ที่ดูเหมือนกันทุกโปรเจกต์
- **พร้อม production** — โค้ดที่ใช้งานได้จริง ไม่ใช่แค่ต้นแบบ
- **มีจุดยืนด้านสุนทรียศาสตร์** — เลือก typography, สี, และ animation ที่เหมาะกับบริบท

---

## วิธีเรียกใช้

พูดหรือพิมพ์คำร้องขอเกี่ยวกับ Frontend เช่น:

- "สร้างหน้า landing page สำหรับสตาร์ทอัพ"
- "ทำ dashboard แสดงข้อมูลยอดขาย"
- "ออกแบบ component ฟอร์มลงทะเบียน"
- "สร้างเว็บพอร์ตโฟลิโอส่วนตัว"

---

## กระบวนการทำงานของ Claude

เมื่อได้รับคำร้องขอ Claude จะทำตามขั้นตอน:

### 1. วิเคราะห์บริบท

ก่อนเขียนโค้ด Claude จะทำความเข้าใจ:
- **วัตถุประสงค์** — อินเทอร์เฟซนี้แก้ปัญหาอะไร? ใครเป็นผู้ใช้?
- **โทนและสไตล์** — เลือกทิศทางสุนทรียศาสตร์ที่เหมาะสม เช่น minimalist สุดขีด, maximalist เต็มที่, retro-futuristic, luxury/ประณีต, playful/น่ารัก, editorial/นิตยสาร, brutalist/ดิบ ฯลฯ
- **ข้อจำกัดทางเทคนิค** — framework ที่ใช้, ประสิทธิภาพ, accessibility

### 2. กำหนดทิศทางการออกแบบ

Claude จะเลือกทิศทาง **ชัดเจนและกล้าหาญ** หนึ่งทิศทาง จากนั้นดำเนินการด้วยความแม่นยำ กุญแจสำคัญคือ **ความตั้งใจ** ไม่ใช่ความเข้มข้น

### 3. สร้างโค้ดที่ใช้งานได้จริง

Claude จะสร้าง HTML/CSS/JS, React, Vue หรือ framework ที่เหมาะสม โดยเน้น:

**Typography**
เลือก font ที่สวยงามและมีเอกลักษณ์ หลีกเลี่ยง Arial, Inter, Roboto จับคู่ display font โดดเด่นกับ body font ที่ประณีต

**สีและธีม**
ยึดมั่นกับสุนทรียศาสตร์ที่สอดคล้องกัน ใช้ CSS variables สีหลักพร้อม accent สด ๆ ดีกว่าสีที่กระจายอย่างขี้กลัว

**Motion และ Animation**
ใช้ CSS animation และ micro-interactions สำหรับช่วงเวลาที่มีผลกระทบสูง เช่น page load ด้วย staggered reveals, hover states ที่น่าประหลาดใจ

**การจัดองค์ประกอบพื้นที่**
Layout ที่ไม่คาดคิด, asymmetry, ซ้อนทับ, การไหลแนวทแยง, พื้นที่ว่างที่กว้างขวาง

**พื้นหลังและรายละเอียดภาพ**
สร้างบรรยากาศด้วย gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows

---

## สิ่งที่ Claude จะ **ไม่** ทำ

- ใช้ font ทั่วไป (Inter, Roboto, Arial, system fonts)
- ใช้ purple gradient บนพื้นหลังขาว (สีที่ AI ใช้บ่อยเกินไป)
- สร้าง layout ที่คาดเดาได้และ cookie-cutter
- ทำงานออกแบบที่ขาดเอกลักษณ์เฉพาะบริบท

---

## ตัวอย่างสิ่งที่ได้รับ

เมื่อขอ "สร้างหน้า landing page สำหรับแอปฟิตเนส" Claude อาจเลือก:
- ธีม industrial/utilitarian ด้วย Bebas Neue + mono font
- สีหลักสีดำ + สี neon เขียว/เหลือง
- Layout asymmetric พร้อม diagonal sections
- Animation ที่รู้สึกเหมือน "พลังงาน" และ "ความแข็งแกร่ง"

แทนที่จะเป็น gradient สีม่วงทั่วไปที่เหมือนทุกโปรเจกต์ AI

---

## เรียนรู้เพิ่มเติม

ดู [Frontend Aesthetics Cookbook](https://github.com/anthropics/claude-cookbooks/blob/main/coding/prompting_for_frontend_aesthetics.ipynb) สำหรับคำแนะนำเชิงลึกเกี่ยวกับการออกแบบ Frontend คุณภาพสูง

---

*สกิลนี้สร้างโดย Prithvi Rajasekaran และ Alexander Bricken จาก Anthropic — แปลและ localize โดย WARROOM-CEO*
