<!DOCTYPE html>
<html lang="id" class="h-full bg-slate-50">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SIPAGU - Layanan Administrasi Guru</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#ecfdf5',
                            100: '#d1fae5',
                            500: '#10b981',
                            600: '#059669',
                            700: '#047857',
                            900: '#064e3b',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        .custom-scrollbar::-webkit-scrollbar { width: 6px; height: 6px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #f1f5f9; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
        @media print {
            .no-print { display: none !important; }
            .print-only { display: block !important; }
            body { background: white; font-size: 12pt; }
        }
    </style>
</head>
<body class="h-full flex flex-col text-slate-800 antialiased custom-scrollbar">

    <div id="toast-container" class="fixed top-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <header class="bg-slate-900 text-white shadow-lg sticky top-0 z-30 no-print">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Logo & Title -->
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-lg bg-emerald-500 flex items-center justify-center text-white shadow-md font-bold text-xl">
                        <i class="fa-solid fa-graduation-cap"></i>
                    </div>
                    <div>
                        <span class="font-bold text-lg leading-none block tracking-wide text-white">SIPAGU</span>
                        <span class="text-xs text-emerald-400 font-medium">Layanan Administrasi Guru</span>
                    </div>
                </div>

                <!-- View Mode Switcher & Profile -->
                <div class="flex items-center space-x-4">
                    <!-- Mode Switcher -->
                    <div class="bg-slate-800 p-1 rounded-xl flex items-center border border-slate-700">
                        <button id="btn-mode-guru" onclick="switchViewMode('guru')" class="px-3 py-1.5 rounded-lg text-xs font-semibold transition-all duration-200 bg-emerald-600 text-white shadow">
                            <i class="fa-solid fa-user-tie mr-1"></i> Mode Guru
                        </button>
                        <button id="btn-mode-supervisor" onclick="switchViewMode('supervisor')" class="px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition-all duration-200">
                            <i class="fa-solid fa-user-shield mr-1"></i> Supervisor / Kurikulum
                        </button>
                    </div>

                    <!-- Profile Avatar -->
                    <div class="hidden sm:flex items-center space-x-3 pl-4 border-l border-slate-700">
                        <div class="text-right">
                            <p id="header-user-name" class="text-sm font-semibold text-slate-100">Redi Fitrianda,S.Pd</p>
                            <p id="header-user-role" class="text-xs text-slate-400">NIP. 19830511 200604 1 009</p>
                        </div>
                        <img class="h-9 w-9 rounded-full ring-2 ring-emerald-500 object-cover" src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&q=80&w=256" alt="Profile">
                    </div>
                </div>
            </div>
        </div>
    </header>

    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">

        <!-- ================= MODE GURU VIEW ================= -->
        <div id="view-guru" class="space-y-6">
            
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-5 sm:p-6 transition-all">
                <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between gap-6">
                    <!-- Identity Info -->
                    <div class="flex items-start sm:items-center space-x-4">
                        <img class="h-16 w-16 sm:h-20 sm:w-20 rounded-2xl object-cover ring-4 ring-emerald-50 shadow-sm" src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&q=80&w=256" alt="Guru Avatar">
                        <div>
                            <div class="flex items-center space-x-2">
                                <h1 class="text-xl sm:text-2xl font-bold text-slate-900">Muhammad Rasyid, S.Pd</h1>
                                <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800">Aktif</span>
                            </div>
                            <p class="text-xs sm:text-sm text-slate-500 font-medium">NIP: 19920202 202321 1 012 • </p>
                            
                            <div class="mt-2 flex flex-wrap gap-2 text-xs">
                                <span class="bg-slate-100 text-slate-700 px-2.5 py-1 rounded-md font-medium"><i class="fa-solid fa-book-open text-emerald-600 mr-1"></i>Penjas Orkes</span>
                                <span class="bg-slate-100 text-slate-700 px-2.5 py-1 rounded-md font-medium"><i class="fa-solid fa-chalkboard-user text-emerald-600 mr-1"></i> Kelas VII-A, VII-B, VIII-A, VIII-B, IX-A, IX-B</span>
                                <span class="bg-slate-100 text-slate-700 px-2.5 py-1 rounded-md font-medium"><i class="fa-solid fa-calendar-days text-emerald-600 mr-1"></i> Semester Ganjil 2026/2027</span>
                            </div>
                        </div>
                    </div>

                    <!-- Overall Progress Card -->
                    <div class="bg-slate-50 border border-slate-200 rounded-xl p-4 min-w-[280px]">
                        <div class="flex justify-between items-center mb-2">
                            <span class="text-xs font-bold text-slate-600 uppercase tracking-wider">Progres Kelengkapan</span>
                            <span id="overall-progress-text" class="text-sm font-extrabold text-emerald-600">75%</span>
                        </div>
                        <div class="w-full bg-slate-200 rounded-full h-3 overflow-hidden">
                            <div id="overall-progress-bar" class="bg-emerald-500 h-3 rounded-full transition-all duration-500" style="width: 75%"></div>
                        </div>
                        <div class="mt-3 flex justify-between text-[11px] text-slate-500">
                            <span>Target Selesai: 15 Okt 2026</span>
                            <span id="overall-progress-count" class="font-semibold text-slate-700">12 / 16 Berkas</span>
                        </div>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-3">
                    <div class="p-3 bg-blue-50 text-blue-600 rounded-lg">
                        <i class="fa-solid fa-folder-open text-xl"></i>
                    </div>
                    <div>
                        <p class="text-xs font-medium text-slate-500">Total Berkas</p>
                        <p id="stat-total" class="text-xl font-bold text-slate-800">16</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-3">
                    <div class="p-3 bg-emerald-50 text-emerald-600 rounded-lg">
                        <i class="fa-solid fa-circle-check text-xl"></i>
                    </div>
                    <div>
                        <p class="text-xs font-medium text-slate-500">Disetujui</p>
                        <p id="stat-approved" class="text-xl font-bold text-emerald-600">12</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-3">
                    <div class="p-3 bg-amber-50 text-amber-600 rounded-lg">
                        <i class="fa-solid fa-clock text-xl"></i>
                    </div>
                    <div>
                        <p class="text-xs font-medium text-slate-500">Verifikasi</p>
                        <p id="stat-pending" class="text-xl font-bold text-amber-600">2</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-3">
                    <div class="p-3 bg-rose-50 text-rose-600 rounded-lg">
                        <i class="fa-solid fa-triangle-exclamation text-xl"></i>
                    </div>
                    <div>
                        <p class="text-xs font-medium text-slate-500">Perlu Revisi / Belum</p>
                        <p id="stat-revision" class="text-xl font-bold text-rose-600">2</p>
                    </div>
                </div>
            </div>

            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4 border-b border-slate-200 pb-2">
                <!-- Navigation Tabs -->
                <div class="flex overflow-x-auto space-x-2 custom-scrollbar pb-2 sm:pb-0">
                    <button onclick="switchGuruTab('perencanaan')" id="tab-btn-perencanaan" class="guru-tab-btn active px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all bg-emerald-600 text-white shadow-sm">
                        <i class="fa-solid fa-compass mr-1.5"></i> Perencanaan Pembelajaran
                    </button>
                    <button onclick="switchGuruTab('pelaksanaan')" id="tab-btn-pelaksanaan" class="guru-tab-btn px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all text-slate-600 hover:bg-slate-200 hover:text-slate-900">
                        <i class="fa-solid fa-clipboard-user mr-1.5"></i> Pelaksanaan & Presensi
                    </button>
                    <button onclick="switchGuruTab('penilaian')" id="tab-btn-penilaian" class="guru-tab-btn px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all text-slate-600 hover:bg-slate-200 hover:text-slate-900">
                        <i class="fa-solid fa-chart-line mr-1.5"></i> Penilaian & Evaluasi
                    </button>
                    <button onclick="switchGuruTab('tugas')" id="tab-btn-tugas" class="guru-tab-btn px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all text-slate-600 hover:bg-slate-200 hover:text-slate-900">
                        <i class="fa-solid fa-award mr-1.5"></i> Tugas Tambahan & Diklat
                    </button>
                    <button onclick="switchGuruTab('jurnal-harian')" id="tab-btn-jurnal-harian" class="guru-tab-btn px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all text-purple-700 bg-purple-50 hover:bg-purple-100 border border-purple-200">
                        <i class="fa-solid fa-book mr-1.5"></i> Jurnal Mengajar Harian
                    </button>
                </div>

                <!-- Upload New Document Button -->
                <button onclick="openUploadModal()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg text-sm font-semibold shadow flex items-center justify-center transition-all shrink-0">
                    <i class="fa-solid fa-cloud-arrow-up mr-2"></i> Unggah Dokumen
                </button>
            </div>

            <div id="filter-controls-container" class="flex flex-col sm:flex-row gap-3 bg-white p-3 rounded-xl border border-slate-200 shadow-sm">
                <div class="relative flex-1">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3 text-slate-400"></i>
                    <input type="text" id="doc-search-input" onkeyup="filterDocuments()" placeholder="Cari nama dokumen, modul, atau catatan..." class="w-full pl-10 pr-4 py-2 border border-slate-300 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none">
                </div>
                <div class="flex gap-2">
                    <select id="doc-status-filter" onchange="filterDocuments()" class="px-3 py-2 border border-slate-300 rounded-lg text-sm bg-white focus:ring-2 focus:ring-emerald-500 outline-none">
                        <option value="ALL">Semua Status</option>
                        <option value="Disetujui">Disetujui</option>
                        <option value="Menunggu Verifikasi">Menunggu Verifikasi</option>
                        <option value="Perlu Perbaikan">Perlu Perbaikan</option>
                        <option value="Belum Diunggah">Belum Diunggah</option>
                    </select>
                </div>
            </div>

            <div id="guru-tab-content" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
                <!-- Document Cards dynamically rendered by JavaScript -->
            </div>

            <div id="jurnal-harian-view" class="hidden space-y-6">
                <!-- Section Title & Add Form Button -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    
                    <!-- Left Column: Form Pengisian Jurnal Harian -->
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm space-y-4 lg:col-span-1">
                        <h2 class="text-base font-bold text-slate-900 border-b pb-2 flex items-center">
                            <i class="fa-solid fa-pen-to-square text-purple-600 mr-2"></i> Isi Jurnal Mengajar Harian
                        </h2>
                        
                        <form id="form-jurnal-harian" onsubmit="handleSaveJurnal(event)" class="space-y-3">
                            <div>
                                <label class="block text-xs font-medium text-slate-700 mb-1">Tanggal & Jam Ke</label>
                                <div class="grid grid-cols-2 gap-2">
                                    <input type="date" id="jurnal-tanggal" required class="w-full px-3 py-1.5 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-purple-500">
                                    <input type="text" id="jurnal-jam" placeholder="Misal: 1 - 2 (07.30-09.00)" required class="w-full px-3 py-1.5 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-purple-500">
                                </div>
                            </div>

                            <div class="grid grid-cols-2 gap-2">
                                <div>
                                    <label class="block text-xs font-medium text-slate-700 mb-1">Kelas</label>
                                    <select id="jurnal-kelas" required class="w-full px-3 py-1.5 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-purple-500 bg-white">
                                        <option value="VII-A">VII-A (Penjas Orkes)</option>
                                        <option value="VII-B">VII-B (Penjas Orkes)</option>
                                        <option value="VIII-A">VIII-A (Penjas Orkes)</option>
					<option value="VIII-B">VIII-B (Penjas Orkes)</option>
					<option value="IX-A">IX-A (Penjas Orkes)</option>
					<option value="IX-B">IX-B (Penjas Orkes)</option>

                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs font-medium text-slate-700 mb-1">Mata Pelajaran</label>
                                    <input type="text" id="jurnal-mapel" value="Penjas Orkes" readonly class="w-full px-3 py-1.5 border border-slate-200 bg-slate-50 rounded-lg text-xs text-slate-600 font-medium">
                                </div>
                            </div>

                            <div>
                                <label class="block text-xs font-medium text-slate-700 mb-1">Materi Pembelajaran / Pembahasan</label>
                                <textarea id="jurnal-materi" rows="2" placeholder="Tulis ringkasan materi pembelajaran..." required class="w-full px-3 py-1.5 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-purple-500"></textarea>
                            </div>

                            <div>
                                <label class="block text-xs font-medium text-slate-700 mb-1">Presensi Siswa (Jumlah)</label>
                                <div class="grid grid-cols-4 gap-1 text-center">
                                    <div>
                                        <span class="text-[10px] text-emerald-700 font-medium">Hadir</span>
                                        <input type="number" id="jurnal-hadir" value="32" min="0" class="w-full px-2 py-1 text-center border border-slate-300 rounded text-xs">
                                    </div>
                                    <div>
                                        <span class="text-[10px] text-blue-700 font-medium">Sakit</span>
                                        <input type="number" id="jurnal-sakit" value="0" min="0" class="w-full px-2 py-1 text-center border border-slate-300 rounded text-xs">
                                    </div>
                                    <div>
                                        <span class="text-[10px] text-amber-700 font-medium">Izin</span>
                                        <input type="number" id="jurnal-izin" value="1" min="0" class="w-full px-2 py-1 text-center border border-slate-300 rounded text-xs">
                                    </div>
                                    <div>
                                        <span class="text-[10px] text-rose-700 font-medium">Alpha</span>
                                        <input type="number" id="jurnal-alpha" value="0" min="0" class="w-full px-2 py-1 text-center border border-slate-300 rounded text-xs">
                                    </div>
                                </div>
                            </div>

                            <div>
                                <label class="block text-xs font-medium text-slate-700 mb-1">Catatan Kejadian Penting / Kendala</label>
                                <input type="text" id="jurnal-catatan" placeholder="Opsional: Misal kendala proyektor atau antusiasme siswa" class="w-full px-3 py-1.5 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-purple-500">
                            </div>

                            <div>
                                <label class="block text-xs font-medium text-slate-700 mb-1">Link Foto Kegiatan / Dokumentasi</label>
                                <input type="url" id="jurnal-foto" placeholder="https://drive.google.com/..." class="w-full px-3 py-1.5 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-purple-500">
                            </div>

                            <button type="submit" class="w-full py-2 bg-purple-600 hover:bg-purple-700 text-white font-semibold rounded-lg text-xs transition shadow">
                                <i class="fa-solid fa-floppy-disk mr-1"></i> Simpan Jurnal Mengajar
                            </button>
                        </form>
                    </div>

                    <!-- Right Column: Riwayat & Daftar Jurnal -->
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm space-y-4 lg:col-span-2">
                        <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-3 border-b pb-2">
                            <h2 class="text-base font-bold text-slate-900 flex items-center">
                                <i class="fa-solid fa-clock-rotate-left text-slate-600 mr-2"></i> Riwayat Jurnal Mengajar
                            </h2>
                            <div class="flex space-x-2">
                                <select id="filter-jurnal-kelas" onchange="renderJurnalHistory()" class="px-2.5 py-1 border border-slate-300 rounded-lg text-xs bg-white outline-none">
                                    <option value="ALL">Semua Kelas</option>
                                    <option value="VII-A">VII-A (Penjas Orkes)</option>
                                    <option value="VII-B">VII-B (Penjas Orkes)</option>
                                    <option value="VIII-A">VIII-A (Penjas Orkes)</option>
					<option value="VIII-B">VIII-B (Penjas Orkes)</option>
					<option value="IX-A">IX-A (Penjas Orkes)</option>
					<option value="IX-B">IX-B (Penjas Orkes)</option>

                                </select>
                            </div>
                        </div>

                        <!-- Jurnal Table -->
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs text-slate-600">
                                <thead class="bg-slate-100 text-slate-700 uppercase font-bold text-[10px]">
                                    <tr>
                                        <th class="p-2.5 rounded-l-lg">Tgl / Jam</th>
                                        <th class="p-2.5">Kelas</th>
                                        <th class="p-2.5">Materi Pembelajaran</th>
                                        <th class="p-2.5">Kehadiran</th>
                                        <th class="p-2.5">Catatan</th>
                                        <th class="p-2.5 rounded-r-lg text-center">Aksi</th>
                                    </tr>
                                </thead>
                                <tbody id="jurnal-table-body" class="divide-y divide-slate-100">
                                    <!-- Dynamic Rows Rendered by JS -->
                                </tbody>
                            </table>
                        </div>
                    </div>

                </div>
            </div>

        </div>

        <!-- ================= MODE SUPERVISOR / KURIKULUM VIEW ================= -->
        <div id="view-supervisor" class="hidden space-y-6">
            
            <div class="bg-slate-900 text-white rounded-2xl p-6 shadow-md border border-slate-800">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <div class="flex items-center space-x-2">
                            <span class="px-2.5 py-0.5 rounded-full text-xs font-bold bg-amber-500 text-slate-950 uppercase tracking-wider">Akses Supervisor</span>
                            <h1 class="text-xl sm:text-2xl font-bold text-white">Monitoring Administrasi Guru & Supervisi</h1>
                        </div>
                        <p class="text-xs sm:text-sm text-slate-300 mt-1">Pantau, periksa, dan verifikasi berkas administrasi pembelajaran guru secara real-time.</p>
                    </div>

                    <div class="flex items-center space-x-3 no-print">
                        <button onclick="window.print()" class="px-3.5 py-2 bg-slate-800 hover:bg-slate-700 text-slate-200 border border-slate-700 rounded-lg text-xs font-semibold flex items-center shadow-sm">
                            <i class="fa-solid fa-print mr-1.5"></i> Cetak / Export PDF
                        </button>
                        <button onclick="exportToCSV()" class="px-3.5 py-2 bg-emerald-600 hover:bg-emerald-500 text-white rounded-lg text-xs font-semibold flex items-center shadow-sm">
                            <i class="fa-solid fa-file-excel mr-1.5"></i> Export Excel (.CSV)
                        </button>
                    </div>
                </div>

                <!-- Supervisor Stats Summary Grid -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mt-6 pt-6 border-t border-slate-800">
                    <div>
                        <p class="text-xs text-slate-400 font-medium">Total Guru Terdaftar</p>
                        <p class="text-xl font-bold text-white mt-0.5">8 Orang</p>
                    </div>
                    <div>
                        <p class="text-xs text-slate-400 font-medium">Rata-Rata Kelengkapan</p>
                        <p class="text-xl font-bold text-emerald-400 mt-0.5">82.5%</p>
                    </div>
                    <div>
                        <p class="text-xs text-slate-400 font-medium">Perlu Verifikasi Hari Ini</p>
                        <p class="text-xl font-bold text-amber-400 mt-0.5">5 Berkas</p>
                    </div>
                    <div>
                        <p class="text-xs text-slate-400 font-medium">Status Periode</p>
                        <p class="text-xl font-bold text-blue-400 mt-0.5">Ganjil 2026/2027</p>
                    </div>
                </div>
            </div>

            <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm flex flex-col md:flex-row gap-4 items-center justify-between no-print">
                <div class="flex flex-col sm:flex-row gap-3 w-full md:w-auto flex-1">
                    <div class="relative flex-1">
                        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3 text-slate-400"></i>
                        <input type="text" id="supervisor-search-guru" onkeyup="renderSupervisorTable()" placeholder="Cari nama guru atau NIP..." class="w-full pl-10 pr-4 py-2 border border-slate-300 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none">
                    </div>
                    <select id="supervisor-filter-mapel" onchange="renderSupervisorTable()" class="px-3 py-2 border border-slate-300 rounded-lg text-sm bg-white focus:ring-2 focus:ring-emerald-500 outline-none">
                        <option value="ALL">Semua Mata Pelajaran</option>
                        <option value="Penjas Orkes">Penjas Orkes</option>
                        <option value="Matematika">Matematika</option>
                        <option value="Bahasa Indonesia">Bahasa Indonesia</option>
                        <option value="Bahasa Inggris">Bahasa Inggris</option>
                        <option value="Fisika">Fisika</option>
			<option value="IPA">IPA</option>
                        <option value="IPS">IPS</option>
                        <option value="PKN">PKN</option>
                        <option value="Informatika">Informatika</option>
                        <option value="Prakarya">Prakarya</option>
			<option value="Bimbingan Konseling">Bimbingan Konseling</option>
                    </select>
                </div>

                <div class="text-xs text-slate-500 font-medium">
                    Menampilkan <span id="supervisor-count" class="font-bold text-slate-800">0</span> Guru
                </div>
            </div>

            <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs border-collapse">
                        <thead class="bg-slate-100 text-slate-700 font-bold uppercase tracking-wider border-b border-slate-200">
                            <tr>
                                <th class="p-3.5">Guru / NIP</th>
                                <th class="p-3.5">Mata Pelajaran</th>
                                <th class="p-3.5 text-center">RPP / Modul</th>
                                <th class="p-3.5 text-center">Jurnal / Absens</th>
                                <th class="p-3.5 text-center">Prota / Promes</th>
                                <th class="p-3.5 text-center">Penilaian</th>
                                <th class="p-3.5 text-center">Kelengkapan</th>
                                <th class="p-3.5 text-center no-print">Aksi & Catatan</th>
                            </tr>
                        </thead>
                        <tbody id="supervisor-table-body" class="divide-y divide-slate-200">
                            <!-- Dynamic Rows Rendered by JS -->
                        </tbody>
                    </table>
                </div>
            </div>

        </div>

    </main>

    <div id="modal-upload" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-lg w-full shadow-2xl overflow-hidden border border-slate-100 transform transition-all">
            <!-- Modal Header -->
            <div class="bg-slate-900 text-white p-4 px-6 flex justify-between items-center">
                <h3 id="modal-upload-title" class="text-base font-bold flex items-center">
                    <i class="fa-solid fa-cloud-arrow-up text-emerald-400 mr-2"></i> Unggah Dokumen Administrasi
                </h3>
                <button onclick="closeUploadModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <!-- Modal Form -->
            <form id="form-upload-doc" onsubmit="handleSaveDocument(event)" class="p-6 space-y-4">
                <input type="hidden" id="upload-doc-id">
                
                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Kategori Administrasi</label>
                    <select id="upload-category" required onchange="updateSubCategoryOptions()" class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs bg-white focus:ring-2 focus:ring-emerald-500 outline-none">
                        <option value="perencanaan">1. Perencanaan Pembelajaran</option>
                        <option value="pelaksanaan">2. Pelaksanaan & Presensi</option>
                        <option value="penilaian">3. Penilaian & Evaluasi</option>
                        <option value="tugas">4. Tugas Tambahan & Diklat</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Jenis Dokumen</label>
                    <select id="upload-subcategory" required class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs bg-white focus:ring-2 focus:ring-emerald-500 outline-none">
                        <!-- Populated dynamically based on category -->
                    </select>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Semester</label>
                        <select id="upload-semester" class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs bg-white outline-none">
                            <option value="Ganjil">Ganjil</option>
                            <option value="Genap">Genap</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Tahun Ajaran</label>
                        <input type="text" id="upload-tahun" value="2026/2027" required class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-emerald-500">
                    </div>
                </div>

                <!-- Interactive File Upload / Google Drive Link Option -->
                <div class="space-y-2">
                    <label class="block text-xs font-semibold text-slate-700">Sumber File / Link Dokumen</label>
                    
                    <!-- Drag & Drop Zone Simulation -->
                    <div id="drop-zone" onclick="triggerFileInput()" class="border-2 border-dashed border-slate-300 rounded-xl p-4 text-center cursor-pointer hover:border-emerald-500 hover:bg-emerald-50/50 transition">
                        <i class="fa-solid fa-file-pdf text-3xl text-slate-400 mb-1"></i>
                        <p class="text-xs font-semibold text-slate-700">Klik atau Drag & Drop Berkas di sini</p>
                        <p class="text-[11px] text-slate-400">Format: PDF, DOCX, XLSX (Maks. 15MB)</p>
                        <input type="file" id="file-input-hidden" class="hidden" onchange="handleFileSelect(event)">
                    </div>

                    <div id="file-preview-badge" class="hidden bg-emerald-50 border border-emerald-200 p-2.5 rounded-lg flex items-center justify-between text-xs">
                        <div class="flex items-center space-x-2 truncate">
                            <i class="fa-solid fa-file-circle-check text-emerald-600"></i>
                            <span id="preview-filename" class="font-semibold text-emerald-900 truncate">nama_file.pdf</span>
                        </div>
                        <span id="preview-filesize" class="text-[10px] text-emerald-700 font-mono">1.2 MB</span>
                    </div>

                    <div class="relative my-2 text-center">
                        <span class="bg-white px-2 text-[10px] text-slate-400 font-bold uppercase relative z-10">Atau Gunakan Link Cloud</span>
                        <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-slate-200"></div></div>
                    </div>

                    <div>
                        <input type="url" id="upload-link" placeholder="https://drive.google.com/file/d/..." class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-emerald-500">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Catatan Tambahan untuk Supervisor</label>
                    <textarea id="upload-notes" rows="2" placeholder="Misal: Sudah disesuaikan dengan revisi Kurikulum Merdeka..." class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-emerald-500"></textarea>
                </div>

                <!-- Modal Actions -->
                <div class="pt-3 flex justify-end space-x-2 border-t border-slate-100">
                    <button type="button" onclick="closeUploadModal()" class="px-4 py-2 border border-slate-300 rounded-lg text-xs font-semibold text-slate-600 hover:bg-slate-100 transition">
                        Batal
                    </button>
                    <button type="submit" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg text-xs font-semibold shadow transition">
                        <i class="fa-solid fa-paper-plane mr-1"></i> Simpan & Upload
                    </button>
                </div>
            </form>
        </div>
    </div>

    <div id="modal-supervisor-verify" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-lg w-full shadow-2xl overflow-hidden border border-slate-100">
            <div class="bg-slate-900 text-white p-4 px-6 flex justify-between items-center">
                <h3 class="text-base font-bold flex items-center">
                    <i class="fa-solid fa-user-check text-emerald-400 mr-2"></i> Verifikasi & Supervisi Berkas
                </h3>
                <button onclick="closeVerifyModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <div class="p-6 space-y-4">
                <div class="bg-slate-50 p-3 rounded-lg border border-slate-200 text-xs space-y-1">
                    <p class="font-bold text-slate-800" id="verify-guru-name">Nama Guru: -</p>
                    <p class="text-slate-600" id="verify-doc-title">Dokumen: Modul Ajar Informatika Bab 1</p>
                    <p class="text-slate-500" id="verify-upload-time">Tanggal Upload: -</p>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Status Keputusan Verifikasi</label>
                    <div class="grid grid-cols-2 gap-2">
                        <button type="button" onclick="selectVerifyStatus('Disetujui')" id="btn-status-approve" class="p-2.5 rounded-lg border-2 border-emerald-500 bg-emerald-50 text-emerald-800 text-xs font-bold flex items-center justify-center">
                            <i class="fa-solid fa-circle-check mr-1.5 text-emerald-600"></i> Setujui Berkas
                        </button>
                        <button type="button" onclick="selectVerifyStatus('Perlu Perbaikan')" id="btn-status-reject" class="p-2.5 rounded-lg border border-slate-300 text-slate-700 text-xs font-bold flex items-center justify-center">
                            <i class="fa-solid fa-circle-exclamation mr-1.5 text-amber-600"></i> Minta Perbaikan
                        </button>
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 mb-1">Catatan / Masukan Supervisor</label>
                    <textarea id="verify-notes" rows="3" placeholder="Tulis catatan masukan atau instruksi revisi..." class="w-full px-3 py-2 border border-slate-300 rounded-lg text-xs outline-none focus:ring-2 focus:ring-emerald-500"></textarea>
                </div>

                <div class="pt-3 flex justify-end space-x-2 border-t border-slate-100">
                    <button type="button" onclick="closeVerifyModal()" class="px-4 py-2 border border-slate-300 rounded-lg text-xs font-semibold text-slate-600 hover:bg-slate-100">
                        Batal
                    </button>
                    <button type="button" onclick="saveVerificationResult()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg text-xs font-semibold shadow">
                        Simpan Keputusan
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="modal-preview" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-2xl w-full shadow-2xl overflow-hidden border border-slate-100 flex flex-col max-h-[85vh]">
            <div class="bg-slate-900 text-white p-4 px-6 flex justify-between items-center">
                <div class="truncate mr-4">
                    <h3 id="preview-modal-title" class="text-base font-bold truncate">Preview Dokumen</h3>
                    <p id="preview-modal-sub" class="text-xs text-slate-400 truncate">Sistem Layanan Administrasi</p>
                </div>
                <button onclick="closePreviewModal()" class="text-slate-400 hover:text-white transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <div class="p-6 flex-1 overflow-y-auto space-y-4">
                <!-- File Header Box -->
                <div class="bg-slate-50 border border-slate-200 rounded-xl p-4 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <div class="w-12 h-12 rounded-lg bg-rose-100 text-rose-600 flex items-center justify-center text-2xl font-bold">
                            <i class="fa-solid fa-file-pdf"></i>
                        </div>
                        <div>
                            <h4 id="preview-doc-name" class="text-sm font-bold text-slate-800">Nama_Dokumen.pdf</h4>
                            <p id="preview-doc-meta" class="text-xs text-slate-500">1.4 MB • Diunggah 04 Okt 2026</p>
                        </div>
                    </div>
                    <a id="preview-doc-download-link" href="#" target="_blank" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-white text-xs font-semibold rounded-lg shadow transition">
                        <i class="fa-solid fa-arrow-down-long mr-1"></i> Unduh
                    </a>
                </div>

                <!-- Simulated PDF Visual Viewer -->
                <div class="border border-slate-200 rounded-xl bg-slate-100 p-8 text-center space-y-4">
                    <i class="fa-solid fa-book-open-reader text-5xl text-slate-400"></i>
                    <div class="max-w-md mx-auto">
                        <p class="text-sm font-semibold text-slate-700">Simulasi Tampilan Preview Dokumen</p>
                        <p class="text-xs text-slate-500 mt-1">Dokumen telah terverifikasi aman. Anda dapat membuka atau mengunduh dokumen secara lengkap melalui tautan cloud penyimpanan resmi.</p>
                    </div>
                </div>

                <!-- Notes History Box -->
                <div class="bg-amber-50 border border-amber-200 rounded-xl p-4 space-y-1">
                    <p class="text-xs font-bold text-amber-900"><i class="fa-solid fa-comment-dots mr-1"></i> Catatan Evaluasi Supervisor:</p>
                    <p id="preview-doc-notes" class="text-xs text-amber-800 italic">"Dokumen RPP sudah sesuai dengan CP Kurikulum Merdeka 2026."</p>
                </div>
            </div>

            <div class="p-4 bg-slate-50 border-t border-slate-200 text-right">
                <button onclick="closePreviewModal()" class="px-4 py-2 bg-slate-800 text-white rounded-lg text-xs font-semibold">Tutup Preview</button>
            </div>
        </div>
    </div>

    <script>
        // Default Subcategories mapping
        const CATEGORY_MAP = {
            'perencanaan': [
                'Capaian Pembelajaran (CP) / Ki-KD',
                'Alur Tujuan Pembelajaran (ATP) / Silabus',
                'Modul Ajar / RPP',
                'Program Tahunan (Prota) & Program Semester (Promes)',
                'Kriteria Ketercapaian Tujuan Pembelajaran (KKTP) / KKM'
            ],
            'pelaksanaan': [
                'Jurnal Mengajar / Agenda Harian Guru',
                'Daftar Hadir Siswa',
                'Buku Batas / Catatan Pembelajaran'
            ],
            'penilaian': [
                'Kisi-kisi & Soal Asesmen / Ujian',
                'Analisis Hasil Belajar / Analisis Ulangan',
                'Bank Soal & Rubrik Penilaian'
            ],
            'tugas': [
                'SK / Laporan Tugas Tambahan',
                'Sertifikat Pelatihan / Diklat / Web Seminar',
                'Laporan Kinerja Guru (LKG) / SKP'
            ]
        };

        // Application State Data
        let currentViewMode = 'guru'; // 'guru' or 'supervisor'
        let activeGuruTab = 'perencanaan'; // 'perencanaan', 'pelaksanaan', 'penilaian', 'tugas', 'jurnal-harian'
        let activeVerifyStatus = 'Disetujui';
        let currentVerifyingDocId = null;

        // Dummy Documents for Current Teacher
        let documentList = [
            {
                id: 1,
                category: 'perencanaan',
                subCategory: 'Capaian Pembelajaran (CP) / Ki-KD',
                title: 'CP Informatika Fase E Tahun 2026',
                semester: 'Ganjil',
                tahun: '2026/2027',
                fileUrl: 'https://drive.google.com/sample_cp',
                fileName: 'CP_Informatika_Fase_E.pdf',
                fileSize: '1.2 MB',
                uploadDate: '2026-09-10',
                status: 'Disetujui',
                notes: 'Sudah sesuai SKBS terbaru.',
                supervisorNotes: 'Sangat baik, lengkap.'
            },
            {
                id: 2,
                category: 'perencanaan',
                subCategory: 'Modul Ajar / RPP',
                title: 'Modul Ajar Algoritma & Pemrograman Kelas X',
                semester: 'Ganjil',
                tahun: '2026/2027',
                fileUrl: 'https://drive.google.com/sample_rpp',
                fileName: 'Modul_Ajar_Algoritma_X.pdf',
                fileSize: '2.5 MB',
                uploadDate: '2026-09-15',
                status: 'Disetujui',
                notes: 'Termasuk LKPD dan asesmen diagnostik.',
                supervisorNotes: 'Telah diverifikasi oleh Kurikulum.'
            },
            {
                id: 3,
                category: 'perencanaan',
                subCategory: 'Program Tahunan (Prota) & Program Semester (Promes)',
                title: 'Prota & Promes Informatika 2026/2027',
                semester: 'Ganjil',
                tahun: '2026/2027',
                fileUrl: '',
                fileName: 'Prota_Promes_2026.xlsx',
                fileSize: '850 KB',
                uploadDate: '2026-09-28',
                status: 'Menunggu Verifikasi',
                notes: 'Mohon masukan untuk alokasi jam projek.',
                supervisorNotes: ''
            },
            {
                id: 4,
                category: 'pelaksanaan',
                subCategory: 'Daftar Hadir Siswa',
                title: 'Absensi Siswa Kelas X-1 & X-2',
                semester: 'Ganjil',
                tahun: '2026/2027',
                fileUrl: '',
                fileName: 'Absensi_Oktober_2026.pdf',
                fileSize: '620 KB',
                uploadDate: '2026-10-01',
                status: 'Disetujui',
                notes: 'Rekap kehadiran bulan September.',
                supervisorNotes: 'Bagus, teratur.'
            },
            {
                id: 5,
                category: 'penilaian',
                subCategory: 'Kisi-kisi & Soal Asesmen / Ujian',
                title: 'Soal Assessment Sumatif Tengah Semester (STS)',
                semester: 'Ganjil',
                tahun: '2026/2027',
                fileUrl: '',
                fileName: 'Soal_STS_Informatika.docx',
                fileSize: '1.8 MB',
                uploadDate: '2026-09-20',
                status: 'Perlu Perbaikan',
                notes: 'Draft awal soal STS.',
                supervisorNotes: 'Harap tambahkan kunci jawaban dan rubrik penilaian HOTS.'
            },
            {
                id: 6,
                category: 'tugas',
                subCategory: 'SK / Laporan Tugas Tambahan',
                title: 'SK Kepala Laboratorium Komputer',
                semester: 'Ganjil',
                tahun: '2026/2027',
                fileUrl: '',
                fileName: 'SK_Ka_Lab_Komputer.pdf',
                fileSize: '1.1 MB',
                uploadDate: '2026-08-25',
                status: 'Disetujui',
                notes: 'SK Tugas Tambahan dari Kepala Sekolah.',
                supervisorNotes: 'Valid.'
            }
        ];

        // Dummy Jurnal Mengajar Harian
        let jurnalList = [
            {
                id: 101,
                tanggal: '2026-10-02',
                jam: '1 - 3 (07.30 - 09.45)',
                kelas: 'X-1',
                mapel: 'Informatika',
                materi: 'Konsep Pemrograman Terstruktur dan Variabel C++',
                hadir: 34, sakit: 1, izin: 0, alpha: 0,
                catatan: 'Siswa antusias saat praktek lab komputer.',
                fotoUrl: 'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&q=80&w=300'
            },
            {
                id: 102,
                tanggal: '2026-10-04',
                jam: '4 - 5 (10.00 - 11.30)',
                kelas: 'X-2',
                mapel: 'Informatika',
                materi: 'Analisis Data & Visualisasi dengan Excel',
                hadir: 32, sakit: 0, izin: 2, alpha: 0,
                catatan: 'Proyektor ruang lab sempat terkendala koneksi HDMI.',
                fotoUrl: ''
            }
        ];

        // Dummy Supervisor Teachers Master Data
        let supervisorTeachers = [
            { id: 1, name: 'Kamaruddin, S.Pd', nip: '19710504 199802 1 003', mapel: 'Matematika', rpp: 'Disetujui', jurnal: 'Lengkap', prota: 'Menunggu Verifikasi', penilaian: 'Perlu Perbaikan', progress: 75, notes: 'Mohon lengkapi perbaikan revisi soal STS.' },
            { id: 2, name: 'Pahriatie, S.Pd', nip: '19750223 200604 1 003', mapel: 'Bimbingan Konseling', rpp: 'Disetujui', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Disetujui', progress: 100, notes: 'Administrasi sangat rapi dan lengkap.' },
            { id: 3, name: 'Susilawati, S.Pd', nip: '19821030 200804 2 003', mapel: 'IPA', rpp: 'Disetujui', jurnal: 'Belum', prota: 'Disetujui', penilaian: 'Menunggu Verifikasi', progress: 65, notes: 'Jurnal harian belum diisi bulan ini.' },
            { id: 4, name: 'Yulida Agustina, S.Pd', nip: '19830729 201001 2 011', mapel: 'Bahasa Indonesia', rpp: 'Perlu Perbaikan', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Disetujui', progress: 80, notes: 'RPP butuh penyesuaian asesmen formatif.' },
            { id: 5, name: 'Rahmatullah, S.Pd.I', nip: '19840710 200904 1 009', mapel: 'Bahasa Inggris', rpp: 'Disetujui', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Disetujui', progress: 100, notes: 'Sempurna.' },
            { id: 6, name: 'Eka Purnamasari, S.Pd', nip: '19860523 200904 2 003', mapel: 'IPS', rpp: 'Menunggu Verifikasi', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Belum', progress: 60, notes: 'Proses verifikasi RPP.' }
            { id: 7, name: 'Misda Liani, S.Pd', nip: '19921017 201903 2 015', mapel: 'Bahasa Inggris', rpp: 'Menunggu Verifikasi', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Belum', progress: 60, notes: 'Proses verifikasi RPP.' }
 	{ id: 8, name: 'Muhammad Rasyid, S.Pd', nip: '19920202 202321 1 012', mapel: 'Penjas Orkes', rpp: 'Menunggu Verifikasi', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Belum', progress: 60, notes: 'Proses verifikasi RPP.' }
    	 { id: 9, name: 'Pia Ramadayanti, S.Pd', nip: '19980103 202421 2 034', mapel: 'PKN', rpp: 'Menunggu Verifikasi', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Belum', progress: 60, notes: 'Proses verifikasi RPP.' }
            { id: 10, name: 'Mau Izzatul Husna, S.Pd', nip: '20010415 202521 2 019', mapel: 'Informatika/Prakarya', rpp: 'Menunggu Verifikasi', jurnal: 'Lengkap', prota: 'Disetujui', penilaian: 'Belum', progress: 60, notes: 'Proses verifikasi RPP.' }

        ];

        window.onload = function() {
            // Set current date on Jurnal Form
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('jurnal-tanggal').value = today;

            updateSubCategoryOptions();
            renderGuruDocuments();
            renderJurnalHistory();
            calculateOverallProgress();
            renderSupervisorTable();
        };

        // Switch View Modes (Mode Guru vs Mode Supervisor)
        function switchViewMode(mode) {
            currentViewMode = mode;
            const guruView = document.getElementById('view-guru');
            const superView = document.getElementById('view-supervisor');
            const btnGuru = document.getElementById('btn-mode-guru');
            const btnSuper = document.getElementById('btn-mode-supervisor');

            if (mode === 'guru') {
                guruView.classList.remove('hidden');
                superView.classList.add('hidden');
                btnGuru.className = "px-3 py-1.5 rounded-lg text-xs font-semibold transition-all duration-200 bg-emerald-600 text-white shadow";
                btnSuper.className = "px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition-all duration-200";
            } else {
                guruView.classList.add('hidden');
                superView.classList.remove('hidden');
                btnSuper.className = "px-3 py-1.5 rounded-lg text-xs font-semibold transition-all duration-200 bg-emerald-600 text-white shadow";
                btnGuru.className = "px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition-all duration-200";
                renderSupervisorTable();
            }
        }

        // Switch Tabs within Mode Guru
        function switchGuruTab(tab) {
            activeGuruTab = tab;
            const tabs = ['perencanaan', 'pelaksanaan', 'penilaian', 'tugas', 'jurnal-harian'];
            
            tabs.forEach(t => {
                const btn = document.getElementById(`tab-btn-${t}`);
                if (btn) {
                    if (t === tab) {
                        btn.className = "guru-tab-btn active px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all bg-emerald-600 text-white shadow-sm";
                    } else if (t === 'jurnal-harian') {
                        btn.className = "guru-tab-btn px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all text-purple-700 bg-purple-50 hover:bg-purple-100 border border-purple-200";
                    } else {
                        btn.className = "guru-tab-btn px-4 py-2 rounded-lg text-sm font-semibold whitespace-nowrap transition-all text-slate-600 hover:bg-slate-200 hover:text-slate-900";
                    }
                }
            });

            const docGrid = document.getElementById('guru-tab-content');
            const jurnalView = document.getElementById('jurnal-harian-view');
            const filterControls = document.getElementById('filter-controls-container');

            if (tab === 'jurnal-harian') {
                docGrid.classList.add('hidden');
                filterControls.classList.add('hidden');
                jurnalView.classList.remove('hidden');
            } else {
                docGrid.classList.remove('hidden');
                filterControls.classList.remove('hidden');
                jurnalView.classList.add('hidden');
                renderGuruDocuments();
            }
        }

        // Render Guru Document Cards
        function renderGuruDocuments() {
            const container = document.getElementById('guru-tab-content');
            const searchKeyword = document.getElementById('doc-search-input').value.toLowerCase();
            const selectedStatus = document.getElementById('doc-status-filter').value;

            // Get subcategories required for current active tab
            const subCats = CATEGORY_MAP[activeGuruTab] || [];

            let html = '';

            subCats.forEach(subCat => {
                // Find existing doc in data
                const existingDoc = documentList.find(d => d.category === activeGuruTab && d.subCategory === subCat);

                // Filter check
                if (existingDoc) {
                    if (selectedStatus !== 'ALL' && existingDoc.status !== selectedStatus) return;
                    if (searchKeyword && !existingDoc.title.toLowerCase().includes(searchKeyword) && !subCat.toLowerCase().includes(searchKeyword)) return;
                } else {
                    if (selectedStatus !== 'ALL' && selectedStatus !== 'Belum Diunggah') return;
                    if (searchKeyword && !subCat.toLowerCase().includes(searchKeyword)) return;
                }

                if (existingDoc) {
                    // Status Badge Styling
                    let statusBadge = '';
                    if (existingDoc.status === 'Disetujui') {
                        statusBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-emerald-100 text-emerald-800 border border-emerald-200"><i class="fa-solid fa-circle-check mr-1"></i> Disetujui</span>`;
                    } else if (existingDoc.status === 'Menunggu Verifikasi') {
                        statusBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-amber-100 text-amber-800 border border-amber-200"><i class="fa-solid fa-clock mr-1"></i> Menunggu Verifikasi</span>`;
                    } else {
                        statusBadge = `<span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-rose-100 text-rose-800 border border-rose-200"><i class="fa-solid fa-triangle-exclamation mr-1"></i> Perlu Perbaikan</span>`;
                    }

                    html += `
                    <div class="bg-white rounded-xl border border-slate-200 shadow-sm hover:shadow-md transition p-5 flex flex-col justify-between">
                        <div>
                            <div class="flex items-start justify-between gap-2 mb-2">
                                <span class="text-[10px] font-bold uppercase tracking-wider text-slate-400">${subCat}</span>
                                ${statusBadge}
                            </div>
                            <h3 class="text-sm font-bold text-slate-900 leading-snug mb-1">${existingDoc.title}</h3>
                            <p class="text-xs text-slate-500 font-medium mb-3"><i class="fa-solid fa-paperclip mr-1"></i> ${existingDoc.fileName} (${existingDoc.fileSize})</p>

                            ${existingDoc.supervisorNotes ? `
                            <div class="bg-slate-50 border-l-2 border-amber-500 p-2 rounded-r text-[11px] text-slate-600 mb-3 italic">
                                <strong>Catatan Supervisor:</strong> "${existingDoc.supervisorNotes}"
                            </div>
                            ` : ''}
                        </div>

                        <div class="pt-3 border-t border-slate-100 flex items-center justify-between text-xs">
                            <span class="text-slate-400 text-[11px]"><i class="fa-regular fa-calendar mr-1"></i> ${existingDoc.uploadDate}</span>
                            <div class="flex space-x-1">
                                <button onclick="openPreviewModal(${existingDoc.id})" class="p-1.5 hover:bg-slate-100 rounded text-slate-600 font-medium" title="Preview">
                                    <i class="fa-solid fa-eye text-emerald-600"></i>
                                </button>
                                <button onclick="editDocument(${existingDoc.id})" class="p-1.5 hover:bg-slate-100 rounded text-slate-600 font-medium" title="Edit">
                                    <i class="fa-solid fa-pen-to-square text-blue-600"></i>
                                </button>
                                <button onclick="deleteDocument(${existingDoc.id})" class="p-1.5 hover:bg-slate-100 rounded text-slate-600 font-medium" title="Hapus">
                                    <i class="fa-solid fa-trash text-rose-600"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                    `;
                } else {
                    // Empty Placeholder Card for missing docs
                    html += `
                    <div class="bg-slate-50/70 rounded-xl border-2 border-dashed border-slate-200 p-5 flex flex-col justify-between hover:border-slate-300 transition">
                        <div>
                            <div class="flex items-start justify-between gap-2 mb-2">
                                <span class="text-[10px] font-bold uppercase tracking-wider text-slate-400">${subCat}</span>
                                <span class="px-2.5 py-1 rounded-full text-[11px] font-bold bg-slate-200 text-slate-600"><i class="fa-solid fa-circle-minus mr-1"></i> Belum Diunggah</span>
                            </div>
                            <h3 class="text-sm font-semibold text-slate-500 leading-snug mb-2">${subCat} belum diunggah</h3>
                            <p class="text-xs text-slate-400">Silakan unggah berkas administrasi ini untuk melengkapi kewajiban semester.</p>
                        </div>

                        <div class="pt-4 mt-3">
                            <button onclick="openUploadModal('${activeGuruTab}', '${subCat}')" class="w-full py-1.5 bg-white border border-slate-300 hover:border-emerald-500 hover:text-emerald-600 text-slate-700 font-semibold rounded-lg text-xs transition shadow-sm flex items-center justify-center">
                                <i class="fa-solid fa-plus mr-1.5 text-emerald-500"></i> Unggah Berkas Ini
                            </button>
                        </div>
                    </div>
                    `;
                }
            });

            container.innerHTML = html || `<div class="col-span-full text-center py-8 text-slate-400 text-xs">Tidak ada dokumen yang sesuai filter.</div>`;
        }

        // Filter Action Trigger
        function filterDocuments() {
            renderGuruDocuments();
        }

        // Handle File Select in Modal
        function handleFileSelect(event) {
            const file = event.target.files[0];
            if (file) {
                document.getElementById('file-preview-badge').classList.remove('hidden');
                document.getElementById('preview-filename').innerText = file.name;
                document.getElementById('preview-filesize').innerText = (file.size / (1024 * 1024)).toFixed(2) + ' MB';
            }
        }

        function triggerFileInput() {
            document.getElementById('file-input-hidden').click();
        }

        // Dynamic Subcategory update in Modal
        function updateSubCategoryOptions() {
            const catSelect = document.getElementById('upload-category');
            const subSelect = document.getElementById('upload-subcategory');
            const selectedCat = catSelect.value;

            const options = CATEGORY_MAP[selectedCat] || [];
            subSelect.innerHTML = options.map(opt => `<option value="${opt}">${opt}</option>`).join('');
        }

        // Open Modal for Uploading
        function openUploadModal(category = null, subcategory = null) {
            document.getElementById('form-upload-doc').reset();
            document.getElementById('upload-doc-id').value = '';
            document.getElementById('file-preview-badge').classList.add('hidden');
            document.getElementById('modal-upload-title').innerHTML = `<i class="fa-solid fa-cloud-arrow-up text-emerald-400 mr-2"></i> Unggah Dokumen Administrasi`;

            if (category) {
                document.getElementById('upload-category').value = category;
                updateSubCategoryOptions();
            }
            if (subcategory) {
                document.getElementById('upload-subcategory').value = subcategory;
            }

            document.getElementById('modal-upload').classList.remove('hidden');
        }

        function closeUploadModal() {
            document.getElementById('modal-upload').classList.add('hidden');
        }

        // Save Uploaded or Edited Document
        function handleSaveDocument(e) {
            e.preventDefault();
            const docId = document.getElementById('upload-doc-id').value;
            const category = document.getElementById('upload-category').value;
            const subCategory = document.getElementById('upload-subcategory').value;
            const semester = document.getElementById('upload-semester').value;
            const tahun = document.getElementById('upload-tahun').value;
            const link = document.getElementById('upload-link').value;
            const notes = document.getElementById('upload-notes').value;
            const fileInput = document.getElementById('file-input-hidden');

            let fileName = 'Dokumen_Administrasi.pdf';
            let fileSize = '1.5 MB';

            if (fileInput.files.length > 0) {
                fileName = fileInput.files[0].name;
                fileSize = (fileInput.files[0].size / (1024 * 1024)).toFixed(2) + ' MB';
            }

            if (docId) {
                // Edit Existing
                const index = documentList.findIndex(d => d.id == docId);
                if (index !== -1) {
                    documentList[index].category = category;
                    documentList[index].subCategory = subCategory;
                    documentList[index].semester = semester;
                    documentList[index].tahun = tahun;
                    documentList[index].fileUrl = link;
                    documentList[index].notes = notes;
                    documentList[index].status = 'Menunggu Verifikasi'; // Reset to pending after edit
                    showToast('Dokumen berhasil diperbarui & dikirim ulang!', 'success');
                }
            } else {
                // Create New
                const newDoc = {
                    id: Date.now(),
                    category,
                    subCategory,
                    title: `${subCategory} (${semester} ${tahun})`,
                    semester,
                    tahun,
                    fileUrl: link,
                    fileName,
                    fileSize,
                    uploadDate: new Date().toISOString().split('T')[0],
                    status: 'Menunggu Verifikasi',
                    notes,
                    supervisorNotes: ''
                };
                documentList.push(newDoc);
                showToast('Dokumen berhasil diunggah untuk verifikasi!', 'success');
            }

            calculateOverallProgress();
            renderGuruDocuments();
            closeUploadModal();
        }

        // Edit Document
        function editDocument(id) {
            const doc = documentList.find(d => d.id === id);
            if (!doc) return;

            document.getElementById('upload-doc-id').value = doc.id;
            document.getElementById('upload-category').value = doc.category;
            updateSubCategoryOptions();
            document.getElementById('upload-subcategory').value = doc.subCategory;
            document.getElementById('upload-semester').value = doc.semester;
            document.getElementById('upload-tahun').value = doc.tahun;
            document.getElementById('upload-link').value = doc.fileUrl || '';
            document.getElementById('upload-notes').value = doc.notes || '';

            document.getElementById('modal-upload-title').innerHTML = `<i class="fa-solid fa-pen-to-square text-emerald-400 mr-2"></i> Edit Dokumen Administrasi`;
            document.getElementById('modal-upload').classList.remove('hidden');
        }

        // Delete Document
        function deleteDocument(id) {
            if (confirm('Apakah Anda yakin ingin menghapus dokumen ini?')) {
                documentList = documentList.filter(d => d.id !== id);
                calculateOverallProgress();
                renderGuruDocuments();
                showToast('Dokumen berhasil dihapus.', 'info');
            }
        }

        // Calculate Guru Overall Progress
        function calculateOverallProgress() {
            // Total required items across categories = 16
            const totalRequired = 16;
            const approvedCount = documentList.filter(d => d.status === 'Disetujui').length;
            const pendingCount = documentList.filter(d => d.status === 'Menunggu Verifikasi').length;
            const revisionCount = documentList.filter(d => d.status === 'Perlu Perbaikan').length;

            const percentage = Math.round((approvedCount / totalRequired) * 100);

            document.getElementById('overall-progress-text').innerText = `${percentage}%`;
            document.getElementById('overall-progress-bar').style.width = `${percentage}%`;
            document.getElementById('overall-progress-count').innerText = `${approvedCount} / ${totalRequired} Berkas`;

            document.getElementById('stat-total').innerText = totalRequired;
            document.getElementById('stat-approved').innerText = approvedCount;
            document.getElementById('stat-pending').innerText = pendingCount;
            document.getElementById('stat-revision').innerText = revisionCount + (totalRequired - documentList.length);
        }

        // Save Jurnal Mengajar Harian
        function handleSaveJurnal(e) {
            e.preventDefault();
            const tanggal = document.getElementById('jurnal-tanggal').value;
            const jam = document.getElementById('jurnal-jam').value;
            const kelas = document.getElementById('jurnal-kelas').value;
            const mapel = document.getElementById('jurnal-mapel').value;
            const materi = document.getElementById('jurnal-materi').value;
            const hadir = parseInt(document.getElementById('jurnal-hadir').value) || 0;
            const sakit = parseInt(document.getElementById('jurnal-sakit').value) || 0;
            const izin = parseInt(document.getElementById('jurnal-izin').value) || 0;
            const alpha = parseInt(document.getElementById('jurnal-alpha').value) || 0;
            const catatan = document.getElementById('jurnal-catatan').value;
            const fotoUrl = document.getElementById('jurnal-foto').value;

            const newJurnal = {
                id: Date.now(),
                tanggal,
                jam,
                kelas,
                mapel,
                materi,
                hadir, sakit, izin, alpha,
                catatan,
                fotoUrl
            };

            jurnalList.unshift(newJurnal);
            renderJurnalHistory();
            document.getElementById('form-jurnal-harian').reset();
            document.getElementById('jurnal-tanggal').value = new Date().toISOString().split('T')[0];
            showToast('Jurnal mengajar harian tersimpan!', 'success');
        }

        // Render Jurnal Table
        function renderJurnalHistory() {
            const tbody = document.getElementById('jurnal-table-body');
            const filterKelas = document.getElementById('filter-jurnal-kelas').value;

            let filtered = jurnalList;
            if (filterKelas !== 'ALL') {
                filtered = jurnalList.filter(j => j.kelas === filterKelas);
            }

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="text-center py-6 text-slate-400">Belum ada catatan jurnal harian.</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map(j => `
                <tr class="hover:bg-slate-50 transition">
                    <td class="p-2.5 font-medium text-slate-800">
                        <div>${j.tanggal}</div>
                        <div class="text-[10px] text-slate-400">Jam: ${j.jam}</div>
                    </td>
                    <td class="p-2.5"><span class="px-2 py-0.5 rounded bg-slate-100 font-bold text-slate-700 text-[10px]">${j.kelas}</span></td>
                    <td class="p-2.5 font-medium text-slate-800 max-w-xs truncate">${j.materi}</td>
                    <td class="p-2.5 text-[11px]">
                        <span class="text-emerald-700 font-bold">H:${j.hadir}</span> • 
                        <span class="text-blue-600">S:${j.sakit}</span> • 
                        <span class="text-amber-600">I:${j.izin}</span> • 
                        <span class="text-rose-600">A:${j.alpha}</span>
                    </td>
                    <td class="p-2.5 text-slate-500 italic max-w-xs truncate">${j.catatan || '-'}</td>
                    <td class="p-2.5 text-center">
                        <button onclick="deleteJurnal(${j.id})" class="text-rose-600 hover:text-rose-800 font-bold"><i class="fa-solid fa-trash-can"></i></button>
                    </td>
                </tr>
            `).join('');
        }

        function deleteJurnal(id) {
            if (confirm('Hapus entri jurnal ini?')) {
                jurnalList = jurnalList.filter(j => j.id !== id);
                renderJurnalHistory();
                showToast('Jurnal dihapus.', 'info');
            }
        }

        // Render Supervisor Table
        function renderSupervisorTable() {
            const tbody = document.getElementById('supervisor-table-body');
            const keyword = document.getElementById('supervisor-search-guru').value.toLowerCase();
            const filterMapel = document.getElementById('supervisor-filter-mapel').value;

            let filtered = supervisorTeachers.filter(t => {
                const matchKeyword = t.name.toLowerCase().includes(keyword) || t.nip.includes(keyword);
                const matchMapel = filterMapel === 'ALL' || t.mapel === filterMapel;
                return matchKeyword && matchMapel;
            });

            document.getElementById('supervisor-count').innerText = filtered.length;

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="text-center py-6 text-slate-400">Tidak ada data guru yang cocok.</td></tr>`;
                return;
            }

            tbody.innerHTML = filtered.map(t => {
                // Status badge helper for columns
                const getStatusPill = (status) => {
                    if (status === 'Disetujui' || status === 'Lengkap') return `<span class="px-2 py-0.5 rounded text-[10px] font-bold bg-emerald-100 text-emerald-800">Lengkap</span>`;
                    if (status === 'Menunggu Verifikasi') return `<span class="px-2 py-0.5 rounded text-[10px] font-bold bg-amber-100 text-amber-800">Periksa</span>`;
                    if (status === 'Perlu Perbaikan') return `<span class="px-2 py-0.5 rounded text-[10px] font-bold bg-rose-100 text-rose-800">Revisi</span>`;
                    return `<span class="px-2 py-0.5 rounded text-[10px] font-bold bg-slate-100 text-slate-500">Belum</span>`;
                };

                return `
                <tr class="hover:bg-slate-50 transition border-b border-slate-100">
                    <td class="p-3.5">
                        <p class="font-bold text-slate-900">${t.name}</p>
                        <p class="text-[11px] text-slate-500">NIP: ${t.nip}</p>
                    </td>
                    <td class="p-3.5 font-medium text-slate-700">${t.mapel}</td>
                    <td class="p-3.5 text-center">${getStatusPill(t.rpp)}</td>
                    <td class="p-3.5 text-center">${getStatusPill(t.jurnal)}</td>
                    <td class="p-3.5 text-center">${getStatusPill(t.prota)}</td>
                    <td class="p-3.5 text-center">${getStatusPill(t.penilaian)}</td>
                    <td class="p-3.5 text-center">
                        <div class="flex items-center justify-center space-x-1.5">
                            <span class="font-extrabold text-xs text-slate-800">${t.progress}%</span>
                            <div class="w-12 bg-slate-200 rounded-full h-1.5 overflow-hidden">
                                <div class="bg-emerald-500 h-1.5 rounded-full" style="width: ${t.progress}%"></div>
                            </div>
                        </div>
                    </td>
                    <td class="p-3.5 text-center space-x-1 no-print">
                        <button onclick="openVerifyModal(${t.id})" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 text-white font-semibold rounded text-[11px] shadow-sm">
                            <i class="fa-solid fa-clipboard-check mr-1"></i> Verifikasi
                        </button>
                    </td>
                </tr>
                `;
            }).join('');
        }

        // Open Verify Modal for Supervisor
        function openVerifyModal(teacherId) {
            const teacher = supervisorTeachers.find(t => t.id === teacherId);
            if (!teacher) return;

            currentVerifyingDocId = teacherId;
            document.getElementById('verify-guru-name').innerText = `Nama Guru: ${teacher.name} (${teacher.mapel})`;
            document.getElementById('verify-doc-title').innerText = `Dokumen: Berkas Administrasi Utama (RPP / Prota / Penilaian)`;
            document.getElementById('verify-upload-time').innerText = `Tanggal Upload Terakhir: 04 Oktober 2026`;
            document.getElementById('verify-notes').value = teacher.notes || '';

            selectVerifyStatus('Disetujui');
            document.getElementById('modal-supervisor-verify').classList.remove('hidden');
        }

        function closeVerifyModal() {
            document.getElementById('modal-supervisor-verify').classList.add('hidden');
        }

        function selectVerifyStatus(status) {
            activeVerifyStatus = status;
            const btnApprove = document.getElementById('btn-status-approve');
            const btnReject = document.getElementById('btn-status-reject');

            if (status === 'Disetujui') {
                btnApprove.className = "p-2.5 rounded-lg border-2 border-emerald-500 bg-emerald-50 text-emerald-800 text-xs font-bold flex items-center justify-center shadow-sm";
                btnReject.className = "p-2.5 rounded-lg border border-slate-300 text-slate-700 text-xs font-bold flex items-center justify-center";
            } else {
                btnReject.className = "p-2.5 rounded-lg border-2 border-amber-500 bg-amber-50 text-amber-800 text-xs font-bold flex items-center justify-center shadow-sm";
                btnApprove.className = "p-2.5 rounded-lg border border-slate-300 text-slate-700 text-xs font-bold flex items-center justify-center";
            }
        }

        function saveVerificationResult() {
            const notes = document.getElementById('verify-notes').value;
            const teacher = supervisorTeachers.find(t => t.id === currentVerifyingDocId);

            if (teacher) {
                teacher.notes = notes;
                if (activeVerifyStatus === 'Disetujui') {
                    teacher.rpp = 'Disetujui';
                    teacher.prota = 'Disetujui';
                    teacher.progress = 100;
                } else {
                    teacher.rpp = 'Perlu Perbaikan';
                    teacher.progress = 70;
                }
            }

            renderSupervisorTable();
            closeVerifyModal();
            showToast('Keputusan verifikasi berhasil disimpan!', 'success');
        }

        // Open Preview Modal
        function openPreviewModal(docId) {
            const doc = documentList.find(d => d.id === docId);
            if (!doc) return;

            document.getElementById('preview-modal-title').innerText = doc.title;
            document.getElementById('preview-modal-sub').innerText = `${doc.subCategory} • ${doc.semester} ${doc.tahun}`;
            document.getElementById('preview-doc-name').innerText = doc.fileName;
            document.getElementById('preview-doc-meta').innerText = `${doc.fileSize} • Diunggah ${doc.uploadDate}`;
            document.getElementById('preview-doc-notes').innerText = doc.supervisorNotes ? `"${doc.supervisorNotes}"` : 'Belum ada catatan dari supervisor.';

            document.getElementById('modal-preview').classList.remove('hidden');
        }

        function closePreviewModal() {
            document.getElementById('modal-preview').classList.add('hidden');
        }

        // Export Supervisor Rekap to CSV
        function exportToCSV() {
            let csvContent = "data:text/csv;charset=utf-8,";
            csvContent += "Nama Guru,NIP,Mata Pelajaran,RPP,Jurnal,Prota,Penilaian,Kelengkapan (%),Catatan\n";

            supervisorTeachers.forEach(t => {
                csvContent += `"${t.name}","${t.nip}","${t.mapel}","${t.rpp}","${t.jurnal}","${t.prota}","${t.penilaian}","${t.progress}%","${t.notes}"\n`;
            });

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `Rekap_Administrasi_Guru_SIPAGU_${new Date().toISOString().split('T')[0]}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);

            showToast('Rekapitulasi CSV berhasil diunduh!', 'success');
        }

        // Toast Notification Helper
        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');

            let bg = 'bg-slate-900 text-white';
            let icon = 'fa-info-circle text-blue-400';

            if (type === 'success') {
                bg = 'bg-emerald-900 text-white border border-emerald-700';
                icon = 'fa-circle-check text-emerald-400';
            } else if (type === 'error') {
                bg = 'bg-rose-900 text-white border border-rose-700';
                icon = 'fa-circle-xmark text-rose-400';
            }

            toast.className = `${bg} px-4 py-3 rounded-xl shadow-xl flex items-center space-x-3 text-xs font-semibold pointer-events-auto transform transition duration-300 translate-y-2 opacity-0`;
            toast.innerHTML = `<i class="fa-solid ${icon} text-base"></i> <span>${message}</span>`;

            container.appendChild(toast);

            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 10);

            setTimeout(() => {
                toast.classList.add('opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }
    </script>
</body>
</html>
