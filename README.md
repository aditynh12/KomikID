<!DOCTYPE html>
<html lang="id" class="h-full dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ComicVault – Luxury Manga & Manhwa Tracker</title>
    <!-- Tailwind CSS v4 CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- FontAwesome Pro / Free Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Plus Jakarta Sans & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', 'Inter', sans-serif;
            background-color: #030712;
            color: #f8fafc;
            overflow-x: hidden;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #090d16;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #334155;
        }
        .glass-panel {
            background: rgba(15, 23, 42, 0.65);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.07);
        }
        .glass-card {
            background: linear-gradient(135deg, rgba(30, 41, 59, 0.5) 0%, rgba(15, 23, 42, 0.7) 100%);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .card-lift {
            transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.3s ease, border-color 0.3s ease;
        }
        .card-lift:hover {
            transform: translateY(-6px);
            box-shadow: 0 20px 30px -10px rgba(99, 102, 241, 0.25);
            border-color: rgba(99, 102, 241, 0.4);
        }
        @keyframes pulseGlow {
            0%, 100% { opacity: 0.4; }
            50% { opacity: 0.8; }
        }
        .animate-glow {
            animation: pulseGlow 4s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
    </style>
</head>
<body class="min-h-full flex flex-col selection:bg-indigo-600 selection:text-white">

    <div class="fixed inset-0 pointer-events-none overflow-hidden z-0">
        <div class="absolute -top-40 -left-40 w-96 h-96 bg-indigo-600/15 rounded-full blur-[120px] animate-glow"></div>
        <div class="absolute top-1/3 -right-40 w-96 h-96 bg-violet-600/15 rounded-full blur-[140px] animate-glow" style="animation-delay: 2s;"></div>
        <div class="absolute -bottom-40 left-1/4 w-96 h-96 bg-fuchsia-600/10 rounded-full blur-[150px]"></div>
    </div>

    <header class="sticky top-0 z-40 glass-panel border-b border-slate-800/80 shadow-2xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div class="flex items-center space-x-4">
                <div class="relative group">
                    <div class="absolute -inset-1 bg-gradient-to-r from-indigo-500 to-violet-600 rounded-2xl blur opacity-70 group-hover:opacity-100 transition duration-300"></div>
                    <div class="relative bg-slate-900 border border-slate-700/60 p-3 rounded-2xl flex items-center justify-center text-indigo-400 shadow-xl">
                        <i class="fa-solid fa-book-bookmark text-xl"></i>
                    </div>
                </div>
                <div>
                    <h1 class="font-extrabold text-xl tracking-tight bg-gradient-to-r from-white via-slate-100 to-slate-400 bg-clip-text text-transparent flex items-center gap-2">
                        ComicVault <span class="text-xs px-2 py-0.5 rounded-full bg-indigo-500/20 text-indigo-300 border border-indigo-500/30 font-semibold tracking-wide">PRO v2.5</span>
                    </h1>
                    <p class="text-xs text-slate-400 font-medium tracking-wide">Ultimate Offline Manga & Manhwa Tracker</p>
                </div>
            </div>
            
            <div class="flex items-center gap-3">
                <button onclick="openAiModal()" class="group relative inline-flex items-center gap-2 px-4 py-2.5 rounded-2xl font-semibold text-sm text-indigo-300 bg-indigo-950/60 hover:bg-indigo-900/80 border border-indigo-500/30 shadow-lg shadow-indigo-950/50 active:scale-95 transition-all cursor-pointer">
                    <i class="fa-solid fa-wand-magic-sparkles text-indigo-400"></i>
                    <span>ComicVault AI</span>
                </button>
                <button onclick="openModal()" class="group relative inline-flex items-center gap-2 px-5 py-2.5 rounded-2xl font-semibold text-sm text-white bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 shadow-lg shadow-indigo-600/30 active:scale-95 transition-all cursor-pointer overflow-hidden border border-indigo-400/30">
                    <span class="absolute inset-0 w-full h-full bg-white/10 group-hover:translate-x-full transition-transform duration-500 ease-out"></span>
                    <i class="fa-solid fa-plus text-xs"></i>
                    <span>Tambah Komik</span>
                </button>
            </div>
        </div>
    </header>

    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8 relative z-10">
        
        <!-- Interactive Stat Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <div class="glass-card rounded-3xl p-5 flex items-center justify-between shadow-xl relative overflow-hidden group">
                <div class="absolute -right-6 -bottom-6 w-24 h-24 bg-indigo-500/10 rounded-full blur-xl group-hover:scale-150 transition-transform"></div>
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Total Koleksi</p>
                    <h3 id="statTotal" class="text-3xl font-extrabold mt-1.5 text-white">0</h3>
                    <p class="text-[11px] text-indigo-300 mt-1 flex items-center gap-1 font-medium"><i class="fa-solid fa-layer-group"></i> Seluruh judul tersimpan</p>
                </div>
                <div class="p-3.5 bg-gradient-to-br from-indigo-500/20 to-indigo-500/5 border border-indigo-500/30 text-indigo-400 rounded-2xl shadow-inner">
                    <i class="fa-solid fa-book text-xl"></i>
                </div>
            </div>

            <div class="glass-card rounded-3xl p-5 flex items-center justify-between shadow-xl relative overflow-hidden group">
                <div class="absolute -right-6 -bottom-6 w-24 h-24 bg-emerald-500/10 rounded-full blur-xl group-hover:scale-150 transition-transform"></div>
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Sedang Dibaca</p>
                    <h3 id="statActive" class="text-3xl font-extrabold mt-1.5 text-emerald-400">0</h3>
                    <p class="text-[11px] text-emerald-300 mt-1 flex items-center gap-1 font-medium"><i class="fa-solid fa-spinner"></i> Berjalan aktif</p>
                </div>
                <div class="p-3.5 bg-gradient-to-br from-emerald-500/20 to-emerald-500/5 border border-emerald-500/30 text-emerald-400 rounded-2xl shadow-inner">
                    <i class="fa-solid fa-book-reader text-xl"></i>
                </div>
            </div>

            <div class="glass-card rounded-3xl p-5 flex items-center justify-between shadow-xl relative overflow-hidden group">
                <div class="absolute -right-6 -bottom-6 w-24 h-24 bg-violet-500/10 rounded-full blur-xl group-hover:scale-150 transition-transform"></div>
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Tamat / Selesai</p>
                    <h3 id="statCompleted" class="text-3xl font-extrabold mt-1.5 text-violet-400">0</h3>
                    <p class="text-[11px] text-violet-300 mt-1 flex items-center gap-1 font-medium"><i class="fa-solid fa-circle-check"></i> Telah diselesaikan</p>
                </div>
                <div class="p-3.5 bg-gradient-to-br from-violet-500/20 to-violet-500/5 border border-violet-500/30 text-violet-400 rounded-2xl shadow-inner">
                    <i class="fa-solid fa-trophy text-xl"></i>
                </div>
            </div>

            <div class="glass-card rounded-3xl p-5 flex items-center justify-between shadow-xl relative overflow-hidden group">
                <div class="absolute -right-6 -bottom-6 w-24 h-24 bg-amber-500/10 rounded-full blur-xl group-hover:scale-150 transition-transform"></div>
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Terakhir Update</p>
                    <h3 id="statLastUpdate" class="text-xs font-bold mt-2 text-slate-200 truncate max-w-[160px]">-</h3>
                    <p class="text-[11px] text-amber-300 mt-1 flex items-center gap-1 font-medium"><i class="fa-solid fa-clock-rotate-left"></i> Aktivitas pembaca</p>
                </div>
                <div class="p-3.5 bg-gradient-to-br from-amber-500/20 to-amber-500/5 border border-amber-500/30 text-amber-400 rounded-2xl shadow-inner">
                    <i class="fa-solid fa-bolt text-xl"></i>
                </div>
            </div>
        </div>

        <!-- Toolbar: Search, Status Filter, Backup/Restore, View Switcher -->
        <div class="glass-panel p-4 sm:p-5 rounded-3xl flex flex-col md:flex-row gap-4 items-center justify-between shadow-xl">
            <div class="flex flex-col sm:flex-row gap-3 w-full md:w-auto items-center">
                <!-- Search Input -->
                <div class="relative w-full sm:w-80">
                    <span class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none text-slate-400">
                        <i class="fa-solid fa-magnifying-glass text-sm"></i>
                    </span>
                    <input type="text" id="searchInput" oninput="handleSearch()" placeholder="Cari judul manga / manhwa..." 
                        class="w-full pl-11 pr-4 py-3 bg-slate-950/80 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-500 transition-all shadow-inner">
                </div>
                <!-- Status Category Filter Tabs -->
                <div class="flex bg-slate-950/80 p-1.5 rounded-2xl border border-slate-800/80 w-full sm:w-auto overflow-x-auto">
                    <button onclick="setStatusFilter('All')" id="statusAll" class="px-4 py-2 text-xs font-semibold rounded-xl transition-all cursor-pointer whitespace-nowrap bg-indigo-600 text-white shadow-sm">Semua</button>
                    <button onclick="setStatusFilter('Reading')" id="statusReading" class="px-4 py-2 text-xs font-semibold rounded-xl transition-all cursor-pointer whitespace-nowrap text-slate-400 hover:text-white">Dibaca</button>
                    <button onclick="setStatusFilter('Completed')" id="statusCompletedBtn" class="px-4 py-2 text-xs font-semibold rounded-xl transition-all cursor-pointer whitespace-nowrap text-slate-400 hover:text-white">Selesai</button>
                    <button onclick="setStatusFilter('On-Hold')" id="statusOnHold" class="px-4 py-2 text-xs font-semibold rounded-xl transition-all cursor-pointer whitespace-nowrap text-slate-400 hover:text-white">Ditunda</button>
                </div>
            </div>

            <!-- Actions & View Switcher -->
            <div class="flex items-center gap-2.5 w-full md:w-auto justify-end flex-wrap">
                <button onclick="exportData()" class="px-3.5 py-2.5 text-xs font-semibold bg-slate-800/80 hover:bg-slate-700 text-slate-300 rounded-2xl transition-all border border-slate-700/60 flex items-center gap-2 cursor-pointer shadow-sm" title="Backup JSON">
                    <i class="fa-solid fa-cloud-arrow-down text-indigo-400"></i> Backup
                </button>
                <label class="px-3.5 py-2.5 text-xs font-semibold bg-slate-800/80 hover:bg-slate-700 text-slate-300 rounded-2xl transition-all border border-slate-700/60 flex items-center gap-2 cursor-pointer shadow-sm" title="Restore JSON">
                    <i class="fa-solid fa-cloud-arrow-up text-violet-400"></i> Restore <input type="file" id="importFile" onchange="importData(event)" accept=".json" class="hidden">
                </label>
                <div class="h-6 w-px bg-slate-800 mx-1 hidden sm:block"></div>
                <div class="flex bg-slate-950/80 p-1.5 rounded-2xl border border-slate-800/80">
                    <button onclick="setViewMode('poster')" id="viewPosterBtn" class="p-2.5 text-sm bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm" title="Poster Grid (Cinematic)">
                        <i class="fa-solid fa-film"></i>
                    </button>
                    <button onclick="setViewMode('grid')" id="viewGridBtn" class="p-2.5 text-sm bg-slate-900 text-slate-400 hover:text-white rounded-xl transition-all cursor-pointer" title="Card Grid">
                        <i class="fa-solid fa-grip"></i>
                    </button>
                    <button onclick="setViewMode('table')" id="viewTableBtn" class="p-2.5 text-sm bg-slate-900 text-slate-400 hover:text-white rounded-xl transition-all cursor-pointer" title="Compact Table">
                        <i class="fa-solid fa-table-list"></i>
                    </button>
                </div>
            </div>
        </div>

        <div class="glass-panel p-4 sm:p-5 rounded-3xl shadow-xl space-y-3">
            <div class="flex items-center justify-between">
                <div>
                    <h3 class="text-sm font-bold text-white flex items-center gap-2">
                        <i class="fa-solid fa-filter text-indigo-400"></i> Filter Abjad Judul Komik
                    </h3>
                    <p class="text-[11px] text-slate-400">Klik huruf awal untuk menyaring koleksi instan</p>
                </div>
                <button onclick="setLetterFilter('')" id="letterAllBtn"
                    class="px-4 py-1.5 text-xs font-bold bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm">
                    Semua Huruf
                </button>
            </div>
            <div id="alphabetFilter" class="flex flex-wrap gap-1.5 sm:gap-2 pt-1"></div>
        </div>

        <div id="comicContainer" class="min-h-[300px]">
            <!-- Dynamic items rendered here -->
        </div>
    </main>

    <!-- AI Assistant Modal -->
    <div id="aiModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-950/80 backdrop-blur-md hidden transition-all duration-300">
        <div class="glass-panel border border-indigo-500/30 rounded-3xl w-full max-w-2xl overflow-hidden shadow-2xl scale-95 transition-transform duration-300 flex flex-col max-h-[85vh]" id="aiModalBox">
            <div class="px-6 py-5 border-b border-slate-800/80 flex items-center justify-between bg-slate-900/60">
                <div class="flex items-center gap-3">
                    <div class="p-2.5 bg-indigo-500/20 border border-indigo-500/30 text-indigo-300 rounded-2xl shadow-inner">
                        <i class="fa-solid fa-wand-magic-sparkles text-lg"></i>
                    </div>
                    <div>
                        <h3 class="font-bold text-lg text-white flex items-center gap-2">ComicVault AI <span class="text-[10px] px-2 py-0.5 bg-indigo-500/20 text-indigo-300 rounded-full border border-indigo-500/30">Gemini 3 Flash</span></h3>
                        <p class="text-xs text-slate-400">Asisten cerdas berbasis AI untuk analisis & rekomendasi manga</p>
                    </div>
                </div>
                <button onclick="closeAiModal()" class="text-slate-400 hover:text-white p-2.5 rounded-xl hover:bg-slate-800 transition-all cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <div class="p-6 space-y-4 overflow-y-auto flex-grow">
                <!-- AI Feature Tabs -->
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-2 bg-slate-950/80 p-2 rounded-2xl border border-slate-800">
                    <button onclick="setAiTab('recommend')" id="aiTabRecommend" class="py-2.5 px-3 rounded-xl text-xs font-bold transition-all bg-indigo-600 text-white shadow-sm flex items-center justify-center gap-2 cursor-pointer">
                        <i class="fa-solid fa-compass"></i> Rekomendasi Pintar
                    </button>
                    <button onclick="setAiTab('synopsis')" id="aiTabSynopsis" class="py-2.5 px-3 rounded-xl text-xs font-semibold transition-all text-slate-400 hover:text-white flex items-center justify-center gap-2 cursor-pointer">
                        <i class="fa-solid fa-book-open-reader"></i> Ringkasan Judul
                    </button>
                    <button onclick="setAiTab('chat')" id="aiTabChat" class="py-2.5 px-3 rounded-xl text-xs font-semibold transition-all text-slate-400 hover:text-white flex items-center justify-center gap-2 cursor-pointer">
                        <i class="fa-solid fa-comments"></i> Tanya AI Bebas
                    </button>
                </div>

                <!-- Tab 1: Recommendation Generator -->
                <div id="aiSectionRecommend" class="space-y-4">
                    <p class="text-xs text-slate-300">Analisis koleksi bacaan Anda saat ini dan dapatkan rekomendasi komik serupa yang sedang tren atau legendaris.</p>
                    <button onclick="generateAiRecommendations()" id="aiRecBtn" class="w-full py-3 px-4 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white rounded-2xl text-sm font-bold shadow-lg shadow-indigo-600/30 transition-all cursor-pointer flex items-center justify-center gap-2">
                        <i class="fa-solid fa-brain"></i> Analisis Koleksi & Buat Rekomendasi
                    </button>
                </div>

                <!-- Tab 2: Synopsis / Lore Helper -->
                <div id="aiSectionSynopsis" class="space-y-4 hidden">
                    <div>
                        <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1.5">Pilih atau Ketik Judul Manga/Manhwa</label>
                        <input type="text" id="aiQueryTitle" placeholder="Contoh: Solo Leveling, One Piece, Tower of God..." 
                            class="w-full px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600 shadow-inner">
                    </div>
                    <button onclick="generateAiSynopsis()" id="aiSynBtn" class="w-full py-3 px-4 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white rounded-2xl text-sm font-bold shadow-lg shadow-indigo-600/30 transition-all cursor-pointer flex items-center justify-center gap-2">
                        <i class="fa-solid fa-magnifying-glass-chart"></i> Cari Ringkasan & Karakter Utama
                    </button>
                </div>

                <!-- Tab 3: Free Chat -->
                <div id="aiSectionChat" class="space-y-3 hidden">
                    <div id="aiChatBox" class="h-56 bg-slate-950/80 border border-slate-800 rounded-2xl p-4 overflow-y-auto space-y-3 text-sm">
                        <div class="flex items-start gap-2.5">
                            <div class="w-7 h-7 rounded-full bg-indigo-600 flex items-center justify-center text-white text-xs shrink-0 font-bold">AI</div>
                            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-3 text-slate-200 text-xs leading-relaxed max-w-[85%]">
                                Halo! Saya asisten ComicVault AI. Tanyakan apa saja tentang manga, manhwa, teori alur cerita, atau jadwal rilis!
                            </div>
                        </div>
                    </div>
                    <div class="flex gap-2">
                        <input type="text" id="aiChatInput" onkeypress="if(event.key==='Enter') sendAiChat()" placeholder="Tanya tentang manga..." 
                            class="flex-grow px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600 shadow-inner">
                        <button onclick="sendAiChat()" class="px-5 py-3 bg-indigo-600 hover:bg-indigo-500 text-white rounded-2xl text-sm font-bold shadow-md transition-all cursor-pointer">
                            <i class="fa-solid fa-paper-plane"></i>
                        </button>
                    </div>
                </div>

                <!-- AI Output Display Box -->
                <div id="aiOutputContainer" class="hidden space-y-2 pt-2">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-bold uppercase tracking-wider text-indigo-400 flex items-center gap-1.5"><i class="fa-solid fa-robot"></i> Hasil Analisis AI:</span>
                        <button onclick="copyAiOutput()" class="text-xs text-slate-400 hover:text-white bg-slate-800/80 px-2.5 py-1 rounded-xl border border-slate-700/60 transition-all cursor-pointer"><i class="fa-solid fa-copy mr-1"></i> Salin</button>
                    </div>
                    <div id="aiOutputContent" class="bg-slate-950/90 border border-slate-800 rounded-2xl p-4 text-sm text-slate-200 leading-relaxed max-h-60 overflow-y-auto"></div>
                </div>
            </div>

            <div class="px-6 py-4 border-t border-slate-800/80 flex items-center justify-end bg-slate-900/40">
                <button onclick="closeAiModal()" class="px-5 py-2.5 text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition-all cursor-pointer">Tutup</button>
            </div>
        </div>
    </div>

    <div id="comicModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-950/80 backdrop-blur-md hidden transition-all duration-300">
        <div class="glass-panel border border-slate-700/80 rounded-3xl w-full max-w-lg overflow-hidden shadow-2xl scale-95 transition-transform duration-300" id="modalBox">
            <div class="px-6 py-5 border-b border-slate-800/80 flex items-center justify-between bg-slate-900/40">
                <div class="flex items-center gap-3">
                    <div class="p-2.5 bg-indigo-500/10 border border-indigo-500/20 text-indigo-400 rounded-2xl">
                        <i class="fa-solid fa-book-medical text-lg"></i>
                    </div>
                    <h3 id="modalTitle" class="font-bold text-lg text-white">Tambah Komik Baru</h3>
                </div>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white p-2.5 rounded-xl hover:bg-slate-800 transition-all cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            
            <form id="comicForm" onsubmit="saveComic(event)" class="p-6 space-y-4 max-h-[80vh] overflow-y-auto">
                <input type="hidden" id="comicId">
                <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1.5">Judul Komik / Manhwa</label>
                    <input type="text" id="formTitle" required placeholder="Contoh: Solo Leveling, Omniscient Reader..." 
                        class="w-full px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600 shadow-inner">
                </div>
                <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1.5">Link Website Baca (URL)</label>
                    <input type="url" id="formUrl" required placeholder="https://example.com/komik/chapter-1" 
                        class="w-full px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600 shadow-inner">
                    <p class="text-[11px] text-indigo-300/80 mt-1.5 flex items-center gap-1 font-medium"><i class="fa-solid fa-circle-info"></i> URL otomatis memperbarui nomor chapter saat Anda menaikkan/menurunkan chapter.</p>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1.5">Chapter Terakhir</label>
                        <input type="number" step="0.5" id="formChapter" required placeholder="1" min="0" 
                            class="w-full px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600 shadow-inner">
                    </div>
                    <div>
                        <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1.5">Status Membaca</label>
                        <select id="formStatus" class="w-full px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 shadow-inner">
                            <option value="Reading">Sedang Dibaca</option>
                            <option value="Completed">Tamat / Selesai</option>
                            <option value="On-Hold">Ditunda</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1.5">URL Cover Poster (Opsional)</label>
                    <input type="url" id="formCover" placeholder="https://images.unsplash.com/..." oninput="previewCover()"
                        class="w-full px-4 py-3 bg-slate-950/90 border border-slate-800 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600 shadow-inner">
                </div>
                
                <!-- Live Cover Preview Box -->
                <div id="coverPreviewContainer" class="hidden pt-2">
                    <p class="text-[11px] text-slate-400 mb-2 font-semibold">Pratinjau Cover:</p>
                    <div class="h-36 w-24 rounded-xl overflow-hidden border border-slate-700 shadow-md">
                        <img id="formCoverPreview" src="" alt="Preview" class="w-full h-full object-cover">
                    </div>
                </div>

                <div class="pt-4 flex items-center justify-end gap-3 border-t border-slate-800/80">
                    <button type="button" onclick="closeModal()" class="px-5 py-3 text-sm font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-2xl transition-all cursor-pointer">Batal</button>
                    <button type="submit" class="px-6 py-3 text-sm font-semibold bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white rounded-2xl shadow-lg shadow-indigo-600/30 transition-all cursor-pointer">Simpan Komik</button>
                </div>
            </form>
        </div>
    </div>

    <div id="toast" class="fixed bottom-6 right-6 z-50 translate-y-24 opacity-0 transition-all duration-300 glass-panel border border-slate-700/80 shadow-2xl px-5 py-4 rounded-2xl flex items-center gap-3.5">
        <div id="toastIcon" class="text-emerald-400 text-xl"></div>
        <div>
            <h4 class="text-xs font-bold text-slate-400 uppercase tracking-wider">ComicVault System</h4>
            <div id="toastMessage" class="text-sm font-semibold text-slate-100"></div>
        </div>
    </div>

    <script>
        // Initial Database Store with Cinematic Sample Data
        let comics = JSON.parse(localStorage.getItem('comicvault_luxury_comics')) || [
            {
                id: '1',
                title: 'Solo Leveling',
                url: 'https://asurascans.com/manga/solo-leveling/chapter-179/',
                chapter: 179,
                status: 'Completed',
                cover: 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=600&auto=format&fit=crop',
                updatedAt: new Date().toISOString()
            },
            {
                id: '2',
                title: 'Omniscient Reader’s Viewpoint',
                url: 'https://flamescans.org/manga/omniscient-readers-viewpoint-chapter-195/',
                chapter: 195,
                status: 'Reading',
                cover: 'https://images.unsplash.com/photo-1534447677768-be436bb09401?q=80&w=600&auto=format&fit=crop',
                updatedAt: new Date(Date.now() - 3600000).toISOString()
            },
            {
                id: '3',
                title: 'The Beginning After The End',
                url: 'https://asurascans.com/manga/tbate-chapter-175/',
                chapter: 175,
                status: 'Reading',
                cover: 'https://images.unsplash.com/photo-1579546929518-9e396f3cc809?q=80&w=600&auto=format&fit=crop',
                updatedAt: new Date(Date.now() - 86400000).toISOString()
            }
        ];

        let viewMode = 'poster'; // 'poster', 'grid', 'table'
        let searchQuery = '';
        let selectedLetter = '';
        let selectedStatusFilter = 'All';
        const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');

        // AI Assistant State & Functions
        let currentAiTab = 'recommend';
        let chatHistory = [];

        function openAiModal() {
            const modal = document.getElementById('aiModal');
            const box = document.getElementById('aiModalBox');
            modal.classList.remove('hidden');
            setTimeout(() => box.classList.remove('scale-95'), 10);
        }

        function closeAiModal() {
            const modal = document.getElementById('aiModal');
            const box = document.getElementById('aiModalBox');
            box.classList.add('scale-95');
            setTimeout(() => modal.classList.add('hidden'), 200);
        }

        function setAiTab(tab) {
            currentAiTab = tab;
            ['recommend', 'synopsis', 'chat'].forEach(t => {
                const btn = document.getElementById(`aiTab${t.charAt(0).toUpperCase() + t.slice(1)}`);
                const sec = document.getElementById(`aiSection${t.charAt(0).toUpperCase() + t.slice(1)}`);
                if (!btn || !sec) return;
                if (t === tab) {
                    btn.className = 'py-2.5 px-3 rounded-xl text-xs font-bold transition-all bg-indigo-600 text-white shadow-sm flex items-center justify-center gap-2 cursor-pointer';
                    sec.classList.remove('hidden');
                } else {
                    btn.className = 'py-2.5 px-3 rounded-xl text-xs font-semibold transition-all text-slate-400 hover:text-white flex items-center justify-center gap-2 cursor-pointer';
                    sec.classList.add('hidden');
                }
            });
        }

        async function callGeminiApi(systemPrompt, userPrompt) {
            const apiKey = "";
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;
            const payload = {
                contents: [{ parts: [{ text: userPrompt }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] }
            };

            for (let attempt = 0; attempt < 3; attempt++) {
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    const result = await response.json();
                    const candidate = result.candidates?.[0];
                    if (candidate && candidate.content?.parts?.[0]?.text) {
                        return candidate.content.parts[0].text;
                    }
                    throw new Error('Respon AI kosong atau format tidak valid');
                } catch (err) {
                    if (attempt === 2) throw err;
                    await new Promise(r => setTimeout(r, Math.pow(2, attempt) * 1000));
                }
            }
        }

        async function generateAiRecommendations() {
            const outputContainer = document.getElementById('aiOutputContainer');
            const outputContent = document.getElementById('aiOutputContent');
            const btn = document.getElementById('aiRecBtn');

            outputContainer.classList.remove('hidden');
            outputContent.innerHTML = '<div class="flex items-center justify-center py-6 text-indigo-400 gap-2"><i class="fa-solid fa-spinner fa-spin"></i><span>Gemini sedang menganalisis koleksi komik Anda...</span></div>';
            btn.disabled = true;

            const titles = comics.map(c => `${c.title} (Status: ${c.status}, Chapter: ${c.chapter})`).join(', ');
            const systemPrompt = "Anda adalah seorang ahli manga, manhwa, dan webtoon kelas dunia. Berikan 3 rekomendasi komik yang relevan, menarik, dan sesuai dengan selera pembaca berdasarkan koleksi mereka.";
            const userPrompt = `Koleksi komik saya saat ini: ${titles || 'Belum ada komik'}. Berikan 3 rekomendasi manga/manhwa baru yang sejenis atau menarik untuk dibaca beserta alasan singkatnya dalam bahasa Indonesia yang santai dan menarik.`;

            try {
                const text = await callGeminiApi(systemPrompt, userPrompt);
                outputContent.innerHTML = text.replace(/\n/g, '<br>');
                showToast('Rekomendasi AI berhasil dibuat!');
            } catch (err) {
                outputContent.innerHTML = '<span class="text-rose-400">Gagal terhubung dengan Gemini API. Silakan coba lagi beberapa saat.</span>';
            } finally {
                btn.disabled = false;
            }
        }

        async function generateAiSynopsis() {
            const query = document.getElementById('aiQueryTitle').value.trim();
            if (!query) {
                showToast('Masukkan judul komik terlebih dahulu!');
                return;
            }

            const outputContainer = document.getElementById('aiOutputContainer');
            const outputContent = document.getElementById('aiOutputContent');
            const btn = document.getElementById('aiSynBtn');

            outputContainer.classList.remove('hidden');
            outputContent.innerHTML = '<div class="flex items-center justify-center py-6 text-indigo-400 gap-2"><i class="fa-solid fa-spinner fa-spin"></i><span>Menyusun ringkasan & informasi karakter...</span></div>';
            btn.disabled = true;

            const systemPrompt = "Anda adalah ensiklopedia manga & manhwa profesional. Berikan ringkasan alur cerita (tanpa spoiler berat), karakter utama, dan genre dengan format yang rapi dalam bahasa Indonesia.";
            const userPrompt = `Tuliskan ringkasan, karakter utama, dan keunikan dari komik: ${query}`;

            try {
                const text = await callGeminiApi(systemPrompt, userPrompt);
                outputContent.innerHTML = text.replace(/\n/g, '<br>');
                showToast('Ringkasan komik berhasil dimuat!');
            } catch (err) {
                outputContent.innerHTML = '<span class="text-rose-400">Gagal terhubung dengan Gemini API. Silakan coba lagi.</span>';
            } finally {
                btn.disabled = false;
            }
        }

        async function sendAiChat() {
            const inputEl = document.getElementById('aiChatInput');
            const chatBox = document.getElementById('aiChatBox');
            const msg = inputEl.value.trim();
            if (!msg) return;

            chatBox.innerHTML += `
                <div class="flex items-start gap-2.5 justify-end">
                    <div class="bg-indigo-600 text-white rounded-2xl p-3 text-xs leading-relaxed max-w-[85%]">${escapeHtml(msg)}</div>
                    <div class="w-7 h-7 rounded-full bg-slate-800 flex items-center justify-center text-slate-300 text-xs shrink-0 font-bold">Anda</div>
                </div>
            `;
            inputEl.value = '';
            chatBox.scrollTop = chatBox.scrollHeight;

            const loadingId = 'loading-' + Date.now();
            chatBox.innerHTML += `
                <div id="${loadingId}" class="flex items-start gap-2.5">
                    <div class="w-7 h-7 rounded-full bg-indigo-600 flex items-center justify-center text-white text-xs shrink-0 font-bold">AI</div>
                    <div class="bg-slate-900 border border-slate-800 rounded-2xl p-3 text-slate-400 text-xs italic flex items-center gap-2">
                        <i class="fa-solid fa-spinner fa-spin"></i> Mengetik jawaban...
                    </div>
                </div>
            `;
            chatBox.scrollTop = chatBox.scrollHeight;

            const systemPrompt = "Anda adalah asisten AI yang cerdas dan ramah dalam aplikasi ComicVault. Bantu pengguna dengan pertanyaan seputar manga, manhwa, rekomendasi, maupun teori cerita.";
            
            try {
                const text = await callGeminiApi(systemPrompt, msg);
                document.getElementById(loadingId).remove();
                chatBox.innerHTML += `
                    <div class="flex items-start gap-2.5">
                        <div class="w-7 h-7 rounded-full bg-indigo-600 flex items-center justify-center text-white text-xs shrink-0 font-bold">AI</div>
                        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-3 text-slate-200 text-xs leading-relaxed max-w-[85%]">${text.replace(/\n/g, '<br>')}</div>
                    </div>
                `;
            } catch (err) {
                document.getElementById(loadingId).remove();
                chatBox.innerHTML += `
                    <div class="flex items-start gap-2.5">
                        <div class="w-7 h-7 rounded-full bg-indigo-600 flex items-center justify-center text-white text-xs shrink-0 font-bold">AI</div>
                        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-3 text-rose-400 text-xs leading-relaxed max-w-[85%]">Maaf, terjadi kendala saat menghubungi AI.</div>
                    </div>
                `;
            }
            chatBox.scrollTop = chatBox.scrollHeight;
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }

        function copyAiOutput() {
            const content = document.getElementById('aiOutputContent').innerText;
            const textarea = document.createElement('textarea');
            textarea.value = content;
            document.body.appendChild(textarea);
            textarea.select();
            document.execCommand('copy');
            document.body.removeChild(textarea);
            showToast('Hasil AI berhasil disalin ke clipboard!');
        }

        window.addEventListener('DOMContentLoaded', () => {
            renderAlphabetFilter();
            renderComics();
            updateStats();
        });

        function saveToStorage() {
            localStorage.setItem('comicvault_luxury_comics', JSON.stringify(comics));
            updateStats();
        }

        function updateStats() {
            document.getElementById('statTotal').innerText = comics.length;
            const activeCount = comics.filter(c => c.status === 'Reading').length;
            const completedCount = comics.filter(c => c.status === 'Completed').length;
            
            document.getElementById('statActive').innerText = activeCount;
            document.getElementById('statCompleted').innerText = completedCount;

            if (comics.length > 0) {
                const sorted = [...comics].sort((a, b) => new Date(b.updatedAt) - new Date(a.updatedAt));
                document.getElementById('statLastUpdate').innerText = sorted[0].title;
            } else {
                document.getElementById('statLastUpdate').innerText = '-';
            }
        }

        function formatDate(isoString) {
            if (!isoString) return '-';
            const date = new Date(isoString);
            return date.toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric', hour: '2-digit', minute: '2-digit' });
        }

        // Smart dynamic URL chapter updater
        function updateUrlChapter(oldUrl, newChapter) {
            if (!oldUrl) return '';
            const keywordRegex = /(\b(?:chapter|chap|ch|episode|eps|c)[-_.\s]?)(\d+(?:\.\d+)?)/gi;
            if (keywordRegex.test(oldUrl)) {
                keywordRegex.lastIndex = 0;
                return oldUrl.replace(keywordRegex, (match, prefix, digits) => prefix + newChapter);
            }
            const trailingNumRegex = /(\D+)(\d+(?:\.\d+)?)([\D]*)$/;
            if (trailingNumRegex.test(oldUrl)) {
                return oldUrl.replace(trailingNumRegex, (match, p1, p2, p3) => p1 + newChapter + p3);
            }
            return oldUrl;
        }

        function renderAlphabetFilter() {
            const container = document.getElementById('alphabetFilter');
            container.innerHTML = alphabet.map(letter => `
                <button
                    onclick="setLetterFilter('${letter}')"
                    id="letterBtn-${letter}"
                    class="w-9 h-9 sm:w-10 sm:h-10 rounded-xl border border-slate-800 bg-slate-950/70 text-slate-400 hover:bg-indigo-600 hover:text-white transition-all text-xs sm:text-sm font-bold cursor-pointer shadow-sm">
                    ${letter}
                </button>
            `).join('');
            updateAlphabetButtons();
        }

        function setLetterFilter(letter) {
            selectedLetter = letter;
            updateAlphabetButtons();
            renderComics();
        }

        function updateAlphabetButtons() {
            const allBtn = document.getElementById('letterAllBtn');
            if (allBtn) {
                allBtn.className = selectedLetter === ''
                    ? 'px-4 py-1.5 text-xs font-bold bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm'
                    : 'px-4 py-1.5 text-xs font-bold bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition-all cursor-pointer';
            }

            alphabet.forEach(letter => {
                const btn = document.getElementById(`letterBtn-${letter}`);
                if (!btn) return;
                btn.className = selectedLetter === letter
                    ? 'w-9 h-9 sm:w-10 sm:h-10 rounded-xl border border-indigo-500 bg-indigo-600 text-white shadow-lg shadow-indigo-500/30 transition-all text-xs sm:text-sm font-bold cursor-pointer'
                    : 'w-9 h-9 sm:w-10 sm:h-10 rounded-xl border border-slate-800 bg-slate-950/70 text-slate-400 hover:bg-slate-800 hover:text-white transition-all text-xs sm:text-sm font-bold cursor-pointer';
            });
        }

        function setStatusFilter(status) {
            selectedStatusFilter = status;
            ['All', 'Reading', 'Completed', 'On-Hold'].forEach(s => {
                const btnId = s === 'All' ? 'statusAll' : s === 'Reading' ? 'statusReading' : s === 'Completed' ? 'statusCompletedBtn' : 'statusOnHold';
                const btn = document.getElementById(btnId);
                if (!btn) return;
                btn.className = selectedStatusFilter === s
                    ? 'px-4 py-2 text-xs font-semibold rounded-xl transition-all cursor-pointer whitespace-nowrap bg-indigo-600 text-white shadow-sm'
                    : 'px-4 py-2 text-xs font-semibold rounded-xl transition-all cursor-pointer whitespace-nowrap text-slate-400 hover:text-white';
            });
            renderComics();
        }

        function handleSearch() {
            searchQuery = document.getElementById('searchInput').value;
            renderComics();
        }

        function renderComics() {
            const container = document.getElementById('comicContainer');
            const normalizedSearch = searchQuery.trim().toLowerCase();

            const filtered = comics.filter(c => {
                const title = (c.title || '').trim();
                const matchesSearch = !normalizedSearch || title.toLowerCase().includes(normalizedSearch);
                const matchesLetter = !selectedLetter || title.toUpperCase().startsWith(selectedLetter);
                const matchesStatus = selectedStatusFilter === 'All' || c.status === selectedStatusFilter;
                return matchesSearch && matchesLetter && matchesStatus;
            });

            if (filtered.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-24 glass-panel rounded-3xl border border-slate-800/80 shadow-2xl">
                        <div class="inline-flex p-5 bg-slate-800/50 rounded-2xl text-slate-500 mb-4 text-3xl shadow-inner">
                            <i class="fa-solid fa-ghost"></i>
                        </div>
                        <h3 class="text-slate-200 font-bold text-xl">Tidak ada komik ditemukan</h3>
                        <p class="text-slate-400 text-sm mt-1 max-w-sm mx-auto">Coba ubah kata kunci pencarian, filter status, atau abjad huruf awal.</p>
                    </div>
                `;
                return;
            }

            if (viewMode === 'poster') {
                // Cinematic Manhwa Poster Grid View (Vertical Ratio)
                let html = '<div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-6">';
                filtered.forEach(comic => {
                    const statusColor = comic.status === 'Completed' ? 'bg-emerald-500/20 text-emerald-300 border-emerald-500/30' : 
                                        comic.status === 'Reading' ? 'bg-indigo-500/20 text-indigo-300 border-indigo-500/30' : 'bg-amber-500/20 text-amber-300 border-amber-500/30';
                    const statusText = comic.status === 'Completed' ? 'Selesai' : comic.status === 'Reading' ? 'Dibaca' : 'Ditunda';
                    const coverImg = comic.cover || 'https://placehold.co/500x750/1e293b/94a3b8?text=No+Cover';

                    html += `
                        <div class="glass-card rounded-3xl overflow-hidden flex flex-col justify-between card-lift group border border-slate-800/80 shadow-xl">
                            <div>
                                <div class="relative aspect-[3/4] w-full overflow-hidden bg-slate-950">
                                    <img src="${coverImg}" alt="${comic.title}" onerror="this.src='https://placehold.co/500x750/1e293b/94a3b8?text=Image+Error'" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700">
                                    <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-slate-950/20 to-transparent opacity-80 group-hover:opacity-60 transition-opacity"></div>
                                    <span class="absolute top-3 left-3 text-[10px] px-2.5 py-1 rounded-full border font-bold backdrop-blur-md shadow-lg ${statusColor}">
                                        ${statusText}
                                    </span>
                                    <div class="absolute bottom-3 left-3 right-3 flex items-center justify-between">
                                        <div class="bg-slate-900/90 backdrop-blur-md px-3 py-1.5 rounded-xl border border-white/10 shadow-lg">
                                            <span class="text-[10px] text-slate-400 block font-medium">Chapter</span>
                                            <span class="text-sm font-extrabold text-indigo-400">Ch. ${comic.chapter}</span>
                                        </div>
                                    </div>
                                </div>
                                <div class="p-4 space-y-2.5">
                                    <h3 class="font-bold text-sm text-white line-clamp-1 group-hover:text-indigo-300 transition-colors" title="${comic.title}">${comic.title}</h3>
                                    <div class="flex items-center justify-between gap-1">
                                        <button onclick="adjustChapter('${comic.id}', -1)" class="w-7 h-7 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 flex items-center justify-center transition-all cursor-pointer shadow-sm"><i class="fa-solid fa-minus text-[10px]"></i></button>
                                        <span class="text-[11px] text-slate-400 font-medium">Ubah Chapter</span>
                                        <button onclick="adjustChapter('${comic.id}', 1)" class="w-7 h-7 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 flex items-center justify-center transition-all cursor-pointer shadow-sm"><i class="fa-solid fa-plus text-[10px]"></i></button>
                                    </div>
                                </div>
                            </div>
                            <div class="p-4 pt-0 grid grid-cols-3 gap-2">
                                <a href="${comic.url}" target="_blank" class="col-span-2 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white py-2 px-3 rounded-xl text-xs font-bold flex items-center justify-center gap-1.5 transition-all shadow-md shadow-indigo-600/20">
                                    <i class="fa-solid fa-book-open text-[10px]"></i> Baca
                                </a>
                                <button onclick="editComic('${comic.id}')" class="bg-slate-800 hover:bg-slate-700 text-slate-300 py-2 rounded-xl text-xs font-semibold transition-all flex items-center justify-center cursor-pointer shadow-sm" title="Edit">
                                    <i class="fa-solid fa-pen"></i>
                                </button>
                                <button onclick="deleteComic('${comic.id}')" class="col-span-3 bg-rose-500/10 hover:bg-rose-500/20 text-rose-400 border border-rose-500/20 py-2 rounded-xl text-xs font-semibold transition-all flex items-center justify-center gap-1.5 cursor-pointer mt-1" title="Hapus">
                                    <i class="fa-solid fa-trash text-[10px]"></i> Hapus Koleksi
                                </button>
                            </div>
                        </div>
                    `;
                });
                html += '</div>';
                container.innerHTML = html;
            } else if (viewMode === 'grid') {
                // Standard Card Grid View
                let html = '<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">';
                filtered.forEach(comic => {
                    const statusColor = comic.status === 'Completed' ? 'bg-emerald-500/20 text-emerald-300 border-emerald-500/30' : 
                                        comic.status === 'Reading' ? 'bg-indigo-500/20 text-indigo-300 border-indigo-500/30' : 'bg-amber-500/20 text-amber-300 border-amber-500/30';
                    const coverImg = comic.cover || 'https://placehold.co/400x300/1e293b/94a3b8?text=No+Cover';
                    
                    html += `
                        <div class="glass-card rounded-3xl p-5 flex flex-col justify-between card-lift border border-slate-800/80 shadow-xl space-y-4">
                            <div class="flex items-start gap-4">
                                <img src="${coverImg}" alt="${comic.title}" onerror="this.src='https://placehold.co/200x200/1e293b/94a3b8?text=Error'" class="w-20 h-24 object-cover rounded-2xl border border-slate-700 shadow-md">
                                <div class="flex-1 min-w-0">
                                    <div class="flex items-center justify-between mb-1">
                                        <span class="text-[10px] px-2.5 py-0.5 rounded-full border font-bold ${statusColor}">${comic.status}</span>
                                        <span class="text-[11px] text-slate-500"><i class="fa-regular fa-clock"></i></span>
                                    </div>
                                    <h3 class="font-bold text-base text-white truncate" title="${comic.title}">${comic.title}</h3>
                                    <p class="text-xs text-indigo-400 font-bold mt-1">Chapter ${comic.chapter}</p>
                                    <p class="text-[11px] text-slate-500 truncate mt-1"><i class="fa-solid fa-link mr-1"></i>${comic.url}</p>
                                </div>
                            </div>
                            <div class="flex items-center justify-between bg-slate-950/60 p-3 rounded-2xl border border-slate-800/80">
                                <span class="text-xs text-slate-400 font-medium">Ubah Chapter:</span>
                                <div class="flex items-center gap-2">
                                    <button onclick="adjustChapter('${comic.id}', -1)" class="w-7 h-7 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 flex items-center justify-center transition-all cursor-pointer"><i class="fa-solid fa-minus text-[10px]"></i></button>
                                    <span class="font-bold text-indigo-400 text-sm">Ch. ${comic.chapter}</span>
                                    <button onclick="adjustChapter('${comic.id}', 1)" class="w-7 h-7 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 flex items-center justify-center transition-all cursor-pointer"><i class="fa-solid fa-plus text-[10px]"></i></button>
                                </div>
                            </div>
                            <div class="grid grid-cols-3 gap-2 pt-1">
                                <a href="${comic.url}" target="_blank" class="col-span-2 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white py-2 px-3 rounded-xl text-xs font-bold flex items-center justify-center gap-1.5 shadow-md shadow-indigo-600/20">
                                    <i class="fa-solid fa-external-link-alt text-[10px]"></i> Baca Website
                                </a>
                                <button onclick="editComic('${comic.id}')" class="bg-slate-800 hover:bg-slate-700 text-slate-300 py-2 rounded-xl text-xs font-semibold transition-all flex items-center justify-center cursor-pointer" title="Edit">
                                    <i class="fa-solid fa-pen"></i>
                                </button>
                                <button onclick="deleteComic('${comic.id}')" class="bg-rose-500/10 hover:bg-rose-500/20 text-rose-400 border border-rose-500/20 py-2 rounded-xl text-xs font-semibold transition-all flex items-center justify-center cursor-pointer" title="Hapus">
                                    <i class="fa-solid fa-trash"></i>
                                </button>
                            </div>
                        </div>
                    `;
                });
                html += '</div>';
                container.innerHTML = html;
            } else {
                // Compact Table View
                let html = `
                    <div class="glass-panel rounded-3xl overflow-x-auto shadow-2xl border border-slate-800/80">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-800 text-xs text-slate-400 uppercase tracking-wider bg-slate-950/60">
                                    <th class="p-4 font-bold">Judul Komik</th>
                                    <th class="p-4 font-bold">Status</th>
                                    <th class="p-4 font-bold">Chapter Terakhir</th>
                                    <th class="p-4 font-bold">Terakhir Diperbarui</th>
                                    <th class="p-4 font-bold text-right">Aksi</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-800/60 text-sm">
                `;
                filtered.forEach(comic => {
                    const statusColor = comic.status === 'Completed' ? 'bg-emerald-500/20 text-emerald-300 border-emerald-500/30' : 
                                        comic.status === 'Reading' ? 'bg-indigo-500/20 text-indigo-300 border-indigo-500/30' : 'bg-amber-500/20 text-amber-300 border-amber-500/30';
                    
                    html += `
                        <tr class="hover:bg-slate-800/40 transition-all">
                            <td class="p-4">
                                <div class="font-bold text-white">${comic.title}</div>
                                <a href="${comic.url}" target="_blank" class="text-xs text-indigo-400 hover:underline flex items-center gap-1 mt-0.5 max-w-xs truncate" title="${comic.url}">
                                    <span>${comic.url}</span> <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i>
                                </a>
                            </td>
                            <td class="p-4">
                                <span class="text-xs px-3 py-1 rounded-full border font-bold ${statusColor}">${comic.status}</span>
                            </td>
                            <td class="p-4">
                                <div class="flex items-center gap-2">
                                    <button onclick="adjustChapter('${comic.id}', -1)" class="w-6 h-6 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-200 flex items-center justify-center transition-all cursor-pointer"><i class="fa-solid fa-minus text-[10px]"></i></button>
                                    <span class="font-bold text-indigo-400">Ch. ${comic.chapter}</span>
                                    <button onclick="adjustChapter('${comic.id}', 1)" class="w-6 h-6 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-200 flex items-center justify-center transition-all cursor-pointer"><i class="fa-solid fa-plus text-[10px]"></i></button>
                                </div>
                            </td>
                            <td class="p-4 text-xs text-slate-400">${formatDate(comic.updatedAt)}</td>
                            <td class="p-4 text-right">
                                <div class="flex items-center justify-end gap-2">
                                    <a href="${comic.url}" target="_blank" class="p-2.5 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white rounded-xl text-xs transition-all shadow-sm" title="Baca"><i class="fa-solid fa-book-open"></i></a>
                                    <button onclick="editComic('${comic.id}')" class="p-2.5 bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl text-xs transition-all cursor-pointer" title="Edit"><i class="fa-solid fa-pen"></i></button>
                                    <button onclick="deleteComic('${comic.id}')" class="p-2.5 bg-rose-500/10 hover:bg-rose-500/20 text-rose-400 border border-rose-500/20 rounded-xl text-xs transition-all cursor-pointer" title="Hapus"><i class="fa-solid fa-trash"></i></button>
                                </div>
                            </td>
                        </tr>
                    `;
                });
                html += '</tbody></table></div>';
                container.innerHTML = html;
            }
        }

        function setViewMode(mode) {
            viewMode = mode;
            ['poster', 'grid', 'table'].forEach(m => {
                const btnId = m === 'poster' ? 'viewPosterBtn' : m === 'grid' ? 'viewGridBtn' : 'viewTableBtn';
                const btn = document.getElementById(btnId);
                if (!btn) return;
                btn.className = viewMode === m
                    ? 'p-2.5 text-sm bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm'
                    : 'p-2.5 text-sm bg-slate-900 text-slate-400 hover:text-white rounded-xl transition-all cursor-pointer';
            });
            renderComics();
        }

        function openModal(id = null) {
            const modal = document.getElementById('comicModal');
            const modalBox = document.getElementById('modalBox');
            modal.classList.remove('hidden');
            setTimeout(() => modalBox.classList.remove('scale-95'), 10);

            if (id) {
                document.getElementById('modalTitle').innerText = 'Edit Koleksi Komik';
                const comic = comics.find(c => c.id === id);
                if (comic) {
                    document.getElementById('comicId').value = comic.id;
                    document.getElementById('formTitle').value = comic.title;
                    document.getElementById('formUrl').value = comic.url;
                    document.getElementById('formChapter').value = comic.chapter;
                    document.getElementById('formStatus').value = comic.status;
                    document.getElementById('formCover').value = comic.cover || '';
                    previewCover();
                }
            } else {
                document.getElementById('modalTitle').innerText = 'Tambah Komik Baru';
                document.getElementById('comicForm').reset();
                document.getElementById('comicId').value = '';
                document.getElementById('coverPreviewContainer').classList.add('hidden');
            }
        }

        function closeModal() {
            const modal = document.getElementById('comicModal');
            const modalBox = document.getElementById('modalBox');
            modalBox.classList.add('scale-95');
            setTimeout(() => modal.classList.add('hidden'), 200);
        }

        function previewCover() {
            const url = document.getElementById('formCover').value;
            const container = document.getElementById('coverPreviewContainer');
            const img = document.getElementById('formCoverPreview');
            if (url.trim() !== '') {
                img.src = url;
                container.classList.remove('hidden');
            } else {
                container.classList.add('hidden');
            }
        }

        function saveComic(e) {
            e.preventDefault();
            const id = document.getElementById('comicId').value;
            const title = document.getElementById('formTitle').value;
            let url = document.getElementById('formUrl').value;
            const chapter = parseFloat(document.getElementById('formChapter').value);
            const status = document.getElementById('formStatus').value;
            const cover = document.getElementById('formCover').value;
            const now = new Date().toISOString();

            url = updateUrlChapter(url, chapter);

            if (id) {
                comics = comics.map(c => c.id === id ? { ...c, title, url, chapter, status, cover, updatedAt: now } : c);
                showToast('Komik & URL chapter berhasil diperbarui!');
            } else {
                const newComic = {
                    id: Date.now().toString(),
                    title,
                    url,
                    chapter,
                    status,
                    cover,
                    updatedAt: now
                };
                comics.unshift(newComic);
                showToast('Komik baru berhasil ditambahkan!');
            }

            saveToStorage();
            renderComics();
            closeModal();
        }

        function adjustChapter(id, amount) {
            comics = comics.map(c => {
                if (c.id === id) {
                    const newChap = Math.max(0, c.chapter + amount);
                    const updatedUrl = updateUrlChapter(c.url, newChap);
                    return { ...c, chapter: newChap, url: updatedUrl, updatedAt: new Date().toISOString() };
                }
                return c;
            });
            saveToStorage();
            renderComics();
            showToast('Chapter & URL web diperbarui otomatis!');
        }

        function editComic(id) {
            openModal(id);
        }

        function deleteComic(id) {
            if (confirm('Apakah Anda yakin ingin menghapus komik ini dari ComicVault?')) {
                comics = comics.filter(c => c.id !== id);
                saveToStorage();
                renderComics();
                showToast('Komik berhasil dihapus dari koleksi.');
            }
        }

        function exportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(comics, null, 2));
            const dlAnchorElem = document.createElement('a');
            dlAnchorElem.setAttribute("href", dataStr);
            dlAnchorElem.setAttribute("download", `comicvault_luxury_backup_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(dlAnchorElem);
            dlAnchorElem.click();
            dlAnchorElem.remove();
            showToast('Backup JSON berhasil diunduh!');
        }

        function importData(event) {
            const fileReader = new FileReader();
            if (event.target.files[0]) {
                fileReader.readAsText(event.target.files[0], "UTF-8");
                fileReader.onload = (e) => {
                    try {
                        const parsed = JSON.parse(e.target.result);
                        if (Array.isArray(parsed)) {
                            comics = parsed;
                            saveToStorage();
                            renderComics();
                            showToast('Data koleksi berhasil direstore!');
                        } else {
                            showToast('Format file backup tidak valid.');
                        }
                    } catch (err) {
                        showToast('Gagal membaca file JSON.');
                    }
                };
            }
        }

        function showToast(message) {
            const toast = document.getElementById('toast');
            const toastMessage = document.getElementById('toastMessage');
            const toastIcon = document.getElementById('toastIcon');
            
            toastMessage.innerText = message;
            toastIcon.innerHTML = '<i class="fa-solid fa-circle-check"></i>';
            
            toast.classList.remove('translate-y-24', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 3200);
        }
    </script>
</body>
</html>
