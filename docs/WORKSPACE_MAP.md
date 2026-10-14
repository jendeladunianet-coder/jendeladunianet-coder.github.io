# 🗺️ Peta Workspace JD Production (WORKSPACE_MAP.md)

Dokumen ini berisi peta direktori semua sub-proyek aktif di bawah folder `C:\Users\USER`. Agen AI wajib membaca file ini saat startup untuk mengetahui konteks proyek sebelum melakukan tugas.

> [!IMPORTANT]
> **Single Source of Truth (SSOT) Informasi Bisnis:**
> Sebelum memulai tugas operasional, keuangan, atau komunikasi, Agen wajib membaca berkas [info_usaha_terintegrasi.md](file:///C:/Users/USER/_docs/info_usaha_terintegrasi.md) yang berisi seluruh detail alamat cabang, nomor kontak, tautan web app, kredensial API, harga paket, dan ringkasan SOP agar tidak perlu mencari informasi secara berulang.

---

## 📂 1. Dashboard & Antarmuka Utama (Front-End)
*   **[intern_dashboard](file:///C:/Users/USER/dashboards/intern_dashboard)** — Dasbor visual untuk memantau kehadiran dan kinerja anak magang.
*   **[karyawan_dashboard](file:///C:/Users/USER/karyawan_dashboard)** — Dasbor pelaporan kerja harian karyawan studio (tetap di root karena terkunci).
*   **[agents_dashboard](file:///C:/Users/USER/dashboards/agents_dashboard)** — Panel monitoring status operasional dan log multi-agent.
*   **[jd_owner_hub](file:///C:/Users/USER/dashboards/jd_owner_hub)** — Konsol monitoring eksekutif untuk Owner/CEO.
*   **[jd-booking-web](file:///C:/Users/USER/jd-booking-web)** — Landing page reservasi booking online terpisah (Vercel) dengan integrasi Meta Pixel & TikTok Pixel yang terhubung langsung ke ERP.

## ⚙️ 2. Sistem Inti Operasional & Database
*   **[jd_operations_hub](file:///C:/Users/USER/jd_operations_hub)** — Hub operasional utama. Menyimpan backend Google Apps Script (`Code.gs`), laporan keuangan, analisis chat, dan data transaksi lokal (`transactions.json`).
*   **[jdproduction_erp](file:///C:/Users/USER/erp/jdproduction_erp)** — Sistem ERP terintegrasi (versi aktif).
*   **[jdproduction_erp_dev](file:///C:/Users/USER/erp/jdproduction_erp_dev)** — Versi development ERP.
*   **[ERP Archive](file:///C:/Users/USER/erp/_archive)** — Versi ERP lawas (non-aktif) untuk referensi.
*   **[intern_attendance_db](file:///C:/Users/USER/core_systems/intern_attendance_db)** — Database pencatatan absensi magang.
*   **[jd_local_analytics](file:///C:/Users/USER/jd_local_analytics)** — Sistem utilitas lokal (CLI) untuk mencatat HPP, log baterai kamera, dan analisis repeat order customer tanpa port conflict.


## 📸 3. Proyek Photobooth & Store
*   **[jd-photobooth](file:///C:/Users/USER/photobooth_store/jd-photobooth)** — Aplikasi Progressive Web App (PWA) utama untuk sistem booking dan operasional photobooth.
*   **[neobrutalism-photobooth](file:///C:/Users/USER/photobooth_store/neobrutalism-photobooth)** — Versi visual photobooth bertema Neo-Brutalisme.
*   **[jd-digital-store](file:///C:/Users/USER/photobooth_store/jd-digital-store)** — E-commerce / catalog digital untuk produk dan merchandise studio.

## 💻 4. Persewaan Laptop & Aset
*   **[laptop-rental-tracker](file:///C:/Users/USER/laptop_rental/laptop-rental-tracker)** — API backend untuk pelacakan sisa unit sewa laptop Fujitsu/aset lainnya.
*   **[laptop-tracker-client](file:///C:/Users/USER/laptop_rental/laptop-tracker-client)** — Aplikasi web front-end klien untuk tracking sewa laptop.

## 🤖 5. Mesin AI, Otomatisasi & Media Sosial
*   **[jd_agent_orchestrator](file:///C:/Users/USER/jd_agent_orchestrator)** — Modul utama mesin orkestrasi agen (Virtual COO / `ceo_agent`). Subfolder: `queue/` (log eksekusi), `agents_root/` (role prompts).
*   **[wa_monitoring](file:///C:/Users/USER/wa_monitoring)** — Skrip monitoring log WhatsApp Customer Service.
*   **[ig_auto_uploader](file:///C:/Users/USER/social_media/ig_auto_uploader)** — Bot pengunggah konten otomatis Instagram Feed (pagi hari via scheduler).
*   **[ig_story_uploader](file:///C:/Users/USER/social_media/ig_story_uploader)** — Bot pengunggah konten Story Instagram.
*   **[metricool_uploader](file:///C:/Users/USER/social_media/metricool_uploader)** — Sistem auto-uploader video ke Metricool (TikTok, IG, YouTube Shorts) dengan Local Approval Dashboard.
*   **[unified_social_uploader](file:///C:/Users/USER/social_media/unified_social_uploader)** — Sistem uploader media sosial terpadu berbasis database Supabase.
*   **[task_dispatcher](file:///C:/Users/USER/social_media/task_dispatcher)** — Dashboard lokal penyusunan dan pengiriman tugas harian tim & magang via WhatsApp Fonnte API.
*   **[ads_downloader](file:///C:/Users/USER/social_media/ads_downloader)** — Sistem otomatisasi unduh & ekstraksi data laporan iklan Meta & TikTok via Playwright.
*   **[ig_analyzer](file:///C:/Users/USER/social_media/ig_analyzer)** — Sistem analisis data performa media sosial.
*   **[shopee_exporter](file:///C:/Users/USER/social_media/shopee_exporter)** — Ekstraktor data belanja Shopee (manual, via Playwright).
*   **[jd_osint_hub](file:///C:/Users/USER/core_systems/jd_osint_hub)** — Alat bantu OSINT untuk verifikasi kontak/audit data blacklist pelanggan.
*   **[multi_agent_sandbox](file:///C:/Users/USER/multi_agent_sandbox)** — Sandbox koordinasi Multi-CLI AI Agent (Claude Code + Antigravity CLI) untuk optimasi token dan pembagian peran Planner-Executor.
*   **[wa_mimo_chat_analyzer](file:///C:/Users/USER/wa_mimo_chat_analyzer)** — CLI tool interaktif untuk membaca dan menganalisis transkrip chat WA lengkap menggunakan AI mimo lokal via 9Router.


## 📦 6. Utilitas, Background Service & Cadangan
*   **[_backups](file:///C:/Users/USER/_backups)** — Wadah penyimpanan zip backup berkala dan arsip sistem lama (`approval_sistem_legacy`, `jd_operations_hub_temp`, `jd_backup_studio`).
*   **[legacy_projects/frontend_legacy](file:///C:/Users/USER/legacy_projects/frontend_legacy)** — Kumpulan halaman landing page static non-repositori (`landing_pasfoto.html`, dsb.).
*   **[tools/services](file:///C:/Users/USER/tools/services)** — Folder kumpulan servis latar belakang studio (seperti `upload_qr`).
*   **[tools](file:///C:/Users/USER/tools)** — Kumpulan perkakas eksternal & utilitas pendukung (seperti OSINT `sherlock`, `Legendary_OSINT`, utility `pinchtab`, camera firmware `magiclantern_simplified`).
*   **[legacy_projects](file:///C:/Users/USER/legacy_projects)** — Kumpulan proyek web legacy studio (`jdverifikasi_new`, `qc_photo`, `teamwork_projects`).
*   **[waha](file:///C:/Users/USER/waha)** — Layanan WhatsApp HTTP API gateway (berjalan aktif di root).

---

## 📄 Dokumen SOP & Aturan Utama (Root)
*   **Aturan Kerja Agent:** [AGENTS.md](file:///C:/Users/USER/.agents/AGENTS.md)
*   **Daftar Tugas Harian Agent:** [tugas_harian_spesialis_agent.md](file:///C:/Users/USER/_docs/tugas_harian_spesialis_agent.md)
*   **Panduan Cara Memanggil Agent:** [panduan_panggilan_agent.md](file:///C:/Users/USER/_docs/panduan_panggilan_agent.md)
*   **Memory & Log:** [`_docs/memory/`](file:///C:/Users/USER/_docs/memory) — Dokumen konteks bisnis, glossary, keputusan, dan kalender konten.

---

## 🤖 6. Sistem Multi-Agent Context & Handoff

Sistem ini memastikan setiap AI yang masuk langsung paham konteks tanpa harus baca puluhan file.

### Alur Startup AI (Wajib)
```
AI masuk → baca AI_CONTEXT.md → cek ai_session_state.json → cek ai_task_registry.json → mulai kerja
```

### File-File Sistem Handoff

| File | Lokasi | Fungsi |
|------|--------|--------|
| `AI_CONTEXT.md` | `C:\Users\USER\AI_CONTEXT.md` | **Primer utama** — baca ini pertama. Ringkasan bisnis, rules, project map, dan status sistem dalam 1 file |
| `ai_session_state.json` | `C:\Users\USER\ai_session_state.json` | State handoff antar AI — siapa yang terakhir kerja, apa yang sudah/belum diselesaikan, metrik terkini |
| `ai_task_registry.json` | `C:\Users\USER\ai_task_registry.json` | Task lock & tracking — mencegah dua AI mengerjakan hal yang sama, menyimpan hasil task |
| `sync_agent_state.py` | `C:\Users\USER\_scripts\sync_agent_state.py` | Script auto-sync — update `ai_session_state.json` dari semua log files secara otomatis |

### Cara Pakai sync_agent_state.py
```bash
python _scripts/sync_agent_state.py           # Full sync + tampilkan status
python _scripts/sync_agent_state.py --status  # Tampilkan status saat ini saja
python _scripts/sync_agent_state.py --tasks   # Tampilkan task registry saja
```

### Kewajiban AI di Akhir Sesi
Setiap AI **wajib** update `ai_session_state.json` → field `last_session` sebelum sesi berakhir.
Format: `{ "ai": "nama", "timestamp": "ISO8601", "tasks_completed": [], "tasks_pending": [], "notes_for_next_ai": "" }`

### Registry Agent Lengkap
*   **Config:** [jd_agent_orchestrator/config/agents_registry.json](file:///C:/Users/USER/jd_agent_orchestrator/config/agents_registry.json)
*   **13 agent aktif:** ceo_agent, wa_auditor, finance_auditor, content_planner, ads_optimizer, network_technician, brand_monitor, web_developer, python_developer, graphic_designer, browser_agent, funnel_agent, competitor_analyst
