# ADR-0002: USB Transport ระหว่าง Android กับ Embedded Host

- **สถานะ:** Proposed — รอการอนุมัติ
- **วันที่:** 2026-11-04

## บริบท
USB เป็นแบบ host/device; x86 motherboard ทั่วไปมีเฉพาะ USB host controller → ต้องให้มือถือเป็นฝั่ง device หรือใช้ตัวกลาง

## ตัวเลือก
| ID | Transport | สรุป |
|---|---|---|
| T1 | Android Open Accessory (AOA) | Host = Linux (libusb), Phone = accessory; ไม่ต้องใช้ developer mode; host จ่ายไฟให้มือถือ |
| T2 | USB tethering (NCM/RNDIS) + TCP | ง่าย แต่ต้องเปิด tethering เองและ routing ปนอินเทอร์เน็ต |
| T3 | `adb reverse` + TCP | สำหรับพัฒนาเท่านั้น (ต้องเปิด USB debugging) |
| T4 | Phone เป็น USB host + USB-Ethernet chip ในกล่อง | TCP มาตรฐาน แต่มือถือไม่ถูกชาร์จ, รองรับ chip ต่างกันตามรุ่น |

## ข้อเสนอ
- Phase 1b–1c: T3 (เร็วที่สุดในการพิสูจน์ pipeline)
- Phase 1d เป็นต้นไป: T1 เป็น transport หลัก
- ออกแบบ `Transport` interface ให้เปลี่ยน backend ได้ ทั้งฝั่ง host และ Android SDK

## ความเสี่ยงที่ยังเปิดอยู่
- Throughput ของ AOA บนมือถือ USB 3.x: `[TBD]` ต้องวัดจริง
- มือถือบางรุ่นอาจไม่รองรับ accessory mode: ตรวจด้วย `android.hardware.usb.accessory`
