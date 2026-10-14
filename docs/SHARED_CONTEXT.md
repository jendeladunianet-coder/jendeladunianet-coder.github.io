# SHARED_CONTEXT.md — JD Production Unified Operational Context
> Auto-refreshed: 2026-09-22 03:18 WIB | Plafon Budget: < 3 KB | SSOT: info_usaha_terintegrasi.md

## 1. Identitas & Jalur Kerja
- Studio Host: Jambi (Operasional Studio, Kasir POS, Rental Kamera)
- Remote HQ: Padang (Owner remote control via Telegram & Hermes)
- Active CLIs: HERMES
- Standard Environment: Terminal = Alacritty | Browser = Chromium only (bukan Chrome biasa)
- Mindset Default: Auto ADHD (ideasi/arsitektur/fuzzy bug) + Auto Ponytail (eksekusi kode/YAGNI/stdlib-first).
- Auto-Termination: AI wajib kill/close browser, dev server lokal, dan proses idle segera setelah tugas tuntas (hemat RAM).

## 2. Parameter Bisnis & Keuangan Kritis
- Plafon CAPEX Baru: Maks Rp 3.000.000 / bulan (ShopeePayLater Rp 1.7jt s/d Sep 2026).
- Rental B2B: Lunas 100% di awal (JD Production sistem NO PIUTANG).
- Iklan Berbayar: Meta Ads & TikTok Ads saat ini NONAKTIF (Spend Rp 0).
- Penjualan Kasir: SSOT transaksi harian di master ERP (Downloads/ERP jdproduction.xlsx).

## 3. Status Antrean Tugas (Task Registry)
- Sedang Berjalan (0): Tidak ada
- Antrean Pending (1): TASK-2026-09-21-008: DEPLOY BESOK (saat komputer Jambi hidup)

## 4. Perintah Cepat Satu Pintu
- Task Registry: python task.py list | python task.py claim <id> <ai> | python task.py done <id> "..."
- Remote PC Jambi: python ssh_jambi.py "<command>" (Direct SSH AMD Athlon 32GB)
- AI Native CLI (Rust): aichat "<prompt>" (Instant AI via 9Router, 0MB RAM idle)
- Fast File Search: fd <pattern> (Rust ultra-fast search) | File Manager: yazi
- Token Optimizer (Rust): rtk <command> (Hemat 60-90% token output terminal untuk LLM/Claude/Hermes)
- Syntax Highlighter: bat <file> (Pengganti cat/type cepat) | Directory Jumper: zoxide
- WhatsApp Audit: python wa.py audit
- ERP Sinkronisasi & Master Cloud: python erp.py sync | python erp.py status | python erp.py open | python erp.py url
- Master Ads Database: python ads.py sync | python ads.py status
- Master Keuangan SSOT: python finance.py status | python finance.py open | python finance.py url | python finance.py push-sheets
- Watchdog & Resource: python _system/resource_watchdog.py

- **WA Web Server (Gateway)**: Primary server AKTIF di PC Kasir Jambi (100.111.222.24:4000). Server di laptop Padang SUDAH DINONAKTIFKAN & DI-ZIP. DILARANG menjalankan server WA di laptop lokal.