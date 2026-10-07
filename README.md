from pathlib import Path
import re

src = Path("/mnt/data/mykomik_abjad.html")
html = src.read_text(encoding="utf-8")

# Change branding/title.
html = html.replace(
    "<title>ComicVault - Offline Manga & Manhwa Tracker</title>",
    "<title>MyKomik - Koleksi Komik</title>"
)
html = html.replace(
    '<h1 class="font-bold text-lg tracking-tight bg-gradient-to-r from-white via-slate-200 to-slate-400 bg-clip-text text-transparent">ComicVault</h1>',
    '<h1 class="font-black text-xl tracking-tight text-white">My<span class="text-rose-500">Komik</span></h1>'
)
html = html.replace(
    '<p class="text-xs text-slate-400">Offline Manga & Manhwa Tracker</p>',
    '<p class="text-[11px] text-slate-500">Koleksi Manga & Manhwa Kamu</p>'
)

# Add a Shinigami-inspired visual layer without copying site assets/code.
visual_css = r"""
<style id="mykomik-shinigami-style">
:root {
    --mk-bg: #0b0b0d;
    --mk-panel: #121216;
    --mk-panel-2: #18181d;
    --mk-border: #27272f;
    --mk-text: #f4f4f5;
    --mk-muted: #9a9aa3;
    --mk-accent: #ef4444;
    --mk-accent-2: #fb7185;
}
html { background: var(--mk-bg) !important; }
body {
    background:
      radial-gradient(circle at 15% -10%, rgba(239,68,68,.14), transparent 28rem),
      radial-gradient(circle at 90% 5%, rgba(244,63,94,.08), transparent 24rem),
      var(--mk-bg) !important;
    color: var(--mk-text) !important;
}
header {
    background: rgba(11,11,13,.92) !important;
    border-bottom: 1px solid #202026 !important;
    box-shadow: 0 8px 30px rgba(0,0,0,.18);
}
header .bg-gradient-to-tr {
    background: linear-gradient(135deg,#ef4444,#be123c) !important;
    box-shadow: 0 8px 24px rgba(239,68,68,.22) !important;
    border-radius: 10px !important;
}
main { max-width: 1180px !important; }
main > .grid.grid-cols-1.sm\:grid-cols-3 {
    display: grid !important;
    grid-template-columns: repeat(3,minmax(0,1fr)) !important;
    gap: 12px !important;
}
main > .grid.grid-cols-1.sm\:grid-cols-3 > div {
    background: linear-gradient(180deg,#16161b,#111114) !important;
    border: 1px solid var(--mk-border) !important;
    border-radius: 12px !important;
    padding: 14px 16px !important;
}
main > .grid.grid-cols-1.sm\:grid-cols-3 > div > div:last-child {
    background: rgba(239,68,68,.08) !important;
    border-color: rgba(239,68,68,.18) !important;
    color: #fb7185 !important;
}
main > div:nth-of-type(2),
#alphabetFilter,
#comicContainer > div,
#comicContainer > div > div {
    border-color: var(--mk-border) !important;
}
main > div:nth-of-type(2) {
    background: rgba(18,18,22,.82) !important;
    border-radius: 12px !important;
}
#searchInput {
    background: #0d0d10 !important;
    border-color: #2b2b33 !important;
    border-radius: 9px !important;
}
#searchInput:focus {
    --tw-ring-color: rgba(239,68,68,.35) !important;
}
#alphabetFilter {
    display: flex !important;
    gap: 6px !important;
}
#alphabetFilter button {
    width: 34px !important;
    height: 34px !important;
    border-radius: 8px !important;
    background: #101014 !important;
    border: 1px solid #292930 !important;
    color: #a1a1aa !important;
}
#alphabetFilter button:hover {
    background: #27272d !important;
    color: white !important;
    border-color: #3f3f46 !important;
}
#alphabetFilter button.bg-indigo-600,
#alphabetFilter button[class*="border-indigo-500"] {
    background: #dc2626 !important;
    border-color: #ef4444 !important;
    color: white !important;
}
#letterAllBtn {
    background: #dc2626 !important;
    border-radius: 8px !important;
}
#comicContainer .bg-slate-900\/60 {
    background: #141418 !important;
    border-color: #28282f !important;
}
#comicContainer .bg-slate-900\/60:hover {
    border-color: #3a3a43 !important;
    transform: translateY(-2px);
    box-shadow: 0 14px 30px rgba(0,0,0,.24);
}
#comicContainer img {
    opacity: .92 !important;
}
#comicContainer .bg-gradient-to-t {
    background: linear-gradient(to top,rgba(20,20,24,.98),transparent) !important;
}
#comicContainer a.bg-indigo-600 {
    background: #dc2626 !important;
}
#comicContainer a.bg-indigo-600:hover {
    background: #ef4444 !important;
}
#comicContainer .text-indigo-400 {
    color: #fb7185 !important;
}
#comicContainer .bg-indigo-500\/10 {
    background: rgba(239,68,68,.08) !important;
}
button.bg-indigo-600 {
    background: #dc2626 !important;
}
button.bg-indigo-600:hover {
    background: #ef4444 !important;
}
#comicModal > div {
    background: #141418 !important;
    border-color: #2b2b32 !important;
}
#comicModal input, #comicModal select {
    background: #0d0d10 !important;
    border-color: #2b2b33 !important;
}
@media (max-width: 640px) {
    main { padding-top: 18px !important; }
    main > .grid.grid-cols-1.sm\:grid-cols-3 {
        grid-template-columns: 1fr !important;
    }
    #alphabetFilter { gap: 5px !important; }
    #alphabetFilter button {
        width: 30px !important;
        height: 30px !important;
        font-size: 11px !important;
    }
    header .h-16 { height: 58px !important; }
}
</style>
"""
html = html.replace("</head>", visual_css + "\n</head>", 1)

# Add a small catalog-style hero under the header.
hero_marker = """    <!-- Main Content -->
    <main class="flex-grow"""
hero = """    <!-- Catalog Hero -->
    <section class="border-b border-zinc-900 bg-zinc-950/70">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-7">
            <div class="flex flex-col md:flex-row md:items-end md:justify-between gap-4">
                <div>
                    <p class="text-[11px] uppercase tracking-[.22em] text-rose-500 font-bold mb-2">MYKOMIK LIBRARY</p>
                    <h2 class="text-2xl sm:text-3xl font-black text-white">Daftar Komik</h2>
                    <p class="text-sm text-zinc-500 mt-1">Simpan dan lanjutkan komik yang sedang kamu baca.</p>
                </div>
                <div class="text-xs text-zinc-500">Offline • Tersimpan di perangkat</div>
            </div>
        </div>
    </section>

    <!-- Main Content -->
    <main class="flex-grow"""
html = html.replace(hero_marker, hero, 1)

out = Path("/mnt/data/mykomik_shinigami_style.html")
out.write_text(html, encoding="utf-8")
print(f"Berhasil dibuat: {out}")
print("Tampilan diubah menjadi katalog manga dark/minimal bergaya Shinigami-inspired, sambil mempertahankan fitur dan data lokal.")
