
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ComicVault - Offline Manga & Manhwa Tracker</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-full flex flex-col selection:bg-indigo-500 selection:text-white">

    <!-- Header / Navbar -->
    <header class="bg-slate-900/80 backdrop-blur-md sticky top-0 z-40 border-b border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-gradient-to-tr from-indigo-600 to-violet-500 p-2.5 rounded-xl shadow-lg shadow-indigo-500/30">
                    <i class="fa-solid fa-book-open text-white text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg tracking-tight bg-gradient-to-r from-white via-slate-200 to-slate-400 bg-clip-text text-transparent">ComicVault</h1>
                    <p class="text-xs text-slate-400">Offline Manga & Manhwa Tracker</p>
                </div>
            </div>
            <div class="flex items-center gap-3">
                <button onclick="openModal()" class="bg-indigo-600 hover:bg-indigo-500 active:scale-95 transition-all text-white px-4 py-2 rounded-xl font-medium text-sm shadow-lg shadow-indigo-600/20 flex items-center gap-2 cursor-pointer">
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
            <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-5 flex items-center justify-between shadow-sm">
                <div>
                    <p class="text-xs font-medium text-slate-400 uppercase tracking-wider">Total Koleksi</p>
                    <h3 id="statTotal" class="text-2xl font-bold mt-1 text-white">0</h3>
                </div>
                <div class="p-3 bg-indigo-500/10 border border-indigo-500/20 text-indigo-400 rounded-xl">
                    <i class="fa-solid fa-layer-group text-xl"></i>
                </div>
            </div>
            <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-5 flex items-center justify-between shadow-sm">
                <div>
                    <p class="text-xs font-medium text-slate-400 uppercase tracking-wider">Sedang Dibaca</p>
                    <h3 id="statActive" class="text-2xl font-bold mt-1 text-emerald-400">0</h3>
                </div>
                <div class="p-3 bg-emerald-500/10 border border-emerald-500/20 text-emerald-400 rounded-xl">
                    <i class="fa-solid fa-book-reader text-xl"></i>
                </div>
            </div>
            <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-5 flex items-center justify-between shadow-sm">
                <div>
                    <p class="text-xs font-medium text-slate-400 uppercase tracking-wider">Terakhir Diperbarui</p>
                    <h3 id="statLastUpdate" class="text-sm font-semibold mt-2 text-slate-300">-</h3>
                </div>
                <div class="p-3 bg-violet-500/10 border border-violet-500/20 text-violet-400 rounded-xl">
                    <i class="fa-solid fa-clock-rotate-left text-xl"></i>
                </div>
            </div>
        </div>

        <!-- Toolbar: Search, Backup, View Switch -->
        <div class="flex flex-col sm:flex-row gap-4 items-center justify-between bg-slate-900/40 p-4 border border-slate-800/60 rounded-2xl backdrop-blur-sm">
            <div class="relative w-full sm:w-96">
                <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center pointer-events-none text-slate-400">
                    <i class="fa-solid fa-magnifying-glass"></i>
                </span>
                <input type="text" id="searchInput" oninput="handleSearch()" placeholder="Cari judul komik..." 
                    class="w-full pl-10 pr-4 py-2.5 bg-slate-950/60 border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-500 transition-all">
            </div>
            <div class="flex items-center gap-2 w-full sm:w-auto justify-end">
                <button onclick="exportData()" class="px-3.5 py-2 text-xs font-medium bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition-all border border-slate-700/50 flex items-center gap-1.5 cursor-pointer" title="Backup JSON">
                    <i class="fa-solid fa-download"></i> Backup
                </button>
                <label class="px-3.5 py-2 text-xs font-medium bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition-all border border-slate-700/50 flex items-center gap-1.5 cursor-pointer" title="Restore JSON">
                    <i class="fa-solid fa-upload"></i> Restore <input type="file" id="importFile" onchange="importData(event)" accept=".json" class="hidden">
                </label>
                <div class="h-5 w-px bg-slate-800 mx-1"></div>
                <button onclick="setViewMode('grid')" id="gridBtn" class="p-2 text-sm bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm" title="Tampilan Grid">
                    <i class="fa-solid fa-grip"></i>
                </button>
                <button onclick="setViewMode('table')" id="tableBtn" class="p-2 text-sm bg-slate-800 hover:bg-slate-700 text-slate-400 rounded-xl transition-all cursor-pointer" title="Tampilan Tabel">
                    <i class="fa-solid fa-table-list"></i>
                </button>
            </div>
        </div>

        <!-- Alphabet Filter -->
        <div class="bg-slate-900/40 p-4 border border-slate-800/60 rounded-2xl backdrop-blur-sm">
            <div class="flex items-center justify-between mb-3">
                <div>
                    <h3 class="text-sm font-semibold text-white">Pilih Abjad</h3>
                    <p class="text-[11px] text-slate-500">Tampilkan komik berdasarkan huruf awal judul</p>
                </div>
                <button onclick="setLetterFilter('')" id="letterAllBtn"
                    class="px-3 py-1.5 text-xs font-semibold bg-indigo-600 text-white rounded-lg transition-all cursor-pointer">
                    Semua
                </button>
            </div>
            <div id="alphabetFilter" class="flex flex-wrap gap-2"></div>
        </div>

        <!-- Comic Container (Daftar Isi) -->
        <div id="comicContainer">
            <!-- Rendered dynamically -->
        </div>
    </main>

    <!-- Modal Form (Tambah / Edit) -->
    <div id="comicModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/70 backdrop-blur-sm hidden">
        <div class="bg-slate-900 border border-slate-800 rounded-3xl w-full max-w-md overflow-hidden shadow-2xl">
            <div class="px-6 py-4 border-b border-slate-800 flex items-center justify-between">
                <h3 id="modalTitle" class="font-bold text-lg text-white">Tambah Komik Baru</h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white p-2 rounded-xl transition-all cursor-pointer">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <form id="comicForm" onsubmit="saveComic(event)" class="p-6 space-y-4">
                <input type="hidden" id="comicId">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-1.5">Judul Komik</label>
                    <input type="text" id="formTitle" required placeholder="Contoh: Solo Leveling" 
                        class="w-full px-4 py-2.5 bg-slate-950 border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600">
                </div>
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-1.5">Link Website Baca (URL)</label>
                    <input type="url" id="formUrl" required placeholder="https://example.com/komik/solo-leveling/chapter-1" 
                        class="w-full px-4 py-2.5 bg-slate-950 border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600">
                    <p class="text-[11px] text-slate-500 mt-1">💡 URL dapat berisi nomor chapter (misal: .../chapter-1 atau .../ch-1). URL akan otomatis diperbarui saat chapter berubah.</p>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-1.5">Chapter Terakhir</label>
                        <input type="number" step="0.5" id="formChapter" required placeholder="1" min="0" 
                            class="w-full px-4 py-2.5 bg-slate-950 border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-1.5">Status</label>
                        <select id="formStatus" class="w-full px-4 py-2.5 bg-slate-950 border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100">
                            <option value="Reading">Sedang Dibaca</option>
                            <option value="Completed">Tamat / Selesai</option>
                            <option value="On-Hold">Ditunda</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-1.5">URL Gambar Cover (Opsional)</label>
                    <input type="url" id="formCover" placeholder="https://images.unsplash.com/..." 
                        class="w-full px-4 py-2.5 bg-slate-950 border border-slate-800 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-100 placeholder-slate-600">
                </div>
                <div class="pt-4 flex items-center justify-end gap-3 border-t border-slate-800/80">
                    <button type="button" onclick="closeModal()" class="px-4 py-2.5 text-sm font-medium bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition-all cursor-pointer">Batal</button>
                    <button type="submit" class="px-5 py-2.5 text-sm font-medium bg-indigo-600 hover:bg-indigo-500 text-white rounded-xl shadow-lg shadow-indigo-600/20 transition-all cursor-pointer">Simpan Komik</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 translate-y-20 opacity-0 transition-all duration-300 bg-slate-900 border border-slate-700 shadow-2xl px-4 py-3 rounded-2xl flex items-center gap-3">
        <div id="toastIcon" class="text-emerald-400 text-lg"></div>
        <div id="toastMessage" class="text-sm font-medium text-slate-200"></div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        let comics = JSON.parse(localStorage.getItem('comicvault_comics')) || [
            {
                id: '1',
                title: 'Solo Leveling',
                url: 'https://asurascans.com/manga/solo-leveling/chapter-179/',
                chapter: 179,
                status: 'Completed',
                cover: 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=400&auto=format&fit=crop',
                updatedAt: new Date().toISOString()
            },
            {
                id: '2',
                title: 'Omniscient Reader’s Viewpoint',
                url: 'https://flamescans.org/manga/omniscient-readers-viewpoint-chapter-195/',
                chapter: 195,
                status: 'Reading',
                cover: 'https://images.unsplash.com/photo-1534447677768-be436bb09401?q=80&w=400&auto=format&fit=crop',
                updatedAt: new Date(Date.now() - 86400000).toISOString()
            }
        ];

        let viewMode = 'grid'; // 'grid' or 'table'
        let searchQuery = '';
        let selectedLetter = '';
        const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');

        window.addEventListener('DOMContentLoaded', () => {
            renderAlphabetFilter();
            renderComics();
            updateStats();
        });

        function saveToStorage() {
            localStorage.setItem('comicvault_comics', JSON.stringify(comics));
            updateStats();
        }

        function updateStats() {
            document.getElementById('statTotal').innerText = comics.length;
            const activeCount = comics.filter(c => c.status === 'Reading').length;
            document.getElementById('statActive').innerText = activeCount;

            if (comics.length > 0) {
                const sorted = [...comics].sort((a, b) => new Date(b.updatedAt) - new Date(a.updatedAt));
                document.getElementById('statLastUpdate').innerText = formatDate(sorted[0].updatedAt);
            } else {
                document.getElementById('statLastUpdate').innerText = '-';
            }
        }

        function formatDate(isoString) {
            if (!isoString) return '-';
            const date = new Date(isoString);
            return date.toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric', hour: '2-digit', minute: '2-digit' });
        }

        // Helper function to update chapter number inside a URL string dynamically
        function updateUrlChapter(oldUrl, newChapter) {
            if (!oldUrl) return '';
            
            // Pattern 1: Matches words like chapter-179, ch-179, chap-179, c-179, episode-179, eps-179 (case-insensitive)
            // Example: .../chapter-179/ or .../chapter-179
            const keywordRegex = /(\b(?:chapter|chap|ch|episode|eps|c)[-_.\s]?)(\d+(?:\.\d+)?)/gi;
            if (keywordRegex.test(oldUrl)) {
                // Reset regex lastIndex
                keywordRegex.lastIndex = 0;
                return oldUrl.replace(keywordRegex, (match, prefix, digits) => {
                    return prefix + newChapter;
                });
            }

            // Pattern 2: Fallback if no keyword found, look for standalone numbers near the end or in paths
            // Searches for the last occurrence of a number sequence in the URL
            const trailingNumRegex = /(\D+)(\d+(?:\.\d+)?)([\D]*)$/;
            if (trailingNumRegex.test(oldUrl)) {
                return oldUrl.replace(trailingNumRegex, (match, p1, p2, p3) => {
                    return p1 + newChapter + p3;
                });
            }

            return oldUrl;
        }

        function renderAlphabetFilter() {
            const container = document.getElementById('alphabetFilter');
            container.innerHTML = alphabet.map(letter => `
                <button
                    onclick="setLetterFilter('${letter}')"
                    id="letterBtn-${letter}"
                    class="w-9 h-9 sm:w-10 sm:h-10 rounded-lg border border-slate-800 bg-slate-950/60 text-slate-400 hover:bg-slate-800 hover:text-white transition-all text-xs sm:text-sm font-semibold cursor-pointer">
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
                    ? 'px-3 py-1.5 text-xs font-semibold bg-indigo-600 text-white rounded-lg transition-all cursor-pointer'
                    : 'px-3 py-1.5 text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-lg transition-all cursor-pointer';
            }

            alphabet.forEach(letter => {
                const btn = document.getElementById(`letterBtn-${letter}`);
                if (!btn) return;
                btn.className = selectedLetter === letter
                    ? 'w-9 h-9 sm:w-10 sm:h-10 rounded-lg border border-indigo-500 bg-indigo-600 text-white shadow-sm transition-all text-xs sm:text-sm font-semibold cursor-pointer'
                    : 'w-9 h-9 sm:w-10 sm:h-10 rounded-lg border border-slate-800 bg-slate-950/60 text-slate-400 hover:bg-slate-800 hover:text-white transition-all text-xs sm:text-sm font-semibold cursor-pointer';
            });
        }

        function renderComics() {
            const container = document.getElementById('comicContainer');
            const normalizedSearch = searchQuery.trim().toLowerCase();

            const filtered = comics.filter(c => {
                const title = (c.title || '').trim();
                const matchesSearch = !normalizedSearch || title.toLowerCase().includes(normalizedSearch);
                const matchesLetter = !selectedLetter || title.toUpperCase().startsWith(selectedLetter);
                return matchesSearch && matchesLetter;
            });

            if (filtered.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-20 bg-slate-900/30 border border-slate-800/80 rounded-3xl">
                        <div class="inline-flex p-4 bg-slate-800/50 rounded-2xl text-slate-500 mb-3 text-2xl">
                            <i class="fa-solid fa-ghost"></i>
                        </div>
                        <h3 class="text-slate-300 font-semibold text-lg">Tidak ada komik ditemukan</h3>
                        <p class="text-slate-500 text-sm mt-1">Coba cari judul lain atau tambahkan komik baru.</p>
                    </div>
                `;
                return;
            }

            if (viewMode === 'grid') {
                let html = '<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-5">';
                filtered.forEach(comic => {
                    const statusColor = comic.status === 'Completed' ? 'bg-emerald-500/10 text-emerald-400 border-emerald-500/20' : 
                                        comic.status === 'Reading' ? 'bg-indigo-500/10 text-indigo-400 border-indigo-500/20' : 'bg-amber-500/10 text-amber-400 border-amber-500/20';
                    const coverImg = comic.cover || 'https://placehold.co/400x300/1e293b/94a3b8?text=No+Cover';
                    
                    html += `
                        <div class="bg-slate-900/60 border border-slate-800 rounded-2xl overflow-hidden flex flex-col justify-between hover:border-slate-700 transition-all shadow-sm group">
                            <div>
                                <div class="relative h-40 w-full overflow-hidden bg-slate-950">
                                    <img src="${coverImg}" alt="${comic.title}" onerror="this.src='https://placehold.co/400x300/1e293b/94a3b8?text=Image+Error'" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500 opacity-80">
                                    <div class="absolute inset-0 bg-gradient-to-t from-slate-900 via-transparent"></div>
                                    <span class="absolute top-3 right-3 text-xs px-2.5 py-1 rounded-full border font-medium backdrop-blur-md ${statusColor}">
                                        ${comic.status}
                                    </span>
                                </div>
                                <div class="p-5 space-y-3">
                                    <h3 class="font-bold text-base text-white line-clamp-1" title="${comic.title}">${comic.title}</h3>
                                    <div class="flex items-center justify-between text-xs text-slate-400 bg-slate-950/40 p-2.5 rounded-xl border border-slate-800/50">
                                        <span>Chapter Terakhir</span>
                                        <div class="flex items-center gap-2">
                                            <button onclick="adjustChapter('${comic.id}', -1)" class="w-6 h-6 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-200 flex items-center justify-center transition-all cursor-pointer"><i class="fa-solid fa-minus text-[10px]"></i></button>
                                            <span class="font-bold text-indigo-400 text-sm">Ch. ${comic.chapter}</span>
                                            <button onclick="adjustChapter('${comic.id}', 1)" class="w-6 h-6 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-200 flex items-center justify-center transition-all cursor-pointer"><i class="fa-solid fa-plus text-[10px]"></i></button>
                                        </div>
                                    </div>
                                    <p class="text-[11px] text-slate-500 truncate" title="${comic.url}"><i class="fa-solid fa-link mr-1"></i> ${comic.url}</p>
                                    <p class="text-[11px] text-slate-500"><i class="fa-regular fa-clock mr-1"></i> Diperbarui: ${formatDate(comic.updatedAt)}</p>
                                </div>
                            </div>
                            <div class="p-4 pt-0 grid grid-cols-3 gap-2">
                                <a href="${comic.url}" target="_blank" class="col-span-2 bg-indigo-600 hover:bg-indigo-500 text-white py-2 px-3 rounded-xl text-xs font-semibold flex items-center justify-center gap-1.5 transition-all shadow-sm">
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
                let html = `
                    <div class="bg-slate-900/60 border border-slate-800 rounded-2xl overflow-x-auto shadow-sm">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-800 text-xs text-slate-400 uppercase tracking-wider bg-slate-950/40">
                                    <th class="p-4 font-semibold">Komik</th>
                                    <th class="p-4 font-semibold">Status</th>
                                    <th class="p-4 font-semibold">Chapter</th>
                                    <th class="p-4 font-semibold">Terakhir Dibaca</th>
                                    <th class="p-4 font-semibold text-right">Aksi</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-800/60 text-sm">
                `;
                filtered.forEach(comic => {
                    const statusColor = comic.status === 'Completed' ? 'bg-emerald-500/10 text-emerald-400 border-emerald-500/20' : 
                                        comic.status === 'Reading' ? 'bg-indigo-500/10 text-indigo-400 border-indigo-500/20' : 'bg-amber-500/10 text-amber-400 border-amber-500/20';
                    
                    html += `
                        <tr class="hover:bg-slate-800/30 transition-all">
                            <td class="p-4">
                                <div class="font-bold text-white">${comic.title}</div>
                                <a href="${comic.url}" target="_blank" class="text-xs text-indigo-400 hover:underline flex items-center gap-1 mt-0.5 max-w-xs truncate" title="${comic.url}">
                                    <span>${comic.url}</span> <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i>
                                </a>
                            </td>
                            <td class="p-4">
                                <span class="text-xs px-2.5 py-1 rounded-full border font-medium ${statusColor}">${comic.status}</span>
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
                                    <a href="${comic.url}" target="_blank" class="p-2 bg-indigo-600 hover:bg-indigo-500 text-white rounded-xl text-xs transition-all" title="Baca"><i class="fa-solid fa-book-open"></i></a>
                                    <button onclick="editComic('${comic.id}')" class="p-2 bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl text-xs transition-all cursor-pointer" title="Edit"><i class="fa-solid fa-pen"></i></button>
                                    <button onclick="deleteComic('${comic.id}')" class="p-2 bg-rose-500/10 hover:bg-rose-500/20 text-rose-400 border border-rose-500/20 rounded-xl text-xs transition-all cursor-pointer" title="Hapus"><i class="fa-solid fa-trash"></i></button>
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
            if (mode === 'grid') {
                document.getElementById('gridBtn').className = 'p-2 text-sm bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm';
                document.getElementById('tableBtn').className = 'p-2 text-sm bg-slate-800 hover:bg-slate-700 text-slate-400 rounded-xl transition-all cursor-pointer';
            } else {
                document.getElementById('tableBtn').className = 'p-2 text-sm bg-indigo-600 text-white rounded-xl transition-all cursor-pointer shadow-sm';
                document.getElementById('gridBtn').className = 'p-2 text-sm bg-slate-800 hover:bg-slate-700 text-slate-400 rounded-xl transition-all cursor-pointer';
            }
            renderComics();
        }

        function handleSearch() {
            searchQuery = document.getElementById('searchInput').value;
            renderComics();
        }

        function openModal(id = null) {
            document.getElementById('comicModal').classList.remove('hidden');
            if (id) {
                document.getElementById('modalTitle').innerText = 'Edit Komik';
                const comic = comics.find(c => c.id === id);
                if (comic) {
                    document.getElementById('comicId').value = comic.id;
                    document.getElementById('formTitle').value = comic.title;
                    document.getElementById('formUrl').value = comic.url;
                    document.getElementById('formChapter').value = comic.chapter;
                    document.getElementById('formStatus').value = comic.status;
                    document.getElementById('formCover').value = comic.cover || '';
                }
            } else {
                document.getElementById('modalTitle').innerText = 'Tambah Komik Baru';
                document.getElementById('comicForm').reset();
                document.getElementById('comicId').value = '';
            }
        }

        function closeModal() {
            document.getElementById('comicModal').classList.add('hidden');
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

            // Automatically synchronize URL with chapter on save/edit
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
                showToast('Komik berhasil ditambahkan!');
            }

            saveToStorage();
            renderComics();
            closeModal();
        }

        function adjustChapter(id, amount) {
            comics = comics.map(c => {
                if (c.id === id) {
                    const newChap = Math.max(0, c.chapter + amount);
                    // Automatically update URL based on new chapter
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
            if (confirm('Apakah Anda yakin ingin menghapus komik ini?')) {
                comics = comics.filter(c => c.id !== id);
                saveToStorage();
                renderComics();
                showToast('Komik berhasil dihapus!');
            }
        }

        function exportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(comics, null, 2));
            const dlAnchorElem = document.createElement('a');
            dlAnchorElem.setAttribute("href", dataStr);
            dlAnchorElem.setAttribute("download", `comicvault_backup_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(dlAnchorElem);
            dlAnchorElem.click();
            dlAnchorElem.remove();
            showToast('Backup data berhasil didownload!');
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
                            showToast('Data berhasil direstore!');
                        } else {
                            showToast('Format file backup salah.');
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
            
            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
