<!DOCTYPE html>
<html lang="kk" class="h-full bg-slate-50">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Тәрбие ісі мен Сынып жетекшілерінің бірыңғай порталы</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
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
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            500: '#0284c7',
                            600: '#0369a1',
                            700: '#075985',
                            800: '#0c4a6e',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="h-full font-sans text-slate-800 antialiased flex flex-col min-h-screen">

    <!-- Top Header Navigation -->
    <header class="bg-gradient-to-r from-slate-900 via-brand-800 to-slate-900 text-white shadow-lg sticky top-0 z-30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Organization Branding -->
                <div class="flex items-center space-x-3">
                    <div class="bg-brand-500/20 p-2 rounded-xl border border-brand-400/30">
                        <i class="fa-solid fa-school text-brand-400 text-2xl"></i>
                    </div>
                    <div>
                        <h1 id="orgNameHeader" class="text-base sm:text-lg font-bold tracking-wide text-white leading-tight">№15 Жалпы білім беретін мектеп-лицейі</h1>
                        <p class="text-xs text-brand-200">Тәрбие ісі жөніндегі орынбасарлары мен Сынып жетекшілер цифрлық порталы</p>
                    </div>
                </div>

                <!-- Right Actions & User Profile -->
                <div class="flex items-center space-x-3">
                    <!-- Global Search Quick trigger -->
                    <div class="hidden md:flex items-center bg-slate-800/80 rounded-lg px-3 py-1.5 border border-slate-700 text-slate-300 text-xs">
                        <i class="fa-solid fa-magnifying-glass mr-2 text-slate-400"></i>
                        <span id="academicYearBadge">2026-2027 Оқу жылы</span>
                    </div>

                    <!-- Auth State Badge -->
                    <div id="userBadge" class="flex items-center space-x-2 bg-slate-800/90 border border-slate-700 px-3 py-1.5 rounded-lg text-xs">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                        <span id="currentUserRole" class="font-medium text-emerald-300">Администратор (Гугл)</span>
                    </div>

                    <!-- System Auth Dropdown Switcher -->
                    <div class="relative inline-block text-left">
                        <button onclick="toggleAuthMenu()" class="p-2 text-slate-300 hover:text-white rounded-lg hover:bg-slate-800 transition">
                            <i class="fa-solid fa-user-gear text-lg"></i>
                        </button>
                        <div id="authMenuDropdown" class="hidden absolute right-0 mt-2 w-64 bg-white rounded-xl shadow-2xl border border-slate-100 py-2 z-50 text-slate-700">
                            <div class="px-4 py-2 border-b border-slate-100 bg-slate-50">
                                <p class="text-xs text-slate-500 font-semibold uppercase">Жүйеге кіру режимі</p>
                                <p id="dropdownCurrentInfo" class="text-xs font-bold text-slate-800 mt-0.5">Гугл аккаунтпен админ</p>
                            </div>
                            <button onclick="openGoogleAdminLogin()" class="w-full text-left px-4 py-2 text-xs hover:bg-brand-50 flex items-center text-slate-700 font-medium">
                                <i class="fa-brands fa-google text-red-500 mr-2.5 text-sm"></i>
                                Админ болып кіру (Google)
                            </button>
                            <button onclick="openTeacherLoginModal()" class="w-full text-left px-4 py-2 text-xs hover:bg-brand-50 flex items-center text-slate-700 font-medium">
                                <i class="fa-solid fa-key text-amber-500 mr-2.5 text-sm"></i>
                                Сынып жетекші (1 реттік кодпен)
                            </button>
                            <hr class="my-1 border-slate-100">
                            <button onclick="openOrgSettingsModal()" class="w-full text-left px-4 py-2 text-xs hover:bg-slate-100 flex items-center text-slate-600">
                                <i class="fa-solid fa-pen-to-square mr-2.5 text-slate-400"></i>
                                Мекеме атауын өзгерту
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content Container -->
    <div class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col md:flex-row gap-6">
        
        <!-- Sidebar Navigation -->
        <aside class="w-full md:w-64 flex-shrink-0">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-3 sticky top-20">
                <p class="px-3 py-2 text-[11px] font-bold tracking-wider text-slate-400 uppercase">Негізгі Мәзір</p>
                <nav class="space-y-1" id="sidebarNav">
                    <button onclick="switchTab('dashboard')" id="nav-dashboard" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-brand-700 bg-brand-50 transition">
                        <i class="fa-solid fa-chart-pie w-5 mr-3 text-brand-600"></i>
                        <span>Басқару панелі</span>
                    </button>
                    <button onclick="switchTab('orders')" id="nav-orders" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-file-signature w-5 mr-3 text-slate-500"></i>
                        <span>Тәрбие бұйрықтары</span>
                    </button>
                    <button onclick="switchTab('classFolder')" id="nav-classFolder" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-folder-open w-5 mr-3 text-slate-500"></i>
                        <span>Сынып папкасы</span>
                    </button>
                    <button onclick="switchTab('parents')" id="nav-parents" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-users-between-lines w-5 mr-3 text-slate-500"></i>
                        <span>Ата-аналармен жұмыс</span>
                    </button>
                    <button onclick="switchTab('certificates')" id="nav-certificates" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-file-contract w-5 mr-3 text-slate-500"></i>
                        <span>Анықтама & Хаттама</span>
                    </button>
                    <button onclick="switchTab('students')" id="nav-students" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-id-card w-5 mr-3 text-slate-500"></i>
                        <span>Оқушы құжаттары</span>
                    </button>
                    <button onclick="switchTab('events')" id="nav-events" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-calendar-check w-5 mr-3 text-slate-500"></i>
                        <span>Іс-шаралар тізімі</span>
                    </button>
                    <button onclick="switchTab('teachers')" id="nav-teachers" class="nav-btn w-full flex items-center px-3.5 py-2.5 text-sm font-medium rounded-xl text-slate-600 hover:bg-slate-50 hover:text-slate-900 transition">
                        <i class="fa-solid fa-user-tie w-5 mr-3 text-slate-500"></i>
                        <span>Сынып жетекшілері</span>
                    </button>
                </nav>

                <div class="mt-6 pt-4 border-t border-slate-100 px-3">
                    <div class="bg-amber-50 rounded-xl p-3 border border-amber-200/60">
                        <p class="text-xs font-semibold text-amber-800 flex items-center">
                            <i class="fa-solid fa-shield-halved mr-1.5 text-amber-600"></i>
                            Қолжетімділік деңгейі
                        </p>
                        <p id="accessStatusNotice" class="text-[11px] text-amber-700 mt-1 leading-snug">
                            Администраторлық толық құқық берілген.
                        </p>
                    </div>
                </div>
            </div>
        </aside>

        <!-- Main Content View Areas -->
        <main class="flex-1 space-y-6">

            <!-- 0. DASHBOARD TAB -->
            <section id="tab-dashboard" class="tab-content space-y-6">
                <!-- Welcome Banner -->
                <div class="bg-gradient-to-r from-brand-600 to-indigo-700 rounded-2xl p-6 text-white shadow-md relative overflow-hidden">
                    <div class="relative z-10">
                        <h2 class="text-xl sm:text-2xl font-bold">Қош келдіңіз, Тәрбие саласының цифрлық кабинетіне!</h2>
                        <p class="text-brand-100 text-sm mt-1 max-w-2xl">
                            Мұнда бұйрықтар, 1-11 сынып папкалары, ата-аналар хаттамалары, оқушылар контингенті және ҚМЖ/КТП құжаттары бірыңғай жүйеленген.
                        </p>
                        <div class="mt-4 flex flex-wrap gap-2">
                            <button onclick="openAddDocModal()" class="bg-white text-brand-700 hover:bg-brand-50 px-4 py-2 rounded-xl text-xs font-semibold shadow-sm transition flex items-center">
                                <i class="fa-solid fa-circle-plus mr-2 text-brand-600"></i>
                                Жаңа құжат енгізу
                            </button>
                            <button onclick="switchTab('students')" class="bg-brand-500/40 hover:bg-brand-500/60 border border-brand-300/30 text-white px-4 py-2 rounded-xl text-xs font-semibold transition flex items-center">
                                <i class="fa-solid fa-users mr-2"></i>
                                Оқушылар тізімі
                            </button>
                        </div>
                    </div>
                    <i class="fa-solid fa-graduation-cap absolute -right-6 -bottom-6 text-9xl text-white/10 pointer-events-none"></i>
                </div>

                <!-- Summary Cards Grid -->
                <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="bg-white p-4 rounded-2xl border border-slate-200/80 shadow-sm flex items-center space-x-3">
                        <div class="w-12 h-12 rounded-xl bg-blue-50 text-blue-600 flex items-center justify-center text-xl font-bold">
                            <i class="fa-solid fa-folder"></i>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-slate-500">Сынып жиынтығы</p>
                            <p id="statClasses" class="text-xl font-bold text-slate-800">44 сынып (1-11)</p>
                        </div>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-slate-200/80 shadow-sm flex items-center space-x-3">
                        <div class="w-12 h-12 rounded-xl bg-emerald-50 text-emerald-600 flex items-center justify-center text-xl font-bold">
                            <i class="fa-solid fa-user-graduate"></i>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-slate-500">Барлық Оқушылар</p>
                            <p id="statStudents" class="text-xl font-bold text-slate-800">1,120</p>
                        </div>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-slate-200/80 shadow-sm flex items-center space-x-3">
                        <div class="w-12 h-12 rounded-xl bg-purple-50 text-purple-600 flex items-center justify-center text-xl font-bold">
                            <i class="fa-solid fa-hand-holding-heart"></i>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-slate-500">Ерекше оқушылар (ЕБҚ)</p>
                            <p id="statInclusive" class="text-xl font-bold text-slate-800">18</p>
                        </div>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-slate-200/80 shadow-sm flex items-center space-x-3">
                        <div class="w-12 h-12 rounded-xl bg-amber-50 text-amber-600 flex items-center justify-center text-xl font-bold">
                            <i class="fa-solid fa-file-lines"></i>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-slate-500">Тәрбие бұйрықтары</p>
                            <p id="statOrders" class="text-xl font-bold text-slate-800">28</p>
                        </div>
                    </div>
                </div>

                <!-- Recent Activities & Quick Access Grid -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    <div class="lg:col-span-2 bg-white rounded-2xl border border-slate-200/80 p-5 shadow-sm">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-base font-bold text-slate-800 flex items-center">
                                <i class="fa-solid fa-clock-rotate-left text-brand-600 mr-2"></i>
                                Соңғы енгізілген құжаттар
                            </h3>
                            <button onclick="switchTab('orders')" class="text-xs text-brand-600 hover:text-brand-800 font-medium">Барлығын көру &rarr;</button>
                        </div>
                        <div id="recentDocsList" class="space-y-3">
                            <!-- Dynamic recent list -->
                        </div>
                    </div>

                    <!-- Class Category Overview -->
                    <div class="bg-white rounded-2xl border border-slate-200/80 p-5 shadow-sm flex flex-col justify-between">
                        <div>
                            <h3 class="text-base font-bold text-slate-800 mb-3 flex items-center">
                                <i class="fa-solid fa-layer-group text-indigo-600 mr-2"></i>
                                Сынып кешендері (1-11)
                            </h3>
                            <div class="grid grid-cols-3 gap-2 text-center text-xs">
                                <div class="bg-slate-50 p-2.5 rounded-xl border border-slate-100">
                                    <span class="block font-bold text-slate-800 text-sm">1 - 4</span>
                                    <span class="text-[10px] text-slate-500">Бастауыш</span>
                                </div>
                                <div class="bg-slate-50 p-2.5 rounded-xl border border-slate-100">
                                    <span class="block font-bold text-slate-800 text-sm">5 - 9</span>
                                    <span class="text-[10px] text-slate-500">Негізгі</span>
                                </div>
                                <div class="bg-slate-50 p-2.5 rounded-xl border border-slate-100">
                                    <span class="block font-bold text-slate-800 text-sm">10 - 11</span>
                                    <span class="text-[10px] text-slate-500">Жоғары</span>
                                </div>
                            </div>
                        </div>
                        <div class="mt-4 pt-4 border-t border-slate-100 bg-brand-50/50 -mx-5 -mb-5 p-4 rounded-b-2xl">
                            <p class="text-xs font-semibold text-brand-900">Жүйелік файл форматтары:</p>
                            <div class="flex items-center gap-2 mt-2 text-xs text-slate-600 flex-wrap">
                                <span class="bg-red-100 text-red-700 px-2 py-0.5 rounded font-mono font-bold">PDF</span>
                                <span class="bg-blue-100 text-blue-700 px-2 py-0.5 rounded font-mono font-bold">DOCX</span>
                                <span class="bg-emerald-100 text-emerald-700 px-2 py-0.5 rounded font-mono font-bold">XLSX</span>
                                <span class="bg-amber-100 text-amber-700 px-2 py-0.5 rounded font-mono font-bold">PNG/JPG</span>
                                <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded font-mono font-bold">MP4</span>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- 1. ТӘРБИЕ БҰЙРЫҚТАРЫ -->
            <section id="tab-orders" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Тәрбие саласының бұйрықтары</h2>
                        <p class="text-xs text-slate-500">Мектеп директорының тәрбие жұмыстары, іс-шаралар және қауіпсіздік бұйрықтары</p>
                    </div>
                    <div class="flex items-center gap-2">
                        <button onclick="openAddDocModal('orders')" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-sm transition flex items-center">
                            <i class="fa-solid fa-plus mr-2"></i>
                            Бұйрық енгізу
                        </button>
                    </div>
                </div>

                <!-- Filter & Search Bar -->
                <div class="bg-white p-4 rounded-xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row gap-3">
                    <div class="relative flex-1">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-slate-400 text-sm"></i>
                        <input type="text" id="searchOrders" onkeyup="renderOrders()" placeholder="Бұйрық атауы немесе нөмірі бойынша іздеу..." class="w-full pl-9 pr-4 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:bg-white focus:outline-none focus:ring-2 focus:ring-brand-500">
                    </div>
                    <select id="filterOrderCategory" onchange="renderOrders()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                        <option value="">Барлық санаттар</option>
                        <option value="Жылдық жоспар">Жылдық жоспар</option>
                        <option value="Қауіпсіздік & Тәртіп">Қауіпсіздік & Тәртіп</option>
                        <option value="Іс-шара бұйрығы">Іс-шара бұйрығы</option>
                    </select>
                </div>

                <!-- Orders List -->
                <div class="bg-white rounded-2xl border border-slate-200/80 shadow-sm overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="bg-slate-50 text-slate-500 text-[11px] font-bold uppercase tracking-wider border-b border-slate-200">
                                    <th class="p-3.5">№ / Бұйрық Атауы</th>
                                    <th class="p-3.5">Санаты</th>
                                    <th class="p-3.5">Мезгілі</th>
                                    <th class="p-3.5">Тіркелген Файл</th>
                                    <th class="p-3.5 text-right">Әрекеттер</th>
                                </tr>
                            </thead>
                            <tbody id="ordersTableBody" class="divide-y divide-slate-100 text-xs">
                                <!-- JS rendered -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 2. СЫНЫП ПАПКАСЫ -->
            <section id="tab-classFolder" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Сынып папкасы (1 - 11 Сыныптар)</h2>
                        <p class="text-xs text-slate-500">Сынып жетекшілерінің оқу жылына арналған тәрбие папкалары, жоспарлары</p>
                    </div>
                    <button onclick="openAddDocModal('classFolder')" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold transition flex items-center">
                        <i class="fa-solid fa-folder-plus mr-2"></i>
                        Папкаға құжат жүктеу
                    </button>
                </div>

                <!-- Grade Filter buttons -->
                <div class="flex items-center space-x-1.5 overflow-x-auto pb-2 custom-scrollbar text-xs">
                    <button onclick="filterClassGrade('ALL')" class="grade-filter-btn px-3 py-1.5 rounded-lg font-medium bg-brand-600 text-white flex-shrink-0">Барлық сыныптар</button>
                    <!-- 1 through 11 -->
                    <template id="gradeBtnTemplate">
                        <!-- JS generated -->
                    </template>
                    <div id="gradeButtonsContainer" class="flex items-center space-x-1.5"></div>
                </div>

                <!-- Class Folders Grid -->
                <div id="classFoldersGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <!-- JS rendered cards -->
                </div>
            </section>

            <!-- 3. АТА-АНАЛАРМЕН ЖҰМЫС -->
            <section id="tab-parents" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Ата-аналармен жұмыс</h2>
                        <p class="text-xs text-slate-500">Ата-аналар жиналыстарының хаттамалары, комитет құрамы, педагогикалық тренингтер</p>
                    </div>
                    <button onclick="openAddDocModal('parents')" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold transition flex items-center">
                        <i class="fa-solid fa-plus mr-2"></i>
                        Жиналыс/Хаттама қосу
                    </button>
                </div>

                <div class="bg-white p-4 rounded-xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row gap-3">
                    <input type="text" id="searchParents" onkeyup="renderParents()" placeholder="Сынып, тақырып немесе хаттама бойынша іздеу..." class="w-full px-4 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                </div>

                <div id="parentsCardsContainer" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <!-- JS rendered -->
                </div>
            </section>

            <!-- 4. АНЫҚТАМАЛАР МЕН ХАТТАМАЛАР -->
            <section id="tab-certificates" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Анықтамалар мен Хаттамалар</h2>
                        <p class="text-xs text-slate-[500]">Педагогикалық кеңес, тәрбиелік тексеру анықтамалары, ресми хаттамалар</p>
                    </div>
                    <button onclick="openAddDocModal('certificates')" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold transition flex items-center">
                        <i class="fa-solid fa-file-circle-plus mr-2"></i>
                        Анықтама/Хаттама енгізу
                    </button>
                </div>

                <div id="certificatesTableContainer" class="bg-white rounded-2xl border border-slate-200/80 shadow-sm overflow-hidden">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-50 text-slate-500 text-[11px] font-bold uppercase tracking-wider border-b border-slate-200">
                                <th class="p-3.5">Құжат атауы & Рет саны</th>
                                <th class="p-3.5">Түрі</th>
                                <th class="p-3.5">Күні</th>
                                <th class="p-3.5">Файл & Медиа</th>
                                <th class="p-3.5 text-right">Әрекеттер</th>
                            </tr>
                        </thead>
                        <tbody id="certificatesTableBody" class="divide-y divide-slate-100 text-xs">
                            <!-- JS rendered -->
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- 5. ОҚУШЫ ҚҰЖАТТАРЫ (Mandatory exact columns required) -->
            <section id="tab-students" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Оқушы құжаттары</h2>
                        <p class="text-xs text-slate-500">Оқушылар контингенті, әлеуметтік жағдайы, ерекше білім алу қажеттілігі бар (ЕБҚ) балалар</p>
                    </div>
                    <div class="flex items-center gap-2">
                        <button onclick="openAddStudentModal()" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-sm transition flex items-center">
                            <i class="fa-solid fa-user-plus mr-2"></i>
                            Оқушы қосу
                        </button>
                    </div>
                </div>

                <!-- Filter Controls -->
                <div class="bg-white p-4 rounded-xl border border-slate-200/80 shadow-sm flex flex-col md:flex-row gap-3">
                    <div class="relative flex-1">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-slate-400 text-sm"></i>
                        <input type="text" id="searchStudents" onkeyup="renderStudents()" placeholder="Аты-жөні немесе ИИН бойынша іздеу..." class="w-full pl-9 pr-4 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                    </div>
                    <select id="filterStudentGrade" onchange="renderStudents()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                        <option value="">Барлық сыныптар (1-11)</option>
                        <!-- 1-11 Options generated -->
                    </select>
                    <select id="filterSocialStatus" onchange="renderStudents()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                        <option value="">Барлық әлеуметтік мәртебе</option>
                        <option value="Жалпы">Жалпы</option>
                        <option value="Ерекше білім беру қажеттілігі (ЕБҚ)">Ерекше білім беру (ЕБҚ)</option>
                        <option value="Көпбалалы отбасы">Көпбалалы отбасы</option>
                        <option value="Аз қамтылған">Аз қамтылған</option>
                    </select>
                </div>

                <!-- Main Exact Table -->
                <div class="bg-white rounded-2xl border border-slate-200/80 shadow-sm overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="bg-slate-800 text-white text-[11px] font-bold uppercase tracking-wider">
                                    <th class="p-3.5">СЫНЫБЫ</th>
                                    <th class="p-3.5">АТЫ-ЖӨНІ</th>
                                    <th class="p-3.5">ТУЫЛҒАН КҮНІ</th>
                                    <th class="p-3.5">ИИН</th>
                                    <th class="p-3.5">ӘЛЕУМЕТТІК ЖАҒДАЙЫ</th>
                                    <th class="p-3.5">ҚҰЖАТТАР ЖҮКТЕУ & КӨРУ</th>
                                    <th class="p-3.5 text-right">ӘРЕКЕТ</th>
                                </tr>
                            </thead>
                            <tbody id="studentsTableBody" class="divide-y divide-slate-100 text-xs">
                                <!-- Exact requirement rendered dynamically -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 6. ІС-ШАРАЛАР МЕН ТІЗІМ (Video, Photo, KMJ, KTP) -->
            <section id="tab-events" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Тәрбиелік іс-шаралар тізімі</h2>
                        <p class="text-xs text-slate-500">Өткізілген шаралар, фото/видео есептер, ҚМЖ (қысқа мерзімді жоспар), КТП (күнтізбелік жоспар)</p>
                    </div>
                    <button onclick="openAddEventModal()" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-sm transition flex items-center">
                        <i class="fa-solid fa-calendar-plus mr-2"></i>
                        Іс-шара қосу (ҚМЖ/КТП/Видео)
                    </button>
                </div>

                <div class="bg-white p-4 rounded-xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row gap-3">
                    <input type="text" id="searchEvents" onkeyup="renderEvents()" placeholder="Іс-шара атауы, жауапты тұлға бойынша іздеу..." class="w-full px-4 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                </div>

                <!-- Events List Container -->
                <div id="eventsContainer" class="space-y-4">
                    <!-- Dynamic rendering -->
                </div>
            </section>

            <!-- 7. СЫНЫП ЖЕТЕКШІЛЕРА (Admin Control, 1-Time Password Generation, Access Toggle) -->
            <section id="tab-teachers" class="tab-content hidden space-y-4">
                <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Сынып жетекшілері бөлімі</h2>
                        <p class="text-xs text-slate-500">Сынып жетекшілер тізімі, 1-11 сыныптарды бекіту, 1 реттік кіру кодтарын беру (Администратор)</p>
                    </div>
                    <button onclick="openAddTeacherModal()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-sm transition flex items-center">
                        <i class="fa-solid fa-user-plus mr-2"></i>
                        Жаңа сынып жетекшісін қосу
                    </button>
                </div>

                <div class="bg-white rounded-2xl border border-slate-200/80 shadow-sm overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="bg-slate-50 text-slate-500 text-[11px] font-bold uppercase tracking-wider border-b border-slate-200">
                                    <th class="p-3.5">Сынып жетекші Аты-жөні</th>
                                    <th class="p-3.5">Бекітілген Сыныбы</th>
                                    <th class="p-3.5">Жүйелік Логин</th>
                                    <th class="p-3.5">1-Реттік Кіру Коды</th>
                                    <th class="p-3.5">Админ Рұқсаты</th>
                                    <th class="p-3.5 text-right">Басқару</th>
                                </tr>
                            </thead>
                            <tbody id="teachersTableBody" class="divide-y divide-slate-100 text-xs">
                                <!-- JS rendered -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

        </main>
    </div>

    <!-- MODAL 1: ADD DOCUMENT / FILE UPLOAD MODAL -->
    <div id="addDocModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-lg rounded-2xl shadow-2xl border border-slate-100 overflow-hidden flex flex-col max-h-[90vh]">
            <div class="px-6 py-4 bg-slate-800 text-white flex items-center justify-between">
                <h3 id="addDocModalTitle" class="font-bold text-sm flex items-center">
                    <i class="fa-solid fa-cloud-arrow-up mr-2 text-brand-400"></i>
                    Жаңа құжат енгізу / Жүктеу
                </h3>
                <button onclick="closeModal('addDocModal')" class="text-slate-400 hover:text-white text-lg">&times;</button>
            </div>
            <form id="docForm" onsubmit="handleDocSubmit(event)" class="p-6 space-y-4 overflow-y-auto custom-scrollbar flex-1 text-xs">
                <input type="hidden" id="docTargetSection" value="orders">
                
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Құжаттың атауы / Тақырыбы *</label>
                    <input type="text" id="docTitle" required placeholder="Мәселен: №45 Мектеп ішілік тәртіп бұйрығы" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 outline-none">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Сынып (1-11 немесе Жалпы)</label>
                        <select id="docGrade" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                            <option value="Жалпы">Жалпы мектептік</option>
                            <option value="1-Сынып">1-Сынып</option>
                            <option value="2-Сынып">2-Сынып</option>
                            <option value="3-Сынып">3-Сынып</option>
                            <option value="4-Сынып">4-Сынып</option>
                            <option value="5-Сынып">5-Сынып</option>
                            <option value="6-Сынып">6-Сынып</option>
                            <option value="7-Сынып">7-Сынып</option>
                            <option value="8-Сынып">8-Сынып</option>
                            <option value="9-Сынып">9-Сынып</option>
                            <option value="10-Сынып">10-Сынып</option>
                            <option value="11-Сынып">11-Сынып</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Санаты / Түрі</label>
                        <input type="text" id="docCategory" placeholder="Бұйрық / Хаттама / Анықтама" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                    </div>
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Қосымша сипаттама / Түсініктеме</label>
                    <textarea id="docDescription" rows="2" placeholder="Құжаттың қысқаша мазмұны..." class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none"></textarea>
                </div>

                <!-- File Attachments Area (PDF, Word, Excel, Photo, Video) -->
                <div class="border-2 border-dashed border-slate-200 rounded-xl p-4 text-center bg-slate-50 hover:bg-brand-50/30 transition">
                    <i class="fa-solid fa-file-arrow-up text-3xl text-brand-500 mb-2"></i>
                    <p class="font-semibold text-slate-700 text-xs">Файлды таңдаңыз немесе осы жерге сүйреңіз</p>
                    <p class="text-[10px] text-slate-400 mt-0.5">Форматтар: PDF, WORD (.docx), EXCEL (.xlsx), PNG/JPG, MP4 Видео</p>
                    <input type="file" id="docFileInput" onchange="handleFileSelected(this)" class="mt-3 text-xs text-slate-500 block w-full file:mr-3 file:py-1.5 file:px-3 file:rounded-lg file:border-0 file:text-xs file:font-semibold file:bg-brand-600 file:text-white hover:file:bg-brand-700 cursor-pointer">
                    <div id="fileSelectedInfo" class="mt-2 text-xs text-emerald-600 font-medium hidden"></div>
                </div>

                <div class="flex items-center justify-end space-x-2 pt-2">
                    <button type="button" onclick="closeModal('addDocModal')" class="px-4 py-2 border border-slate-200 text-slate-600 rounded-xl hover:bg-slate-50 font-medium">Бас тарту</button>
                    <button type="submit" class="px-5 py-2 bg-brand-600 hover:bg-brand-700 text-white rounded-xl font-semibold shadow-sm">Сақтау & Жүктеу</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 2: ADD STUDENT MODAL -->
    <div id="addStudentModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-lg rounded-2xl shadow-2xl border border-slate-100 overflow-hidden">
            <div class="px-6 py-4 bg-slate-800 text-white flex items-center justify-between">
                <h3 class="font-bold text-sm flex items-center">
                    <i class="fa-solid fa-user-graduate mr-2 text-emerald-400"></i>
                    Жаңа оқушы құжатын енгізу
                </h3>
                <button onclick="closeModal('addStudentModal')" class="text-slate-400 hover:text-white text-lg">&times;</button>
            </div>
            <form onsubmit="handleStudentSubmit(event)" class="p-6 space-y-3 text-xs">
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">СЫНЫБЫ *</label>
                        <select id="stGrade" required class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                            <option value="1-А">1-А сыныбы</option>
                            <option value="3-Ә">3-Ә сыныбы</option>
                            <option value="5-Б">5-Б сыныбы</option>
                            <option value="7-А">7-А сыныбы</option>
                            <option value="9-В">9-В сыныбы</option>
                            <option value="11-А">11-А сыныбы</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">ТУЫЛҒАН КҮНІ *</label>
                        <input type="date" id="stBirth" required class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                    </div>
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">АТЫ-ЖӨНІ (Толық) *</label>
                    <input type="text" id="stName" required placeholder="Мысалы: Арманұлы Бақытжан" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">ИИН (12 сан) *</label>
                        <input type="text" id="stIin" required maxlength="12" placeholder="100512501234" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none font-mono">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">ӘЛЕУМЕТТІК ЖАҒДАЙЫ *</label>
                        <select id="stSocial" required class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                            <option value="Жалпы">Жалпы</option>
                            <option value="Ерекше білім беру қажеттілігі (ЕБҚ)">Ерекше білім беру (ЕБҚ)</option>
                            <option value="Көпбалалы отбасы">Көпбалалы отбасы</option>
                            <option value="Аз қамтылған отбасы">Аз қамтылған отбасы</option>
                            <option value="Толық емес отбасы">Толық емес отбасы</option>
                        </select>
                    </div>
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Оқушының жеке файлын жүктеу (Туу куәлігі / ИПР / Анықтама)</label>
                    <input type="file" id="stFileInput" class="w-full text-slate-500 border border-slate-200 rounded-xl p-2 file:mr-3 file:py-1 file:px-2 file:rounded-lg file:border-0 file:bg-slate-800 file:text-white">
                </div>

                <div class="flex items-center justify-end space-x-2 pt-3">
                    <button type="button" onclick="closeModal('addStudentModal')" class="px-4 py-2 border border-slate-200 text-slate-600 rounded-xl font-medium">Бас тарту</button>
                    <button type="submit" class="px-5 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-xl font-semibold">Оқушыны енгізу</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 3: ADD EVENT (KMJ/KTP/MEDIA) -->
    <div id="addEventModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-lg rounded-2xl shadow-2xl border border-slate-100 overflow-hidden">
            <div class="px-6 py-4 bg-slate-800 text-white flex items-center justify-between">
                <h3 class="font-bold text-sm flex items-center">
                    <i class="fa-solid fa-calendar-check mr-2 text-indigo-400"></i>
                    Іс-шара қосу (Фото, Видео, ҚМЖ, КТП)
                </h3>
                <button onclick="closeModal('addEventModal')" class="text-slate-400 hover:text-white text-lg">&times;</button>
            </div>
            <form onsubmit="handleEventSubmit(event)" class="p-6 space-y-3 text-xs">
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Іс-шара атауы *</label>
                    <input type="text" id="evTitle" required placeholder="Мысалы: Тәуелсіздік - Тұғырым тәрбие сағаты" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Өткізілетін күні *</label>
                        <input type="date" id="evDate" required class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Жауапты сынып / Жетекші</label>
                        <input type="text" id="evResponsible" placeholder="8-А сыныбы (Ахметова А.)" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                    </div>
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">ҚМЖ немесе КТП Файлын жүктеу (DOCX / PDF)</label>
                    <input type="file" id="evKmjInput" class="w-full text-slate-500 border border-slate-200 rounded-xl p-2 file:bg-indigo-600 file:text-white file:rounded-lg file:border-0 file:px-2 file:py-1">
                </div>

                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Фото немесе Видео файл жүктеу (PNG / JPG / MP4)</label>
                    <input type="file" id="evMediaInput" accept="image/*,video/*" class="w-full text-slate-500 border border-slate-200 rounded-xl p-2 file:bg-slate-700 file:text-white file:rounded-lg file:border-0 file:px-2 file:py-1">
                </div>

                <div class="flex items-center justify-end space-x-2 pt-2">
                    <button type="button" onclick="closeModal('addEventModal')" class="px-4 py-2 border border-slate-200 text-slate-600 rounded-xl">Бас тарту</button>
                    <button type="submit" class="px-5 py-2 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl font-semibold">Іс-шараны тіркеу</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 4: ADD CLASS TEACHER & GENERATE 1-TIME PASSWORD CODE -->
    <div id="addTeacherModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-md rounded-2xl shadow-2xl border border-slate-100 overflow-hidden">
            <div class="px-6 py-4 bg-slate-800 text-white flex items-center justify-between">
                <h3 class="font-bold text-sm flex items-center">
                    <i class="fa-solid fa-user-plus mr-2 text-emerald-400"></i>
                    Сынып жетекшісін тіркеу
                </h3>
                <button onclick="closeModal('addTeacherModal')" class="text-slate-400 hover:text-white text-lg">&times;</button>
            </div>
            <form onsubmit="handleTeacherSubmit(event)" class="p-6 space-y-3 text-xs">
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Сынып жетекшінің Аты-жөні *</label>
                    <input type="text" id="tName" required placeholder="Мысалы: Нұрбекова Қарлығаш" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Бекітілетін Сыныбы *</label>
                        <select id="tGrade" required class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
                            <option value="1-А">1-А</option>
                            <option value="2-Ә">2-Ә</option>
                            <option value="4-Б">4-Б</option>
                            <option value="6-А">6-А</option>
                            <option value="7-Ә">7-Ә</option>
                            <option value="8-В">8-В</option>
                            <option value="10-А">10-А</option>
                            <option value="11-Б">11-Б</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-700 mb-1">Логин (ID)</label>
                        <input type="text" id="tLogin" required placeholder="m_nurbekova" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none font-mono">
                    </div>
                </div>

                <div class="bg-amber-50 p-3 rounded-xl border border-amber-200">
                    <p class="font-semibold text-amber-800 text-[11px] flex items-center justify-between">
                        <span>1-Реттік Жүйелік Кіру Коды:</span>
                        <button type="button" onclick="generateTeacherCode()" class="text-brand-600 underline text-[10px]">Қайта генерациялау</button>
                    </p>
                    <input type="text" id="tCode" readonly class="w-full mt-1.5 px-3 py-1.5 bg-white border border-amber-300 font-mono font-bold text-amber-900 rounded-lg text-center tracking-widest text-sm">
                    <p class="text-[10px] text-amber-700 mt-1">Осы код арқылы мұғалім жүйеге бір рет кіріп, өзіне рұқсат алады.</p>
                </div>

                <div class="flex items-center justify-end space-x-2 pt-2">
                    <button type="button" onclick="closeModal('addTeacherModal')" class="px-4 py-2 border border-slate-200 text-slate-600 rounded-xl">Бас тарту</button>
                    <button type="submit" class="px-5 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-xl font-semibold">Жетекшіні қосу</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 5: FILE PREVIEW & DOWNLOAD MODAL -->
    <div id="filePreviewModal" class="fixed inset-0 bg-slate-900/70 backdrop-blur-md z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-2xl rounded-2xl shadow-2xl border border-slate-100 overflow-hidden flex flex-col max-h-[85vh]">
            <div class="px-6 py-4 bg-slate-900 text-white flex items-center justify-between">
                <div class="flex items-center space-x-2 overflow-hidden">
                    <i id="previewTypeIcon" class="fa-solid fa-file text-brand-400 text-lg"></i>
                    <h3 id="previewModalTitle" class="font-bold text-xs sm:text-sm truncate">Файлды алдын ала көру</h3>
                </div>
                <button onclick="closeModal('filePreviewModal')" class="text-slate-400 hover:text-white text-xl">&times;</button>
            </div>
            
            <div class="p-6 overflow-y-auto flex-1 flex flex-col items-center justify-center bg-slate-50 min-h-[250px]" id="previewModalBody">
                <!-- Dynamic File Render / Image / Video / Text -->
            </div>

            <div class="px-6 py-3 bg-white border-t border-slate-200 flex items-center justify-between">
                <span id="previewMeta" class="text-xs text-slate-500 font-mono">Формат: PDF</span>
                <a id="previewDownloadBtn" href="#" download class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold flex items-center shadow-sm">
                    <i class="fa-solid fa-download mr-2"></i>
                    Файлды Жүктеу
                </a>
            </div>
        </div>
    </div>

    <!-- MODAL 6: GOOGLE LOGIN FOR ADMIN SIMULATION -->
    <div id="googleAdminModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-sm rounded-2xl shadow-2xl p-6 text-center space-y-4">
            <div class="w-14 h-14 bg-red-50 text-red-500 rounded-full flex items-center justify-center mx-auto text-2xl border border-red-100">
                <i class="fa-brands fa-google"></i>
            </div>
            <div>
                <h3 class="font-bold text-slate-800 text-base">Google арқылы кіру</h3>
                <p class="text-xs text-slate-500 mt-1">Тәрбие ісі жөніндегі мектеп Администраторы аккаунты</p>
            </div>

            <div class="bg-slate-50 p-3 rounded-xl border border-slate-200 text-left text-xs space-y-1">
                <p class="font-semibold text-slate-700">Тіркелген Гугл аккаунт:</p>
                <p class="text-brand-700 font-mono">admin.tarbiye@mektep.edu.kz</p>
            </div>

            <button onclick="confirmAdminGoogleAuth()" class="w-full py-2.5 bg-red-600 hover:bg-red-700 text-white rounded-xl text-xs font-bold transition flex items-center justify-center shadow-sm">
                <i class="fa-brands fa-google mr-2"></i>
                Google аккаунтын растау
            </button>
            <button onclick="closeModal('googleAdminModal')" class="text-xs text-slate-400 hover:text-slate-600">Бас тарту</button>
        </div>
    </div>

    <!-- MODAL 7: TEACHER 1-TIME CODE LOGIN MODAL -->
    <div id="teacherLoginModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-sm rounded-2xl shadow-2xl p-6 space-y-4">
            <div class="text-center">
                <div class="w-12 h-12 bg-amber-50 text-amber-600 rounded-full flex items-center justify-center mx-auto text-xl mb-2">
                    <i class="fa-solid fa-key"></i>
                </div>
                <h3 class="font-bold text-slate-800 text-base">Сынып жетекші порталы</h3>
                <p class="text-xs text-slate-500 mt-0.5">Администратор берген 1 реттік кодты енгізіңіз</p>
            </div>

            <form onsubmit="handleTeacherCodeLogin(event)" class="space-y-3 text-xs">
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">Сынып жетекші логині</label>
                    <input type="text" id="loginInputUser" required placeholder="Мысалы: m_nurbekova" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none font-mono">
                </div>
                <div>
                    <label class="block font-semibold text-slate-700 mb-1">1-Реттік Кіру Коды</label>
                    <input type="text" id="loginInputCode" required placeholder="X7B9K2" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none font-mono tracking-widest text-center uppercase font-bold text-amber-700">
                </div>
                <button type="submit" class="w-full py-2.5 bg-brand-600 hover:bg-brand-700 text-white rounded-xl font-bold shadow-sm">
                    Жүйеге кіру
                </button>
            </form>
            <div class="text-center">
                <button onclick="closeModal('teacherLoginModal')" class="text-xs text-slate-400 hover:text-slate-600">Жабу</button>
            </div>
        </div>
    </div>

    <!-- MODAL 8: ORG NAME SETTINGS -->
    <div id="orgModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-sm rounded-2xl shadow-2xl p-5 space-y-3 text-xs">
            <h3 class="font-bold text-slate-800 text-sm">Мекеме атауын жаңарту</h3>
            <div>
                <label class="block text-slate-600 mb-1">Мектеп / Білім беру ұйымының атауы:</label>
                <input type="text" id="orgNameInput" class="w-full px-3 py-2 border border-slate-200 rounded-xl outline-none">
            </div>
            <div class="flex justify-end space-x-2 pt-2">
                <button onclick="closeModal('orgModal')" class="px-3 py-1.5 border border-slate-200 rounded-lg">Бас тарту</button>
                <button onclick="saveOrgName()" class="px-4 py-1.5 bg-brand-600 text-white rounded-lg font-semibold">Сақтау</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification Popup -->
    <div id="toastNotification" class="fixed bottom-5 right-5 z-50 transform translate-y-20 opacity-0 transition-all duration-300 bg-slate-900 text-white px-4 py-3 rounded-xl shadow-2xl flex items-center space-x-3 text-xs pointer-events-none">
        <i id="toastIcon" class="fa-solid fa-circle-check text-emerald-400 text-base"></i>
        <span id="toastMessage">Әрекет сәтті орындалды!</span>
    </div>

    <!-- Application Logic Script -->
    <script>
        // Global State & Storage Key
        const STORAGE_KEY = 'SCHOOL_TARBIYE_SYSTEM_DATA_V1';

        // Default initial application state
        let appState = {
            orgName: "№15 Жалпы білім беретін мектеп-лицейі",
            currentUser: {
                role: "ADMIN", // 'ADMIN' or 'TEACHER'
                name: "Администратор (Гугл)",
                grade: "Барлық сыныптар",
                accessGranted: true
            },
            orders: [
                { id: "ORD-01", title: "Тәрбие жұмысының 2026-2027 оқу жылына арналған жылдық жоспарын бекіту туралы", category: "Жылдық жоспар", date: "2026-08-15", fileName: "Tarbiye_Zhospar_2026.pdf", fileType: "pdf", fileSize: "2.4 MB", url: "#" },
                { id: "ORD-02", title: "Оқушылардың жол қозғалысы қауіпсіздігі мен мектеп ішілік тәртібін қамтамасыз ету", category: "Қауіпсіздік & Тәртіп", date: "2026-08-20", fileName: "Kauipsizdik_Buiryk.docx", fileType: "docx", fileSize: "512 KB", url: "#" },
                { id: "ORD-03", title: "Ата-аналар мектебі мен сынып жетекшілер әдістемелік бірлестігін құру бұйрығы", category: "Іс-шара бұйрығы", date: "2026-08-25", fileName: "Ata_Ana_Mektebi.xlsx", fileType: "xlsx", fileSize: "1.1 MB", url: "#" }
            ],
            classFolders: [
                { id: "CF-1", grade: "1-А", teacher: "Сарсенова А.Қ.", topic: "1-Сынып Тәрбие папкасы & Ата-аналар бұрышы", fileCount: 8, kmjCount: 12, fileName: "1A_Tarbiye_Papka.pdf", fileType: "pdf" },
                { id: "CF-2", grade: "5-Б", teacher: "Нұрланов Б.М.", topic: "5-Сынып Адаптациялық тәрбие жоспары", fileCount: 14, kmjCount: 20, fileName: "5B_Plan_KTP.docx", fileType: "docx" },
                { id: "CF-3", grade: "7-Ә", teacher: "Асан Н.Ә.", topic: "7-Сынып Ерекше оқушылармен жұмыс картотекасы", fileCount: 10, kmjCount: 18, fileName: "7A_Erekse_Oku.xlsx", fileType: "xlsx" },
                { id: "CF-4", grade: "11-А", teacher: "Оспанова Г.Т.", topic: "11-Сынып Кәсіптік бағдар және ҰБТ психологиялық дайындық", fileCount: 16, kmjCount: 24, fileName: "11A_Kasip_Bagdar.pdf", fileType: "pdf" }
            ],
            parentsWork: [
                { id: "P-1", grade: "7-Ә", title: "Жалпы сыныптық Ата-аналар жиналысы №1", date: "2026-08-28", type: "Ата-аналар жиналысы", attendance: "92%", fileName: "Hattama_AtaAna_7A.docx", fileType: "docx" },
                { id: "P-2", grade: "9-В", title: "Жасөспірімдер арасындағы суицидтің алдын алу тренингі", date: "2026-08-22", type: "Педагогикалық Тренинг", attendance: "88%", fileName: "Trening_Esep.png", fileType: "png" }
            ],
            certificates: [
                { id: "CERT-101", title: "Мектеп оқушыларының тамақтану сапасын тексеру анықтамасы", date: "2026-08-21", type: "Анықтама", fileName: "Tamaktanu_Anyktama.pdf", fileType: "pdf" },
                { id: "CERT-102", title: "Тәрбие кеңесінің №3 маңызды хаттамасы", date: "2026-08-18", type: "Хаттама", fileName: "Tarbiye_Kenges_3.docx", fileType: "docx" }
            ],
            // EXACT REQUIREMENT COLUMNS FOR STUDENTS: СЫНЫБЫ, АТЫ-ЖӨНІ, ТУЫЛҒАН КҮНІ, ИИН, ӘЛЕУМЕТТІК ЖАҒДАЙЫ
            students: [
                { id: "ST-1", grade: "7-Ә", fullName: "Аманжолов Әлішер Маратұлы", birthDate: "2013-04-12", iin: "130412501982", socialStatus: "Ерекше білім беру қажеттілігі (ЕБҚ)", fileName: "Tuu_Kualik_Alisher.pdf", fileType: "pdf" },
                { id: "ST-2", grade: "5-Б", fullName: "Бейбітқызы Айару", birthDate: "2015-09-25", iin: "150925602341", socialStatus: "Көпбалалы отбасы", fileName: "Aneket_Aiaru.docx", fileType: "docx" },
                { id: "ST-3", grade: "1-А", fullName: "Серік Азамат Дәулетұлы", birthDate: "2019-01-10", iin: "190110504123", socialStatus: "Жалпы", fileName: "Med_Karta.pdf", fileType: "pdf" },
                { id: "ST-4", grade: "9-В", fullName: "Қайратов Данияр", birthDate: "2011-11-05", iin: "111105509876", socialStatus: "Аз қамтылған отбасы", fileName: "Anyktama_Kairatov.xlsx", fileType: "xlsx" },
                { id: "ST-5", grade: "11-А", fullName: "Жұмабекова Аружан", birthDate: "2009-06-30", iin: "090630601122", socialStatus: "Жалпы", fileName: "Arudzan_Doc.pdf", fileType: "pdf" }
            ],
            events: [
                { id: "EV-1", title: "«Сұңқар» әскери-патриоттық спорттық жарысы", date: "2026-08-24", responsible: "9-11 Сыныптар (АҚТ мұғалімі)", kmjFile: "KMJ_Sunkar.docx", mediaFile: "Sunkar_Video_Report.mp4", mediaType: "video" },
                { id: "EV-2", title: "«Отбасы – бақыт мекені» суреттер көрмесі", date: "2026-08-19", responsible: "1-4 Сыныптар", kmjFile: "KTP_Otbasi.pdf", mediaFile: "Korinis_Photo.png", mediaType: "image" }
            ],
            teachers: [
                { id: "T-1", name: "Асан Нұрлан Әлібекұлы", grade: "7-Ә", login: "n_asan", code: "7A9K2M", accessGranted: true },
                { id: "T-2", name: "Сарсенова Айгүл Қанатқызы", grade: "1-А", login: "a_sarsenova", code: "1A3P8X", accessGranted: true },
                { id: "T-3", name: "Нұрланов Болат Мұратұлы", grade: "5-Б", login: "b_nurlanov", code: "5B4L9Q", accessGranted: true },
                { id: "T-4", name: "Оспанова Гүлнар Төлеуқызы", grade: "11-А", login: "g_ospanova", code: "11A8Z1", accessGranted: false }
            ]
        };

        // Load data from LocalStorage
        function loadStorage() {
            const saved = localStorage.getItem(STORAGE_KEY);
            if (saved) {
                try {
                    appState = JSON.parse(saved);
                } catch(e) {
                    console.error("Local storage error:", e);
                }
            } else {
                saveStorage();
            }
        }

        function saveStorage() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(appState));
        }

        // Window Load Bootstrapper
        window.onload = function() {
            loadStorage();
            initGradeButtons();
            updateHeaderAndUserUI();
            renderDashboard();
            renderOrders();
            renderClassFolders();
            renderParents();
            renderCertificates();
            renderStudents();
            renderEvents();
            renderTeachers();
        };

        function switchTab(tabId) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            
            // Remove active classes on nav buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('bg-brand-50', 'text-brand-700');
                btn.classList.add('text-slate-600');
            });

            // Show selected tab
            const target = document.getElementById(`tab-${tabId}`);
            if (target) target.classList.remove('hidden');

            // Highlight nav button
            const activeNav = document.getElementById(`nav-${tabId}`);
            if (activeNav) {
                activeNav.classList.add('bg-brand-50', 'text-brand-700');
                activeNav.classList.remove('text-slate-600');
            }
        }

        function toggleAuthMenu() {
            const dropdown = document.getElementById('authMenuDropdown');
            dropdown.classList.toggle('hidden');
        }

        function showToast(message, type = 'success') {
            const toast = document.getElementById('toastNotification');
            const msgEl = document.getElementById('toastMessage');
            const iconEl = document.getElementById('toastIcon');

            msgEl.textContent = message;
            if (type === 'error') {
                iconEl.className = "fa-solid fa-triangle-exclamation text-red-400 text-base";
            } else {
                iconEl.className = "fa-solid fa-circle-check text-emerald-400 text-base";
            }

            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        function updateHeaderAndUserUI() {
            document.getElementById('orgNameHeader').textContent = appState.orgName;
            const badge = document.getElementById('currentUserRole');
            const currentInfo = document.getElementById('dropdownCurrentInfo');
            const notice = document.getElementById('accessStatusNotice');

            if (appState.currentUser.role === 'ADMIN') {
                badge.textContent = "Администратор (Гугл)";
                badge.className = "font-medium text-emerald-300";
                currentInfo.textContent = "Гугл арқылы Администратор";
                notice.textContent = "Администраторлық толық басқару құқығы белсенді.";
            } else {
                badge.textContent = `Сынып жетекші: ${appState.currentUser.name} (${appState.currentUser.grade})`;
                badge.className = "font-medium text-amber-300";
                currentInfo.textContent = `Мұғалім: ${appState.currentUser.name}`;
                notice.textContent = appState.currentUser.accessGranted 
                    ? `Администратор берген рұқсат белсенді (${appState.currentUser.grade}).` 
                    : "Назар аударыңыз! Администратор рұқсаты шектелген.";
            }
        }

        function initGradeButtons() {
            const container = document.getElementById('gradeButtonsContainer');
            const studentSelect = document.getElementById('filterStudentGrade');
            if (!container) return;

            container.innerHTML = '';
            for (let i = 1; i <= 11; i++) {
                const btn = document.createElement('button');
                btn.className = 'grade-filter-btn px-3 py-1.5 rounded-lg font-medium bg-slate-100 text-slate-700 hover:bg-slate-200 flex-shrink-0';
                btn.textContent = `${i}-Сыныптар`;
                btn.onclick = () => filterClassGrade(`${i}`);
                container.appendChild(btn);

                // Populate student grade filter select options
                if (studentSelect) {
                    const opt = document.createElement('option');
                    opt.value = `${i}`;
                    opt.textContent = `${i}-Сыныптар`;
                    studentSelect.appendChild(opt);
                }
            }
        }

        function renderDashboard() {
            document.getElementById('statOrders').textContent = appState.orders.length;
            document.getElementById('statStudents').textContent = appState.students.length;
            
            // Inclusive education filter
            const inclusiveCount = appState.students.filter(s => s.socialStatus.includes('ЕБҚ') || s.socialStatus.includes('Ерекше')).length;
            document.getElementById('statInclusive').textContent = inclusiveCount;

            const recentList = document.getElementById('recentDocsList');
            recentList.innerHTML = '';

            // Combine latest items
            const combined = [
                ...appState.orders.map(o => ({ title: o.title, type: o.category, date: o.date, file: o.fileName, fileType: o.fileType })),
                ...appState.certificates.map(c => ({ title: c.title, type: c.type, date: c.date, file: c.fileName, fileType: c.fileType }))
            ].slice(0, 5);

            combined.forEach(item => {
                const div = document.createElement('div');
                div.className = "flex items-center justify-between p-3 rounded-xl bg-slate-50 border border-slate-100 hover:border-brand-200 transition";
                div.innerHTML = `
                    <div class="flex items-center space-x-3 overflow-hidden">
                        ${getFileIconHtml(item.fileType)}
                        <div class="truncate">
                            <p class="font-semibold text-slate-800 truncate">${item.title}</p>
                            <span class="text-[10px] text-slate-400">${item.type} • ${item.date}</span>
                        </div>
                    </div>
                    <button onclick="previewFile('${item.file}', '${item.fileType}')" class="text-xs bg-white border border-slate-200 hover:bg-brand-50 hover:text-brand-700 px-3 py-1.5 rounded-lg font-medium shadow-2xs transition flex-shrink-0">
                        <i class="fa-solid fa-eye mr-1"></i> Көру
                    </button>
                `;
                recentList.appendChild(div);
            });
        }

        function renderOrders() {
            const tbody = document.getElementById('ordersTableBody');
            const search = document.getElementById('searchOrders').value.toLowerCase();
            const catFilter = document.getElementById('filterOrderCategory').value;

            tbody.innerHTML = '';

            const filtered = appState.orders.filter(ord => {
                const matchesSearch = ord.title.toLowerCase().includes(search) || ord.id.toLowerCase().includes(search);
                const matchesCat = catFilter ? ord.category === catFilter : true;
                return matchesSearch && matchesCat;
            });

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="5" class="p-6 text-center text-slate-400">Бұйрықтар табылмады</td></tr>`;
                return;
            }

            filtered.forEach(ord => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50/80 transition";
                tr.innerHTML = `
                    <td class="p-3.5 font-semibold text-slate-800">
                        <span class="font-mono text-slate-400 text-[10px] block">${ord.id}</span>
                        ${ord.title}
                    </td>
                    <td class="p-3.5"><span class="bg-slate-100 text-slate-700 px-2.5 py-1 rounded-md text-[11px] font-medium">${ord.category}</span></td>
                    <td class="p-3.5 text-slate-500 whitespace-nowrap">${ord.date}</td>
                    <td class="p-3.5">
                        <div class="flex items-center space-x-2">
                            ${getFileIconHtml(ord.fileType)}
                            <span class="font-medium text-slate-700 truncate max-w-[120px]">${ord.fileName}</span>
                        </div>
                    </td>
                    <td class="p-3.5 text-right whitespace-nowrap">
                        <button onclick="previewFile('${ord.fileName}', '${ord.fileType}')" class="px-2.5 py-1.5 bg-brand-50 text-brand-700 hover:bg-brand-100 rounded-lg font-medium mr-1">
                            <i class="fa-solid fa-eye mr-1"></i>Көру
                        </button>
                        <button onclick="downloadMockFile('${ord.fileName}')" class="px-2.5 py-1.5 bg-slate-100 text-slate-700 hover:bg-slate-200 rounded-lg font-medium">
                            <i class="fa-solid fa-download mr-1"></i>Жүктеу
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        let currentGradeFilter = 'ALL';
        function filterClassGrade(grade) {
            currentGradeFilter = grade;
            renderClassFolders();
        }

        function renderClassFolders() {
            const grid = document.getElementById('classFoldersGrid');
            grid.innerHTML = '';

            const filtered = appState.classFolders.filter(cf => {
                if (currentGradeFilter === 'ALL') return true;
                return cf.grade.startsWith(currentGradeFilter);
            });

            if (filtered.length === 0) {
                grid.innerHTML = `<div class="col-span-full p-8 text-center text-slate-400 bg-white rounded-2xl border border-slate-200">Таңдалған сынып бойынша тәрбие папкалары табылмады</div>`;
                return;
            }

            filtered.forEach(cf => {
                const card = document.createElement('div');
                card.className = "bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm hover:shadow-md transition flex flex-col justify-between";
                card.innerHTML = `
                    <div>
                        <div class="flex items-center justify-between mb-3">
                            <span class="bg-brand-100 text-brand-800 font-bold px-3 py-1 rounded-xl text-xs">${cf.grade} Сыныбы</span>
                            <span class="text-[11px] text-slate-400 font-mono"><i class="fa-solid fa-folder-closed mr-1"></i>Папка №${cf.id}</span>
                        </div>
                        <h4 class="font-bold text-slate-800 text-sm mb-1">${cf.topic}</h4>
                        <p class="text-xs text-slate-500 mb-3"><i class="fa-solid fa-user-tie mr-1 text-slate-400"></i>Жетекші: ${cf.teacher}</p>
                        
                        <div class="bg-slate-50 p-2.5 rounded-xl border border-slate-100 flex items-center justify-between text-[11px] text-slate-600 mb-4">
                            <span><i class="fa-solid fa-file-lines text-brand-500 mr-1"></i>Құжаттар: <strong>${cf.fileCount}</strong></span>
                            <span><i class="fa-solid fa-clipboard-check text-emerald-500 mr-1"></i>ҚМЖ/КТП: <strong>${cf.kmjCount}</strong></span>
                        </div>
                    </div>

                    <div class="pt-3 border-t border-slate-100 flex items-center justify-between">
                        <div class="flex items-center space-x-1.5 text-xs text-slate-600">
                            ${getFileIconHtml(cf.fileType)}
                            <span class="truncate max-w-[100px] font-medium">${cf.fileName}</span>
                        </div>
                        <div class="flex space-x-1">
                            <button onclick="previewFile('${cf.fileName}', '${cf.fileType}')" class="p-2 text-brand-600 hover:bg-brand-50 rounded-lg">
                                <i class="fa-solid fa-eye"></i>
                            </button>
                            <button onclick="downloadMockFile('${cf.fileName}')" class="p-2 text-slate-600 hover:bg-slate-100 rounded-lg">
                                <i class="fa-solid fa-download"></i>
                            </button>
                        </div>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function renderParents() {
            const container = document.getElementById('parentsCardsContainer');
            const search = document.getElementById('searchParents').value.toLowerCase();
            container.innerHTML = '';

            const filtered = appState.parentsWork.filter(p => p.title.toLowerCase().includes(search) || p.grade.toLowerCase().includes(search));

            filtered.forEach(p => {
                const card = document.createElement('div');
                card.className = "bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col justify-between";
                card.innerHTML = `
                    <div>
                        <div class="flex items-center justify-between mb-2">
                            <span class="bg-purple-100 text-purple-800 text-[11px] font-semibold px-2.5 py-0.5 rounded-lg">${p.type}</span>
                            <span class="text-xs text-slate-400"><i class="fa-regular fa-calendar mr-1"></i>${p.date}</span>
                        </div>
                        <h4 class="font-bold text-slate-800 text-sm">${p.title}</h4>
                        <p class="text-xs text-slate-500 mt-1">Сынып: <strong class="text-slate-700">${p.grade}</strong> | Қатысу пайызы: <strong class="text-emerald-600">${p.attendance}</strong></p>
                    </div>

                    <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between text-xs">
                        <div class="flex items-center space-x-2">
                            ${getFileIconHtml(p.fileType)}
                            <span class="font-medium text-slate-700 truncate max-w-[140px]">${p.fileName}</span>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="previewFile('${p.fileName}', '${p.fileType}')" class="px-3 py-1.5 bg-brand-50 text-brand-700 rounded-lg font-medium">Көру</button>
                            <button onclick="downloadMockFile('${p.fileName}')" class="px-3 py-1.5 bg-slate-100 text-slate-700 rounded-lg font-medium">Жүктеу</button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function renderCertificates() {
            const tbody = document.getElementById('certificatesTableBody');
            tbody.innerHTML = '';

            appState.certificates.forEach(c => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50/80 transition";
                tr.innerHTML = `
                    <td class="p-3.5 font-semibold text-slate-800">
                        <span class="font-mono text-slate-400 text-[10px] block">${c.id}</span>
                        ${c.title}
                    </td>
                    <td class="p-3.5"><span class="bg-indigo-50 text-indigo-700 px-2 py-0.5 rounded text-[11px] font-semibold">${c.type}</span></td>
                    <td class="p-3.5 text-slate-500">${c.date}</td>
                    <td class="p-3.5">
                        <div class="flex items-center space-x-2">
                            ${getFileIconHtml(c.fileType)}
                            <span class="font-medium text-slate-700">${c.fileName}</span>
                        </div>
                    </td>
                    <td class="p-3.5 text-right whitespace-nowrap">
                        <button onclick="previewFile('${c.fileName}', '${c.fileType}')" class="px-2.5 py-1.5 bg-brand-50 text-brand-700 rounded-lg font-medium mr-1">Көру</button>
                        <button onclick="downloadMockFile('${c.fileName}')" class="px-2.5 py-1.5 bg-slate-100 text-slate-700 rounded-lg font-medium">Жүктеу</button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        // MANDATORY COLUMNS: СЫНЫБЫ, АТЫ-ЖӨНІ, ТУЫЛҒАН КҮНІ, ИИН, ӘЛЕУМЕТТІК ЖАҒДАЙЫ
        function renderStudents() {
            const tbody = document.getElementById('studentsTableBody');
            const search = document.getElementById('searchStudents').value.toLowerCase();
            const gradeFilter = document.getElementById('filterStudentGrade').value;
            const socialFilter = document.getElementById('filterSocialStatus').value;

            tbody.innerHTML = '';

            const filtered = appState.students.filter(st => {
                const matchSearch = st.fullName.toLowerCase().includes(search) || st.iin.includes(search);
                const matchGrade = gradeFilter ? st.grade.startsWith(gradeFilter) : true;
                const matchSocial = socialFilter ? st.socialStatus.includes(socialFilter) : true;
                return matchSearch && matchGrade && matchSocial;
            });

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-6 text-center text-slate-400">Оқушылар тізімі бос немесе іздеу нәтижесі табылмады</td></tr>`;
                return;
            }

            filtered.forEach(st => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 transition border-b border-slate-100";
                
                // Highlight Special Education Needs (ЕБҚ / Ерекше)
                let socialBadgeClass = "bg-slate-100 text-slate-700";
                if (st.socialStatus.includes('ЕБҚ') || st.socialStatus.includes('Ерекше')) {
                    socialBadgeClass = "bg-purple-100 text-purple-800 font-bold border border-purple-200";
                } else if (st.socialStatus.includes('Көпбалалы')) {
                    socialBadgeClass = "bg-blue-100 text-blue-800 font-semibold";
                } else if (st.socialStatus.includes('Аз қамтылған')) {
                    socialBadgeClass = "bg-amber-100 text-amber-800 font-semibold";
                }

                tr.innerHTML = `
                    <td class="p-3.5 font-bold text-slate-800">${st.grade}</td>
                    <td class="p-3.5 font-semibold text-slate-900">${st.fullName}</td>
                    <td class="p-3.5 text-slate-600">${st.birthDate}</td>
                    <td class="p-3.5 font-mono text-slate-700">${st.iin}</td>
                    <td class="p-3.5">
                        <span class="px-2.5 py-1 rounded-lg text-[11px] inline-block ${socialBadgeClass}">
                            ${st.socialStatus}
                        </span>
                    </td>
                    <td class="p-3.5">
                        <div class="flex items-center space-x-2">
                            ${getFileIconHtml(st.fileType)}
                            <button onclick="previewFile('${st.fileName}', '${st.fileType}')" class="text-brand-600 hover:underline font-medium truncate max-w-[120px]">
                                ${st.fileName}
                            </button>
                        </div>
                    </td>
                    <td class="p-3.5 text-right whitespace-nowrap">
                        <button onclick="downloadMockFile('${st.fileName}')" class="px-3 py-1.5 bg-brand-600 hover:bg-brand-700 text-white rounded-lg font-semibold shadow-2xs">
                            <i class="fa-solid fa-download mr-1"></i> Жүктеу
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderEvents() {
            const container = document.getElementById('eventsContainer');
            const search = document.getElementById('searchEvents').value.toLowerCase();
            container.innerHTML = '';

            const filtered = appState.events.filter(ev => ev.title.toLowerCase().includes(search) || ev.responsible.toLowerCase().includes(search));

            filtered.forEach(ev => {
                const isVideo = ev.mediaType === 'video';
                const card = document.createElement('div');
                card.className = "bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm flex flex-col md:flex-row justify-between gap-4";
                card.innerHTML = `
                    <div class="flex-1 space-y-2">
                        <div class="flex items-center space-x-2">
                            <span class="bg-indigo-100 text-indigo-800 text-[11px] font-bold px-2.5 py-0.5 rounded-md"><i class="fa-solid fa-calendar-day mr-1"></i>${ev.date}</span>
                            <span class="text-xs text-slate-500">Жауапты: <strong>${ev.responsible}</strong></span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base">${ev.title}</h3>
                        
                        <div class="flex flex-wrap items-center gap-3 pt-2">
                            <div class="flex items-center bg-slate-50 px-3 py-1.5 rounded-xl border border-slate-200 text-xs text-slate-700">
                                <i class="fa-solid fa-file-word text-blue-600 mr-2 text-sm"></i>
                                <span>ҚМЖ/КТП: <strong>${ev.kmjFile}</strong></span>
                                <button onclick="previewFile('${ev.kmjFile}', 'docx')" class="ml-2 text-brand-600 hover:underline text-[11px]">Көру</button>
                            </div>

                            <div class="flex items-center bg-slate-50 px-3 py-1.5 rounded-xl border border-slate-200 text-xs text-slate-700">
                                ${isVideo ? '<i class="fa-solid fa-video text-purple-600 mr-2 text-sm"></i>' : '<i class="fa-solid fa-image text-emerald-600 mr-2 text-sm"></i>'}
                                <span>Медиа: <strong>${ev.mediaFile}</strong></span>
                                <button onclick="previewFile('${ev.mediaFile}', '${isVideo ? 'mp4' : 'png'}')" class="ml-2 text-brand-600 hover:underline text-[11px]">Көру</button>
                            </div>
                        </div>
                    </div>

                    <div class="flex items-center space-x-2 border-t md:border-t-0 md:border-l border-slate-100 pt-3 md:pt-0 md:pl-4">
                        <button onclick="downloadMockFile('${ev.kmjFile}')" class="px-3 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl font-medium text-xs">
                            <i class="fa-solid fa-download mr-1"></i>ҚМЖ Жүктеу
                        </button>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function renderTeachers() {
            const tbody = document.getElementById('teachersTableBody');
            tbody.innerHTML = '';

            appState.teachers.forEach(t => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 transition";
                tr.innerHTML = `
                    <td class="p-3.5 font-bold text-slate-800">${t.name}</td>
                    <td class="p-3.5"><span class="bg-brand-50 text-brand-800 font-bold px-2.5 py-1 rounded-lg text-xs">${t.grade}</span></td>
                    <td class="p-3.5 font-mono text-slate-600">${t.login}</td>
                    <td class="p-3.5">
                        <span class="font-mono font-bold bg-amber-50 text-amber-900 border border-amber-200 px-2.5 py-1 rounded-md tracking-wider text-xs">
                            ${t.code}
                        </span>
                    </td>
                    <td class="p-3.5">
                        <button onclick="toggleTeacherAccess('${t.id}')" class="px-2.5 py-1 rounded-full text-[11px] font-bold flex items-center ${t.accessGranted ? 'bg-emerald-100 text-emerald-800' : 'bg-red-100 text-red-800'}">
                            <i class="fa-solid ${t.accessGranted ? 'fa-check' : 'fa-ban'} mr-1"></i>
                            ${t.accessGranted ? 'Рұқсат Берілген' : 'Бұғатталған'}
                        </button>
                    </td>
                    <td class="p-3.5 text-right">
                        <button onclick="regenerateCodeForTeacher('${t.id}')" class="text-xs text-brand-600 hover:text-brand-800 font-medium underline">
                            Кодты жаңарту
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function toggleTeacherAccess(teacherId) {
            const teacher = appState.teachers.find(t => t.id === teacherId);
            if (teacher) {
                teacher.accessGranted = !teacher.accessGranted;
                saveStorage();
                renderTeachers();
                showToast(`Рұқсат мәртебесі өзгертілді: ${teacher.name}`);
            }
        }

        function regenerateCodeForTeacher(teacherId) {
            const teacher = appState.teachers.find(t => t.id === teacherId);
            if (teacher) {
                teacher.code = generateRandomCode();
                saveStorage();
                renderTeachers();
                showToast(`Жаңа 1 реттік код берілді: ${teacher.code}`);
            }
        }

        function getFileIconHtml(type) {
            const t = (type || '').toLowerCase();
            if (t.includes('pdf')) return '<i class="fa-solid fa-file-pdf text-red-500 text-base"></i>';
            if (t.includes('doc')) return '<i class="fa-solid fa-file-word text-blue-500 text-base"></i>';
            if (t.includes('xls')) return '<i class="fa-solid fa-file-excel text-emerald-500 text-base"></i>';
            if (t.includes('png') || t.includes('jpg') || t.includes('jpeg')) return '<i class="fa-solid fa-file-image text-amber-500 text-base"></i>';
            if (t.includes('mp4') || t.includes('video')) return '<i class="fa-solid fa-file-video text-purple-500 text-base"></i>';
            return '<i class="fa-solid fa-file text-slate-400 text-base"></i>';
        }

        function previewFile(fileName, fileType) {
            const modal = document.getElementById('filePreviewModal');
            const title = document.getElementById('previewModalTitle');
            const body = document.getElementById('previewModalBody');
            const meta = document.getElementById('previewMeta');
            const downloadBtn = document.getElementById('previewDownloadBtn');

            title.textContent = `Алдын ала көру: ${fileName}`;
            meta.textContent = `Типі: ${fileType.toUpperCase()}`;
            downloadBtn.onclick = function() { downloadMockFile(fileName); };

            const type = (fileType || '').toLowerCase();
            body.innerHTML = '';

            if (type.includes('png') || type.includes('jpg') || type.includes('jpeg')) {
                body.innerHTML = `
                    <img src="https://placehold.co/600x350/0284c7/ffffff?text=${encodeURIComponent(fileName)}" alt="Preview Image" class="max-w-full rounded-xl shadow-md border border-slate-200">
                `;
            } else if (type.includes('mp4') || type.includes('video')) {
                body.innerHTML = `
                    <div class="w-full bg-slate-900 rounded-xl p-8 text-center text-white space-y-3">
                        <i class="fa-solid fa-circle-play text-5xl text-brand-400 animate-pulse"></i>
                        <p class="font-bold text-sm">${fileName}</p>
                        <p class="text-xs text-slate-400">Бейне таспа ойнатылуға дайын</p>
                    </div>
                `;
            } else {
                // PDF / WORD / EXCEL simulated document viewer
                body.innerHTML = `
                    <div class="w-full max-w-md bg-white p-6 rounded-2xl shadow-sm border border-slate-200 text-center space-y-3">
                        <div class="w-16 h-16 rounded-full bg-brand-50 text-brand-600 flex items-center justify-center mx-auto text-2xl">
                            ${getFileIconHtml(fileType)}
                        </div>
                        <h4 class="font-bold text-slate-800 text-sm">${fileName}</h4>
                        <p class="text-xs text-slate-500 leading-relaxed">
                            Құжат сәтті оқылды. Толық мазмұнын көру және басып шығару үшін төмендегі «Файлды Жүктеу» батырмасын басыңыз.
                        </p>
                    </div>
                `;
            }

            modal.classList.remove('hidden');
        }

        function downloadMockFile(fileName) {
            // Create Blob and download
            const content = `Мектеп тәрбие жүйесі құжаты: ${fileName}\nКүні: ${new Date().toLocaleDateString()}\nМәртебесі: Ресми куәландырылған.`;
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = fileName.includes('.') ? fileName : `${fileName}.txt`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            showToast(`Файл жүктелді: ${fileName}`);
        }

        function openAddDocModal(section = 'orders') {
            document.getElementById('docTargetSection').value = section;
            document.getElementById('addDocModal').classList.remove('hidden');
        }

        function openAddStudentModal() {
            document.getElementById('addStudentModal').classList.remove('hidden');
        }

        function openAddEventModal() {
            document.getElementById('addEventModal').classList.remove('hidden');
        }

        function openAddTeacherModal() {
            generateTeacherCode();
            document.getElementById('addTeacherModal').classList.remove('hidden');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
        }

        function handleFileSelected(input) {
            const info = document.getElementById('fileSelectedInfo');
            if (input.files && input.files[0]) {
                info.textContent = `Таңдалған файл: ${input.files[0].name} (${(input.files[0].size / 1024).toFixed(1)} KB)`;
                info.classList.remove('hidden');
            }
        }

        function generateRandomCode() {
            return Math.random().toString(36).substring(2, 8).toUpperCase();
        }

        function generateTeacherCode() {
            document.getElementById('tCode').value = generateRandomCode();
        }

        // Add Document Submit Handler
        function handleDocSubmit(e) {
            e.preventDefault();
            const title = document.getElementById('docTitle').value;
            const target = document.getElementById('docTargetSection').value;
            const category = document.getElementById('docCategory').value || 'Жалпы';
            const grade = document.getElementById('docGrade').value;
            const fileInput = document.getElementById('docFileInput');

            let fileName = "Kujat_Satti_Jukteldi.pdf";
            let fileType = "pdf";

            if (fileInput.files && fileInput.files[0]) {
                fileName = fileInput.files[0].name;
                const ext = fileName.split('.').pop().toLowerCase();
                fileType = ext;
            }

            const newDoc = {
                id: `DOC-${Math.floor(1000 + Math.random() * 9000)}`,
                title: title,
                category: category,
                date: new Date().toISOString().split('T')[0],
                fileName: fileName,
                fileType: fileType,
                fileSize: "1.2 MB"
            };

            if (target === 'orders') {
                appState.orders.unshift(newDoc);
                renderOrders();
            } else if (target === 'classFolder') {
                appState.classFolders.unshift({
                    id: `CF-${appState.classFolders.length + 1}`,
                    grade: grade === 'Жалпы' ? '1-А' : grade,
                    teacher: appState.currentUser.name,
                    topic: title,
                    fileCount: 1,
                    kmjCount: 1,
                    fileName: fileName,
                    fileType: fileType
                });
                renderClassFolders();
            } else if (target === 'certificates') {
                appState.certificates.unshift({
                    id: `CERT-${appState.certificates.length + 100}`,
                    title: title,
                    type: category,
                    date: new Date().toISOString().split('T')[0],
                    fileName: fileName,
                    fileType: fileType
                });
                renderCertificates();
            } else {
                appState.parentsWork.unshift({
                    id: `P-${appState.parentsWork.length + 1}`,
                    grade: grade,
                    title: title,
                    date: new Date().toISOString().split('T')[0],
                    type: category,
                    attendance: "95%",
                    fileName: fileName,
                    fileType: fileType
                });
                renderParents();
            }

            saveStorage();
            closeModal('addDocModal');
            showToast("Жаңа құжат жүйеге сәтті қосылды!");
            document.getElementById('docForm').reset();
            document.getElementById('fileSelectedInfo').classList.add('hidden');
        }

        // Add Student Submit Handler
        function handleStudentSubmit(e) {
            e.preventDefault();
            const grade = document.getElementById('stGrade').value;
            const name = document.getElementById('stName').value;
            const birth = document.getElementById('stBirth').value;
            const iin = document.getElementById('stIin').value;
            const social = document.getElementById('stSocial').value;
            const fileInput = document.getElementById('stFileInput');

            let fileName = "Student_Document.pdf";
            let fileType = "pdf";

            if (fileInput.files && fileInput.files[0]) {
                fileName = fileInput.files[0].name;
                fileType = fileName.split('.').pop().toLowerCase();
            }

            appState.students.unshift({
                id: `ST-${appState.students.length + 1}`,
                grade: grade,
                fullName: name,
                birthDate: birth,
                iin: iin,
                socialStatus: social,
                fileName: fileName,
                fileType: fileType
            });

            saveStorage();
            renderStudents();
            renderDashboard();
            closeModal('addStudentModal');
            showToast("Оқушы құжаттары тізімге қосылды!");
        }

        // Add Event Submit Handler
        function handleEventSubmit(e) {
            e.preventDefault();
            const title = document.getElementById('evTitle').value;
            const date = document.getElementById('evDate').value;
            const resp = document.getElementById('evResponsible').value || 'Тәрбие тобы';
            const kmjInput = document.getElementById('evKmjInput');
            const mediaInput = document.getElementById('evMediaInput');

            let kmjFile = "KTP_Jozpar.docx";
            let mediaFile = "Event_Photo.png";
            let mediaType = "image";

            if (kmjInput.files && kmjInput.files[0]) kmjFile = kmjInput.files[0].name;
            if (mediaInput.files && mediaInput.files[0]) {
                mediaFile = mediaInput.files[0].name;
                if (mediaFile.endsWith('.mp4')) mediaType = "video";
            }

            appState.events.unshift({
                id: `EV-${appState.events.length + 1}`,
                title: title,
                date: date,
                responsible: resp,
                kmjFile: kmjFile,
                mediaFile: mediaFile,
                mediaType: mediaType
            });

            saveStorage();
            renderEvents();
            closeModal('addEventModal');
            showToast("Іс-шара ҚМЖ/КТП құжаттарымен қосылды!");
        }

        // Add Teacher Submit Handler
        function handleTeacherSubmit(e) {
            e.preventDefault();
            const name = document.getElementById('tName').value;
            const grade = document.getElementById('tGrade').value;
            const login = document.getElementById('tLogin').value;
            const code = document.getElementById('tCode').value;

            appState.teachers.unshift({
                id: `T-${appState.teachers.length + 1}`,
                name: name,
                grade: grade,
                login: login,
                code: code,
                accessGranted: true
            });

            saveStorage();
            renderTeachers();
            closeModal('addTeacherModal');
            showToast(`Сынып жетекші сақталды. 1-Реттік Код: ${code}`);
        }

        function openGoogleAdminLogin() {
            toggleAuthMenu();
            document.getElementById('googleAdminModal').classList.remove('hidden');
        }

        function confirmAdminGoogleAuth() {
            appState.currentUser = {
                role: 'ADMIN',
                name: 'Администратор (Гугл)',
                grade: 'Барлық сыныптар',
                accessGranted: true
            };
            saveStorage();
            updateHeaderAndUserUI();
            closeModal('googleAdminModal');
            showToast("Гугл аккаунтпен Администратор болып кірдіңіз!");
        }

        function openTeacherLoginModal() {
            toggleAuthMenu();
            document.getElementById('teacherLoginModal').classList.remove('hidden');
        }

        function handleTeacherCodeLogin(e) {
            e.preventDefault();
            const login = document.getElementById('loginInputUser').value.trim();
            const code = document.getElementById('loginInputCode').value.trim().toUpperCase();

            const teacher = appState.teachers.find(t => t.login === login && t.code === code);

            if (teacher) {
                if (!teacher.accessGranted) {
                    showToast("Администратор сіздің аккаунтыңызды бұғаттаған!", "error");
                    return;
                }
                appState.currentUser = {
                    role: 'TEACHER',
                    name: teacher.name,
                    grade: teacher.grade,
                    accessGranted: true
                };
                saveStorage();
                updateHeaderAndUserUI();
                closeModal('teacherLoginModal');
                showToast(`Қош келдіңіз, ${teacher.name}! (${teacher.grade})`);
            } else {
                showToast("Қате логин немесе 1 реттік код!", "error");
            }
        }

        function openOrgSettingsModal() {
            toggleAuthMenu();
            document.getElementById('orgNameInput').value = appState.orgName;
            document.getElementById('orgModal').classList.remove('hidden');
        }

        function saveOrgName() {
            const val = document.getElementById('orgNameInput').value.trim();
            if (val) {
                appState.orgName = val;
                saveStorage();
                updateHeaderAndUserUI();
                closeModal('orgModal');
                showToast("Мекеме атауы сәтті жаңартылды!");
            }
        }
    </script>
</body>
</html>
