# MDEG — Mobile Direct External GPU

อุปกรณ์ภายนอกที่ให้ Android smartphone ส่งงานคำนวณ (CUDA workloads) ผ่าน USB-C ไปประมวลผลบน NVIDIA GPU
ซึ่งติดตั้งอยู่ในกล่องที่มี embedded x86 host computer, PSU และระบบระบายความร้อนของตัวเอง

> **สถานะปัจจุบัน: Phase 0 — Feasibility Study (รอการอนุมัติ)**
> ยังไม่มีการทดสอบบนฮาร์ดแวร์จริง ยังไม่มี RTL / PCB / แอป

## เอกสารเริ่มต้น
- [Phase 0 Feasibility Report](docs/feasibility/PHASE0_FEASIBILITY_REPORT.md)
- [Initial BOM (estimates)](hardware/bom/bom_v1_estimate.csv)
- [Architecture Decision Records](docs/decisions/)

## โครงสร้างโปรเจค
```
docs/        architecture, feasibility, datasheets, decisions (ADR), testing
hardware/    schematics, pcb (KiCad), bom, enclosure (Fusion)
fpga/        rtl (SystemVerilog), testbench, constraints, simulation
embedded/    host-service, cuda, usb, fpga-interface
android/     app, sdk, usb-client (Kotlin)
benchmarks/  benchmark harness and recorded results (real vs simulated clearly labelled)
scripts/     setup and utility scripts
```

## กฎของโปรเจค (ย่อ)
- ไม่แต่งสเปคฮาร์ดแวร์หรือผล benchmark — ค่าที่ไม่ทราบให้ระบุเป็น `TBD`
- แยกผล simulation กับผลจากฮาร์ดแวร์จริงอย่างชัดเจน
- ไม่สร้างไฟล์สำหรับการผลิต (Gerber ฯลฯ) ก่อนผ่าน electrical/mechanical review
