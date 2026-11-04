# ADR-0001: System Topology — Android เป็น Client, x86 Host เป็น PCIe Root ของ GPU

- **สถานะ:** Accepted (กำหนดโดย project requirements)
- **วันที่:** 2026-11-04

## บริบท
Android smartphone ไม่มี PCIe ภายนอก และไม่มี NVIDIA driver/CUDA สำหรับ discrete GPU จึงไม่สามารถเป็น PCIe host ของ NVIDIA GPU ได้

## การตัดสินใจ
- Embedded x86_64 host ภายในกล่องเป็น PCIe Root Complex ของ NVIDIA GPU (ต่อตรง ไม่ผ่าน FPGA)
- Android เป็น client ที่ส่ง task + data ผ่าน USB-C และรับผลลัพธ์กลับ
- FPGA เป็นตัวควบคุม/monitor ด้านข้าง (side-band) ไม่อยู่ใน data path

## ผลที่ตามมา
- ต้องมี protocol ระดับ application (ไม่ใช่ transparent GPU)
- เฉพาะแอปที่ใช้ MDEG SDK เท่านั้นที่ใช้งานได้
- ประสิทธิภาพถูกจำกัดด้วย USB bandwidth ของมือถือ
