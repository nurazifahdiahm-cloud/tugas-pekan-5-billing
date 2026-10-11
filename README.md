# Pekan 05 - Git Workflows and Reproducibility

Proyek ini merupakan contoh implementasi Git workflow, manajemen dependency, konfigurasi lingkungan, unit testing, dan reproducibility untuk mata kuliah Pemrograman Lanjut.

## 1. Struktur Repository

```text
.
|-- .env.example
|-- .gitignore
|-- README.md
|-- pyproject.toml
|-- uv.lock
|-- scripts/
|   `-- verify_reproducibility.py
|-- src/
|   |-- siakad_billing/
|   |   |-- __init__.py
|   |   `-- billing_core.py
|   `-- siakad_config/
|       |-- __init__.py
|       `-- settings.py
`-- tests/
    `-- test_config_and_billing.py
```

## 2. Prasyarat

Pastikan Python 3.11 atau versi yang sesuai dengan konfigurasi proyek dan `uv` sudah terpasang.

Periksa instalasi dengan perintah:

```powershell
python --version
uv --version
```

## 3. Clone Repository

```powershell
git clone https://github.com/nurazifahdiahm-cloud/tugas-pekan-5-billing.git
cd tugas-pekan-5-billing
```

## 4. Instalasi Dependency

Pasang dependency berdasarkan lockfile agar versi paket konsisten:

```powershell
uv sync --locked --extra dev
```

## 5. Konfigurasi Environment

Buat file `.env` lokal berdasarkan template yang tersedia:

```powershell
Copy-Item .env.example .env
```

File `.env` berisi konfigurasi lokal dan tidak boleh diunggah ke repository. Gunakan `.env.example` sebagai template konfigurasi publik.

## 6. Menjalankan Unit Test

Jalankan seluruh unit test dengan perintah:

```powershell
uv run python -m unittest discover -s tests -p "test_*.py" -v
```

Pengujian dinyatakan berhasil apabila seluruh test selesai dengan status `OK`.

## 7. Audit Reproducibility

Jalankan audit otomatis dengan perintah:

```powershell
uv run python scripts/verify_reproducibility.py
```

Audit memeriksa aturan `.gitignore`, keberadaan `.env.example`, konfigurasi `pyproject.toml`, dan hasil unit test.

Pada pengujian fresh clone, audit menghasilkan skor 100/100.

## 8. Git Workflow

Periksa perubahan file:

```powershell
git status
```

Tambahkan perubahan yang relevan dan buat commit dengan pesan yang menjelaskan perubahan:

```powershell
git add README.md
git commit -m "docs: improve setup and testing instructions"
git push
```

Gunakan Conventional Commits, misalnya `feat:`, `fix:`, `test:`, `docs:`, atau `chore:`, sesuai jenis perubahan yang benar-benar dilakukan.

## 9. Fresh Clone Test

Untuk memvalidasi reproducibility, clone repository ke folder baru, pasang dependency, buat file `.env`, jalankan unit test, dan jalankan audit. Pastikan semua tahap berhasil.

