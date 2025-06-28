<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sebuah Pesan Untukmu</title>
    
    <!-- Menggunakan Tailwind CSS untuk styling yang cepat dan responsif -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Mengimpor font kustom dari Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Inter:wght@400;600&display=swap" rel="stylesheet">
    
    <style>
        /* CSS Kustom untuk elemen spesifik */
        body {
            /* Gradasi latar belakang yang lembut dan romantis */
            background: linear-gradient(135deg, #ffdde1, #ee9ca7);
            font-family: 'Inter', sans-serif;
        }

        /* Menetapkan font "Dancing Script" untuk kelas kustom */
        .font-dancing-script {
            font-family: 'Dancing Script', cursive;
        }

        /* Animasi untuk kartu utama */
        @keyframes pop-in {
            0% {
                opacity: 0;
                transform: scale(0.8) translateY(20px);
            }
            100% {
                opacity: 1;
                transform: scale(1) translateY(0);
            }
        }
        
        /* Animasi untuk teks */
        @keyframes fade-in-text {
            0% {
                opacity: 0;
                transform: translateY(15px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* Menerapkan animasi */
        .card-animation {
            animation: pop-in 0.8s ease-out forwards;
        }
        
        .text-animation {
            opacity: 0; /* Mulai dari transparan */
            animation: fade-in-text 0.7s ease-out forwards;
            /* Delay animasi agar muncul setelah kartu */
            animation-delay: 0.5s;
        }
        
        .button-animation {
             opacity: 0;
             animation: fade-in-text 0.7s ease-out forwards;
             animation-delay: 1.2s; /* Delay lebih lama untuk tombol */
        }
        
        /* Efek kelopak bunga yang berjatuhan */
        .petal {
            position: absolute;
            background-color: rgba(255, 192, 203, 0.7); /* Warna pink lembut */
            border-radius: 50% 0;
            width: 15px;
            height: 20px;
            animation: fall 10s linear infinite;
            top: -20px;
        }
        
        @keyframes fall {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }

        /* Animasi loading sederhana */
        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #ec4899; /* pink-500 */
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="overflow-hidden">
    <!-- Kontainer utama untuk kelopak bunga -->
    <div id="petal-container"></div>
    
    <!-- Kontainer untuk memusatkan konten -->
    <div class="flex items-center justify-center min-h-screen p-4">
        
        <!-- Kartu utama sebagai pusat perhatian -->
        <div id="card" class="card-animation relative w-full max-w-md bg-white/80 backdrop-blur-sm rounded-2xl shadow-xl p-8 text-center overflow-hidden transition-all duration-300">
            
            <!-- Elemen hati sebagai dekorasi -->
            <div class="absolute top-4 right-4 text-pink-400">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>
            </div>

            <div id="content">
                <!-- Ucapan utama dengan font romantis -->
                <p class="text-animation text-4xl md:text-5xl font-dancing-script text-pink-700 leading-tight">
                    "adee kamu ikutt akuu yaa sayaang nantii kondangan"
                </p>
                
                <!-- Tombol interaktif -->
                <div class="mt-10 button-animation flex flex-col sm:flex-row gap-4 justify-center">
                    <button id="yesButton" class="bg-pink-500 text-white font-bold py-3 px-6 rounded-full shadow-lg transform hover:scale-105 transition-all duration-300 ease-in-out">
                        Tentu, Aku Ikut!
                    </button>
                    <button id="geminiButton" class="bg-purple-500 text-white font-bold py-3 px-6 rounded-full shadow-lg transform hover:scale-105 transition-all duration-300 ease-in-out">
                        ✨ Buatkan Balasan Puitis
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // --- Script untuk kelopak bunga berjatuhan ---
        const petalContainer = document.getElementById('petal-container');
        const numberOfPetals = 20; // Jumlah kelopak bunga

        for (let i = 0; i < numberOfPetals; i++) {
            const petal = document.createElement('div');
            petal.className = 'petal';
            
            petal.style.left = Math.random() * 100 + 'vw';
            petal.style.animationDuration = Math.random() * 5 + 5 + 's';
            petal.style.animationDelay = Math.random() * 10 + 's';
            
            const size = Math.random() * 10 + 10;
            petal.style.width = size + 'px';
            petal.style.height = size * 1.2 + 'px';
            
            petalContainer.appendChild(petal);
        }

        // --- Variabel elemen ---
        const yesButton = document.getElementById('yesButton');
        const geminiButton = document.getElementById('geminiButton');
        const cardContent = document.getElementById('content');
        const card = document.getElementById('card');

        // --- Event Listener untuk Tombol 'Ya' ---
        yesButton.addEventListener('click', () => {
            cardContent.innerHTML = `
                <div class="text-animation" style="animation-delay: 0s;">
                    <p class="text-3xl font-dancing-script text-pink-700">Yeay! Sampai ketemu nanti yaa, sayang ❤️</p>
                    <div class="mt-6 text-5xl">🥰</div>
                </div>
            `;
            card.style.boxShadow = '0 0 30px 10px rgba(255, 105, 180, 0.5)';
        });
        
        // --- Event Listener untuk Tombol Gemini ---
        geminiButton.addEventListener('click', async () => {
            // Tampilkan status loading
            cardContent.innerHTML = `
                <div class="text-animation" style="animation-delay: 0s;">
                    <p class="text-xl font-semibold text-purple-700">Merangkai kata terindah untukmu...</p>
                    <div class="loader"></div>
                </div>
            `;

            // Prompt untuk Gemini API
            const prompt = "Buatkan sebuah balasan puitis yang sangat romantis dan singkat dari 'adee' yang menerima ajakan untuk pergi ke kondangan. Buat seolah-olah dia sangat senang dan tidak sabar.";
            const chatHistory = [{ role: "user", parts: [{ text: prompt }] }];
            const payload = { contents: chatHistory };
            const apiKey = ""; // Kunci API akan disediakan secara otomatis oleh lingkungan
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

            try {
                // Panggil Gemini API
                const response = await fetch(apiUrl, {
                     method: 'POST',
                     headers: { 'Content-Type': 'application/json' },
                     body: JSON.stringify(payload)
                });
                
                if (!response.ok) {
                    throw new Error(`API error: ${response.statusText}`);
                }
                
                const result = await response.json();

                // Pastikan respons memiliki struktur yang diharapkan
                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    
                    const poem = result.candidates[0].content.parts[0].text;

                    // Tampilkan puisi yang dihasilkan
                    cardContent.innerHTML = `
                        <div class="text-animation" style="animation-delay: 0s;">
                             <p class="text-2xl md:text-3xl font-dancing-script text-purple-800 leading-relaxed whitespace-pre-wrap">${poem}</p>
                             <div class="mt-6 text-5xl">💖</div>
                        </div>
                    `;
                    card.style.boxShadow = '0 0 30px 10px rgba(192, 132, 252, 0.5)'; // Efek glow ungu

                } else {
                    throw new Error("Struktur respons tidak valid dari API.");
                }

            } catch (error) {
                console.error("Error calling Gemini API:", error);
                // Tampilkan pesan error kepada pengguna
                cardContent.innerHTML = `
                    <div class="text-animation" style="animation-delay: 0s;">
                        <p class="text-xl font-semibold text-red-500">Oops! Sepertinya ada sedikit kendala.</p>
                        <p class="text-gray-600 mt-2">Coba lagi sesaat lagi ya.</p>
                    </div>
                `;
            }
        });
    </script>
</body>
</html>
