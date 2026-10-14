# CLAUDE Rules — JD Production Workspace

> **💬 Cara baca file ini:**
> Setiap bagian berisi **aturan** (wajib diikuti AI) dan **penjelasan singkat** di bawahnya (tulisan miring) — supaya kamu mudah paham kenapa aturan itu ada.

---

## Konteks Proyek & Lazy Loading (JIT)
- **Quick Entry Point (<3KB)**: `SHARED_CONTEXT.md` (wajib dibaca pertama kali).
- **Just-in-Time (JIT) On-Demand**:
  - `task.py` / `ai_task_registry.json`: Cek & klaim task sebelum mulai kerja.
  - `WORKSPACE_MAP.md`: Hanya saat butuh pemetaan path folder atau project baru.
  - `info_usaha_terintegrasi.md`: Hanya saat urusan CS, harga paket, atau stok unit.
  - `AGENTS.md`: Universal SSOT & guardrails operasional lengkap.
  - `RUNBOOK_PERBAIKAN.md`: Hanya saat investigasi atau penanganan bug/error.

> *Terapkan prinsip Lazy Loading: Jangan membaca semua file di awal sesi. Cukup baca `SHARED_CONTEXT.md`, file lain hanya dibuka saat tugas spesifik memerlukannya.*

---

## Aturan Operasional Wajib

### 🚫 Push & Deploy
Jangan push/deploy ke cloud/production (clasp push, server GAS, git push main, dll) tanpa instruksi eksplisit Owner.
Semua pengembangan wajib lokal saja.

> *AI tidak boleh upload atau publish kode ke internet sendiri. Harus di komputer lokal dulu sampai Owner menyuruh.*

---

### 📱 WhatsApp — WAJIB APPROVAL
Dilarang keras mengirim WA ke siapa pun (pelanggan, tim) tanpa approval eksplisit Owner.
Wajib tampilkan: draft pesan lengkap + nomor tujuan → tunggu konfirmasi "YA, kirim" → baru eksekusi.
Tidak ada pengiriman otomatis dalam kondisi apa pun.

> *AI tidak boleh kirim WA sendirian. Harus tunjukkan draftnya dulu ke Owner, tunggu "YA, kirim" — baru boleh kirim.*

---

### 🔒 Operasi File
- Read / download / create → auto-approve, tidak perlu konfirmasi
- Delete / rm / unlink → butuh persetujuan eksplisit Owner
- Upload / push ke server → butuh approval tertulis Owner

> *Baca/buat file → boleh langsung. Hapus file atau upload ke server → harus minta izin Owner dulu.*

---

### 📊 Anggaran & Transaksi
- CAPEX rekomendasi aset: max Rp3.000.000/bulan (kamera, laptop, alat).
- Rental B2B (instansi/sekolah): lunas 100% di awal, no termin.

> *Beli alat max Rp3 juta/bulan. Sewa ke instansi/sekolah harus bayar lunas dulu sebelum alat boleh keluar studio.*

---

### 🎯 TikTok Ads
- Evaluasi kreatif setelah 48 jam.
- Pause kreatif dengan CTR < 0.5% (khusus Awareness, evaluasi setelah 50.000 tayangan).

> *Tunggu 48 jam baru nilai iklan. Kalau klik-nya di bawah 0.5%, langsung pause — jangan buang budget.*

---

## Startup Checklist (Progressive & Opt-In)
1. **Pintu Masuk Tunggal**: Baca `SHARED_CONTEXT.md` (<3KB).
2. **Klaim Tugas**: Cek tugas aktif di `ai_task_registry.json` via `python task.py list`.
3. **Briefing / Health Dashboard**: Bersifat **OPT-IN** (Hanya jika Owner secara eksplisit meminta *"briefing"*, *"laporan"*, atau *"status"*).
4. **Langsung Eksekusi**: Jika Owner memberikan instruksi tugas spesifik, lewati briefing dan langsung kerjakan secara to-the-point.
5. **Dokumen Lanjutan (JIT)**: Buka file teknis / bisnis mendalam hanya saat tugas membutuhkannya.

> *Prinsip: Hemat token, eksekusi cepat, hindari membaca berkas yang tidak relevan dengan tugas saat ini.*
