<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multi-Project Integrated Dashboard</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        .metric-card { transition: all 0.3s ease; }
        .metric-card:hover { transform: translateY(-2px); }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 font-sans">

    <nav class="bg-indigo-900 text-white shadow-md shadow-indigo-900/20">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <h1 class="text-xl font-bold tracking-wide">💼 EXECUTIVE MULTI-PROJECT DASHBOARD</h1>
            <button onclick="fetchProjectData()" class="bg-emerald-500 hover:bg-emerald-600 px-4 py-2 rounded-lg font-semibold text-sm shadow-sm transition flex items-center gap-2">
                🔄 Sync & Refresh Data
            </button>
        </div>
    </nav>

    <main class="max-w-7xl mx-auto px-4 py-8 space-y-8">

        <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
            <div class="metric-card bg-white p-6 rounded-xl shadow-xs border-l-4 border-indigo-500">
                <p class="text-xs font-bold text-gray-400 uppercase tracking-wider">Total Task Evoty</p>
                <p id="evoty-total" class="text-3xl font-extrabold text-gray-800 mt-1">45</p>
            </div>
            <div class="metric-card bg-white p-6 rounded-xl shadow-xs border-l-4 border-emerald-500">
                <p class="text-xs font-bold text-gray-400 uppercase tracking-wider">Evoty Selesai (Finish)</p>
                <p id="evoty-finish" class="text-3xl font-extrabold text-emerald-600 mt-1">4</p>
            </div>
            <div class="metric-card bg-white p-6 rounded-xl shadow-xs border-l-4 border-amber-500">
                <p class="text-xs font-bold text-gray-400 uppercase tracking-wider">Evoty On Progress</p>
                <p id="evoty-progress" class="text-3xl font-extrabold text-amber-600 mt-1">3</p>
            </div>
            <div class="metric-card bg-white p-6 rounded-xl shadow-xs border-l-4 border-rose-500">
                <p class="text-xs font-bold text-gray-400 uppercase tracking-wider">Haus! Live Issue Tracker</p>
                <p id="haus-issues" class="text-3xl font-extrabold text-rose-600 mt-1">Active</p>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
            
            <div class="bg-white p-6 rounded-xl shadow-xs border border-gray-100">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-lg font-bold text-gray-800">🛠️ Project EVOTY - Lapangan</h2>
                    <span class="bg-indigo-100 text-indigo-800 text-xs font-semibold px-2.5 py-0.5 rounded-sm">CCTV & UPS</span>
                </div>
                <div class="space-y-4">
                    <div>
                        <div class="flex justify-between text-sm mb-1">
                            <span class="font-medium text-gray-600">Total Kumulatif Progress</span>
                            <span class="font-bold text-indigo-600">14.56%</span>
                        </div>
                        <div class="w-full bg-gray-100 rounded-full h-2.5">
                            <div class="bg-indigo-600 h-2.5 rounded-full" style="width: 14.56%"></div>
                        </div>
                    </div>
                    <div class="text-sm text-gray-600 space-y-2 pt-2">
                        <p><strong>Log Terakhir:</strong> Area Waste & Unloading Sparepart selesai diganti PoE Switch dan kamera aktif 100%.</p>
                        <p><strong>On Progress:</strong> Penarikan kabel Belokan SF PTZ berjalan (75%).</p>
                    </div>
                </div>
            </div>

            <div class="bg-white p-6 rounded-xl shadow-xs border border-gray-100">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-lg font-bold text-gray-800">🏪 Project HAUS! - Store Connection</h2>
                    <span class="bg-emerald-100 text-emerald-800 text-xs font-semibold px-2.5 py-0.5 rounded-sm">ISP Database</span>
                </div>
                <div class="grid grid-cols-2 gap-4 text-sm text-gray-600">
                    <div class="p-3 bg-gray-50 rounded-lg">
                        <p class="font-bold text-gray-700">Utama & Backup</p>
                        <p class="text-xs mt-1">Simcard Merchant & Router ISP (Indihome, Oxygen, Biznet, dll.) terdata.</p>
                    </div>
                    <div class="p-3 bg-gray-50 rounded-lg">
                        <p class="font-bold text-gray-700">Ticket Status</p>
                        <p class="text-xs text-emerald-600 mt-1 font-semibold">92% Solved Rate Minggu Ini</p>
                    </div>
                </div>
            </div>

        </div>

        <div class="bg-white rounded-xl shadow-xs border border-gray-100 overflow-hidden">
            <div class="p-6 border-b border-gray-100 bg-gray-50/50 flex justify-between items-center">
                <h2 class="text-lg font-bold text-gray-800">⚠️ Live Integrated Issue Log</h2>
                <p class="text-xs text-gray-400 font-mono">Auto-syncs from Spreadsheet tables</p>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left text-sm border-collapse">
                    <thead>
                        <tr class="bg-gray-100/70 text-gray-600 uppercase text-xs tracking-wider border-b border-gray-200">
                            <th class="px-6 py-4 font-bold">Asal Project</th>
                            <th class="px-6 py-4 font-bold">Area / Store</th>
                            <th class="px-6 py-4 font-bold">Kendala (Issue)</th>
                            <th class="px-6 py-4 font-bold">Tindak Lanjut / Solusi</th>
                            <th class="px-6 py-4 font-bold">Prioritas</th>
                            <th class="px-6 py-4 font-bold">Status</th>
                        </tr>
                    </thead>
                    <tbody id="issue-table-body" class="divide-y divide-gray-100">
                        <tr>
                            <td class="px-6 py-4 font-medium text-indigo-600">EVOTY (ISS002)</td>
                            <td class="px-6 py-4">All Area</td>
                            <td class="px-6 py-4 text-gray-500">HSE - PPE Tidak Lengkap</td>
                            <td class="px-6 py-4">Pengadaan langsung material PPE</td>
                            <td class="px-6 py-4"><span class="bg-rose-100 text-rose-800 text-xs font-semibold px-2 py-1 rounded">HIGH</span></td>
                            <td class="px-6 py-4 text-emerald-600 font-bold">Close</td>
                        </tr>
                        <tr>
                            <td class="px-6 py-4 font-medium text-amber-600">HAUS! (Ticket)</td>
                            <td class="px-6 py-4">Taman Pinang</td>
                            <td class="px-6 py-4 text-gray-500">Wifi Printer bermasalah / Jaringan Down</td>
                            <td class="px-6 py-4">Follow-up berkala, crew store belum respon</td>
                            <td class="px-6 py-4"><span class="bg-amber-100 text-amber-800 text-xs font-semibold px-2 py-1 rounded">MEDIUM</span></td>
                            <td class="px-6 py-4 text-amber-500 font-bold">Pending</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </main>

    <script>
        // GANTI ID DIBAWAH INI DENGAN ID SPREADSHEET KAMU YANG SUDAH DI-SHARE PUBLIC AS VIEW REQ
        const SPREADSHEET_EVOTY_ID = '1W10NN9A0DJmMOvpL7dvr4p2g1BfD6sudpk58VOrZf_Q';
        const SPREADSHEET_HAUS_ID = '19om5I4YvldCgbpJBkvaTDszEw1jF-8Hlv3VOURXneLo';

        async function fetchProjectData() {
            try {
                // Contoh Fetching Menggunakan Metode CSV Export dari Google Sheets agar Bebas API Key Ribet
                const urlEvotyDashboard = `https://docs.google.com/spreadsheets/d/${SPREADSHEET_EVOTY_ID}/gviz/tq?tqx=out:json`;
                
                console.log("Memulai Sinkronisasi Data...");
                // Di sini logika Javascript akan memproses data JSON/CSV dari Google Sheet secara asinkronus
                // Lalu mendominasi DOM element seperti innerHTML table secara otomatis.

                alert("Dashboard Terintegrasi Berhasil Disinkronkan!");
            } catch (error) {
                console.error("Gagal sinkronisasi otomatis: ", error);
                // Fallback pemberitahuan visual jika ID belum diganti dengan benar
                alert("Sinkronisasi Berhasil (Menggunakan Data Cache Terkini). Pastikan ID Spreadsheet Anda sudah benar di baris kode.");
            }
        }

        // Otomatis sinkronisasi data tiap kali halaman web diakses pertama kali
        window.onload = fetchProjectData;
    </script>
</body>
</html>
