[Uploading code_artifact.html…]()
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ช่างงานเซอร์วิสระบบปรับอากาศและทำความเย็น - ช่างอัฐ</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Prompt & Sarabun -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@500;600;700;800&family=Sarabun:wght@500;600;700;800&display=swap" rel="stylesheet">
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Sarabun', 'sans-serif'],
                        heading: ['Prompt', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Sarabun', sans-serif;
            background-color: #F8FAFC;
            color: #0F172A;
            font-size: 16px;
            -webkit-tap-highlight-color: transparent;
            padding-bottom: 96px;
        }
        h1, h2, h3, .font-heading {
            font-family: 'Prompt', sans-serif;
        }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        
        /* ปุ่มกดขนาดใหญ่สำหรับหน้างานกลางแจ้ง/มือเปียก */
        .btn-outdoor {
            min-height: 52px;
            transition: transform 0.08s ease;
        }
        .btn-outdoor:active {
            transform: scale(0.97);
        }
    </style>
</head>
<body class="antialiased select-none sm:select-auto">

    <!-- Top Header: High Contrast #0F172A -->
    <header class="bg-[#0F172A] text-white sticky top-0 z-30 shadow-xl border-b-4 border-[#EA580C]">
        <div class="max-w-xl mx-auto px-3.5 py-3 flex items-center justify-between gap-2">
            <div class="flex items-center space-x-3 min-w-0">
                <div class="w-12 h-12 rounded-xl bg-[#EA580C] flex items-center justify-center text-white text-2xl shadow-md shrink-0 border-2 border-orange-300">
                    <i class="fa-solid fa-snowflake"></i>
                </div>
                <div class="min-w-0">
                    <h1 id="headerShopName" class="font-heading font-bold text-base sm:text-lg leading-tight truncate">
                        ช่างงานเซอร์วิสระบบปรับอากาศและทำความเย็น
                    </h1>
                    <p id="headerTechInfo" class="text-xs sm:text-sm text-amber-300 font-bold truncate">
                        ช่างอัฐ (ทัฐชวิน) • โทร. 082-191-9619
                    </p>
                </div>
            </div>
            <button onclick="openSettingsModal()" class="btn-outdoor shrink-0 bg-[#1E40AF] hover:bg-blue-700 border-2 border-blue-400 text-white px-3.5 py-2 rounded-xl text-sm font-bold flex items-center gap-1.5 shadow-md">
                <i class="fa-solid fa-gear text-amber-300 text-lg"></i>
                <span class="hidden sm:inline">ตั้งค่า/สำรอง</span>
            </button>
        </div>
    </header>

    <!-- Toast Notification Banner -->
    <div id="toastBanner" class="fixed top-20 left-1/2 transform -translate-x-1/2 z-50 hidden w-[92%] max-w-md">
        <div class="bg-[#0F172A] text-white px-5 py-4 rounded-2xl shadow-2xl border-2 border-[#EA580C] flex items-center gap-3 text-base font-bold">
            <i id="toastIcon" class="fa-solid fa-circle-check text-green-400 text-2xl shrink-0"></i>
            <span id="toastMessage">บันทึกข้อมูลเรียบร้อย</span>
        </div>
    </div>

    <!-- Main Content Container -->
    <main class="max-w-xl mx-auto px-3 pt-4 space-y-4">

        <!-- ========================================================== -->
        <!-- TAB 1: งาน & ลูกค้า (Job Log & Customer History)            -->
        <!-- ========================================================== -->
        <section id="tab-jobs" class="space-y-4">
            
            <!-- ปุ่มเพิ่มงาน/ลูกค้าใหม่ ขนาดใหญ่ -->
            <button onclick="openJobModal()" class="btn-outdoor w-full bg-[#EA580C] hover:bg-orange-700 text-white font-heading font-bold text-xl py-3.5 px-5 rounded-2xl shadow-lg border-2 border-orange-900 flex items-center justify-center gap-3">
                <i class="fa-solid fa-circle-plus text-2xl"></i>
                <span>+ เพิ่มงาน / ลูกค้าใหม่</span>
            </button>

            <!-- ช่องค้นหา Real-time + ตัวกรองสถานะ -->
            <div class="bg-white p-3.5 rounded-2xl shadow-md border-2 border-slate-300 space-y-3">
                <div class="relative">
                    <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-slate-600 text-xl"></i>
                    <input type="text" id="jobSearchInput" oninput="renderJobs()" placeholder="ค้นหาชื่อลูกค้า, ผู้ติดต่อ, เบอร์โทร..." 
                        class="w-full pl-12 pr-12 py-3.5 text-lg font-bold text-[#0F172A] bg-slate-100 border-2 border-slate-400 rounded-xl focus:outline-none focus:border-[#1E40AF] focus:bg-white">
                    <button id="clearSearchBtn" onclick="clearJobSearch()" class="hidden absolute right-3 top-1/2 -translate-y-1/2 text-slate-600 hover:text-red-600 p-2 text-2xl">
                        <i class="fa-solid fa-circle-xmark"></i>
                    </button>
                </div>

                <!-- แถบตัวกรองสถานะงาน -->
                <div class="flex gap-2 overflow-x-auto no-scrollbar pb-1" id="statusFilterBar">
                    <button onclick="setJobFilter('ALL')" data-filter="ALL" class="filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-[#0F172A] bg-[#0F172A] text-white shadow">
                        ทั้งหมด (<span id="count-ALL">0</span>)
                    </button>
                    <button onclick="setJobFilter('DUE')" data-filter="DUE" class="filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-red-600 bg-red-50 text-red-800">
                        🔔 ถึงรอบล้างแอร์ (<span id="count-DUE">0</span>)
                    </button>
                    <button onclick="setJobFilter('รอดำเนินการ')" data-filter="รอดำเนินการ" class="filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-slate-400 bg-white text-[#0F172A]">
                        รอดำเนินการ (<span id="count-PENDING">0</span>)
                    </button>
                    <button onclick="setJobFilter('กำลังทำ')" data-filter="กำลังทำ" class="filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-slate-400 bg-white text-[#0F172A]">
                        กำลังทำ (<span id="count-DOING">0</span>)
                    </button>
                    <button onclick="setJobFilter('เสร็จสิ้น')" data-filter="เสร็จสิ้น" class="filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-slate-400 bg-white text-[#0F172A]">
                        เสร็จสิ้น (<span id="count-DONE">0</span>)
                    </button>
                </div>
            </div>

            <!-- รายการการ์ดลูกค้าและประวัติงาน -->
            <div id="jobListContainer" class="space-y-4"></div>
        </section>

        <!-- ========================================================== -->
        <!-- TAB 2: เช็กอาการ & บิล (Quick Quote & Check)              -->
        <!-- ========================================================== -->
        <section id="tab-quote" class="hidden space-y-5">
            
            <!-- ส่วนที่ 1: ปุ่มเลือกอาการเสียยอดนิยม 6 ปุ่มใหญ่ -->
            <div class="bg-white p-4 rounded-2xl shadow-md border-2 border-slate-300 space-y-3">
                <h2 class="font-heading font-bold text-lg text-[#0F172A] flex items-center gap-2">
                    <i class="fa-solid fa-stethoscope text-[#EA580C] text-xl"></i>
                    <span>1. เช็กอาการเสียหน้างาน (กดเลือกอาการ)</span>
                </h2>
                
                <div class="grid grid-cols-2 gap-2.5" id="symptomButtonsGrid"></div>

                <!-- กล่อง Checklist จุดตรวจเช็กหน้างาน (ติ๊กได้) -->
                <div id="symptomGuideBox" class="hidden mt-3 bg-amber-50 border-2 border-amber-600 rounded-2xl p-4 space-y-3">
                    <div class="flex justify-between items-center border-b border-amber-300 pb-2">
                        <h3 id="symptomGuideTitle" class="font-heading font-bold text-lg text-amber-950"></h3>
                        <button onclick="document.getElementById('symptomGuideBox').classList.add('hidden')" class="text-amber-950 text-2xl px-2">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>
                    <p class="text-sm font-bold text-amber-900">ติ๊กจุดที่ตรวจเช็กแล้ว:</p>
                    <div id="symptomCheckList" class="space-y-2"></div>
                    <div class="pt-2 border-t border-amber-300">
                        <p class="text-sm font-bold text-amber-950 mb-2">เพิ่มรายการซ่อม/บริการที่เกี่ยวข้องลงบิล:</p>
                        <div id="symptomQuickAddBtns" class="flex flex-wrap gap-2"></div>
                    </div>
                </div>
            </div>

            <!-- ส่วนที่ 2: ตารางคำนวณค่าบริการและค่าอะไหล่ -->
            <div class="bg-white p-4 rounded-2xl shadow-md border-2 border-slate-300 space-y-4">
                <div class="flex justify-between items-center">
                    <h2 class="font-heading font-bold text-lg text-[#0F172A] flex items-center gap-2">
                        <i class="fa-solid fa-calculator text-[#1E40AF] text-xl"></i>
                        <span>2. คำนวณราคา / ออกบิล</span>
                    </h2>
                    <span class="bg-[#0F172A] text-amber-300 px-3 py-1 rounded-xl font-bold text-sm">
                        บิลเลขที่ #<span id="displayBillNumber">3460</span>
                    </span>
                </div>

                <!-- เลือกลูกค้าเก่าหรือกรอกชื่อลูกค้าในบิล -->
                <div class="bg-slate-100 p-3.5 rounded-2xl border-2 border-slate-300 space-y-3">
                    <div>
                        <label class="block text-sm font-bold text-slate-800 mb-1">ดึงรายชื่อลูกค้าจากฐานข้อมูล:</label>
                        <select id="quoteCustomerSelect" onchange="fillQuoteCustomerFromSelect()" class="w-full p-3 text-base font-bold bg-white border-2 border-slate-400 rounded-xl text-[#0F172A]">
                            <option value="">-- เลือกลูกค้าเดิม หรือกรอกใหม่ด้านล่าง --</option>
                        </select>
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                        <div>
                            <label class="block text-sm font-bold text-slate-800 mb-1">ชื่อลูกค้า / บริษัท *</label>
                            <input type="text" id="quoteCustomerName" placeholder="เช่น ไร่มณีทิพย์" class="w-full p-3 text-base font-bold bg-white border-2 border-slate-400 rounded-xl">
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-slate-800 mb-1">เบอร์โทร / ที่อยู่ย่อ</label>
                            <input type="text" id="quoteCustomerPhone" placeholder="เช่น 063-232-5789" class="w-full p-3 text-base font-bold bg-white border-2 border-slate-400 rounded-xl">
                        </div>
                    </div>
                </div>

                <!-- ปุ่มเพิ่มรายการมาตรฐานในคลิกเดียว -->
                <div>
                    <p class="text-sm font-bold text-slate-800 mb-2">กดเพิ่มรายการมาตรฐานในคลิกเดียว:</p>
                    <div class="flex flex-wrap gap-2" id="presetServiceButtons"></div>
                </div>

                <!-- รายการในบิล (แก้ไขราคา/จำนวนได้) -->
                <div class="space-y-3" id="quoteItemsContainer"></div>

                <!-- ปุ่มเพิ่มรายการอิสระ -->
                <button onclick="addQuoteItem('', 0, 1)" class="btn-outdoor w-full py-3 px-4 bg-blue-50 hover:bg-blue-100 text-[#1E40AF] border-2 border-dashed border-[#1E40AF] rounded-xl font-bold text-base flex items-center justify-center gap-2">
                    <i class="fa-solid fa-plus text-lg"></i>
                    <span>+ เพิ่มรายการอิสระเอง</span>
                </button>

                <!-- ช่องใส่ส่วนลด และ หมายเหตุมาตรฐานของร้าน -->
                <div class="grid grid-cols-1 gap-3 bg-slate-50 p-3.5 rounded-2xl border-2 border-slate-300">
                    <div class="flex items-center justify-between gap-3">
                        <label class="text-base font-bold text-slate-900 shrink-0">ส่วนลด (บาท):</label>
                        <input type="number" id="quoteDiscountInput" value="0" min="0" oninput="updateQuoteTotals()" 
                            class="w-36 p-2.5 text-lg font-extrabold text-right text-red-700 bg-white border-2 border-slate-400 rounded-xl">
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-slate-800 mb-1">หมายเหตุท้ายบิล (แก้ไขได้):</label>
                        <textarea id="quoteNoteInput" rows="2" class="w-full p-2.5 text-sm font-bold bg-white border-2 border-slate-400 rounded-xl text-slate-800">การตรวจเช็คตามอาการและตามลำดับขั้นตอนจึงไม่สามารถแจ้งราคาเหมารวมลูกค้าในครั้งเดียวได้</textarea>
                    </div>
                </div>

                <!-- กล่องแสดงยอดรวมสุทธิ -->
                <div class="bg-[#0F172A] text-white p-4 rounded-2xl border-2 border-slate-700 flex items-center justify-between shadow-lg">
                    <div>
                        <span class="text-sm text-slate-300 font-bold block">ยอดรวมสุทธิทั้งสิ้น</span>
                        <span class="text-xs text-amber-300 font-bold" id="quoteSummarySubtext">0 รายการ</span>
                    </div>
                    <div class="text-right">
                        <span id="quoteGrandTotal" class="font-heading font-extrabold text-3xl sm:text-4xl text-amber-400">0</span>
                        <span class="text-lg font-bold ml-1">บาท</span>
                    </div>
                </div>

                <!-- ส่วนที่ 3: ปุ่มใหญ่ 3 ปุ่มด้านล่าง -->
                <div class="space-y-3 pt-1">
                    <button onclick="copyBillTextForLine()" class="btn-outdoor w-full bg-[#15803D] hover:bg-green-800 text-white font-heading font-bold text-lg py-3.5 px-4 rounded-2xl shadow-lg border-2 border-green-950 flex items-center justify-center gap-3">
                        <i class="fa-brands fa-line text-2xl"></i>
                        <span>1) คัดลอกข้อความส่ง LINE</span>
                    </button>

                    <button onclick="generateBillCanvasAndOpenModal()" class="btn-outdoor w-full bg-[#1E40AF] hover:bg-blue-900 text-white font-heading font-bold text-lg py-3.5 px-4 rounded-2xl shadow-lg border-2 border-blue-950 flex items-center justify-center gap-3">
                        <i class="fa-solid fa-file-invoice text-2xl text-amber-300"></i>
                        <span>2) สร้างรูปบิล / ใบเสนอราคา</span>
                    </button>

                    <button onclick="recordBillToDailyIncome()" class="btn-outdoor w-full bg-[#EA580C] hover:bg-orange-700 text-white font-heading font-bold text-lg py-3.5 px-4 rounded-2xl shadow-lg border-2 border-orange-950 flex items-center justify-center gap-3">
                        <i class="fa-solid fa-sack-dollar text-2xl"></i>
                        <span>3) บันทึกลงรายรับวันนี้</span>
                    </button>
                </div>
            </div>
        </section>

        <!-- ========================================================== -->
        <!-- TAB 3: บัญชี & กำไร (Daily Profit & Expense)              -->
        <!-- ========================================================== -->
        <section id="tab-finance" class="hidden space-y-4">
            
            <!-- ตัวเลือกวันที่ & สลับโหมด รายวัน / ภาพรวมทั้งหมด -->
            <div class="bg-white p-3.5 rounded-2xl shadow-md border-2 border-slate-300 space-y-3">
                <div class="grid grid-cols-2 gap-2">
                    <button onclick="setFinanceMode('DAILY')" id="finMode-DAILY" class="btn-outdoor py-2.5 rounded-xl font-heading font-bold text-base bg-[#0F172A] text-white border-2 border-[#0F172A]">
                        📅 สรุปรายวัน
                    </button>
                    <button onclick="setFinanceMode('ALL')" id="finMode-ALL" class="btn-outdoor py-2.5 rounded-xl font-heading font-bold text-base bg-slate-100 text-[#0F172A] border-2 border-slate-400">
                        📊 ภาพรวมทั้งหมด
                    </button>
                </div>

                <div id="financeDatePickerRow" class="flex items-center justify-between gap-2 bg-slate-100 p-2.5 rounded-xl border border-slate-300">
                    <label for="financeSelectedDate" class="font-bold text-base text-slate-800 pl-1">เลือกวันที่:</label>
                    <div class="flex items-center gap-2">
                        <input type="date" id="financeSelectedDate" onchange="renderFinance()" class="p-2 text-base font-bold bg-white border-2 border-slate-400 rounded-xl">
                        <button onclick="setFinanceDateToday()" class="px-3 py-2 bg-[#1E40AF] text-white font-bold text-sm rounded-xl">วันนี้</button>
                    </div>
                </div>
            </div>

            <!-- การ์ดสรุปตัวเลขใหญ่ 3 ช่อง: รายรับ (เขียว), รายจ่าย (แดง), กำไรสุทธิ (น้ำเงินเข้ม/ทอง) -->
            <div class="space-y-3">
                <div class="grid grid-cols-2 gap-3">
                    <!-- รายรับรวม -->
                    <div class="bg-[#15803D] text-white p-4 rounded-2xl shadow-lg border-2 border-green-950">
                        <p class="text-sm font-bold text-green-100 flex items-center gap-1.5">
                            <i class="fa-solid fa-arrow-trend-up"></i> รายรับรวม
                        </p>
                        <p id="totalIncomeValue" class="font-heading font-extrabold text-2xl sm:text-3xl mt-1">0 ฿</p>
                    </div>
                    <!-- รายจ่ายรวม -->
                    <div class="bg-red-700 text-white p-4 rounded-2xl shadow-lg border-2 border-red-950">
                        <p class="text-sm font-bold text-red-100 flex items-center gap-1.5">
                            <i class="fa-solid fa-arrow-trend-down"></i> รายจ่ายรวม
                        </p>
                        <p id="totalExpenseValue" class="font-heading font-extrabold text-2xl sm:text-3xl mt-1">0 ฿</p>
                    </div>
                </div>

                <!-- กำไรสุทธิ -->
                <div class="bg-[#0F172A] text-white p-5 rounded-2xl shadow-xl border-2 border-amber-400 flex items-center justify-between">
                    <div>
                        <p id="netProfitLabel" class="text-base font-bold text-slate-200">กำไรสุทธิ (วันนี้)</p>
                        <p class="text-xs text-amber-300 font-semibold">รายรับหักรายจ่ายทั้งหมด</p>
                    </div>
                    <p id="netProfitValue" class="font-heading font-extrabold text-3xl sm:text-4xl text-amber-400">0 ฿</p>
                </div>
            </div>

            <!-- ปุ่มเพิ่มรายการด่วน 2 ปุ่มใหญ่ -->
            <div class="grid grid-cols-2 gap-3">
                <button onclick="openFinanceModal('INCOME')" class="btn-outdoor bg-[#15803D] hover:bg-green-800 text-white font-heading font-bold text-lg py-3.5 px-3 rounded-2xl shadow-lg border-2 border-green-950 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-circle-plus text-2xl"></i>
                    <span>+ บันทึกรายรับ</span>
                </button>
                <button onclick="openFinanceModal('EXPENSE')" class="btn-outdoor bg-red-700 hover:bg-red-800 text-white font-heading font-bold text-lg py-3.5 px-3 rounded-2xl shadow-lg border-2 border-red-950 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-circle-minus text-2xl"></i>
                    <span>+ บันทึกรายจ่าย</span>
                </button>
            </div>

            <!-- รายการธุรกรรม -->
            <div class="bg-white p-4 rounded-2xl shadow-md border-2 border-slate-300 space-y-3">
                <div class="flex justify-between items-center border-b-2 border-slate-200 pb-2">
                    <h3 class="font-heading font-bold text-lg text-[#0F172A]">รายการรายรับ - รายจ่าย</h3>
                    <span class="text-sm font-bold text-slate-600" id="financeEntryCount">0 รายการ</span>
                </div>
                <div id="financeListContainer" class="space-y-3"></div>
            </div>
        </section>

    </main>

    <!-- ========================================================== -->
    <!-- BOTTOM TAB BAR ขนาดใหญ่ 3 แท็บหลัก                          -->
    <!-- ========================================================== -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white border-t-4 border-[#0F172A] z-40 shadow-[0_-4px_14px_rgba(0,0,0,0.18)]">
        <div class="max-w-xl mx-auto grid grid-cols-3 h-[82px]">
            <button onclick="switchTab('jobs')" id="nav-jobs" class="nav-btn flex flex-col items-center justify-center gap-1 bg-[#0F172A] text-amber-300 font-heading font-bold border-r border-slate-700">
                <i class="fa-solid fa-clipboard-list text-2xl"></i>
                <span class="text-sm sm:text-base">1. งาน & ลูกค้า</span>
            </button>
            <button onclick="switchTab('quote')" id="nav-quote" class="nav-btn flex flex-col items-center justify-center gap-1 bg-white text-[#0F172A] hover:bg-slate-100 font-heading font-bold border-r border-slate-300">
                <i class="fa-solid fa-file-invoice-dollar text-2xl"></i>
                <span class="text-sm sm:text-base">2. เช็กอาการ & บิล</span>
            </button>
            <button onclick="switchTab('finance')" id="nav-finance" class="nav-btn flex flex-col items-center justify-center gap-1 bg-white text-[#0F172A] hover:bg-slate-100 font-heading font-bold">
                <i class="fa-solid fa-wallet text-2xl"></i>
                <span class="text-sm sm:text-base">3. บัญชี & กำไร</span>
            </button>
        </div>
    </nav>

    <!-- ========================================================== -->
    <!-- MODAL 1: เพิ่ม / แก้ไขงานและข้อมูลลูกค้า                    -->
    <!-- ========================================================== -->
    <div id="jobModal" class="fixed inset-0 bg-black/80 z-50 hidden overflow-y-auto p-3 sm:p-4">
        <div class="bg-white max-w-lg mx-auto rounded-3xl shadow-2xl border-2 border-slate-400 overflow-hidden my-2">
            <div class="bg-[#0F172A] text-white px-5 py-4 flex justify-between items-center border-b-4 border-[#EA580C]">
                <h2 id="jobModalTitle" class="font-heading font-bold text-xl">เพิ่มงาน / ลูกค้าใหม่</h2>
                <button onclick="closeJobModal()" class="text-white hover:text-amber-300 text-2xl p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            
            <form id="jobForm" onsubmit="saveJobForm(event)" class="p-4 sm:p-5 space-y-4">
                <input type="hidden" id="editJobId">
                
                <!-- เลือกลูกค้าเก่าเพื่อ Auto-fill -->
                <div class="bg-blue-50 p-3.5 rounded-2xl border-2 border-[#1E40AF]">
                    <label class="block text-sm font-bold text-[#0F172A] mb-1.5">
                        <i class="fa-solid fa-address-book text-[#EA580C] mr-1"></i>
                        ดึงข้อมูลลูกค้าเดิม (ถ้าเคยมีประวัติ):
                    </label>
                    <select id="existingCustomerDropdown" onchange="autoFillCustomerToJobForm()" class="w-full p-3 text-base font-bold bg-white border-2 border-[#1E40AF] rounded-xl text-[#0F172A]">
                        <option value="">-- พิมพ์ลูกค้าใหม่ หรือเลือกจากรายชื่อเดิม --</option>
                    </select>
                </div>

                <div>
                    <label class="block text-base font-bold text-[#0F172A] mb-1">ชื่อลูกค้า / บริษัท / สถานที่ *</label>
                    <input type="text" id="jobCustomerName" required placeholder="เช่น ไร่มณีทิพย์ / บ้านคุณนาย" class="w-full p-3.5 text-lg font-bold border-2 border-slate-400 rounded-xl focus:border-[#1E40AF]">
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <label class="block text-base font-bold text-[#0F172A] mb-1">ผู้ติดต่อ</label>
                        <input type="text" id="jobContactPerson" placeholder="เช่น คุณอาอำพร" class="w-full p-3.5 text-base font-bold border-2 border-slate-400 rounded-xl">
                    </div>
                    <div>
                        <label class="block text-base font-bold text-[#0F172A] mb-1">เบอร์โทรศัพท์</label>
                        <input type="tel" id="jobPhone" placeholder="เช่น 063-232-5789" class="w-full p-3.5 text-base font-bold border-2 border-slate-400 rounded-xl">
                    </div>
                </div>

                <!-- ที่อยู่ + ปุ่มดึงพิกัด GPS ปัจจุบัน -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center">
                        <label class="block text-base font-bold text-[#0F172A]">ที่อยู่ / จุดสังเกต</label>
                        <button type="button" onclick="fetchCurrentGPS()" id="btnFetchGps" class="px-3 py-1.5 bg-[#1E40AF] text-white font-bold text-sm rounded-xl flex items-center gap-1.5 shadow">
                            <i class="fa-solid fa-location-crosshairs text-amber-300"></i>
                            <span>ดึงพิกัด GPS ปัจจุบัน</span>
                        </button>
                    </div>
                    <textarea id="jobAddress" rows="2" placeholder="ระบุบ้านเลขที่ หมู่บ้าน หรือกดปุ่มดึงพิกัด GPS ด้านบน" class="w-full p-3 text-base font-semibold border-2 border-slate-400 rounded-xl"></textarea>
                    <input type="text" id="jobGpsUrl" placeholder="ลิงก์พิกัด Google Maps (สร้างอัตโนมัติเมื่อกดปุ่ม GPS)" class="w-full p-2.5 text-sm font-semibold bg-slate-100 border border-slate-300 rounded-xl text-blue-800">
                </div>

                <!-- ยี่ห้อ / ขนาด BTU แอร์ + ปุ่มลัดเลือกเร็ว -->
                <div class="space-y-2">
                    <label class="block text-base font-bold text-[#0F172A]">ยี่ห้อ / ขนาด BTU แอร์</label>
                    <div class="flex flex-wrap gap-1.5">
                        <button type="button" onclick="appendBtuShortcut('9,000 BTU')" class="px-3 py-1.5 bg-slate-200 hover:bg-blue-100 font-bold text-sm rounded-lg border border-slate-400">9,000 BTU</button>
                        <button type="button" onclick="appendBtuShortcut('12,000 BTU')" class="px-3 py-1.5 bg-slate-200 hover:bg-blue-100 font-bold text-sm rounded-lg border border-slate-400">12,000 BTU</button>
                        <button type="button" onclick="appendBtuShortcut('18,000 BTU')" class="px-3 py-1.5 bg-slate-200 hover:bg-blue-100 font-bold text-sm rounded-lg border border-slate-400">18,000 BTU</button>
                        <button type="button" onclick="appendBtuShortcut('24,000 BTU')" class="px-3 py-1.5 bg-slate-200 hover:bg-blue-100 font-bold text-sm rounded-lg border border-slate-400">24,000 BTU</button>
                    </div>
                    <input type="text" id="jobAcModel" placeholder="เช่น Midea 12,000 BTU / Daikin Inverter" class="w-full p-3.5 text-base font-bold border-2 border-slate-400 rounded-xl">
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <label class="block text-base font-bold text-[#0F172A] mb-1">ประเภทงาน *</label>
                        <select id="jobType" class="w-full p-3.5 text-base font-bold bg-white border-2 border-slate-400 rounded-xl">
                            <option value="ล้างแอร์">🚿 ล้างแอร์</option>
                            <option value="ซ่อม">🔧 ซ่อม</option>
                            <option value="ติดตั้ง">❄️ ติดตั้ง</option>
                            <option value="เติมน้ำยา">🧪 เติมน้ำยา</option>
                            <option value="ย้ายแอร์">🚚 ย้ายแอร์</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-base font-bold text-[#0F172A] mb-1">ค่าบริการรวม (บาท)</label>
                        <input type="number" id="jobPrice" placeholder="0" min="0" class="w-full p-3.5 text-lg font-extrabold text-[#15803D] border-2 border-slate-400 rounded-xl">
                    </div>
                </div>

                <div>
                    <label class="block text-base font-bold text-[#0F172A] mb-1">บันทึกอาการ / อะไหล่ที่เปลี่ยน</label>
                    <textarea id="jobDetails" rows="2" placeholder="เช่น ติดตั้งแอร์ Midea 12,000 BTU + ขาแขวนแอร์ 45cm" class="w-full p-3 text-base font-semibold border-2 border-slate-400 rounded-xl"></textarea>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <label class="block text-base font-bold text-[#0F172A] mb-1">วันที่ดำเนินการ</label>
                        <input type="date" id="jobDate" onchange="previewNextReminderDate()" class="w-full p-3.5 text-base font-bold border-2 border-slate-400 rounded-xl">
                    </div>
                    <div>
                        <label class="block text-base font-bold text-[#0F172A] mb-1">สถานะงาน</label>
                        <select id="jobStatus" class="w-full p-3.5 text-base font-bold bg-white border-2 border-slate-400 rounded-xl">
                            <option value="รอดำเนินการ">⏳ รอดำเนินการ</option>
                            <option value="กำลังทำ">🛠️ กำลังทำ</option>
                            <option value="เสร็จสิ้น">✅ เสร็จสิ้น</option>
                        </select>
                    </div>
                </div>

                <!-- รอบนัดล้างถัดไป -->
                <div class="bg-amber-50 p-3.5 rounded-2xl border-2 border-amber-400">
                    <label class="block text-base font-bold text-amber-950 mb-1">รอบนัดล้างแอร์ถัดไป:</label>
                    <select id="jobReminderMonths" onchange="previewNextReminderDate()" class="w-full p-3.5 text-base font-bold bg-white border-2 border-amber-500 rounded-xl">
                        <option value="0">ไม่มี (ไม่ตั้งเตือน)</option>
                        <option value="3">3 เดือน (ร้านค้า / ฝุ่นเยอะ)</option>
                        <option value="4">4 เดือน</option>
                        <option value="6" selected>6 เดือน (มาตรฐานบ้านพัก)</option>
                        <option value="12">12 เดือน (1 ปี)</option>
                    </select>
                    <p id="nextReminderPreviewText" class="text-sm font-bold text-[#EA580C] mt-1.5"></p>
                </div>

                <div class="grid grid-cols-2 gap-3 pt-2">
                    <button type="button" onclick="closeJobModal()" class="btn-outdoor bg-slate-200 text-[#0F172A] font-bold text-lg rounded-2xl border-2 border-slate-400">
                        ยกเลิก
                    </button>
                    <button type="submit" class="btn-outdoor bg-[#EA580C] text-white font-heading font-bold text-lg rounded-2xl shadow-lg border-2 border-orange-950">
                        บันทึกข้อมูล
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- ========================================================== -->
    <!-- MODAL 2: แสดงรูปบิล / ใบเสนอราคา PNG ความละเอียดสูง         -->
    <!-- ========================================================== -->
    <div id="billPngModal" class="fixed inset-0 bg-black/85 z-50 hidden overflow-y-auto p-3 sm:p-4">
        <div class="bg-white max-w-lg mx-auto rounded-3xl shadow-2xl border-2 border-slate-400 overflow-hidden my-2">
            <div class="bg-[#0F172A] text-white px-5 py-4 flex justify-between items-center border-b-4 border-[#EA580C]">
                <h2 class="font-heading font-bold text-xl">รูปบิล / ใบเสนอราคา</h2>
                <button onclick="closeBillPngModal()" class="text-white hover:text-amber-300 text-2xl p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="p-4 space-y-4 text-center">
                <p class="text-sm font-bold text-[#15803D] bg-green-50 border border-green-300 py-2.5 px-3 rounded-xl">
                    ✅ สร้างรูปบิลสำเร็จ! กดปุ่มดาวน์โหลดด้านล่าง หรือกดค้างที่รูปเพื่อส่งเข้า LINE
                </p>

                <div class="border-2 border-slate-400 rounded-2xl overflow-hidden shadow-lg bg-slate-100">
                    <img id="billPngPreviewImg" class="w-full h-auto block mx-auto" alt="ใบเสร็จรับเงิน/ใบเสนอราคา">
                </div>

                <div class="grid grid-cols-1 gap-3">
                    <a id="downloadPngLink" download="บิลส่งงาน_ช่างอัฐ.png" class="btn-outdoor w-full bg-[#1E40AF] hover:bg-blue-900 text-white font-heading font-bold text-lg py-3.5 px-4 rounded-2xl shadow-lg border-2 border-blue-950 flex items-center justify-center gap-2.5">
                        <i class="fa-solid fa-download text-xl text-amber-300"></i>
                        <span>บันทึกรูปภาพ PNG ลงเครื่อง</span>
                    </a>
                    <button onclick="closeBillPngModal()" class="btn-outdoor w-full bg-slate-200 text-[#0F172A] font-bold text-base rounded-2xl border-2 border-slate-400">
                        ปิดหน้าต่างนี้
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- ========================================================== -->
    <!-- MODAL 3: บันทึกรายรับ / รายจ่าย                           -->
    <!-- ========================================================== -->
    <div id="financeModal" class="fixed inset-0 bg-black/80 z-50 hidden overflow-y-auto p-3 sm:p-4">
        <div class="bg-white max-w-md mx-auto rounded-3xl shadow-2xl border-2 border-slate-400 overflow-hidden my-6">
            <div id="financeModalHeader" class="bg-[#15803D] text-white px-5 py-4 flex justify-between items-center">
                <h2 id="financeModalTitle" class="font-heading font-bold text-xl">+ บันทึกรายรับ</h2>
                <button onclick="closeFinanceModal()" class="text-white text-2xl p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            
            <form onsubmit="saveFinanceEntry(event)" class="p-5 space-y-4">
                <input type="hidden" id="financeEntryType" value="INCOME">

                <div>
                    <label class="block text-base font-bold text-[#0F172A] mb-2">เลือกหมวดหมู่ (กดจิ้มได้เลย):</label>
                    <div id="financeCategoryChips" class="grid grid-cols-2 gap-2"></div>
                    <input type="text" id="financeCategoryInput" required placeholder="หรือพิมพ์หมวดหมู่เอง" class="mt-2.5 w-full p-3 text-base font-bold border-2 border-slate-400 rounded-xl bg-slate-50">
                </div>

                <div>
                    <label class="block text-base font-bold text-[#0F172A] mb-1">จำนวนเงิน (บาท) *</label>
                    <input type="number" id="financeAmountInput" required min="1" step="any" placeholder="0" class="w-full p-4 text-3xl font-extrabold text-center border-2 border-slate-500 rounded-2xl focus:border-[#1E40AF]">
                </div>

                <div>
                    <label class="block text-base font-bold text-[#0F172A] mb-1">รายละเอียด / ชื่อลูกค้า / หมายเหตุ</label>
                    <input type="text" id="financeNoteInput" placeholder="เช่น ค่าล้างแอร์บ้านคุณนาย / ค่าน้ำมันรถ" class="w-full p-3.5 text-base font-semibold border-2 border-slate-400 rounded-xl">
                </div>

                <div>
                    <label class="block text-base font-bold text-[#0F172A] mb-1">วันที่</label>
                    <input type="date" id="financeDateInput" required class="w-full p-3 text-base font-bold border-2 border-slate-400 rounded-xl">
                </div>

                <div class="grid grid-cols-2 gap-3 pt-2">
                    <button type="button" onclick="closeFinanceModal()" class="btn-outdoor bg-slate-200 text-[#0F172A] font-bold text-lg rounded-2xl border-2 border-slate-400">
                        ยกเลิก
                    </button>
                    <button type="submit" id="financeSubmitBtn" class="btn-outdoor bg-[#15803D] text-white font-heading font-bold text-lg rounded-2xl shadow-lg">
                        บันทึกรายการ
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- ========================================================== -->
    <!-- MODAL 4: ตั้งค่าร้าน & สำรอง/กู้คืน/รีเซ็ตข้อมูล            -->
    <!-- ========================================================== -->
    <div id="settingsModal" class="fixed inset-0 bg-black/80 z-50 hidden overflow-y-auto p-3 sm:p-4">
        <div class="bg-white max-w-md mx-auto rounded-3xl shadow-2xl border-2 border-slate-400 overflow-hidden my-4">
            <div class="bg-[#0F172A] text-white px-5 py-4 flex justify-between items-center border-b-4 border-[#EA580C]">
                <h2 class="font-heading font-bold text-xl">ตั้งค่าร้าน & สำรองข้อมูล</h2>
                <button onclick="closeSettingsModal()" class="text-white text-2xl p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            
            <div class="p-5 space-y-5">
                <!-- ฟอร์มข้อมูลร้าน -->
                <form onsubmit="saveShopSettings(event)" class="space-y-3 border-b-2 border-slate-200 pb-5">
                    <h3 class="font-heading font-bold text-base text-[#1E40AF]">ข้อมูลหัวบิลและเลขที่บิล</h3>
                    <div>
                        <label class="block text-sm font-bold text-slate-800 mb-1">ชื่อร้าน / กิจการ</label>
                        <input type="text" id="settingShopName" required class="w-full p-3 text-base font-bold border-2 border-slate-400 rounded-xl">
                    </div>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label class="block text-sm font-bold text-slate-800 mb-1">ชื่อช่าง</label>
                            <input type="text" id="settingTechName" required class="w-full p-3 text-base font-bold border-2 border-slate-400 rounded-xl">
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-slate-800 mb-1">เบอร์โทรร้าน</label>
                            <input type="text" id="settingShopPhone" required class="w-full p-3 text-base font-bold border-2 border-slate-400 rounded-xl">
                        </div>
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-slate-800 mb-1">ที่อยู่ร้าน</label>
                        <textarea id="settingShopAddress" rows="2" class="w-full p-3 text-sm font-bold border-2 border-slate-400 rounded-xl"></textarea>
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-slate-800 mb-1">เลขที่บิลถัดไป</label>
                        <input type="number" id="settingNextBillNo" required class="w-full p-3 text-base font-bold border-2 border-slate-400 rounded-xl">
                    </div>
                    <button type="submit" class="btn-outdoor w-full bg-[#1E40AF] text-white font-heading font-bold text-base rounded-xl shadow">
                        บันทึกข้อมูลร้าน
                    </button>
                </form>

                <!-- สำรอง / กู้คืน / รีเซ็ตข้อมูล -->
                <div class="space-y-3">
                    <h3 class="font-heading font-bold text-base text-[#0F172A]">จัดการฐานข้อมูลในเครื่อง (LocalStorage)</h3>
                    <div class="grid grid-cols-2 gap-2.5">
                        <button onclick="exportBackupJSON()" class="btn-outdoor bg-[#0F172A] text-white font-bold text-sm px-3 rounded-xl flex items-center justify-center gap-2 shadow">
                            <i class="fa-solid fa-download text-amber-300"></i>
                            <span>Export ไฟล์ JSON</span>
                        </button>
                        <label class="btn-outdoor bg-white text-[#0F172A] border-2 border-[#0F172A] font-bold text-sm px-3 rounded-xl flex items-center justify-center gap-2 shadow cursor-pointer">
                            <i class="fa-solid fa-upload text-[#1E40AF]"></i>
                            <span>Import ไฟล์ JSON</span>
                            <input type="file" accept=".json" onchange="importBackupJSON(event)" class="hidden">
                        </label>
                    </div>

                    <button onclick="confirmResetDefaultData()" class="btn-outdoor w-full bg-red-50 hover:bg-red-100 text-red-700 border-2 border-red-600 font-bold text-base rounded-xl flex items-center justify-center gap-2">
                        <i class="fa-solid fa-rotate-left"></i>
                        <span>รีเซ็ตข้อมูลเริ่มต้น (โหลดข้อมูลร้านใหม่)</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- ========================================================== -->
    <!-- MODAL 5: ยืนยันการลบ / รีเซ็ต (แทน confirm())              -->
    <!-- ========================================================== -->
    <div id="confirmModal" class="fixed inset-0 bg-black/80 z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white max-w-sm w-full rounded-3xl p-6 text-center shadow-2xl border-2 border-red-500 space-y-4">
            <div class="w-16 h-16 bg-red-100 text-red-700 rounded-full flex items-center justify-center text-3xl mx-auto">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <h3 class="font-heading font-bold text-xl text-[#0F172A]" id="confirmModalTitle">ยืนยันการทำรายการ?</h3>
            <p class="text-base text-slate-700 font-semibold" id="confirmModalDesc">กรุณากดยืนยันเพื่อดำเนินการ</p>
            <div class="grid grid-cols-2 gap-3 pt-2">
                <button onclick="closeConfirmModal()" class="btn-outdoor bg-slate-200 text-[#0F172A] font-bold text-base rounded-2xl border-2 border-slate-400">ยกเลิก</button>
                <button id="confirmModalActionBtn" class="btn-outdoor bg-red-700 text-white font-bold text-base rounded-2xl shadow">ยืนยัน</button>
            </div>
        </div>
    </div>

    <!-- Hidden Canvas สำหรับวาดรูปใบเสร็จ/ใบเสนอราคา -->
    <canvas id="billCanvas" class="hidden"></canvas>

    <script>
        // =========================================================================
        // 1. ข้อมูลตั้งต้น (Seed Data) ของร้าน "ช่างงานเซอร์วิสระบบปรับอากาศและทำความเย็น"
        // =========================================================================
        const STORAGE_KEYS = {
            SHOP: 'chang_ngan_service_shop_v2',
            CUSTOMERS: 'chang_ngan_service_customers_v2',
            JOBS: 'chang_ngan_service_jobs_v2',
            FINANCE: 'chang_ngan_service_finance_v2'
        };

        const DEFAULT_SHOP_INFO = {
            shopName: 'ช่างงานเซอร์วิสระบบปรับอากาศและทำความเย็น',
            techName: 'ช่างอัฐ (ทัฐชวิน)',
            phone: '082-191-9619',
            address: '51/75 ถ. สมัครสรรพการ อ.แม่สอด จ.ตาก 63110',
            nextBillNo: 3460
        };

        // รายชื่อลูกค้าทั้ง 13 รายจากฐานข้อมูลร้าน
        const INITIAL_CUSTOMERS = [
            { id: 'c1', name: 'ไร่มณีทิพย์', contact: 'คุณอาอำพร', phone: '063-232-5789', address: '489 หมู่ 2 ต.แม่ตาว อ.แม่สอด จ.ตาก 63110' },
            { id: 'c2', name: 'บริษัท วิน เลท วาดิ จำกัด', contact: 'คุณ Seksan', phone: '096-218-5017', address: '806 หมู่ที่ 2 ต.แม่ตาว อ.แม่สอด จ.ตาก 63110' },
            { id: 'c3', name: 'พี่โอแม่ปะ', contact: 'พี่ติก', phone: '065-616-6414', address: 'คลินิกกายภาพบำบัดหน้าโรบินสัน อ.แม่สอด จ.ตาก' },
            { id: 'c4', name: 'หอพักทองมนตรี', contact: '', phone: '081-654-1982', address: 'หอพักทองมนตรี ห้องเบอร์ 9 อ.แม่สอด จ.ตาก 63110' },
            { id: 'c5', name: 'บ้านคุณนาย', contact: 'พี่ทัย', phone: '098-295-6995', address: 'แม่ปะหน้าพระธาตุ อ.แม่สอด จ.ตาก 63110' },
            { id: 'c6', name: 'บ้านทรงไทยแม่สอดวิลล่าพี่แอม', contact: 'พี่ติ๊ก', phone: '081-605-6656', address: 'แม่สอดวิลล่า ซ.11 อ.แม่สอด จ.ตาก 63110' },
            { id: 'c7', name: 'ลูกค้าวังตะเคียน', contact: 'พี่ติ๊ก', phone: '081-857-5615', address: 'วังตะเคียนหลังก๋วยเตี๋ยวชามโต อ.แม่สอด จ.ตาก 63110' },
            { id: 'c8', name: "Bite Me Bakery & Cafe'", contact: '', phone: '098-749-3560', address: 'บ้านใต้ อ.แม่สอด จ.ตาก 63110' },
            { id: 'c9', name: 'บริษัท ดิงด่อง เทรดดิ้ง เฟรช ฟุ๊ด จำกัด', contact: 'คุณ Saint', phone: '', address: 'ต.แม่ปะ อ.แม่สอด จ.ตาก' },
            { id: 'c10', name: 'บริษัท จินหยวน มาซาลา จำกัด', contact: 'คุณทู', phone: '', address: '272/46 ถ.ศรีพานิช ต.แม่สอด จ.ตาก' },
            { id: 'c11', name: 'ร้านทุกอย่าง 20 บ้านเหนือ', contact: 'พี่ติ๊ก', phone: '', address: 'ตรงข้ามร้านทองใบ อ.แม่สอด จ.ตาก' },
            { id: 'c12', name: 'บริษัท บี.เค. ออโต้ โมบิล จำกัด', contact: 'คุณแอม ซูซูกิ', phone: '088-293-2659', address: '111 ถ.สายเอเชีย อ.แม่สอด จ.ตาก 63110' },
            { id: 'c13', name: 'ร้านบาสเน็ต', contact: '', phone: '', address: 'ร่วมแรง อ.แม่สอด จ.ตาก' }
        ];

        function getTodayStr() {
            const d = new Date();
            const yyyy = d.getFullYear();
            const mm = String(d.getMonth() + 1).padStart(2, '0');
            const dd = String(d.getDate()).padStart(2, '0');
            return `${yyyy}-${mm}-${dd}`;
        }

        function getOffsetDateStr(daysOffset = 0) {
            const d = new Date();
            d.setDate(d.getDate() + daysOffset);
            const yyyy = d.getFullYear();
            const mm = String(d.getMonth() + 1).padStart(2, '0');
            const dd = String(d.getDate()).padStart(2, '0');
            return `${yyyy}-${mm}-${dd}`;
        }

        function addMonthsToDateStr(dateStr, months) {
            if (!dateStr || !months || months <= 0) return '';
            const parts = dateStr.split('-');
            const d = new Date(parseInt(parts[0]), parseInt(parts[1]) - 1, parseInt(parts[2]));
            d.setMonth(d.getMonth() + parseInt(months));
            const yyyy = d.getFullYear();
            const mm = String(d.getMonth() + 1).padStart(2, '0');
            const dd = String(d.getDate()).padStart(2, '0');
            return `${yyyy}-${mm}-${dd}`;
        }

        // ประวัติงานตั้งต้น (รวมงานติดตั้งแอร์ Midea ไร่มณีทิพย์ 25/11/2569 และตัวอย่างงานเพื่อให้เห็นการทำงานครบทุกสถานะ)
        const INITIAL_JOBS = [
            {
                id: 'j1',
                customerName: 'ไร่มณีทิพย์',
                contactPerson: 'คุณอาอำพร',
                phone: '063-232-5789',
                address: '489 หมู่ 2 ต.แม่ตาว อ.แม่สอด จ.ตาก 63110',
                gpsUrl: '',
                acModel: 'Midea 12,000 BTU',
                jobType: 'ติดตั้ง',
                details: 'ติดตั้งแอร์ Midea 12,000 BTU + ขาแขวนแอร์ 45cm เรียบร้อย ทดสอบแรงดันน้ำยาและระบบระบายน้ำปกติ',
                price: 2350,
                date: '2026-11-25', // 25/11/2569
                status: 'เสร็จสิ้น',
                reminderMonths: 6,
                nextWashDate: '2027-05-25'
            },
            {
                id: 'j2',
                customerName: 'บริษัท บี.เค. ออโต้ โมบิล จำกัด',
                contactPerson: 'คุณแอม ซูซูกิ',
                phone: '088-293-2659',
                address: '111 ถ.สายเอเชีย อ.แม่สอด จ.ตาก 63110',
                gpsUrl: '',
                acModel: 'แอร์แขวน/สี่ทิศทาง 36,000 BTU',
                jobType: 'ล้างแอร์',
                details: 'ล้างแอร์โซนโชว์รูมและห้องรับรองลูกค้า รอบ 6 เดือน',
                price: 2000,
                date: getOffsetDateStr(-176),
                status: 'เสร็จสิ้น',
                reminderMonths: 6,
                nextWashDate: getOffsetDateStr(4) // ใกล้ถึงรอบล้างอีก 4 วัน (ขึ้น Badge แจ้งเตือน)
            },
            {
                id: 'j3',
                customerName: 'พี่โอแม่ปะ',
                contactPerson: 'พี่ติก',
                phone: '065-616-6414',
                address: 'คลินิกกายภาพบำบัดหน้าโรบินสัน อ.แม่สอด จ.ตาก',
                gpsUrl: '',
                acModel: 'Daikin 18,000 BTU',
                jobType: 'ล้างแอร์',
                details: 'นัดล้างแอร์คลินิก 2 เครื่อง + เช็กน้ำยา R32',
                price: 1000,
                date: getTodayStr(),
                status: 'รอดำเนินการ',
                reminderMonths: 6,
                nextWashDate: addMonthsToDateStr(getTodayStr(), 6)
            }
        ];

        const INITIAL_FINANCE = [
            { id: 'f1', type: 'INCOME', category: 'ค่าติดตั้ง', amount: 2350, note: 'ติดตั้งแอร์ Midea 12,000 BTU + ขาแขวน - ไร่มณีทิพย์', date: getTodayStr() },
            { id: 'f2', type: 'EXPENSE', category: 'ค่าอะไหล่/น้ำยาแอร์', amount: 350, note: 'ซื้อขาแขวนแอร์ 45cm + พุกเหล็ก', date: getTodayStr() },
            { id: 'f3', type: 'EXPENSE', category: 'ค่าน้ำมันรถ', amount: 200, note: 'เติมน้ำมันรถวิ่งงานแม่ตาว-แม่สอด', date: getTodayStr() }
        ];

        // อาการเสียยอดนิยม 6 ปุ่มใหญ่
        const SYMPTOM_GUIDES = [
            {
                id: 'not_cold',
                title: '❄️ แอร์ไม่เย็น',
                icon: 'fa-temperature-arrow-up',
                btnClass: 'bg-blue-50 border-[#1E40AF] text-[#0F172A]',
                checks: [
                    'เช็กคอยล์ร้อนด้านนอก: พัดลมระบายความร้อนและคอมเพรสเซอร์ทำงานไหม',
                    'วัดกระแสไฟ (Clamp Meter) เทียบกับค่าแอมป์มาตรฐานข้างเครื่อง',
                    'จับท่อทองแดง: หากท่อเล็กเป็นน้ำแข็ง แสดงว่าน้ำยาขาดหรือรั่ว',
                    'เช็กแคปรัน (Capacitor) คอมเพรสเซอร์ว่าบวมหรือค่าไมโครตกไหม'
                ],
                relatedServices: [
                    { name: 'เติมน้ำยา R32/R410a', price: 800 },
                    { name: 'แคปรัน/แมกเนติก', price: 650 }
                ]
            },
            {
                id: 'water_leak',
                title: '💧 น้ำหยด',
                icon: 'fa-droplet',
                btnClass: 'bg-cyan-50 border-cyan-700 text-[#0F172A]',
                checks: [
                    'ท่อน้ำทิ้งอุดตันจากเมือกฝุ่น (พบบ่อยสุด) ให้ใช้เครื่องดูด/เป่าไล่ท่อ',
                    'เช็กถาดน้ำทิ้งด้านหลังคอยล์เย็นว่าตันหรือร้าวหรือไม่',
                    'ฟิลเตอร์และคอยล์เย็นสกปรกจัด จนน้ำแข็งเกาะแล้วละลายหยดล้นถาด',
                    'ฉนวนหุ้มท่อแอร์ฉีกขาด ทำให้น้ำกลั่นตัวหยดตามแนวท่อ'
                ],
                relatedServices: [
                    { name: 'ล้างแอร์ติดผนัง', price: 500 },
                    { name: 'ล้างแอร์แขวน/สี่ทิศทาง', price: 1000 }
                ]
            },
            {
                id: 'noisy',
                title: '🔊 มีเสียงดัง',
                icon: 'fa-volume-high',
                btnClass: 'bg-amber-50 border-amber-600 text-[#0F172A]',
                checks: [
                    'ฝั่งคอยล์เย็น: เช็กบูชยางมอเตอร์พัดลมสึก หรือใบพัดกรงกระรอกสกปรกเสียศูนย์',
                    'หน้ากากแอร์ปิดไม่สนิท หรือน็อตยึดโครงพลาสติกหลวมสั่น',
                    'ฝั่งคอยล์ร้อน: ใบพัดลมตีโครง, ขาแขวนน็อตคลาย หรือลูกยางรองคอมฯ เสื่อม'
                ],
                relatedServices: [
                    { name: 'ขาแขวนแอร์ 45cm', price: 350 },
                    { name: 'ล้างแอร์ติดผนัง', price: 500 }
                ]
            },
            {
                id: 'outdoor_dead',
                title: '🔌 คอยล์ร้อนไม่ทำงาน',
                icon: 'fa-plug-circle-xmark',
                btnClass: 'bg-red-50 border-red-700 text-[#0F172A]',
                checks: [
                    'เช็กไฟ 220V ที่จุดต่อสายคอยล์ร้อนว่าคอยล์เย็นจ่ายไฟออกมาไหม',
                    'รุ่นธรรมดา: เช็กแมกเนติกคอนแทคเตอร์ หน้าสัมผัสไหม้หรือคอยล์ขาด',
                    'เช็กสายไฟคอนโทรลระหว่างคอยล์เย็น-ร้อน (หนูกัด/สายขาดใน)',
                    'รุ่น Inverter: เช็กฟิวส์และแผงบอร์ดคอยล์ร้อน'
                ],
                relatedServices: [
                    { name: 'แคปรัน/แมกเนติก', price: 650 }
                ]
            },
            {
                id: 'error_blink',
                title: '🚨 ไฟกะพริบ/ขึ้นโค้ด',
                icon: 'fa-triangle-exclamation',
                btnClass: 'bg-purple-50 border-purple-700 text-[#0F172A]',
                checks: [
                    'นับจังหวะไฟกะพริบที่หน้าเครื่อง หรือกดปุ่ม Cancel ค้างที่รีโมทเพื่ออ่านโค้ด',
                    'เช็กเซนเซอร์น้ำแข็ง (Coil Sensor) และเซนเซอร์อุณหภูมิห้อง (Room Sensor)',
                    'เช็กมอเตอร์พัดลมคอยล์เย็น (รอบพัดลมไม่ส่งสัญญาณกลับบอร์ด)',
                    'ลองสับเบรกเกอร์ลง 3 นาทีแล้วเปิดใหม่เพื่อรีเซ็ตระบบ Inverter'
                ],
                relatedServices: [
                    { name: 'ค่าตรวจเช็ก/ซ่อมอาการไฟกะพริบ', price: 500 }
                ]
            },
            {
                id: 'bad_smell',
                title: '🤢 มีกลิ่นอับ',
                icon: 'fa-wind',
                btnClass: 'bg-emerald-50 border-[#15803D] text-[#0F172A]',
                checks: [
                    'คราบเมือกและเชื้อราสะสมในถาดน้ำทิ้งและใบพัดกรงกระรอก',
                    'ปลายท่อน้ำทิ้งต่อตรงเข้าบ่อพัก/ท่อระบายน้ำเสียโดยไม่มีท่อดักกลิ่น (P-Trap)',
                    'แนะนำลูกค้าเปิดโหมดพัดลม (Fan) ไล่ความชื้น 15 นาทีก่อนปิดแอร์'
                ],
                relatedServices: [
                    { name: 'ล้างแอร์ติดผนัง', price: 500 },
                    { name: 'ล้างแอร์แขวน/สี่ทิศทาง', price: 1000 }
                ]
            }
        ];

        // รายการมาตรฐานคลิกเดียวตามโจทย์
        const PRESET_SERVICES = [
            { name: 'ล้างแอร์ติดผนัง', price: 500 },
            { name: 'ล้างแอร์แขวน/สี่ทิศทาง', price: 1000 },
            { name: 'เติมน้ำยา R32/R410a', price: 800 },
            { name: 'ค่าแรงติดตั้งแอร์ 12,000 BTU', price: 2000 },
            { name: 'ขาแขวนแอร์ 45cm', price: 350 },
            { name: 'แคปรัน/แมกเนติก', price: 650 },
            { name: 'เดินท่อน้ำยาเพิ่ม (เมตร)', price: 450 }
        ];

        const INCOME_CATEGORIES = ['ค่าล้างแอร์', 'ค่าซ่อม', 'ค่าติดตั้ง', 'ขายอะไหล่'];
        const EXPENSE_CATEGORIES = ['ค่าน้ำมันรถ', 'ค่าอะไหล่/น้ำยาแอร์', 'ค่าจ้างลูกน้อง', 'ค่าอุปกรณ์/สิ้นเปลือง'];

        // =========================================================================
        // 2. State Management & LocalStorage
        // =========================================================================
        let state = {
            shop: {},
            customers: [],
            jobs: [],
            finance: [],
            currentJobFilter: 'ALL',
            financeMode: 'DAILY',
            quoteItems: [
                { name: 'ล้างแอร์ติดผนัง', price: 500, qty: 1 }
            ]
        };

        function loadAllData() {
            try {
                const sShop = localStorage.getItem(STORAGE_KEYS.SHOP);
                state.shop = sShop ? JSON.parse(sShop) : { ...DEFAULT_SHOP_INFO };

                const sCust = localStorage.getItem(STORAGE_KEYS.CUSTOMERS);
                state.customers = sCust ? JSON.parse(sCust) : [...INITIAL_CUSTOMERS];

                const sJobs = localStorage.getItem(STORAGE_KEYS.JOBS);
                state.jobs = sJobs ? JSON.parse(sJobs) : [...INITIAL_JOBS];

                const sFin = localStorage.getItem(STORAGE_KEYS.FINANCE);
                state.finance = sFin ? JSON.parse(sFin) : [...INITIAL_FINANCE];

                saveAllData();
            } catch (e) {
                console.error('LocalStorage load error:', e);
            }
        }

        function saveAllData() {
            localStorage.setItem(STORAGE_KEYS.SHOP, JSON.stringify(state.shop));
            localStorage.setItem(STORAGE_KEYS.CUSTOMERS, JSON.stringify(state.customers));
            localStorage.setItem(STORAGE_KEYS.JOBS, JSON.stringify(state.jobs));
            localStorage.setItem(STORAGE_KEYS.FINANCE, JSON.stringify(state.finance));
        }

        function showToast(msg, type = 'success') {
            const banner = document.getElementById('toastBanner');
            const icon = document.getElementById('toastIcon');
            document.getElementById('toastMessage').textContent = msg;
            icon.className = type === 'error' 
                ? 'fa-solid fa-circle-exclamation text-red-400 text-2xl shrink-0' 
                : 'fa-solid fa-circle-check text-green-400 text-2xl shrink-0';
            banner.classList.remove('hidden');
            clearTimeout(window.toastTimer);
            window.toastTimer = setTimeout(() => banner.classList.add('hidden'), 3000);
        }

        function formatCurrency(num) {
            return Number(num || 0).toLocaleString('th-TH');
        }

        function formatThaiDate(dateStr) {
            if (!dateStr) return '-';
            const parts = dateStr.split('-');
            if (parts.length !== 3) return dateStr;
            const d = parseInt(parts[2], 10);
            const m = parseInt(parts[1], 10);
            const y = parseInt(parts[0], 10) + 543;
            return `${String(d).padStart(2, '0')}/${String(m).padStart(2, '0')}/${y}`;
        }

        // =========================================================================
        // 3. Navigation (Bottom Tab Bar)
        // =========================================================================
        function switchTab(tabName) {
            ['jobs', 'quote', 'finance'].forEach(t => {
                document.getElementById(`tab-${t}`).classList.add('hidden');
                const btn = document.getElementById(`nav-${t}`);
                btn.className = 'nav-btn flex flex-col items-center justify-center gap-1 bg-white text-[#0F172A] hover:bg-slate-100 font-heading font-bold border-r border-slate-300';
            });

            document.getElementById(`tab-${tabName}`).classList.remove('hidden');
            const activeBtn = document.getElementById(`nav-${tabName}`);
            activeBtn.className = 'nav-btn flex flex-col items-center justify-center gap-1 bg-[#0F172A] text-amber-300 font-heading font-bold border-r border-slate-700';

            if (tabName === 'jobs') renderJobs();
            if (tabName === 'quote') {
                populateCustomerDropdowns();
                document.getElementById('displayBillNumber').textContent = state.shop.nextBillNo || 3460;
                renderQuoteItems();
            }
            if (tabName === 'finance') renderFinance();
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // =========================================================================
        // 4. TAB 1: งาน & ลูกค้า (Job Log & Customer History)
        // =========================================================================
        function isWashDue(nextWashDate) {
            if (!nextWashDate) return false;
            const today = new Date();
            today.setHours(0, 0, 0, 0);
            const parts = nextWashDate.split('-');
            const target = new Date(parseInt(parts[0]), parseInt(parts[1]) - 1, parseInt(parts[2]));
            const diffDays = Math.ceil((target - today) / (1000 * 60 * 60 * 24));
            return diffDays <= 14; // แจ้งเตือนเมื่อใกล้ถึงรอบใน 14 วัน หรือเลยกำหนดแล้ว
        }

        function getDueBadgeHTML(nextWashDate) {
            if (!nextWashDate) return '';
            const today = new Date();
            today.setHours(0, 0, 0, 0);
            const parts = nextWashDate.split('-');
            const target = new Date(parseInt(parts[0]), parseInt(parts[1]) - 1, parseInt(parts[2]));
            const diffDays = Math.ceil((target - today) / (1000 * 60 * 60 * 24));

            if (diffDays < 0) {
                return `<span class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-xl text-sm font-extrabold bg-red-700 text-white shadow">
                    <i class="fa-solid fa-bell"></i> เลยกำหนดล้าง ${Math.abs(diffDays)} วัน (${formatThaiDate(nextWashDate)})
                </span>`;
            } else if (diffDays <= 14) {
                return `<span class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-xl text-sm font-extrabold bg-[#EA580C] text-white shadow">
                    <i class="fa-solid fa-bell"></i> ใกล้ถึงรอบล้างอีก ${diffDays} วัน (${formatThaiDate(nextWashDate)})
                </span>`;
            } else {
                return `<span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-xl text-xs font-bold bg-blue-100 text-[#1E40AF] border border-blue-300">
                    <i class="fa-regular fa-calendar-check"></i> นัดล้างรอบหน้า: ${formatThaiDate(nextWashDate)}
                </span>`;
            }
        }

        function setJobFilter(filter) {
            state.currentJobFilter = filter;
            document.querySelectorAll('.filter-btn').forEach(btn => {
                if (btn.dataset.filter === filter) {
                    btn.className = 'filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-[#0F172A] bg-[#0F172A] text-white shadow';
                } else if (btn.dataset.filter === 'DUE') {
                    btn.className = 'filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-red-600 bg-red-50 text-red-800';
                } else {
                    btn.className = 'filter-btn btn-outdoor shrink-0 px-4 py-2.5 rounded-xl font-bold text-base border-2 border-slate-400 bg-white text-[#0F172A]';
                }
            });
            renderJobs();
        }

        function clearJobSearch() {
            document.getElementById('jobSearchInput').value = '';
            document.getElementById('clearSearchBtn').classList.add('hidden');
            renderJobs();
        }

        function renderJobs() {
            const query = document.getElementById('jobSearchInput').value.trim().toLowerCase();
            const clearBtn = document.getElementById('clearSearchBtn');
            if (query) clearBtn.classList.remove('hidden');
            else clearBtn.classList.add('hidden');

            document.getElementById('count-ALL').textContent = state.jobs.length;
            document.getElementById('count-DUE').textContent = state.jobs.filter(j => isWashDue(j.nextWashDate)).length;
            document.getElementById('count-PENDING').textContent = state.jobs.filter(j => j.status === 'รอดำเนินการ').length;
            document.getElementById('count-DOING').textContent = state.jobs.filter(j => j.status === 'กำลังทำ').length;
            document.getElementById('count-DONE').textContent = state.jobs.filter(j => j.status === 'เสร็จสิ้น').length;

            let filteredJobs = state.jobs.filter(job => {
                const matchText = !query || 
                    (job.customerName && job.customerName.toLowerCase().includes(query)) ||
                    (job.contactPerson && job.contactPerson.toLowerCase().includes(query)) ||
                    (job.phone && job.phone.replace(/-/g, '').includes(query.replace(/-/g, ''))) ||
                    (job.details && job.details.toLowerCase().includes(query));

                if (!matchText) return false;
                if (state.currentJobFilter === 'ALL') return true;
                if (state.currentJobFilter === 'DUE') return isWashDue(job.nextWashDate);
                return job.status === state.currentJobFilter;
            });

            // ค้นหาลูกค้าในสมุดรายชื่อทั้ง 13 ราย (แสดงแม้ยังไม่มีประวัติงานใหม่)
            let matchingDirectoryCustomers = [];
            if (query || state.currentJobFilter === 'ALL') {
                matchingDirectoryCustomers = state.customers.filter(c => {
                    const matchC = !query || 
                        (c.name && c.name.toLowerCase().includes(query)) ||
                        (c.contact && c.contact.toLowerCase().includes(query)) ||
                        (c.phone && c.phone.replace(/-/g, '').includes(query.replace(/-/g, '')));
                    const alreadyHasJobShown = filteredJobs.some(j => j.customerName === c.name);
                    return matchC && !alreadyHasJobShown;
                });
            }

            const container = document.getElementById('jobListContainer');
            let html = '';

            // การ์ดประวัติงานหลัก
            filteredJobs.forEach(job => {
                let statusBadge = 'bg-amber-100 text-amber-950 border-amber-500';
                if (job.status === 'กำลังทำ') statusBadge = 'bg-blue-100 text-blue-950 border-blue-600';
                if (job.status === 'เสร็จสิ้น') statusBadge = 'bg-green-100 text-green-950 border-green-600';

                const cleanPhone = job.phone ? job.phone.replace(/[^0-9+]/g, '') : '';
                const mapHref = job.gpsUrl && job.gpsUrl.startsWith('http')
                    ? job.gpsUrl
                    : `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent((job.customerName || '') + ' ' + (job.address || 'แม่สอด ตาก'))}`;

                html += `
                <article class="bg-white rounded-2xl shadow-md border-2 border-slate-400 overflow-hidden">
                    <div class="p-4 bg-slate-100 border-b-2 border-slate-300 flex justify-between items-start gap-2">
                        <div>
                            <div class="flex flex-wrap items-center gap-1.5 mb-1.5">
                                <span class="px-2.5 py-0.5 rounded-lg text-xs font-extrabold bg-[#0F172A] text-white">${job.jobType}</span>
                                <span class="px-2.5 py-0.5 rounded-lg text-xs font-extrabold border-2 ${statusBadge}">${job.status}</span>
                                <span class="text-xs font-bold text-slate-600">${formatThaiDate(job.date)}</span>
                            </div>
                            <h3 class="font-heading font-bold text-lg sm:text-xl text-[#0F172A] leading-snug">${job.customerName}</h3>
                            <p class="text-sm font-bold text-slate-700 mt-0.5">
                                ติดต่อ: ${job.contactPerson || '-'} ${job.phone ? `• <span class="text-[#1E40AF]">${job.phone}</span>` : ''}
                            </p>
                        </div>
                        <div class="text-right shrink-0">
                            <span class="font-heading font-extrabold text-xl text-[#15803D] block">${formatCurrency(job.price)} ฿</span>
                            <button onclick="confirmDeleteJob('${job.id}')" class="mt-1 text-xs font-bold text-red-700 bg-red-50 border border-red-300 px-2 py-1 rounded-lg">
                                <i class="fa-solid fa-trash"></i> ลบ
                            </button>
                        </div>
                    </div>

                    <div class="p-4 space-y-3">
                        ${job.acModel ? `<p class="text-base font-bold text-[#0F172A]"><i class="fa-solid fa-snowflake text-[#1E40AF] mr-1.5"></i>รุ่นแอร์: ${job.acModel}</p>` : ''}
                        ${job.details ? `<p class="text-base font-semibold text-slate-800 bg-slate-50 p-3 rounded-xl border border-slate-300">${job.details}</p>` : ''}
                        ${job.address ? `<p class="text-sm font-semibold text-slate-700"><i class="fa-solid fa-location-dot text-red-600 mr-1.5"></i>${job.address}</p>` : ''}
                        
                        ${job.nextWashDate ? `<div>${getDueBadgeHTML(job.nextWashDate)}</div>` : ''}

                        <!-- ปุ่มใหญ่ 4 ปุ่มหน้างาน: โทรออก / นำทาง / แก้ไข / ออกบิลงานนี้ -->
                        <div class="grid grid-cols-2 gap-2.5 pt-1">
                            ${cleanPhone ? `
                            <a href="tel:${cleanPhone}" class="btn-outdoor bg-[#15803D] hover:bg-green-800 text-white font-bold text-base rounded-xl flex items-center justify-center gap-2 shadow border-2 border-green-950">
                                <i class="fa-solid fa-phone"></i>
                                <span>โทรออก</span>
                            </a>` : `
                            <button disabled class="btn-outdoor bg-slate-200 text-slate-500 font-bold text-base rounded-xl flex items-center justify-center gap-2 border-2 border-slate-300">
                                <i class="fa-solid fa-phone-slash"></i>
                                <span>ไม่มีเบอร์โทร</span>
                            </button>`}

                            <a href="${mapHref}" target="_blank" rel="noopener noreferrer" class="btn-outdoor bg-[#1E40AF] hover:bg-blue-900 text-white font-bold text-base rounded-xl flex items-center justify-center gap-2 shadow border-2 border-blue-950">
                                <i class="fa-solid fa-map-location-dot"></i>
                                <span>นำทาง</span>
                            </a>

                            <button onclick="editJob('${job.id}')" class="btn-outdoor bg-slate-800 hover:bg-slate-900 text-white font-bold text-base rounded-xl flex items-center justify-center gap-2 shadow border-2 border-slate-950">
                                <i class="fa-solid fa-pen-to-square text-amber-300"></i>
                                <span>แก้ไข/ดูประวัติ</span>
                            </button>

                            <button onclick="sendJobToQuote('${job.id}')" class="btn-outdoor bg-[#EA580C] hover:bg-orange-700 text-white font-bold text-base rounded-xl flex items-center justify-center gap-2 shadow border-2 border-orange-950">
                                <i class="fa-solid fa-file-invoice-dollar"></i>
                                <span>ออกบิลงานนี้</span>
                            </button>
                        </div>
                    </div>
                </article>`;
            });

            // แสดงรายชื่อลูกค้าประจำในสมุดฐานข้อมูลร้าน (ถ้ายังไม่ได้เปิดงานในรอบนี้)
            if (matchingDirectoryCustomers.length > 0) {
                html += `<div class="pt-2 space-y-2.5">
                    <h3 class="font-heading font-bold text-base text-[#0F172A] px-1 flex items-center gap-2">
                        <i class="fa-solid fa-address-book text-[#1E40AF]"></i>
                        <span>สมุดรายชื่อลูกค้าประจำ (${matchingDirectoryCustomers.length} ราย)</span>
                    </h3>`;
                
                matchingDirectoryCustomers.forEach(c => {
                    const cleanPhone = c.phone ? c.phone.replace(/[^0-9+]/g, '') : '';
                    const mapHref = `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent((c.name || '') + ' ' + (c.address || 'แม่สอด ตาก'))}`;
                    html += `
                    <div class="bg-white p-4 rounded-2xl border-2 border-slate-300 shadow-sm space-y-2.5">
                        <div>
                            <h4 class="font-heading font-bold text-lg text-[#0F172A]">${c.name}</h4>
                            <p class="text-sm font-bold text-slate-700">
                                ติดต่อ: ${c.contact || '-'} ${c.phone ? `• <span class="text-[#1E40AF]">${c.phone}</span>` : ''}
                            </p>
                            <p class="text-sm text-slate-600 mt-0.5"><i class="fa-solid fa-location-dot text-red-600 mr-1"></i>${c.address || '-'}</p>
                        </div>
                        <div class="grid grid-cols-3 gap-2">
                            ${cleanPhone ? `
                            <a href="tel:${cleanPhone}" class="btn-outdoor bg-[#15803D] text-white font-bold text-sm rounded-xl flex items-center justify-center gap-1.5 shadow">
                                <i class="fa-solid fa-phone"></i> โทร
                            </a>` : `
                            <button disabled class="btn-outdoor bg-slate-200 text-slate-400 font-bold text-sm rounded-xl">ไม่มีเบอร์</button>`}
                            <a href="${mapHref}" target="_blank" rel="noopener noreferrer" class="btn-outdoor bg-[#1E40AF] text-white font-bold text-sm rounded-xl flex items-center justify-center gap-1.5 shadow">
                                <i class="fa-solid fa-map-location-dot"></i> นำทาง
                            </a>
                            <button onclick="openJobModalWithCustomer('${c.id}')" class="btn-outdoor bg-[#EA580C] text-white font-bold text-sm rounded-xl flex items-center justify-center gap-1 shadow">
                                + เปิดงาน
                            </button>
                        </div>
                    </div>`;
                });
                html += `</div>`;
            }

            if (!html) {
                html = `<div class="bg-white p-8 rounded-2xl border-2 border-dashed border-slate-400 text-center space-y-2">
                    <i class="fa-solid fa-folder-open text-4xl text-slate-400"></i>
                    <p class="font-heading font-bold text-lg text-slate-700">ไม่พบข้อมูลลูกค้าหรือรายการงานที่ค้นหา</p>
                </div>`;
            }

            container.innerHTML = html;
        }

        function populateCustomerDropdowns() {
            const jobSelect = document.getElementById('existingCustomerDropdown');
            const quoteSelect = document.getElementById('quoteCustomerSelect');
            let optionsHTML = '<option value="">-- เลือกรายชื่อลูกค้าเดิม (Auto-fill) --</option>';
            state.customers.forEach(c => {
                optionsHTML += `<option value="${c.id}">${c.name}${c.contact ? ` (${c.contact})` : ''}${c.phone ? ` - ${c.phone}` : ''}</option>`;
            });
            if (jobSelect) jobSelect.innerHTML = optionsHTML;
            if (quoteSelect) quoteSelect.innerHTML = optionsHTML;
        }

        function openJobModal() {
            document.getElementById('jobForm').reset();
            document.getElementById('editJobId').value = '';
            document.getElementById('jobModalTitle').textContent = 'เพิ่มงาน / ลูกค้าใหม่';
            document.getElementById('jobDate').value = getTodayStr();
            document.getElementById('jobReminderMonths').value = '6';
            populateCustomerDropdowns();
            previewNextReminderDate();
            document.getElementById('jobModal').classList.remove('hidden');
        }

        function openJobModalWithCustomer(customerId) {
            openJobModal();
            document.getElementById('existingCustomerDropdown').value = customerId;
            autoFillCustomerToJobForm();
        }

        function closeJobModal() {
            document.getElementById('jobModal').classList.add('hidden');
        }

        function autoFillCustomerToJobForm() {
            const custId = document.getElementById('existingCustomerDropdown').value;
            if (!custId) return;
            const cust = state.customers.find(c => c.id === custId);
            if (cust) {
                document.getElementById('jobCustomerName').value = cust.name || '';
                document.getElementById('jobContactPerson').value = cust.contact || '';
                document.getElementById('jobPhone').value = cust.phone || '';
                document.getElementById('jobAddress').value = cust.address || '';
                showToast(`ดึงข้อมูล "${cust.name}" เรียบร้อย`);
            }
        }

        // ดึงพิกัด GPS ปัจจุบันด้วย Geolocation API
        function fetchCurrentGPS() {
            const btn = document.getElementById('btnFetchGps');
            if (!navigator.geolocation) {
                showToast('เบราว์เซอร์นี้ไม่รองรับการดึงพิกัด GPS', 'error');
                return;
            }
            btn.innerHTML = `<i class="fa-solid fa-spinner fa-spin"></i> กำลังหาพิกัด...`;
            navigator.geolocation.getCurrentPosition(
                (pos) => {
                    const lat = pos.coords.latitude.toFixed(6);
                    const lng = pos.coords.longitude.toFixed(6);
                    const mapsUrl = `https://www.google.com/maps?q=${lat},${lng}`;
                    document.getElementById('jobGpsUrl').value = mapsUrl;
                    const addrEl = document.getElementById('jobAddress');
                    if (!addrEl.value.trim()) {
                        addrEl.value = `พิกัดหน้างาน (${lat}, ${lng})`;
                    }
                    btn.innerHTML = `<i class="fa-solid fa-check text-green-300"></i> ได้พิกัดแล้ว!`;
                    showToast('บันทึกพิกัด GPS ปัจจุบันเรียบร้อย');
                },
                (err) => {
                    btn.innerHTML = `<i class="fa-solid fa-location-crosshairs text-amber-300"></i> ดึงพิกัด GPS ปัจจุบัน`;
                    showToast('ไม่สามารถเข้าถึง GPS ได้ กรุณาเปิดสิทธิ์ตำแหน่งที่ตั้ง', 'error');
                },
                { enableHighAccuracy: true, timeout: 10000 }
            );
        }

        function appendBtuShortcut(btuText) {
            const input = document.getElementById('jobAcModel');
            const cur = input.value.trim();
            if (!cur) {
                input.value = btuText;
            } else if (!cur.includes(btuText)) {
                input.value = `${cur} ${btuText}`;
            }
        }

        function previewNextReminderDate() {
            const dateStr = document.getElementById('jobDate').value || getTodayStr();
            const months = parseInt(document.getElementById('jobReminderMonths').value, 10);
            const previewEl = document.getElementById('nextReminderPreviewText');
            if (months > 0) {
                const nextDate = addMonthsToDateStr(dateStr, months);
                previewEl.textContent = `📅 ระบบจะเตือนล้างรอบหน้าวันที่: ${formatThaiDate(nextDate)}`;
            } else {
                previewEl.textContent = 'ไม่ตั้งแจ้งเตือนรอบล้างแอร์';
            }
        }

        function saveJobForm(e) {
            e.preventDefault();
            const editId = document.getElementById('editJobId').value;
            const customerName = document.getElementById('jobCustomerName').value.trim();
            const contactPerson = document.getElementById('jobContactPerson').value.trim();
            const phone = document.getElementById('jobPhone').value.trim();
            const address = document.getElementById('jobAddress').value.trim();
            const gpsUrl = document.getElementById('jobGpsUrl').value.trim();
            const acModel = document.getElementById('jobAcModel').value.trim();
            const jobType = document.getElementById('jobType').value;
            const price = parseFloat(document.getElementById('jobPrice').value) || 0;
            const details = document.getElementById('jobDetails').value.trim();
            const date = document.getElementById('jobDate').value || getTodayStr();
            const status = document.getElementById('jobStatus').value;
            const reminderMonths = parseInt(document.getElementById('jobReminderMonths').value, 10) || 0;
            const nextWashDate = reminderMonths > 0 ? addMonthsToDateStr(date, reminderMonths) : '';

            const jobObj = {
                id: editId || 'j_' + Date.now(),
                customerName, contactPerson, phone, address, gpsUrl,
                acModel, jobType, price, details, date, status, reminderMonths, nextWashDate
            };

            if (editId) {
                const idx = state.jobs.findIndex(j => j.id === editId);
                if (idx !== -1) state.jobs[idx] = jobObj;
            } else {
                state.jobs.unshift(jobObj);
            }

            // อัปเดตสมุดรายชื่อลูกค้าอัตโนมัติ
            const cIdx = state.customers.findIndex(c => c.name.toLowerCase() === customerName.toLowerCase());
            if (cIdx === -1) {
                state.customers.unshift({
                    id: 'c_' + Date.now(),
                    name: customerName,
                    contact: contactPerson,
                    phone,
                    address
                });
            } else {
                if (contactPerson) state.customers[cIdx].contact = contactPerson;
                if (phone) state.customers[cIdx].phone = phone;
                if (address) state.customers[cIdx].address = address;
            }

            saveAllData();
            closeJobModal();
            renderJobs();
            showToast(editId ? 'อัปเดตประวัติงานเรียบร้อย' : 'บันทึกงานและลูกค้าเรียบร้อย');
        }

        function editJob(jobId) {
            const job = state.jobs.find(j => j.id === jobId);
            if (!job) return;
            openJobModal();
            document.getElementById('jobModalTitle').textContent = 'แก้ไข / ดูประวัติงาน';
            document.getElementById('editJobId').value = job.id;
            document.getElementById('jobCustomerName').value = job.customerName || '';
            document.getElementById('jobContactPerson').value = job.contactPerson || '';
            document.getElementById('jobPhone').value = job.phone || '';
            document.getElementById('jobAddress').value = job.address || '';
            document.getElementById('jobGpsUrl').value = job.gpsUrl || '';
            document.getElementById('jobAcModel').value = job.acModel || '';
            document.getElementById('jobType').value = job.jobType || 'ล้างแอร์';
            document.getElementById('jobPrice').value = job.price || 0;
            document.getElementById('jobDetails').value = job.details || '';
            document.getElementById('jobDate').value = job.date || getTodayStr();
            document.getElementById('jobStatus').value = job.status || 'รอดำเนินการ';
            document.getElementById('jobReminderMonths').value = job.reminderMonths || 0;
            previewNextReminderDate();
        }

        function confirmDeleteJob(jobId) {
            document.getElementById('confirmModalTitle').textContent = 'ลบรายการงานนี้?';
            document.getElementById('confirmModalDesc').textContent = 'ข้อมูลงานนี้จะถูกลบออกจากประวัติ';
            document.getElementById('confirmModalActionBtn').onclick = () => {
                state.jobs = state.jobs.filter(j => j.id !== jobId);
                saveAllData();
                renderJobs();
                closeConfirmModal();
                showToast('ลบรายการงานแล้ว');
            };
            document.getElementById('confirmModal').classList.remove('hidden');
        }

        function sendJobToQuote(jobId) {
            const job = state.jobs.find(j => j.id === jobId);
            if (!job) return;
            document.getElementById('quoteCustomerName').value = `${job.customerName}${job.contactPerson ? ` (${job.contactPerson})` : ''}`;
            document.getElementById('quoteCustomerPhone').value = job.phone || job.address || '';
            state.quoteItems = [
                {
                    name: `${job.jobType}${job.acModel ? ` ${job.acModel}` : ''}`,
                    price: job.price || 500,
                    qty: 1
                }
            ];
            document.getElementById('quoteDiscountInput').value = 0;
            switchTab('quote');
            showToast(`ส่งข้อมูล "${job.customerName}" ไปหน้าออกบิลแล้ว`);
        }

        // =========================================================================
        // 5. TAB 2: เช็กอาการ & บิล (Quick Quote & Check + Canvas PNG)
        // =========================================================================
        function initSymptomAndPresets() {
            const symptomGrid = document.getElementById('symptomButtonsGrid');
            symptomGrid.innerHTML = SYMPTOM_GUIDES.map(s => `
                <button onclick="selectSymptom('${s.id}')" class="btn-outdoor p-3 rounded-2xl border-2 ${s.btnClass} font-heading font-bold text-base text-left flex items-center gap-2 shadow-sm">
                    <i class="fa-solid ${s.icon} text-xl shrink-0"></i>
                    <span class="leading-tight">${s.title.replace(/^[^\s]+\s/, '')}</span>
                </button>
            `).join('');

            const presetContainer = document.getElementById('presetServiceButtons');
            presetContainer.innerHTML = PRESET_SERVICES.map(item => `
                <button onclick="addQuoteItem('${item.name}', ${item.price}, 1)" class="btn-outdoor px-3.5 py-2.5 bg-slate-100 hover:bg-blue-100 border-2 border-slate-400 hover:border-[#1E40AF] rounded-xl text-sm font-bold text-[#0F172A]">
                    + ${item.name} (${formatCurrency(item.price)}฿)
                </button>
            `).join('');
        }

        function selectSymptom(symptomId) {
            const guide = SYMPTOM_GUIDES.find(s => s.id === symptomId);
            if (!guide) return;

            document.getElementById('symptomGuideTitle').textContent = guide.title;
            document.getElementById('symptomCheckList').innerHTML = guide.checks.map((c, i) => `
                <label class="flex items-start gap-3 p-2.5 bg-white rounded-xl border border-amber-300 cursor-pointer">
                    <input type="checkbox" class="w-6 h-6 mt-0.5 accent-[#15803D] shrink-0">
                    <span class="text-base font-semibold text-[#0F172A] leading-snug">${c}</span>
                </label>
            `).join('');

            document.getElementById('symptomQuickAddBtns').innerHTML = guide.relatedServices.map(srv => `
                <button onclick="addQuoteItem('${srv.name}', ${srv.price}, 1)" class="btn-outdoor px-3.5 py-2 bg-[#EA580C] text-white font-bold text-sm rounded-xl shadow">
                    + เพิ่ม "${srv.name}" (${srv.price}฿)
                </button>
            `).join('');

            const box = document.getElementById('symptomGuideBox');
            box.classList.remove('hidden');
            box.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
        }

        function fillQuoteCustomerFromSelect() {
            const custId = document.getElementById('quoteCustomerSelect').value;
            if (!custId) return;
            const cust = state.customers.find(c => c.id === custId);
            if (cust) {
                document.getElementById('quoteCustomerName').value = `${cust.name}${cust.contact ? ` (${cust.contact})` : ''}`;
                document.getElementById('quoteCustomerPhone').value = cust.phone || cust.address || '';
            }
        }

        function addQuoteItem(name = '', price = 0, qty = 1) {
            state.quoteItems.push({ name, price, qty });
            renderQuoteItems();
            if (name) showToast(`เพิ่ม "${name}" ลงบิลแล้ว`);
        }

        function updateQuoteItem(index, field, value) {
            if (!state.quoteItems[index]) return;
            if (field === 'name') state.quoteItems[index].name = value;
            if (field === 'price') state.quoteItems[index].price = parseFloat(value) || 0;
            updateQuoteTotals();
        }

        function changeQuoteQty(index, delta) {
            if (!state.quoteItems[index]) return;
            const newQty = (state.quoteItems[index].qty || 1) + delta;
            if (newQty <= 0) {
                state.quoteItems.splice(index, 1);
            } else {
                state.quoteItems[index].qty = newQty;
            }
            renderQuoteItems();
        }

        function removeQuoteItem(index) {
            state.quoteItems.splice(index, 1);
            renderQuoteItems();
        }

        function renderQuoteItems() {
            const container = document.getElementById('quoteItemsContainer');
            if (state.quoteItems.length === 0) {
                container.innerHTML = `<p class="text-center text-slate-600 font-bold py-4 bg-slate-50 rounded-xl border-2 border-dashed border-slate-300">ยังไม่มีรายการในบิล กดปุ่มด้านบนเพื่อเพิ่มรายการ</p>`;
                updateQuoteTotals();
                return;
            }

            container.innerHTML = state.quoteItems.map((item, idx) => `
                <div class="bg-slate-50 p-3 rounded-2xl border-2 border-slate-400 space-y-2.5">
                    <div class="flex gap-2 items-center">
                        <span class="w-8 h-8 rounded-lg bg-[#0F172A] text-white font-bold text-base flex items-center justify-center shrink-0">${idx + 1}</span>
                        <input type="text" value="${item.name}" oninput="updateQuoteItem(${idx}, 'name', this.value)" placeholder="ชื่อรายการบริการ / อะไหล่" 
                            class="w-full p-2.5 text-base font-bold bg-white border-2 border-slate-400 rounded-xl">
                        <button onclick="removeQuoteItem(${idx})" class="text-red-700 hover:bg-red-100 p-2 rounded-xl text-xl shrink-0">
                            <i class="fa-solid fa-trash"></i>
                        </button>
                    </div>
                    <div class="flex items-center justify-between gap-2 pl-10">
                        <div class="flex items-center gap-1.5">
                            <span class="text-sm font-bold text-slate-700">ราคา:</span>
                            <input type="number" value="${item.price}" oninput="updateQuoteItem(${idx}, 'price', this.value)" 
                                class="w-28 p-2 text-base font-extrabold text-right bg-white border-2 border-slate-400 rounded-xl">
                            <span class="text-sm font-bold text-slate-700">฿</span>
                        </div>
                        <div class="flex items-center gap-2 bg-white border-2 border-slate-400 rounded-xl p-1">
                            <button onclick="changeQuoteQty(${idx}, -1)" class="w-9 h-9 rounded-lg bg-slate-200 font-extrabold text-xl flex items-center justify-center">-</button>
                            <span class="w-8 text-center font-extrabold text-lg">${item.qty}</span>
                            <button onclick="changeQuoteQty(${idx}, 1)" class="w-9 h-9 rounded-lg bg-[#1E40AF] text-white font-extrabold text-xl flex items-center justify-center">+</button>
                        </div>
                    </div>
                </div>
            `).join('');

            updateQuoteTotals();
        }

        function getQuoteCalculations() {
            const subtotal = state.quoteItems.reduce((sum, item) => sum + ((item.price || 0) * (item.qty || 1)), 0);
            const discount = parseFloat(document.getElementById('quoteDiscountInput')?.value) || 0;
            const netTotal = Math.max(0, subtotal - discount);
            return { subtotal, discount, netTotal };
        }

        function updateQuoteTotals() {
            const { subtotal, discount, netTotal } = getQuoteCalculations();
            document.getElementById('quoteGrandTotal').textContent = formatCurrency(netTotal);
            document.getElementById('quoteSummarySubtext').textContent = discount > 0 
                ? `${state.quoteItems.length} รายการ (รวม ${formatCurrency(subtotal)}฿ - ส่วนลด ${formatCurrency(discount)}฿)`
                : `${state.quoteItems.length} รายการ`;
        }

        // 1) คัดลอกข้อความส่ง LINE
        function copyBillTextForLine() {
            const validItems = state.quoteItems.filter(i => i.name.trim() !== '');
            if (validItems.length === 0) {
                showToast('กรุณาเพิ่มรายการอย่างน้อย 1 รายการก่อนคัดลอก', 'error');
                return;
            }
            const custName = document.getElementById('quoteCustomerName').value.trim() || 'ลูกค้า';
            const custPhone = document.getElementById('quoteCustomerPhone').value.trim();
            const note = document.getElementById('quoteNoteInput').value.trim();
            const { subtotal, discount, netTotal } = getQuoteCalculations();
            const billNo = state.shop.nextBillNo || 3460;

            let text = `❄️ ${state.shop.shopName}\n`;
            text += `📍 ${state.shop.address}\n`;
            text += `📞 ${state.shop.techName} โทร. ${state.shop.phone}\n`;
            text += `==============================\n`;
            text += `🧾 ใบเสนอราคา / บิลส่งงาน เลขที่ #${billNo}\n`;
            text += `📅 วันที่: ${formatThaiDate(getTodayStr())}\n`;
            text += `👤 ลูกค้า: ${custName}\n`;
            if (custPhone) text += `📱 ข้อมูลติดต่อ: ${custPhone}\n`;
            text += `------------------------------\n`;
            validItems.forEach((item, idx) => {
                text += `${idx + 1}. ${item.name} (${item.qty} x ${formatCurrency(item.price)}) = ${formatCurrency(item.price * item.qty)} บาท\n`;
            });
            text += `------------------------------\n`;
            if (discount > 0) {
                text += `รวมเป็นเงิน: ${formatCurrency(subtotal)} บาท\n`;
                text += `ส่วนลด: -${formatCurrency(discount)} บาท\n`;
            }
            text += `💰 ยอดรวมสุทธิ: ${formatCurrency(netTotal)} บาท\n`;
            if (note) text += `📝 หมายเหตุ: ${note}\n`;
            text += `ขอบพระคุณที่ใช้บริการครับ 🙏`;

            const tempArea = document.createElement('textarea');
            tempArea.value = text;
            document.body.appendChild(tempArea);
            tempArea.select();
            try {
                document.execCommand('copy');
                showToast('คัดลอกข้อความบิลสำเร็จ! วางส่งใน LINE ได้เลย');
            } catch (err) {
                showToast('ไม่สามารถคัดลอกอัตโนมัติได้', 'error');
            }
            document.body.removeChild(tempArea);
        }

        // 2) สร้างรูปบิล / ใบเสนอราคา PNG ความละเอียดสูงบน HTML5 Canvas
        function generateBillCanvasAndOpenModal() {
            const validItems = state.quoteItems.filter(i => i.name.trim() !== '');
            if (validItems.length === 0) {
                showToast('กรุณาเพิ่มรายการอย่างน้อย 1 รายการก่อนสร้างรูปบิล', 'error');
                return;
            }

            const custName = document.getElementById('quoteCustomerName').value.trim() || 'ลูกค้าทั่วไป';
            const custPhone = document.getElementById('quoteCustomerPhone').value.trim();
            const note = document.getElementById('quoteNoteInput').value.trim();
            const { subtotal, discount, netTotal } = getQuoteCalculations();
            const billNo = state.shop.nextBillNo || 3460;
            const dateStr = formatThaiDate(getTodayStr());

            const canvas = document.getElementById('billCanvas');
            const ctx = canvas.getContext('2d');

            const width = 840;
            const rowHeight = 68;
            const headerHeight = 310;
            const footerHeight = 310;
            const height = headerHeight + (validItems.length * rowHeight) + footerHeight;

            canvas.width = width;
            canvas.height = height;

            // พื้นหลังสีขาว
            ctx.fillStyle = '#FFFFFF';
            ctx.fillRect(0, 0, width, height);

            // หัวบิลสีน้ำเงินเข้ม #0F172A
            ctx.fillStyle = '#0F172A';
            ctx.fillRect(0, 0, width, 180);

            // แถบคาดสีส้ม #EA580C
            ctx.fillStyle = '#EA580C';
            ctx.fillRect(0, 180, width, 12);

            // โลโก้ไอคอนวงกลมมุมซ้าย
            ctx.fillStyle = '#EA580C';
            ctx.beginPath();
            ctx.arc(85, 90, 44, 0, Math.PI * 2);
            ctx.fill();
            ctx.fillStyle = '#FFFFFF';
            ctx.font = 'bold 42px sans-serif';
            ctx.textAlign = 'center';
            ctx.fillText('❄', 85, 105);

            // ชื่อร้าน & ข้อมูลติดต่อ
            ctx.textAlign = 'left';
            ctx.fillStyle = '#FFFFFF';
            ctx.font = 'bold 27px Prompt, Sarabun, sans-serif';
            ctx.fillText(state.shop.shopName, 150, 62);

            ctx.fillStyle = '#E2E8F0';
            ctx.font = '20px Sarabun, sans-serif';
            ctx.fillText(state.shop.address, 150, 100);

            ctx.fillStyle = '#FBBF24';
            ctx.font = 'bold 22px Sarabun, sans-serif';
            ctx.fillText(`${state.shop.techName} • โทร. ${state.shop.phone}`, 150, 138);

            // กล่องข้อมูลบิล & ลูกค้า
            ctx.fillStyle = '#F1F5F9';
            ctx.fillRect(32, 210, width - 64, 86);
            ctx.strokeStyle = '#94A3B8';
            ctx.lineWidth = 2;
            ctx.strokeRect(32, 210, width - 64, 86);

            ctx.textAlign = 'left';
            ctx.fillStyle = '#0F172A';
            ctx.font = 'bold 22px Sarabun, sans-serif';
            ctx.fillText(`ลูกค้า: ${custName}`, 50, 245);
            ctx.fillStyle = '#334155';
            ctx.font = '19px Sarabun, sans-serif';
            ctx.fillText(custPhone ? `ติดต่อ/ที่อยู่: ${custPhone}` : 'ใบเสนอราคา / ใบส่งมอบงานบริการ', 50, 278);

            ctx.textAlign = 'right';
            ctx.fillStyle = '#1E40AF';
            ctx.font = 'bold 24px Prompt, Sarabun, sans-serif';
            ctx.fillText(`เลขที่บิล #${billNo}`, width - 50, 245);
            ctx.fillStyle = '#0F172A';
            ctx.font = 'bold 20px Sarabun, sans-serif';
            ctx.fillText(`วันที่: ${dateStr}`, width - 50, 278);

            // หัวตาราง
            let curY = headerHeight + 10;
            ctx.fillStyle = '#0F172A';
            ctx.fillRect(32, curY, width - 64, 46);
            ctx.fillStyle = '#FFFFFF';
            ctx.font = 'bold 20px Sarabun, sans-serif';
            ctx.textAlign = 'left';
            ctx.fillText('รายการบริการ / อะไหล่', 50, curY + 30);
            ctx.textAlign = 'right';
            ctx.fillText('จำนวนเงิน (บาท)', width - 50, curY + 30);

            curY += 46;

            // วาดรายการทีละแถว
            validItems.forEach((item, idx) => {
                ctx.fillStyle = idx % 2 === 0 ? '#FFFFFF' : '#F8FAFC';
                ctx.fillRect(32, curY, width - 64, rowHeight);
                ctx.strokeStyle = '#CBD5E1';
                ctx.beginPath();
                ctx.moveTo(32, curY + rowHeight);
                ctx.lineTo(width - 32, curY + rowHeight);
                ctx.stroke();

                ctx.textAlign = 'left';
                ctx.fillStyle = '#0F172A';
                ctx.font = 'bold 22px Sarabun, sans-serif';
                ctx.fillText(`${idx + 1}. ${item.name}`, 50, curY + 30);

                ctx.fillStyle = '#475569';
                ctx.font = '18px Sarabun, sans-serif';
                ctx.fillText(`จำนวน ${item.qty} x ${formatCurrency(item.price)} บาท`, 76, curY + 55);

                ctx.textAlign = 'right';
                ctx.fillStyle = '#0F172A';
                ctx.font = 'bold 23px Sarabun, sans-serif';
                ctx.fillText(`${formatCurrency(item.price * item.qty)}`, width - 50, curY + 42);

                curY += rowHeight;
            });

            // ส่วนลด (ถ้ามี)
            curY += 12;
            if (discount > 0) {
                ctx.textAlign = 'right';
                ctx.fillStyle = '#334155';
                ctx.font = 'bold 20px Sarabun, sans-serif';
                ctx.fillText(`รวมเป็นเงิน: ${formatCurrency(subtotal)} บาท   |   ส่วนลด: -${formatCurrency(discount)} บาท`, width - 50, curY + 24);
                curY += 38;
            }

            // แถบยอดรวมสุทธิ
            ctx.fillStyle = '#1E40AF';
            ctx.fillRect(32, curY, width - 64, 72);

            ctx.textAlign = 'left';
            ctx.fillStyle = '#FFFFFF';
            ctx.font = 'bold 25px Prompt, Sarabun, sans-serif';
            ctx.fillText('ยอดรวมสุทธิทั้งสิ้น', 52, curY + 45);

            ctx.textAlign = 'right';
            ctx.fillStyle = '#FBBF24';
            ctx.font = 'bold 34px Prompt, Sarabun, sans-serif';
            ctx.fillText(`${formatCurrency(netTotal)} บาท`, width - 52, curY + 48);

            // หมายเหตุ & ช่องลงชื่อช่างอัฐ
            curY += 98;
            ctx.textAlign = 'left';
            ctx.fillStyle = '#334155';
            ctx.font = '17px Sarabun, sans-serif';
            if (note) {
                // ตัดบรรทัดหมายเหตุถ้ายาวเกิน
                const maxChars = 68;
                const line1 = note.substring(0, maxChars);
                const line2 = note.substring(maxChars, maxChars * 2);
                ctx.fillText(`หมายเหตุ: ${line1}`, 35, curY);
                if (line2) ctx.fillText(line2, 35, curY + 24);
            }

            // ลายเซ็นผู้รับเงิน / ช่างผู้ให้บริการ
            const signY = height - 45;
            ctx.textAlign = 'right';
            ctx.fillStyle = '#0F172A';
            ctx.font = 'bold 20px Sarabun, sans-serif';
            ctx.fillText(`ลงชื่อ .................................................... ผู้รับเงิน/ช่างผู้ให้บริการ`, width - 40, signY - 26);
            ctx.fillStyle = '#15803D';
            ctx.fillText(`(${state.shop.techName})`, width - 135, signY);

            // แปลงเป็น PNG และแสดงใน Modal
            const dataUrl = canvas.toDataURL('image/png');
            document.getElementById('billPngPreviewImg').src = dataUrl;
            const dlLink = document.getElementById('downloadPngLink');
            dlLink.href = dataUrl;
            dlLink.download = `บิลเลขที่_${billNo}_${custName.replace(/\s+/g, '_')}.png`;

            // รันเลขที่บิลถัดไปอัตโนมัติ
            state.shop.nextBillNo = billNo + 1;
            saveAllData();
            document.getElementById('displayBillNumber').textContent = state.shop.nextBillNo;

            document.getElementById('billPngModal').classList.remove('hidden');
            showToast(`สร้างรูปบิลเลขที่ #${billNo} เรียบร้อย!`);
        }

        function closeBillPngModal() {
            document.getElementById('billPngModal').classList.add('hidden');
        }

        // 3) บันทึกลงรายรับวันนี้
        function recordBillToDailyIncome() {
            const { netTotal } = getQuoteCalculations();
            if (netTotal <= 0) {
                showToast('ยอดเงินเป็น 0 บาท ไม่สามารถบันทึกรายรับได้', 'error');
                return;
            }
            const custName = document.getElementById('quoteCustomerName').value.trim() || 'ลูกค้าหน้างาน';
            const firstItem = state.quoteItems[0]?.name || 'ค่าบริการงานแอร์';

            state.finance.unshift({
                id: 'f_' + Date.now(),
                type: 'INCOME',
                category: 'ค่าซ่อม',
                amount: netTotal,
                note: `${firstItem} - ${custName}`,
                date: getTodayStr()
            });

            saveAllData();
            showToast(`บันทึกรายรับ +${formatCurrency(netTotal)} บาท เข้าบัญชีวันนี้เรียบร้อย!`);
        }

        // =========================================================================
        // 6. TAB 3: บัญชี & กำไรรายวัน (Daily Profit & Expense)
        // =========================================================================
        function setFinanceMode(mode) {
            state.financeMode = mode;
            const dailyBtn = document.getElementById('finMode-DAILY');
            const allBtn = document.getElementById('finMode-ALL');
            const dateRow = document.getElementById('financeDatePickerRow');

            if (mode === 'DAILY') {
                dailyBtn.className = 'btn-outdoor py-2.5 rounded-xl font-heading font-bold text-base bg-[#0F172A] text-white border-2 border-[#0F172A]';
                allBtn.className = 'btn-outdoor py-2.5 rounded-xl font-heading font-bold text-base bg-slate-100 text-[#0F172A] border-2 border-slate-400';
                dateRow.classList.remove('hidden');
            } else {
                allBtn.className = 'btn-outdoor py-2.5 rounded-xl font-heading font-bold text-base bg-[#0F172A] text-white border-2 border-[#0F172A]';
                dailyBtn.className = 'btn-outdoor py-2.5 rounded-xl font-heading font-bold text-base bg-slate-100 text-[#0F172A] border-2 border-slate-400';
                dateRow.classList.add('hidden');
            }
            renderFinance();
        }

        function setFinanceDateToday() {
            document.getElementById('financeSelectedDate').value = getTodayStr();
            renderFinance();
        }

        function renderFinance() {
            const selectedDate = document.getElementById('financeSelectedDate').value || getTodayStr();
            const filtered = state.finance.filter(entry => {
                if (state.financeMode === 'DAILY') return entry.date === selectedDate;
                return true;
            });

            const totalIncome = filtered.filter(e => e.type === 'INCOME').reduce((sum, e) => sum + Number(e.amount || 0), 0);
            const totalExpense = filtered.filter(e => e.type === 'EXPENSE').reduce((sum, e) => sum + Number(e.amount || 0), 0);
            const netProfit = totalIncome - totalExpense;

            document.getElementById('totalIncomeValue').textContent = `+${formatCurrency(totalIncome)} ฿`;
            document.getElementById('totalExpenseValue').textContent = `-${formatCurrency(totalExpense)} ฿`;
            document.getElementById('netProfitLabel').textContent = state.financeMode === 'DAILY' 
                ? `กำไรสุทธิ (${formatThaiDate(selectedDate)})` 
                : 'กำไรสุทธิ (ภาพรวมทั้งหมด)';
            document.getElementById('netProfitValue').textContent = `${netProfit < 0 ? '-' : ''}${formatCurrency(Math.abs(netProfit))} ฿`;

            document.getElementById('financeEntryCount').textContent = `${filtered.length} รายการ`;
            const listContainer = document.getElementById('financeListContainer');

            if (filtered.length === 0) {
                listContainer.innerHTML = `<p class="text-center text-slate-500 font-bold py-6">ยังไม่มีรายการรายรับ-รายจ่ายในช่วงนี้</p>`;
                return;
            }

            listContainer.innerHTML = filtered.map(entry => {
                const isIncome = entry.type === 'INCOME';
                return `
                <div class="p-3.5 rounded-2xl border-2 ${isIncome ? 'border-green-300 bg-green-50/70' : 'border-red-300 bg-red-50/70'} flex items-center justify-between gap-2">
                    <div class="flex items-start gap-3">
                        <div class="w-11 h-11 rounded-xl ${isIncome ? 'bg-[#15803D]' : 'bg-red-700'} text-white flex items-center justify-center text-lg shrink-0 mt-0.5">
                            <i class="fa-solid ${isIncome ? 'fa-plus' : 'fa-minus'}"></i>
                        </div>
                        <div>
                            <p class="font-heading font-bold text-base text-[#0F172A]">${entry.category}</p>
                            ${entry.note ? `<p class="text-sm font-semibold text-slate-700">${entry.note}</p>` : ''}
                            <p class="text-xs font-bold text-slate-500 mt-0.5">${formatThaiDate(entry.date)}</p>
                        </div>
                    </div>
                    <div class="text-right shrink-0">
                        <p class="font-heading font-extrabold text-xl ${isIncome ? 'text-[#15803D]' : 'text-red-700'}">
                            ${isIncome ? '+' : '-'}${formatCurrency(entry.amount)} ฿
                        </p>
                        <button onclick="confirmDeleteFinance('${entry.id}')" class="mt-1 text-xs font-bold text-red-700 bg-white border border-red-300 px-2.5 py-1 rounded-lg">
                            ลบรายการ
                        </button>
                    </div>
                </div>`;
            }).join('');
        }

        function openFinanceModal(type) {
            const isIncome = type === 'INCOME';
            document.getElementById('financeEntryType').value = type;
            document.getElementById('financeModalTitle').textContent = isIncome ? '+ บันทึกรายรับ' : '+ บันทึกรายจ่าย';
            document.getElementById('financeModalHeader').className = `${isIncome ? 'bg-[#15803D]' : 'bg-red-700'} text-white px-5 py-4 flex justify-between items-center`;
            document.getElementById('financeSubmitBtn').className = `btn-outdoor ${isIncome ? 'bg-[#15803D]' : 'bg-red-700'} text-white font-heading font-bold text-lg rounded-2xl shadow-lg`;

            const cats = isIncome ? INCOME_CATEGORIES : EXPENSE_CATEGORIES;
            document.getElementById('financeCategoryChips').innerHTML = cats.map(c => `
                <button type="button" onclick="document.getElementById('financeCategoryInput').value='${c}'" 
                    class="btn-outdoor px-3 py-2 rounded-xl border-2 border-slate-400 bg-slate-100 hover:bg-blue-100 font-bold text-sm text-[#0F172A]">
                    ${c}
                </button>
            `).join('');

            document.getElementById('financeCategoryInput').value = cats[0];
            document.getElementById('financeAmountInput').value = '';
            document.getElementById('financeNoteInput').value = '';
            document.getElementById('financeDateInput').value = document.getElementById('financeSelectedDate').value || getTodayStr();

            document.getElementById('financeModal').classList.remove('hidden');
            setTimeout(() => document.getElementById('financeAmountInput').focus(), 120);
        }

        function closeFinanceModal() {
            document.getElementById('financeModal').classList.add('hidden');
        }

        function saveFinanceEntry(e) {
            e.preventDefault();
            const type = document.getElementById('financeEntryType').value;
            const category = document.getElementById('financeCategoryInput').value.trim();
            const amount = parseFloat(document.getElementById('financeAmountInput').value) || 0;
            const note = document.getElementById('financeNoteInput').value.trim();
            const date = document.getElementById('financeDateInput').value || getTodayStr();

            if (amount <= 0) {
                showToast('กรุณากรอกจำนวนเงินให้มากกว่า 0', 'error');
                return;
            }

            state.finance.unshift({
                id: 'f_' + Date.now(),
                type, category, amount, note, date
            });

            saveAllData();
            closeFinanceModal();
            document.getElementById('financeSelectedDate').value = date;
            renderFinance();
            showToast(type === 'INCOME' ? 'บันทึกรายรับเรียบร้อย' : 'บันทึกรายจ่ายเรียบร้อย');
        }

        function confirmDeleteFinance(entryId) {
            document.getElementById('confirmModalTitle').textContent = 'ลบรายการบัญชีนี้?';
            document.getElementById('confirmModalDesc').textContent = 'ยอดรวมรายรับ-รายจ่ายและกำไรจะคำนวณใหม่ทันที';
            document.getElementById('confirmModalActionBtn').onclick = () => {
                state.finance = state.finance.filter(f => f.id !== entryId);
                saveAllData();
                renderFinance();
                closeConfirmModal();
                showToast('ลบรายการเรียบร้อย');
            };
            document.getElementById('confirmModal').classList.remove('hidden');
        }

        function closeConfirmModal() {
            document.getElementById('confirmModal').classList.add('hidden');
        }

        // =========================================================================
        // 7. ตั้งค่าร้าน & Export / Import / รีเซ็ตข้อมูลเริ่มต้น
        // =========================================================================
        function applyShopInfoToHeader() {
            document.getElementById('headerShopName').textContent = state.shop.shopName;
            document.getElementById('headerTechInfo').textContent = `${state.shop.techName} • โทร. ${state.shop.phone}`;
            document.getElementById('displayBillNumber').textContent = state.shop.nextBillNo || 3460;
        }

        function openSettingsModal() {
            document.getElementById('settingShopName').value = state.shop.shopName || '';
            document.getElementById('settingTechName').value = state.shop.techName || '';
            document.getElementById('settingShopPhone').value = state.shop.phone || '';
            document.getElementById('settingShopAddress').value = state.shop.address || '';
            document.getElementById('settingNextBillNo').value = state.shop.nextBillNo || 3460;
            document.getElementById('settingsModal').classList.remove('hidden');
        }

        function closeSettingsModal() {
            document.getElementById('settingsModal').classList.add('hidden');
        }

        function saveShopSettings(e) {
            e.preventDefault();
            state.shop.shopName = document.getElementById('settingShopName').value.trim();
            state.shop.techName = document.getElementById('settingTechName').value.trim();
            state.shop.phone = document.getElementById('settingShopPhone').value.trim();
            state.shop.address = document.getElementById('settingShopAddress').value.trim();
            state.shop.nextBillNo = parseInt(document.getElementById('settingNextBillNo').value, 10) || 3460;
            saveAllData();
            applyShopInfoToHeader();
            closeSettingsModal();
            showToast('บันทึกข้อมูลร้านเรียบร้อย');
        }

        function exportBackupJSON() {
            const payload = {
                exportedAt: new Date().toISOString(),
                shop: state.shop,
                customers: state.customers,
                jobs: state.jobs,
                finance: state.finance
            };
            const blob = new Blob([JSON.stringify(payload, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `สำรองข้อมูล_ช่างงานเซอร์วิส_${getTodayStr()}.json`;
            a.click();
            URL.revokeObjectURL(url);
            showToast('ดาวน์โหลดไฟล์สำรองข้อมูล JSON เรียบร้อย');
        }

        function importBackupJSON(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    if (data.shop) state.shop = data.shop;
                    if (Array.isArray(data.customers)) state.customers = data.customers;
                    if (Array.isArray(data.jobs)) state.jobs = data.jobs;
                    if (Array.isArray(data.finance)) state.finance = data.finance;
                    saveAllData();
                    applyShopInfoToHeader();
                    renderJobs();
                    renderFinance();
                    closeSettingsModal();
                    showToast('กู้คืนข้อมูลจากไฟล์ JSON สำเร็จ!');
                } catch (err) {
                    showToast('ไฟล์ JSON ไม่ถูกต้อง', 'error');
                }
            };
            reader.readAsText(file);
            event.target.value = '';
        }

        function confirmResetDefaultData() {
            document.getElementById('confirmModalTitle').textContent = 'รีเซ็ตข้อมูลเริ่มต้นทั้งหมด?';
            document.getElementById('confirmModalDesc').textContent = 'ระบบจะล้างข้อมูลที่แก้ไขและโหลดฐานข้อมูลลูกค้าเริ่มต้นทั้ง 13 รายกลับมาใหม่';
            document.getElementById('confirmModalActionBtn').onclick = () => {
                localStorage.removeItem(STORAGE_KEYS.SHOP);
                localStorage.removeItem(STORAGE_KEYS.CUSTOMERS);
                localStorage.removeItem(STORAGE_KEYS.JOBS);
                localStorage.removeItem(STORAGE_KEYS.FINANCE);
                loadAllData();
                applyShopInfoToHeader();
                populateCustomerDropdowns();
                renderJobs();
                renderFinance();
                closeConfirmModal();
                closeSettingsModal();
                showToast('รีเซ็ตกลับเป็นข้อมูลเริ่มต้นเรียบร้อย!');
            };
            document.getElementById('confirmModal').classList.remove('hidden');
        }

        // =========================================================================
        // 8. Initialize App on Window Load
        // =========================================================================
        window.onload = function() {
            loadAllData();
            applyShopInfoToHeader();
            initSymptomAndPresets();
            populateCustomerDropdowns();
            document.getElementById('financeSelectedDate').value = getTodayStr();
            renderJobs();
            renderQuoteItems();
            renderFinance();
        };
    </script>
</body>
</html>
