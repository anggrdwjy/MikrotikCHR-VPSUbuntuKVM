<p align="center">
  <img src="banner.png" alt="MikroTik CHR on Cloud VPS">
</p>

# MikroTik CHR on Cloud VPS — Ubuntu KVM Based Proxmox

Solusi MikroTik CHR x86 on Cloud VPS untuk arsitektur VPS Proxmox berbasis Ubuntu KVM.


## Daftar Isi

- [1. Fitur (Features)](#1-fitur-features)
- [2. Versi Teruji (Tested Version)](#2-versi-teruji-tested-version)
- [3. Lisensi dan Batas Bandwidth (License & Bandwidth Limit)](#3-lisensi-dan-batas-bandwidth-license--bandwidth-limit)
- [4. Prasyarat (Prerequisites)](#4-prasyarat-prerequisites)
- [5. Instalasi (Installation)](#5-instalasi-installation)
- [6. Cek Tipe Disk Sebelum Menjalankan Script (Check Disk Type Before Running Script)](#6-cek-tipe-disk-sebelum-menjalankan-script-check-disk-type-before-running-script)
- [7. Contoh Output Instalasi (Installation Output Example)](#7-contoh-output-instalasi-installation-output-example)
- [8. Setelah Instalasi: Reboot](#8-setelah-instalasi-reboot)
- [9. Akses Remote (Remote Access)](#9-akses-remote-remote-access)
- [10. Dukungan (Support)](#10-dukungan-support)
- [11. Laporan Bug (Bugs)](#11-laporan-bug-bugs)
- [12. Lisensi (License)](#12-lisensi-license)


## 1. Fitur (Features)

- Solusi MikroTik CHR x86 on Cloud VPS — Special Case Ubuntu KVM Based Proxmox (VPS Proxmox Architecture).

## 2. Versi Teruji (Tested Version)

| Ubuntu | MikroTik RouterOS |
| --- | --- |
| Ubuntu 24.04 | MikroTik RouterOS 6.49.18 |
| Ubuntu 26.04 | MikroTik RouterOS 7.21.x |

## 3. Lisensi dan Batas Bandwidth (License & Bandwidth Limit)

Periksa License MikroTik CHR x86 sebelum instalasi. Batas berlaku untuk Upload per CHR Interface.

| License | Limit | Masa Berlaku |
| --- | --- | --- |
| Free | Limit 1 Mbit Upload per CHR Interface | — |
| P-Trial | Limit Trial 60 Days | Trial 60 Days |
| P1 Perpetual | Limit 1 Gbit Upload per CHR Interface | Lifetime |
| P10 Perpetual | Limit 10 Gbit Upload per CHR Interface | Lifetime |
| P-Unlimited | Unlimited Speed Upload per CHR Interface | Lifetime |

## 4. Prasyarat (Prerequisites)

- Server baru yang baru di-install direkomendasikan untuk menjalankan script ini.
- Program ini telah diuji pada Ubuntu Server 24.04 dan 26.04.
- Penggunaan program ini menjadi tanggung jawab masing-masing. Pastikan Repository sudah diperbarui dan Git sudah ter-install agar program berjalan maksimal.

```bash
sudo apt update
sudo apt install git -y
```

## 5. Instalasi (Installation)

**Langkah 1 — Clone repository:**

```bash
git clone https://github.com/anggrdwjy/MikrotikCHR-VPSUbuntuKVM.git
cd MikrotikCHR-VPSUbuntuKVM/
```

**Langkah 2 — Beri permission dan periksa isi direktori:**

```bash
chmod -R 777 *
ls -l
```

Contoh output:

```text
total 4
-rwxrwxrwx 1 root root 1328 Jan  3 10:22 install-mikrotik-6.49.sh
```

**Langkah 3 — Jalankan script instalasi:**

```bash
./install-mikrotik-6.49.sh
```

## 6. Cek Tipe Disk Sebelum Menjalankan Script (Check Disk Type Before Running Script)

Periksa Disk Type sebelum menjalankan script. Pastikan nama Disk sesuai dengan output `lsblk`.

```bash
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  30G  0 disk
├─sda1   8:1    0   1M  0 part
├─sda2   8:2    0  27G  0 part /
└─sda3   8:3    0   3G  0 part [SWAP]
```

Saat muncul prompt berikut, input Type Disk sesuai hasil pengecekan, contoh `sda`:

```text
==============================================
        INSTALL MIKROTIK ON UBUNTU VPS
==============================================

Input Type Your Disk : sda
```

## 7. Contoh Output Instalasi (Installation Output Example)

Ringkasan proses yang berjalan pada saat instalasi: update Repository, install `wget` dan `net-tools`, download image CHR, lalu write image ke Disk.

```text
Hit:1 http://id.archive.ubuntu.com/ubuntu noble InRelease
Get:4 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Fetched 219 kB in 2s

The following NEW packages will be installed:
  net-tools

--2026-01-03 10:23:42--  https://download.mikrotik.com/routeros/6.49.18/chr-6.49.18.img.zip
Saving to: 'chr.img.zip'
chr.img.zip  100% [================>]  32.67M   228KB/s    in 2m 16s
2026-01-03 10:26:00 (246 KB/s) - 'chr.img.zip' saved [34257478/34257478]

Device "eth0" does not exist.
65536+0 records in
65536+0 records out
67108864 bytes (67 MB, 64 MiB) copied, 1.42658 s, 47.0 MB/s

Broadcast message from root@ubuntu on pts/1 (Sat 2026-01-03 10:26:02 UTC):
The system will reboot now!
```

> Catatan: Output lengkap `apt` dan `wget` dipadatkan pada contoh di atas. Alur dan hasil akhir tetap sama.

## 8. Setelah Instalasi: Reboot

Lakukan Reboot setelah setup selesai.

```bash
reboot
```

## 9. Akses Remote (Remote Access)

Lakukan Remote SSH atau Telnet ke IP Address server setelah Reboot.

Default Login MikroTik:

| Item | Value |
| --- | --- |
| Username | `admin` |
| Password | Blank (kosong) |

Contoh tampilan awal setelah Login:

```text
  MMMM    MMMM       KKK                          TTTTTTTTTTT      KKK
  MMM MMMM MMM  III  KKK  KKK  RRRRRR     OOOOOO      TTT     III  KKK  KKK
  MMM  MM  MMM  III  KKKKK     RRR  RRR  OOO  OOO     TTT     III  KKKKK
  MMM      MMM  III  KKK KKK   RRRRRR    OOO  OOO     TTT     III  KKK KKK
  MMM      MMM  III  KKK  KKK  RRR  RRR   OOOOOO      TTT     III  KKK  KKK

  MikroTik RouterOS 6.49.18 (c) 1999-2025       http://www.mikrotik.com/

[?]             Gives the list of available commands
command [?]     Gives help on the command and list of arguments

[Tab]           Completes the command/word. If the input is ambiguous,
                a second [Tab] gives possible options

/               Move up to base level
..              Move up one level
/command        Use command at the base level

Change your password

new password>
[admin@MikroTik] >
```

> Setelah Login pertama, segera ganti Password Default.

## 10. Dukungan (Support)

- [:octocat: Follow me on GitHub](https://github.com/anggrdwjy)
- [🔔 Subscribe me on Youtube](https://www.youtube.com/@anggarda.wijaya)

## 11. Laporan Bug (Bugs)

Jika ditemukan Bug, buka Issue di GitHub dengan informasi selengkap mungkin:

- KVM atau VPS yang digunakan
- Semua Log dan Message Output
- Langkah reproduksi dan detail lainnya

## 12. Lisensi (License)

Project ini dilisensikan di bawah **MIT License** — bebas digunakan, dimodifikasi, dan didistribusikan, termasuk untuk keperluan komersial, selama menyertakan Copyright Notice dan License ini.

Lihat file lengkap di [`LICENSE`](LICENSE).
