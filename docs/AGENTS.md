# AGENTS.md — Universal Rules & Operational SSOT (JD Production)
> Universal rules untuk semua AI CLI: Hermes, Antigravity (AGY), Claude Code, Codex, dll.
> Quick entry point harian (<3KB): `SHARED_CONTEXT.md`
> SSOT data bisnis: `info_usaha_terintegrasi.md`
> Peta workspace: `WORKSPACE_MAP.md`

---

## 🛑 1. FAKTA OPERASIONAL TETAP (DILARANG HALUSINASI)
1. **TikTok Ads Padang**: Sudah lama nonaktif/mati (abaikan di log historis).
2. **Status Ads (Meta & TikTok)**: Semua iklan berbayar (Meta Ads & TikTok Ads) saat ini **NONAKTIF / PAUSED** (Spend Rp 0). Dilarang melaporkan status 'Active' dari data cache lama.
3. **Konten Magang**: Anak magang rutin membuat konten harian (dilarang lapor belum post hanya karena sheet kosong).
4. **ERP Overdue**: Status overdue di ERP terjadi akibat bug tombol kembali UI web yang sengaja dibiarkan agar tidak mengganggu kasir (bukan kendala kasir).
5. **FRT WhatsApp CS**: First Response Time terhitung tinggi adalah hal wajar karena akumulasi jam tutup studio pada malam/dini hari.
6. **Strategi Monetisasi Alat Tidur (Cross-Subsidy)**: Kamera & iPhone adalah produk rebutan tapi stok terbatas. Laptop, Infocus, HT, dan alat idle lainnya WAJIB dipush iklannya agar aset tidur menghasilkan cash flow untuk belanja unit baru.
7. **Jangan Mengarang Angka**: Dilarang mengarang/mensimulasikan angka keuangan tanpa dasar. Semua metrik wajib bersumber langsung dari data di Excel Master ERP (`Downloads/ERP jdproduction.xlsx`) atau database JSON terpadu.
8. **Arsitektur Backup Harian 2-Lapis (Aktif Otomatis)**:
   - **Lapis 1 (Cloud Drive)**: Cron job GAS tengah malam (`autoCleanUpMidnight` -> `doAutoBackup`) otomatis menyalin master spreadsheet ke folder Google Drive `JD_PRODUCTION_BACKUPS`.
   - **Lapis 2 (Lokal & Cloud ZIP)**: Windows Task Scheduler `JD_Daily_Backup` otomatis mengeksekusi `_scripts/backup_studio.py` setiap pukul 23:00 WIB (kompresi data inti & unggah ke Google Drive `JD_Production_Backups`).
   - Arsip ZIP lokal diatur dengan retensi otomatis 7 hari.

---

## 🚫 2. GUARDRAILS & KEBIJAKAN IZIN (STRICT RESTRICTIONS)
| Tindakan | Aturan |
|---|---|
| **Push / Deploy Cloud** | ❌ **DILARANG KERAS** tanpa instruksi tertulis Owner (Vercel, Git main, Cloud GAS, dll). Semua pengerjaan LOKAL saja. |
| **Hapus File / Folder** | ❌ **DILARANG KERAS** (`rm`, `delete`, `unlink`) tanpa izin eksplisit Owner. |
| **Kirim WhatsApp** | ❌ **DILARANG KIRIM OTOMATIS**. Wajib tampilkan draf pesan + nomor/grup tujuan, lalu tunggu Owner mengonfirmasi: `"YA, kirim"` (toleran case-insensitive & spasi: *"ya kirim"*, *"YA, kirim"*, *"ya, kirim"*). |
| **Unduh Data Jaringan** | ✅ **DIPERBOLEHKAN** secara mandiri oleh AI jika **TIDAK BERBAHAYA** (AI menilai sendiri; aman = langsung kerjakan; berbahaya/berbiaya/tidak reversibel = tanya Owner). Jalur resmi ERP tetap `python erp.py sync` — boleh jalan otomatis berkala (cron) untuk refresh data karena aman & hanya membaca. |
| **Fase Plan & Diskusi** | ❌ **DILARANG** eksekusi perintah sistem yang mengubah kondisi sistem saat fase perencanaan sebelum persetujuan Owner. |
| **Bahasa Tab Kasir** | ❌ **DILARANG TERJEMAHKAN KE B. INDO**. Seluruh label, header, kolom, dan tombol di Tab Kasir POS (`#tab-kasir`) WAJIB 100% tetap dalam Bahasa Inggris (*English UI*). |
| **Styling CSS Dasbor** | ❌ **DILARANG MENAMBAH ATURAN CSS GLOBAL**. Modifikasi antarmuka wajib di-scope ketat di bawah ID atau class kontainer spesifik (misal: `#tab-kasir`, `.pos-*`) agar tidak merusak tata letak tab lain. |
| **Terminal Interaktif** | ✅ **WAJIB ALACRITTY**. Seluruh pemicuan popup jendela terminal di layar laptop WAJIB menggunakan Alacritty (`C:\Program Files\Alacritty\alacritty.exe`). |
| **Browser Otomasi & Remote** | ✅ **WAJIB CHROMIUM (RINGAN) & BROWSERSKILL / CDP**. Seluruh browser automation, scraping, CUA, navigasi interaktif, dan remote kontrol browser WAJIB menggunakan Chromium (`C:\Users\USER\AppData\Local\Chromium\Application\chrome.exe` atau Playwright Chromium) yang terpasang ekstensi **BrowserSkill** (`hhcmgoofomhgciiibhipgmgkgnoenaoi`) via port CDP terisolasi (`9222-9226`). Dilarang menggunakan Google Chrome biasa agar hemat RAM & CPU. |
| **Testing Ekstensi WA** | ✅ **WAJIB CHROME PROFILE J1 (PROFILE 8)**. Seluruh testing dan verifikasi fungsi ekstensi WA Web (`projects/jd-wa-quickreply-extension`) WAJIB diuji coba langsung di browser Chrome Profile J1 (`Profile 8`) yang memiliki sesi login aktif sebelum diserahkan ke Owner. |
| **Tutup Program & Proses** | 🛑 **WAJIB SAFE-KILL PID (DILARANG BLIND KILL)**. AI hanya boleh mematikan proses browser milik sesi sendiri (`safe_kill(pid)` atau `taskkill /PID <pid> /T /F`). **DILARANG KERAS** mengeksekusi blind `taskkill /IM chrome.exe /IM chromium.exe` karena akan mematikan paksa browser milik AI lain yang sedang aktif bekerja. Wajib daftarkan PID browser ke `_docs/active_browser_lock.json` via `_scripts/browser_lock.py`. |

---

## ⚡ 3. PROTOKOL EKSEKUSI KODE & PENGUJIAN LOKAL
1. **Safety Net (Backup & Rollback Wajib)**: Semua AI boleh mengedit kode **ASAL membuat backup (`.bak` atau `git stash`) sebelum modifikasi**. Jika uji coba gagal/error, **wajib langsung rollback**. Hapus file cadangan hanya setelah uji coba sukses.
2. **Protokol Koreksi Mandiri (Action → Verify → Auto-Fix)**: AI dilarang berasumsi. Setiap kali membuat atau memodifikasi kode, AI **WAJIB menjalankan uji eksekusi lokal (dry-run/test)**. Jika muncul error (exit code != 0), baca traceback, analisis akar masalah, dan perbaiki mandiri sampai tuntas (exit code 0) sebelum melapor.
3. **Keutuhan Struktur HTML**: Pastikan keseimbangan tag HTML (terutama penutup `</div>`) agar tampilan antarmuka tidak rusak.
4. **Proteksi Encoding Windows Console**: Setiap script Python wajib menyertakan blok UTF-8:
   ```python
   if sys.platform == 'win32' and hasattr(sys.stdout, 'reconfigure'):
       sys.stdout.reconfigure(encoding='utf-8', errors='replace')
   ```
5. **Anti-Banned / Stealth Scraping (`Scrapling` & `browser-use`)**: Untuk ekstraksi data web sensitif (TikTok, Instagram, Shopee, FB Marketplace), **WAJIB menggunakan `Scrapling` (`StealthyFetcher`)** karena otomatis mem-bypass Cloudflare/anti-bot tanpa konsumsi token. Untuk tugas navigasi web interaktif (klik tombol, isi form), gunakan **`browser-use`**.
6. **Penanganan Fallback Session Windows & GUI Failures**: Jika eksekusi `computer_use` (CUA) atau kontrol GUI fisik gagal akibat masalah Session 0, layar terkunci, atau kursor tidak bisa dikontrol, AI **WAJIB otomatis mengalihkan fallback ke `browser-use` (via CDP port 9222 / headless)** untuk semua tugas berbasis web/browser agar eksekusi tidak macet.
7. **Eksekusi Non-Interaktif**: Script/command terminal wajib non-blocking (`-y`, `--yes`, timeout) agar proses background / bot Telegram tidak hang.
8. **Auto-Housekeeping**: Bersihkan file scratch/uji coba sementara (`temp_*.py`, `scratch_test.py`, `.bak`) setelah perbaikan sukses (exit code 0).
9. **Proteksi & Efisiensi Berkas Cadangan (Backup Exclusions)**: Dalam setiap skrip pengarsipan/backup sistem, folder cache browser dan sesi aktif (`chrome_profile`, `session_wweb`, `session`, `Cache`, `GPUCache`, `DawnWebGPUCache`, `Service Worker`, `Crashpad`) WAJIB dikecualikan dari arsip ZIP agar ukuran tetap ringkas (<150 MB) dan proses upload ke Google Drive tidak mengalami timeout.
10. **Mode Proaktif Otomatis (Build → Improve → Find)**: AI **BERWENANG** mengerjakan langsung tanpa menunggu instruksi Owner untuk kategori:
    - (a) Belum ada → **BIKIN**;
    - (b) Sudah ada → **IMPROVE**;
    - (c) Data tidak ada → **CARI** (sync/export/scrape sesuai aturan anti-blokir).
    *Tetap wajib*: backup sebelum edit, uji lokal exit 0, tulis hasil ke registry, lapor ringkas.
11. **Batasan Mode Proaktif**: Tetap **DILARANG** otomatis tanpa konfirmasi Owner:
    - Push/Deploy Cloud
    - Hapus file/folder
    - Kirim WhatsApp
    - Belanja CAPEX > plafon
    - Tindakan berbahaya/berbiaya/tidak reversibel (kecuali Owner sudah beri izin di task).
    *Prinsip Owner*: AI memikirkan sendiri & bertindak kalau aman; baru tanya saat berbahaya.
12. **Uji Mandiri Proyek WhatsApp (Wajib Chrome Profile J1 / Profile 8)**: Untuk setiap modifikasi kode pada proyek ekstensi WhatsApp (`projects/jd-wa-quickreply-extension`), AI **WAJIB menjalankan pengujian mandiri (self-test)** langsung di Google Chrome Profile J1 (`Profile 8`) yang memiliki sesi WhatsApp Web aktif. Dilarang berasumsi atau melapor sukses tanpa verifikasi eksekusi nyata pada Chrome J1.
13. **Auto-Termination Program & Proteksi PID Browser (Wajib Tutup Presisi via PID)**: Setiap AI (Hermes, Claude Code, AGY, Codex) yang membuka browser automation (Chromium/Chrome) WAJIB mendaftarkan PID prosesnya ke `_docs/active_browser_lock.json` (`python _scripts/browser_lock.py register --pid <pid> --ai <nama_ai> --task <tugas>`). Saat pekerjaan selesai, AI WAJIB menutup HANYA proses dengan PID miliknya sendiri (`safe_kill(pid)` atau `taskkill /PID <pid> /T /F`). **DILARANG KERAS** menjalankan blind kill global seperti `taskkill /F /IM chrome.exe /IM chromium.exe` agar tidak memutus sesi browser AI lain yang sedang menjalankan tugas live (misal: scraping, posting story, atau pemantauan CUA). Biarkan browser AI lain tetap berjalan sampai tugasnya tuntas.
14. **Auto-Mindset (Auto ADHD & Auto Ponytail)**:
    - **Ideasi / Arsitektur / Fuzzy Debugging (Auto ADHD)**: Wajib gunakan pola divergen & pruning (spawning perspektif alternatif: $0 budget, speedrun, regulasi, child/layman view; deteksi jebakan) untuk keputusan arsitektur, naming, API design, atau debugging tanpa root cause jelas. Hindari jawaban textbook klise di awal.
    - **Eksekusi Solusi & Penulisan Kode (Auto Ponytail)**: Wajib terapkan ladder Ponytail (YAGNI extremist → stdlib first → native platform feature → installed dependency → one-liner → minimum code). Dilarang menambah boilerplate spekulatif, file/abstraksi tak diminta, atau dependency baru bila cukup beberapa baris kode sederhana.

---

## 🤝 4. KOORDINASI MULTI-CLI & HANDOFF
1. **Task Locking via `task.py`**:
   - Sebelum mulai coding, cek tugas di `ai_task_registry.json` menggunakan `python task.py list`.
   - Klaim task: `python task.py claim <TASK_ID> <AI_NAME>`. Dilarang ambil alih task yang sedang `in_progress` oleh CLI lain kecuali idle >2 jam.
   - Selesai task: `python task.py done <TASK_ID> "Hasil"`.
2. **Disk Refresh (Anti-Stale Cache)**: Wajib baca file langsung dari disk (`view_file`) sebelum mengedit. Dilarang mengandalkan memori sesi lama.
3. **Handoff Sesi Akhir**: Sebelum menutup sesi atau berganti CLI, wajib perbarui `ai_session_state.json` (`tasks_completed`, `tasks_pending`, `notes_for_next_ai`).
4. **Pemisahan Peran**:
   - **Hermes (Telegram / Mobile / CLI)**: Dispatcher, quick task check, monitoring lead & alert, eksekusi script cepat.
   - **Antigravity (AGY)**: Heavy executor, coding, debugging lokal, dry-run, browser visual inspection.
   - **Claude Code**: Architect, multi-step planner (`plan_diskusi.md`), code reviewer.

---

## 📊 5. PARAMETER BISNIS, KEUANGAN & OPERASIONAL
* **Plafon CAPEX Aset Baru**: Maksimal **Rp3.000.000 / bulan** (kamera, laptop, alat).
* **Rental B2B (Instansi/Sekolah)**: Wajib **lunas 100% di awal** sebelum alat keluar studio. **Sistem JD Production NO PIUTANG** (semua transaksi kasir & sewa wajib lunas di depan, tidak ada pencatatan piutang).
* **Evaluasi TikTok Ads**: Evaluasi kreatif setelah **48 jam**. Pause kreatif dengan **CTR < 0.5%** (khusus iklan Awareness, evaluasi setelah mencapai **50.000 tayangan**).
* **Format Briefing Sesi**: Bersifat OPT-IN (hanya saat Owner mengetik 'briefing'/'laporan'/'status'). Format baku tersimpan di `_docs/TEMPLATE_BRIEFING.md`.
* **Pencocokan Transaksi Kasir & Booking**: Gunakan nomor WhatsApp (9 digit terakhir) atau Nama Pelanggan dengan window ±30 hari (field `bookingId` sering kosong di kasir).
* **Tanggung Jawab Sosmed**: Upload Metricool harian dipegang oleh **Fajar** dan **Joko**; **Riko** dibebaskan dari tugas sosmed harian.
* **12 Standard Content Rules (SOP Produksi Konten TikTok/Reels)**: 1) Visual hook 3s; 2) Change frame tiap 3s; 3) Audio jernih (suara tak pelan); 4) Konten dari balesan komen; 5) Lensa wajib bersih (bebas buram); 6) Trend ATM (Amati Tiru Modifikasi); 7) Prioritas Voice Over (VO); 8) Top 10 Trending Sound TikTok; 9) Caption + Hashtag max 1; 10) Upload foto min 10 + teks tiap foto; 11) Schedule jam 09:00 WIB; 12) Judul video warna Butter Yellow.
* **Penyimpanan QA Finansial (WAJIB)**: Setiap pertanyaan/jawaban finansial dari Owner WAJIB disimpan lengkap (kategori, pertanyaan, parameter, rumus/logika, hasil perhitungan, sumber) ke `_docs/financial_qa_history.json` — `auto_download_erp.py` akan otomatis mensinkronkannya ke sheet `PertanyaanFinansial` ERP di setiap sync (tidak perlu hitung ulang dari nol di sesi berikutnya).
* **Penyimpanan Laporan Owner (Rule #9)**: Setiap jawaban laporan operasional/finansial kepada Owner WAJIB disimpan ke `_docs/owner_reports.json` dan di-mirror ke sheet ERP `LaporanOwner_AdHoc` serta berkas mirror markdown `_docs/laporan_owner/YYYY-MM-DD_<topik>.md` agar riwayat tidak hilang saat sesi berganti.
* **Anti-AI Content & Text Humanizer (Rule #13)**: Setiap pembuatan draf teks promosi, caption sosmed, story IG/FB, atau script konten WAJIB berformat natural gaya manusia (gaya admin lokal santai, no kata-kata klise AI seperti 'menghadirkan/solusi terbaik/tak terlupakan', gunakan singkatan wajar seperti '80rb/yaa/udah include', struktur kalimat variatif, tanpa emoji hiasan berlebihan) agar 100% lolos dan tidak terdeteksi bot/AI oleh algoritma Meta & TikTok.
* **Standar Safe Zone Konten Video & Gambar Sosmed (Rule #14)**: Setiap desain gambar (carousel/feed 4:5) dan video vertikal (Reels/TikTok/Story 9:16) WAJIB menerapkan batas aman **Safe Zone (UI Overlay Safe Area)**:
  - **Atas**: Minimal margin 150px (bebas dari header/status bar/search).
  - **Bawah**: Minimal margin 250px-300px untuk video (bebas dari caption/username/audio marquee) & 100px untuk carousel foto.
  - **Kanan**: Minimal margin 120px-150px untuk video (bebas dari tombol Like, Comment, Bookmark, Share).
  - **Kiri**: Minimal margin 60px-80px.
  - Seluruh teks penting, headline, dan visual utama WAJIB berada di dalam batas Safe Zone ini agar tidak tertutup tombol/UI aplikasi.
* **Verifikasi Memori Usang (Rule #10)**: Memori atau konteks dengan usia > 90 hari WAJIB diberi flag `[STALE-VERIFY]` pada deskripsi dan diverifikasi ulang sebelum dijadikan dasar keputusan bisnis.
* **Standar Video AI Karakter (Rule #11)**: Setiap pembuatan video promosi/edukasi AI (Google Flow / Gemini CUA), WAJIB cek dan patuhi pedoman di `GUIDELINE_VIDEO_AI.md`: 1) Wajib pakai foto karakter referensi langganan (`wisuda_model.jpg` untuk cowok, `model_cewek.jpg` untuk cewek); 2) Prompt yang didiktekan Owner WAJIB persis (verbatim) tanpa ditambah-tambah; 3) Visual hook kuat di awal 3 detik; 4) Cut-to-cut tiap 2 detik ganti angle kamera; 5) Sound depan kuat dan bertenaga; 6) Format 9:16 vertical; 7) Native Audio Google Flow: Sound & audio wajib dihasilkan langsung dari Google Flow; 8) Non-Selling / Pure Info: Konten berfokus murni pada edukasi, tips, atau informasi menarik tanpa jualan / hard-selling.

---

## 👑 6. PRINSIP EXECUTIVE (OWNER NON-TEKNIS & FORMAT YA / TIDAK)
1. **AI Eksekutor Penuh (Zero-DIY)**: Owner adalah pengambil keputusan bisnis, bukan programmer. AI dilarang menyuruh Owner mengedit file, copy token, atau menjalankan command teknis. AI wajib mengeksekusi sendiri via terminal / Computer Use (CUA) sampai tuntas.
2. **Keputusan Teknis Mandiri**: Dilarang meminta Owner memilih arsitektur/library teknis. AI wajib memilih solusi paling simpel, minim dependensi, dan langsung jalan.
3. **Pertanyaan Wajib Format "Ya / Tidak"**: Saat butuh konfirmasi (izin belanja, CAPTCHA, hapus file), jelaskan dalam 1 kalimat bahasa awam tanpa istilah koding, dan akhiri dengan opsi biner agar Owner cukup menjawab: **"Ya"** atau **"Tidak"**. *(Khusus kirim WA wajib konfirmasi: "YA, kirim" / "ya kirim")*.
4. **Bahasa Hasil Nyata**: Laporkan dampak operasional/bisnisnya secara singkat, bukan teknis koding (contoh: *"Tombol kasir sudah normal dan siap dipakai"* bukan *"Tag div sudah ditutup"*).

---

## 🚀 SKRIP PEMBANTU SATU PINTU
* **WhatsApp**: `python wa.py audit` | `python wa.py broadcast` | `python wa.py login` | `python wa.py status`
* **ERP & Database**: `python erp.py sync` | `python erp.py status` | `python erp.py find <kata>`
* **Master Ads Database**: `python ads.py sync` | `python ads.py status` | `python ads.py open` | `python ads.py url`
* **Task Registry**: `python task.py list` | `python task.py add "..."` | `python task.py claim <id> <ai>` | `python task.py done <id> "..."`
* **Penugasan Tim**: `python tugas.py generate` | `python tugas.py view` | `python tugas.py status`
