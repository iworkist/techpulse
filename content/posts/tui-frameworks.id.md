---
title: "4 Cara Memberi \"Wajah\" GUI pada Terminal, dan Cerita Bisnis di Baliknya"
date: 2026-02-27
tags: ["TUI", "open-source", "Go", "Python", "Rust", "React"]
summary: "Empat framework TUI dengan total 100K+ GitHub stars. Teknologinya menarik, tapi strategi bisnis di baliknya lebih menarik lagi."
ShowToc: true
---

Terminal UI sedang naik daun lagi. Empat framework TUI dengan total GitHub stars lebih dari 100 ribu, yaitu Bubbletea (Go), Textual (Python), Ratatui (Rust), dan Ink (React), masing-masing memecahkan masalah yang sama dengan bahasa, arsitektur, dan model bisnis yang berbeda. Yang menarik justru bukan perbedaan teknisnya, tapi perbedaan strategi di balik masing-masing proyek. Ada yang dapat pendanaan venture capital, ada yang foundernya ambil sabbatical, ada juga yang memang dari awal tidak pernah berniat bikin perusahaan.

## Arsitektur Adalah Filosofi

Perbedaan paling mendasar dari keempat framework ini terletak pada satu pertanyaan: "siapa yang menguasai event loop?"

**Bubbletea** mengadopsi Elm Architecture (TEA) secara langsung. Cukup definisikan tiga fungsi, Init, Update, dan View, lalu framework yang mengurus sisanya. Event loop dimiliki sepenuhnya oleh framework, jadi developer cukup fokus pada state management saja. Ditambah keunggulan Go berupa kompilasi single binary dan concurrency berbasis goroutine, deployment jadi simpel dan performa untuk I/O-bound tasks sangat solid. Dengan 39.900+ GitHub stars dan lebih dari 18.000 aplikasi yang berjalan di atasnya, tool seperti Microsoft Azure Aztfy, TruffleHog, dan CockroachDB memilih Bubbletea justru karena kesederhanaannya.

**Ratatui** mengambil pendekatan sebaliknya. Immediate-mode rendering, artinya seluruh UI digambar ulang setiap frame. Event loop sepenuhnya di tangan developer. Kebebasannya tinggi, memang ada lebih banyak boilerplate, tapi ruang untuk optimasi juga jauh lebih besar. Dalam benchmark 1K datapoints/detik, Ratatui menunjukkan penghematan memori 30-40% dan CPU 15% dibanding Bubbletea. Pilihan yang tepat untuk monitoring tools atau environment embedded di mana resource sangat terbatas.

**Textual** membawa grammar frontend web ke dalam terminal. Component ala React, styling pakai CSS, dan rendering 120 FPS di atas library Rich. Fitur paling uniknya adalah `textual serve` yang memungkinkan aplikasi yang sama berjalan di web browser juga. Karena terintegrasi langsung dengan ekosistem Python (pandas, numpy, torch), Textual jadi pilihan ideal buat data scientist yang perlu bikin dashboard cepat. Download dari PyPI sudah menembus 250 ribu per kuartal.

**Ink** bahkan lebih berani. Framework ini me-retarget React renderer ke terminal. JSX, Hooks, Flexbox (via Yoga layout engine), semuanya bisa dipakai langsung. Kalau kamu sudah React developer, learning curve-nya praktis nol. Tapi karena harus membawa Node.js dan React runtime, ada overhead yang perlu diperhitungkan. Ink lebih cocok untuk interactive setup wizard atau dev tool UI dibanding CLI tool biasa. GitHub stars: 28.300+.

| Aspek | Bubbletea | Textual | Ratatui | Ink |
|-------|-----------|---------|---------|-----|
| Bahasa | Go | Python | Rust | React/Node |
| Arsitektur | Elm (TEA) | Component+CSS | Immediate-mode | React renderer |
| GitHub Stars | 39.900+ | 26.800+ | 12.700+ | 28.300+ |
| Keunggulan | Single binary, ekosistem | Web-ready, data stack | Resource minimal, kontrol penuh | Reuse skill React |
| Kelemahan | Harus pakai Go | Butuh runtime | Boilerplate banyak | Overhead Node.js |

## Kenapa Investasi di Terminal?

Yang lebih menarik dari teknologinya adalah spektrum model bisnisnya.

**Charm** (perusahaan di balik Bubbletea) memasang taruhan paling ambisius. Termasuk round 6 juta dolar yang dipimpin Google Gradient Ventures pada November 2023, total pendanaan mereka sudah sekitar 10 juta dolar. Strateginya adalah playbook open source klasik: bangun komunitas developer lewat framework gratis, lalu monetisasi lewat Charm Cloud (personal KV store, E2E encryption, sinkronisasi antar device) dan enterprise plan. Developer dari AWS, Shopify, Nvidia, dan GitHub sudah menggunakannya, jadi channel bottom-up sales sudah terbentuk. Penggunaan dasar tetap gratis, sementara monetisasi difokuskan pada enterprise dan usage-based pricing.

**Textualize** (di balik Textual) menunjukkan realita pahit startup open source. Will McGugan mendirikannya sendirian di Edinburgh pada 2021, dapat seed funding dari Costanoa, dan membayangkan SaaS yang menggabungkan framework Textual dengan web service. Tapi pada Mei 2025, setelah tiga tahun menanggung tekanan startup, Will memutuskan untuk sabbatical dan Textualize praktis berubah menjadi community project. Dari open source ke startup, lalu kembali ke komunitas. Ini jadi contoh nyata betapa sulitnya solo founder membangun revenue dari open source.

**Ratatui** dan **Ink** sama sekali tidak punya perusahaan di belakangnya. Ratatui lahir ketika proyek asli tui-rs berhenti di-maintain, lalu komunitas mem-fork dan menghidupkannya kembali. Tidak ada vendor lock-in, dan itu justru jadi kekuatan. Ink adalah proyek personal Vadim Demedes. Meski dipakai oleh Vercel dan lainnya, tidak ada model bisnis independen. Ink hidup sebagai turunan dari ekosistem React.

## Jadi, Pilih yang Mana?

Kriteria pemilihannya ternyata cukup straightforward. Kalau environment deployment kamu Go-friendly, pilih Bubbletea. Kalau workflow kamu banyak data analysis, Textual jawabannya. Kalau kamu di ranah systems programming atau punya resource constraint, Ratatui paling pas. Kalau tim kamu mayoritas React developer, Ink pilihan logis. Bukan soal framework mana yang "lebih bagus", tapi soal tech stack tim dan environment deployment yang menentukan jawaban.

Kalau dilihat dari gambaran besar, kebangkitan terminal UI ini adalah paradoks era cloud-native. Semua hal seolah bergerak ke web, tapi kenyataannya, mengelola server lewat satu sesi SSH itu tidak berubah. Dengan ledakan AI agent, container orchestration, dan DevOps tooling, kebutuhan akan "UI yang layak di terminal" justru makin besar. Inilah alasan Charm berani ambil dana VC, dan alasan Textualize pernah mencoba. Karena potensi pertumbuhan market ini nyata.

## Referensi
- [Bubbletea](https://github.com/charmbracelet/bubbletea)
- [Textual](https://github.com/Textualize/textual)
- [Ratatui](https://github.com/ratatui/ratatui)
- [Ink](https://github.com/vadimdemedes/ink)
