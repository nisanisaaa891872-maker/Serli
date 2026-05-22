# Serli<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Warna Favorit Sesuai Perasaan</title>
    <style>
        /* --- GAYA DASAR --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f0fdf4; /* Dominan Hijau Mint Muda */
            color: #166534; /* Teks Hijau Tua */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden; /* Mencegah scrollbar muncul saat tombol lari */
            transition: background-color 0.8s ease; /* Efek transisi halus saat warna perasaan muncul */
        }

        /* --- WADAH UTAMA (CARD) --- */
        .card {
            background-color: #ffffff; /* Dominan Putih */
            padding: 2.5rem;
            border-radius: 24px;
            box-shadow: 0 10px 30px rgba(22, 101, 52, 0.15);
            text-align: center;
            max-width: 450px;
            width: 90%;
            border: 2px solid #bbf7d0;
            z-index: 5;
            transition: transform 0.3s ease;
        }

        /* --- STIKER ANIMASI --- */
        .sticker-container {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 1.5rem;
        }

        .sticker {
            font-size: 3.5rem;
            display: inline-block;
            animation: float 3s ease-in-out infinite;
        }

        /* Efek gerak stiker yang bervariasi */
        .sticker:nth-child(2) { animation-delay: 0.5s; }
        .sticker:nth-child(3) { animation-delay: 1s; }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-12px) rotate(5deg); }
        }

        /* --- TIPOGRAFI --- */
        h1 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            color: #15803d;
            transition: color 0.5s ease;
        }

        p {
            font-size: 1.1rem;
            line-height: 1.6;
            margin-bottom: 2rem;
            color: #4b5563;
            transition: color 0.5s ease;
        }

        #message-display {
            font-weight: 600;
            min-height: 60px;
        }

        /* --- AREA TOMBOL --- */
        .btn-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            min-height: 60px;
            align-items: center;
        }

        .btn {
            padding: 0.8rem 2.2rem;
            font-size: 1rem;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.1s ease, box-shadow 0.15s ease;
        }

        .btn:active {
            transform: scale(0.95);
        }

        #btn-oke {
            background-color: #16a34a; /* Hijau Utama */
            color: white;
            box-shadow: 0 4px 14px rgba(22, 163, 74, 0.3);
        }

        #btn-oke:hover {
            background-color: #15803d;
            box-shadow: 0 6px 20px rgba(21, 128, 61, 0.4);
        }

        #btn-tidak {
            background-color: #ffffff;
            color: #b91c1c;
            border: 2px solid #fca5a5;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            z-index: 100; /* Memastikan tombol tidak berada di atas komponen penting */
        }
    </style>
</head>
<body>

    <div class="card">
        <!-- Stiker Pendukung Tema Perasaan & Warna (Palet lukis, hati, & ekspresi ceria) -->
        <div class="sticker-container">
            <span class="sticker" id="sticker-1">🎨</span>
            <span class="sticker" id="sticker-2">💖</span>
            <span class="sticker" id="sticker-3">🥳</span>
        </div>

        <h1 id="title">Halo, Kamu! ✨</h1>
        <p id="message-display">Mau tahu warna keberuntungan dan pesan favorit yang sesuai dengan perasaanmu hari ini?</p>

        <div class="btn-container">
            <button class="btn" id="btn-oke">Oke!</button>
            <button class="btn" id="btn-tidak">Tidak</button>
        </div>
    </div>

    <script>
        const btnOke = document.getElementById('btn-oke');
        const btnTidak = document.getElementById('btn-tidak');
        const messageDisplay = document.getElementById('message-display');
        const titleText = document.getElementById('title');
        
        // Elemen stiker untuk diganti sesuai warna perasaan nantinya
        const s1 = document.getElementById('sticker-1');
        const s2 = document.getElementById('sticker-2');
        const s3 = document.getElementById('sticker-3');

        // Data emosi, warna latar, warna teks, stiker, dan pesan positif
        const dataPerasaan = [
            {
                emosi: "Gembira & Optimis",
                bg: "#fef08a", // Kuning Cerah
                teks: "#854d0e",
                stikers: ["💛", "☀️", "👑"],
                pesan: "Hari ini harimu! Warna Kuning memancarkan energi positif. Teruslah bersinar dan sebarkan kebahagiaan ke orang sekitarmu! ☀️"
            },
            {
                emosi: "Damai & Tenang",
                bg: "#bfdbfe", // Biru Langit
                teks: "#1e3a8a",
                stikers: ["💙", "🌊", "🕊️"],
                pesan: "Warna Biru membawa ketenangan jiwa. Ambil napas dalam-dalam, nikmati momen ini, semua hal baik sedang berjalan menuju arahmu. 🌊"
            },
            {
                emosi: "Penuh Cinta & Semangat",
                bg: "#fecdd3", // Merah Muda / Pink Soft
                teks: "#9f1239",
                stikers: ["❤️", "🌸", "🌹"],
                pesan: "Warna Merah Muda melambangkan kasih sayang. Jangan lupa untuk mencintai dirimu sendiri terlebih dahulu sebelum membagikannya kepada dunia! 🌸"
            },
            {
                emosi: "Kreatif & Berani",
                bg: "#e9d5ff", // Ungu Lavender
                teks: "#581c87",
                stikers: ["💜", "🔮", "🦄"],
                pesan: "Warna Ungu memicu keajaiban dan imajinasi. Percayalah pada ide-ide unikmu hari ini, buat sesuatu yang luar biasa! 🔮"
            },
            {
                emosi: "Segar & Bertumbuh",
                bg: "#bbf7d0", // Hijau Terang
                teks: "#14532d",
                stikers: ["💚", "🍀", "🚀"],
                pesan: "Warna Hijau menandakan pertumbuhan baru. Setiap langkah kecil yang kamu ambil hari ini membawamu lebih dekat ke impianmu! 🍀"
            }
        ];

        // --- 1. LOGIKA TOMBOL 'TIDAK' (LARI DARI KURSOR) ---
        function tombolLari() {
            // Jarak aman agar tombol tidak melompat terlalu dekat atau keluar dari ujung layar browser
            const batasAman = 130; 
            const xAcak = Math.random() * (window.innerWidth - batasAman);
            const yAcak = Math.random() * (window.innerHeight - batasAman);

            // Mengubah posisi secara instan memanfaatkan koordinat layar browser
            btnTidak.style.position = 'fixed';
            btnAgainstScreenBoundary(xAcak, yAcak);
        }

        // Fungsi pembantu untuk memastikan posisi diterapkan dengan benar
        function btnAgainstScreenBoundary(x, y) {
            btnTidak.style.left = `${x}px`;
            btnTidak.style.top = `${y}px`;
        }

        // Memicu tombol lari saat didekati mouse (PC) atau disentuh jari (HP)
        btnTidak.addEventListener('mouseover', tombolLari);
        btnTidak.addEventListener('touchstart', (e) => {
            e.preventDefault(); // Mencegah klik bawaan perangkat seluler saat disentuh pertama kali
            tombolLari();
        });


        // --- 2. LOGIKA TOMBOL 'OKE' (MEMUNCULKAN WARNA PERASAAN) ---
        btnOke.addEventListener('click', () => {
            // Mengambil satu data perasaan acak
            const acak = Math.floor(Math.random() * dataPerasaan.length);
            const hasil = dataPerasaan[acak];

            // Mengubah warna background seluruh halaman browser
            document.body.style.backgroundColor = hasil.bg;
            document.body.style.color = hasil.teks;

            // Mengubah teks informasi di dalam kartu
            titleText.innerText = `Suasana Hati: ${hasil.emosi}`;
            titleText.style.color = hasil.teks;
            
            messageDisplay.innerHTML = hasil.pesan;
            messageDisplay.style.color = hasil.teks;

            // Memperbarui stiker sesuai warna perasaan yang terpilih
            s1.innerText = hasil.stikers[0];
            s2.innerText = hasil.stikers[1];
            s3.innerText = hasil.stikers[2];

            // Mengembalikan tombol 'Tidak' ke posisi semula jika sebelumnya sempat lari
            btnTidak.style.position = 'relative';
            btnTidak.style.left = 'auto';
            btnTidak.style.top = 'auto';
        });
    </script>

</body>
</html>
