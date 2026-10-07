<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ComicVault - Platform Tracker Manga & Manhwa</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: #090d16; }
        ::-webkit-scrollbar-thumb { background: #1e293b; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #334155; }
    </style>
</head>
<body class="bg-[#0b0f19] text-slate-100 min-h-full flex flex-col selection:bg-red-600 selection:text-white">

    <!-- Header / Navbar ala Web Komik Modern -->
    <header class="bg-[#0f172a]/90 backdrop-blur-md sticky top-0 z-40 border-b border-slate-800/80 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-18 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-gradient-to-tr from-red-600 to-rose-500 p-2.5 rounded-xl shadow-lg shadow-red-600/30 flex items-center justify-center">
                    <i class="fa-solid fa-fire-flame-curved text-white text-xl"></i>
                </div>
                <div>
                    <h1 class="font-extrabold text-xl tracking-tight bg-gradient-to-r from-white via-slate-200 to-slate-400 bg-clip-text text-transparent flex items-center gap-2">
                        ComicVault <span class="text-[10px] bg-red-500/20 text-red-400 border border-red-500/30 px-2 py-0.5 rounded-full font-semibold uppercase tracking-wider">PRO</span>
                    </h1>
                    <p class="text-xs text-slate-400 font-medium">Manhwa, Manga, & Donghua Tracker</p>
                </div>
            </div>
            <div class="flex items-center gap-3">
                <button onclick="openModal()" class="bg-gradient-to-r from-red-600 to-rose-600 hover:from-red-500 hover:to-rose-500 active:scale-95 transition-all text-white px-4 py-2.5 rounded-xl font-semibold text-sm shadow-lg shadow-red-600/25 flex items-center gap-2 cursor-pointer">
                    <i class="fa-solid fa-plus"></i>
                    <span class="hidden sm:inline">Tambah Komik</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">
        
        <!-- Summary Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div class="bg-[#111827] border border-slate-800/80 rounded-2xl p-5 flex items-center justify-between shadow-sm relative overflow-hidden group hover:border-slate-700 transition-all">
                <div class="absolute -right-4 -bottom-4 text-slate-800/40 text-7xl group-hover:scale-110 transition-transform">
                    <i class="fa-solid fa-layer-group"></i>
                </div>
                <div class="z-10">
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Total Koleksi</p>
                    <h3 id="statTotal" class="text-3xl font-extrabold mt-1 text-white">0</h3>
                </div>
                <div class="p-3 bg-red-500/10 border border-red-500/20 text-red-400 rounded-2xl z-10">
                    <i class="fa-solid fa-layer-group text-xl"></i>
                </div>
            </div>
            <div class="bg-[#111827] border border-slate-800/80 rounded-2xl p-5 flex items-center justify-between shadow-sm relative overflow-hidden group hover:border-slate-700 transition-all">
                <div class="absolute -right-4 -bottom-4 text-slate-800/40 text-7xl group-hover:scale-110 transition-transform">
                    <i class="fa-solid fa-book-reader"></i>
                </div>
                <div class="z-10">
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Sedang Dibaca</p>
                    <h3 id="statActive" class="text-3xl font-extrabold mt-1 text-emerald-400">0</h3>
                </div>
                <div class="p-3 bg-emerald-500/10 border border-emerald-500/20 text-emerald-400 rounded-2xl z-10">
                    <i class="fa-solid fa-book-reader text-xl"></i>
                </div>
            </div>
            <div class="bg-[#111827] border border-slate-800/80 rounded-2xl p-5 flex items-center justify-between shadow-sm relative overflow-hidden group hover:border-slate-700 transition-all">
                <div class="absolute -right-4 -bottom-4 text-slate-800/40 text-7xl group-hover:scale-110 transition-transform">
                    <i class="fa-solid fa-clock-rotate-left"></i>
                </div>
                <div class="z-10">
                    <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Terakhir Diperbarui</p>
                    <h3 id="statLastUpdate" class="text-sm font-bold mt-2 text-slate-200">-</h3>
                </div>
                <div class="p-3 bg-amber-500/10 border border-amber-500/20 text-amber-400 rounded-2xl z-10">
                    <i class="fa-solid fa-clock-rotate-left text-xl"></i>
                </div>
            </div>
        </div>

        <!-- Toolbar: Search, Backup, View Switch -->
        <div class="flex flex-col sm:flex-row gap-4 items-center justify-between bg-[#111827]/80 p-4 border border-slate-800/80 rounded-2xl backdrop-blur-sm shadow-sm">
            <div class="relative w-full sm:w-96">
                <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center pointer-events-none text-slate-400">
                    <i class="fa-solid fa-magnifying-glass"></i>
                </span>
                <input type="text" id="searchInput" oninput="handleSearch()" placeholder="Cari judul komik / manhwa..." 
                    class="w-full pl-10 pr-4 py-2.5 bg-[#0b0f19] border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-red-500 text-slate-100 placeholder-slate-500 transition-all">
            </div>
            <div class="flex items-center gap-2.5 w-full sm:w-auto justify-end">
                <button onclick="exportData()" class="px-3.5 py-2.5 text-xs font-semibold bg-slate-800/80 hover:bg-slate-700 text-slate-300 rounded-xl transition-all border border-slate-700/50 flex items-center gap-1.5 cursor-pointer" title="Backup JSON">
                    <i class="fa-solid fa-download text-slate-400"></i> Backup
                </button>
                <label class="px-3.5 py-2.5 text-xs font-semibold bg-slate-800/80 hover:bg-slate-700 text-slate-300 rounded-xl transition-all border border-slate-700/50 flex items-center gap-1.5 cursor-pointer" title="Restore JSON">
                    <i class="fa-solid fa-upload text-slate-400"></i> Restore <input type="file" id="importFile" onchange="importData(event)" accept=".json" class="hidden">
                </label>
                <div class="h-5 w-px bg-slate-800 mx-1"></div>
                <button onclick="setViewMode('grid')" id="gridBtn" class="p-2.5 text-sm bg-red-600 text-white rounded-xl transition-all cursor-pointer shadow-sm" title="Tampilan Grid Cover">
                    <i class="fa-solid fa-grip"></i>
                </button>
                <button onclick="setViewMode('table')" id="tableBtn" class="p-2.5 text-sm bg-slate-800 hover:bg-slate-700 text-slate-400 rounded-xl transition-all cursor-pointer" title="Tampilan Tabel Detail">
                    <i class="fa-solid fa-table-list"></i>
                </button>
            </div>
        </div>

        <!-- Alphabet Filter -->
        <div class="bg-[#111827]/80 p-4 border border-slate-800/80 rounded-2xl backdrop-blur-sm shadow-sm">
            <div class="flex items-center justify-between mb-3">
                <div class="flex items-center gap-2">
                    <i class="fa-solid fa-filter text-red-500 text-xs"></i>
                    <h3 class="text-xs font-bold uppercase tracking-wider text-slate-300">Filter Berdasarkan Abjad</h3>
                </div>
                <button onclick="setLetterFilter('')" id="letterAllBtn"
                    class="px-3 py-1 text-xs font-bold bg-red-600 text-white rounded-lg transition-all cursor-pointer shadow-sm">
                    SEMUA
                </button>
            </div>
            <div id="alphabetFilter" class="flex flex-wrap gap-1.5"></div>
        </div>

        <!-- Comic Container -->
        <div id="comicContainer">
            <!-- Rendered dynamically -->
        </div>
    </main>

    <!-- Modal Form (Tambah / Edit) -->
    <div id="comicModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="bg-[#111827] border border-slate-800 rounded-3xl w-full max-w-md overflow-hidden shadow-2xl">
            <div class="px-6 py-4 border-b border-slate-800 flex items-center justify-between bg-[#0b0f19]/50">
                <h3 id="modalTitle" class="font-bold text-base text-white flex items-center gap-2">
                    <i class="fa-solid fa-book text-red-500"></i> Tambah Komik Baru
                </h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white p-2 rounded-xl transition-all cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <form id="comicForm" onsubmit="saveComic(event)" class="p-6 space-y-4">
                <input type="hidden" id="comicId">
                <div>
                    <label class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1.5">Judul Komik / Manhwa</label>
                    <input type="text" id="formTitle" required placeholder="Contoh: Solo Leveling" 
                        class="w-full px-4 py-2.5 bg-[#0b0f19] border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-red-500 text-slate-100 placeholder-slate-600">
                </div>
                <div>
                    <label class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1.5">Link Website Baca (URL)</label>
                    <input type="url" id="formUrl" required placeholder="https://example.com/komik/chapter-1" 
                        class="w-full px-4 py-2.5 bg-[#0b0f19] border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-red-500 text-slate-100 placeholder-slate-600">
                    <p class="text-[11px] text-slate-500 mt-1">💡 URL akan otomatis memperbarui nomor chapter saat Anda menaikkan/menurunkan chapter.</p>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1.5">Chapter Terakhir</label>
                        <input type="number" step="0.5" id="formChapter" required placeholder="1" min="0" 
                            class="w-full px-4 py-2.5 bg-[#0b0f19] border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-red-500 text-slate-100 placeholder-slate-600">
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1.5">Status Baca</label>
                        <select id="formStatus" class="w-full px-4 py-2.5 bg-[#0b0f19] border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-red-500 text-slate-100">
                            <option value="Reading">Sedang Dibaca</option>
                            <option value="Completed">Tamat</option>
                            <option value="On-Hold">Ditunda</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1.5">URL Gambar Cover (Opsional)</label>
                    <input type="url" id="formCover" placeholder="https://images.unsplash.com/..." 
                        class="w-full px-4 py-2.5 bg-[#0b0f19] border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-red-500 text-slate-100 placeholder-slate-600">
                </div>
                <div class="pt-4 flex items-center justify-end gap-3 border-t border-slate-800">
                    <button type="button" onclick="closeModal()" class="px-4 py-2.5 text-xs font-bold bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition-all cursor-pointer">Batal</button>
                    <button type="submit" class="px-5 py-2.5 text-xs font-bold bg-red-600 hover:bg-red-500 text-white rounded-xl shadow-lg shadow-red-600/25 transition-all cursor-pointer">Simpan Komik</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 translate-y-20 opacity-0 transition-all duration-300 bg-[#111827] border border-slate-700 shadow-2xl px-4 py-3 rounded-2xl flex items-center gap-3">
        <div id="toastIcon" class="text-emerald-400 text-lg"></div>
        <div id="toastMessage" class="text-xs font-bold
