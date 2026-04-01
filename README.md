
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Current Promotion Check list -Landscape</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        @media print {
            @page { size: A4 landscape; margin: 8mm; }
            body { background-color: white !important; -webkit-print-color-adjust: exact; }
            .no-print { display: none !important; }
            .table-scroll { overflow: visible !important; max-height: none !important; }
            table { width: 100% !important; table-layout: fixed; }
            th, td { font-size: 10px !important; padding: 3px !important; }
            textarea { border: none !important; resize: none; }
        }

        .auto-expand { min-height: 40px; height: auto; }
        .table-scroll { overflow-x: auto; max-height: 60vh; border-radius: 8px; }
        input[type="checkbox"] { width: 18px; height: 18px; accent-color: #005e2f; cursor: pointer; }
        .row-non-compliant { background-color: #fff1f2 !important; }
    </style>
</head>

<body class="bg-gray-100 min-h-screen font-sans text-gray-900">

    <nav class="bg-[#1d2521] text-white p-4 shadow-lg sticky top-0 z-50 no-print flex justify-between items-center">
        <div class="flex items-center gap-2">
            <img src="https://www.luluretail.com/media/nyvaa55g/lulu-retail-logo.svg" alt="LuLu" width="150" height="75">
            <h1 class="text-xl font-bold">Current Promotion Checklist📋</h1>
        </div>
        </div>
        <div class="flex gap-2">
            <button onclick="saveAsNewPage()" class="bg-blue-600 hover:bg-blue-700 px-4 py-2 rounded-lg text-xs font-bold uppercase transition">📥 Save HTML</button>
            <button onclick="window.print()" class="bg-red-600 hover:bg-red-700 px-4 py-2 rounded-lg text-xs font-bold uppercase transition">📄 Print / PDF</button>
        </div>
    </nav>

    <div class="max-w-[1140px] mx-auto p-4">

        <div class="grid grid-cols-4 gap-4 mb-4 no-print">
            <div class="bg-white p-3 rounded-lg shadow-sm border-l-4 border-blue-500">
                <p class="text-[10px] text-gray-400 font-bold uppercase">Products</p>
                <p id="dash-total" class="text-xl font-black">0</p>
            </div>
            <div class="bg-white p-3 rounded-lg shadow-sm border-l-4 border-green-500">
                <p class="text-[10px] text-gray-400 font-bold uppercase">Availability</p>
                <p id="dash-avail" class="text-xl font-black text-green-600">0%</p>
            </div>
            <div class="bg-white p-3 rounded-lg shadow-sm border-l-4 border-orange-500">
                <p class="text-[10px] text-gray-400 font-bold uppercase">Price Boards</p>
                <p id="dash-price" class="text-xl font-black text-orange-600">0%</p>
            </div>
            <div class="bg-white p-3 rounded-lg shadow-sm border-l-4 border-purple-500">
                <p class="text-[10px] text-gray-400 font-bold uppercase">Displays</p>
                <p id="dash-pec" class="text-xl font-black text-purple-600">0</p>
            </div>
        </div>

        <div class="bg-white rounded-xl shadow-sm p-6 mb-6 border border-gray-200">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 text-sm">
                
                <div class="relative">
                    <label class="block text-[10px] font-bold text-gray-400 uppercase mb-1">Branch (Type Code or Name)</label>
                    <input list="branchList" id="branchInput" class="w-full border-b border-gray-200 focus:border-green-600 outline-none py-1 bg-transparent font-bold" placeholder="Search Branch...">
                    <datalist id="branchList">
                        <option value="3560-Ibri">
                        <option value="3482-Jalan Bu Ali">
                        <option value="3435-Amerat">
                        <option value="3555-Suwaiq">
                        <option value="3440-Bousher">
                        <option value="3466-Wadi Lawami">
                        <option value="3450-Darsait">
                        <option value="3585-Sinaw">
                        <option value="3464-Ruwi">
                        <option value="3462-Sur">
                        <option value="3500-Barka">
                        <option value="3468-Markaz Al Bahja">
                        <option value="3580-Saada">
                        <option value="3540-Nizwa">
                        <option value="3565-Bidayah">
                        <option value="3510-Buraimi">
                        <option value="3460-Sohar">
                        <option value="3455-Bawadi Mall">
                        <option value="3480-Wadi AlKabir">
                        <option value="3405-Al Burj">
                        <option value="3520-Khasab">
                        <option value="3445-MOM">
                        <option value="3430-Khaburah">
                        <option value="3575-Rustaq">
                        <option value="3545-Al Bandar">
                        <option value="3532-Airport Rd Salalah">
                        <option value="3425-IBRA">
                        <option value="3415-Seeb">
                        <option value="3530-Salalah">
                        <option value="3432-Al ansab">
                        <option value="3437-Zakher Mall">
                        <option value="3458-Falaj Al Qa">
                        <option value="3452-QURUM">
                    </datalist>
                </div>

                <div>
                    <label class="block text-[10px] font-bold text-gray-400 uppercase">Audit Date</label>
                    <input type="date" id="date" class="w-full border-b border-gray-200 focus:border-green-600 outline-none py-1 text-sm">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-gray-400 uppercase">Promotion Name</label>
                    <input type="text" id="promoName" class="w-full border-b border-gray-200 focus:border-green-600 outline-none py-1 text-sm" placeholder="Offer Title">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-gray-400 uppercase">Promotion Period</label>
                    <div class="flex items-center space-x-2">
            <input type="date" id="start-date" 
                class="w-full border-b border-gray-200 focus:border-green-600 outline-none py-1 text-sm transition-colors cursor-pointer"
                title="Start Date">
            
            <span class="text-gray-400 text-xs">to</span>
            
            <input type="date" id="end-date" 
                class="w-full border-b border-gray-200 focus:border-green-600 outline-none py-1 text-sm transition-colors cursor-pointer"
                title="End Date">
        </div>
                </div>
            </div>
        </div>

        <div class="flex justify-between items-center mb-4 no-print">
            <div class="flex gap-2">
                <label class="bg-green-700 text-white px-4 py-2 rounded shadow cursor-pointer text-xs font-bold hover:bg-green-800 transition">
                    📂 Import Excel
                    <input type="file" id="excelUpload" class="hidden" accept=".xlsx, .xls" onchange="handleExcel(this)">
                </label>
                <button onclick="addRow()" class="bg-slate-700 text-white px-4 py-2 rounded shadow text-xs font-bold hover:bg-slate-800 transition">➕ Add Row</button>
            </div>
            <button onclick="clearTable()" class="text-red-500 text-xs font-bold hover:underline">🗑️ Clear All Data</button>
        </div>

        <div class="bg-white rounded-lg shadow-lg border border-gray-200 overflow-hidden">
            <div class="table-scroll">
                <table id="masterTable" class="w-full text-left border-collapse">
                    <thead class="bg-slate-800 text-white text-[10px] uppercase">
                        <tr>
                            <th class="p-4 border-r border-slate-700 w-10">No</th>
                            <th class="p-4 border-r border-slate-700 min-w-[320px]">Product Description</th>
                            <th class="p-4 border-r border-slate-700 text-center w-28">Price Boards highlighted (Yes/No)</th>
                            <th class="p-4 border-r border-slate-700 text-center w-28">Product Availability (Yes/No)</th>
                            <th class="p-4 border-r border-slate-700 text-center w-14">Pallet Display</th>
                            <th class="p-4 border-r border-slate-700 text-center w-14">End Gonlola or Element</th>
                            <th class="p-4 border-r border-slate-700 text-center w-14">Category Display</th>
                            <th class="p-3 border-r border-slate-700">Comments (if any)</th>
                            <th class="p-2 w-10 no-print"></th>
                        </tr>
                    </thead>
                    <tbody id="tableBody" class="divide-y divide-gray-200"></tbody>
                </table>
            </div>
        </div>
        <p class="text-[10px] text-gray-400 mt-2 text-center no-print">* P: Pallet | E: Endcap | C: Category Display   | * Developed by:148271 </p>
    </div>

    <script>
        let rowCount = 0;

        function addRow(data = {}) {
            rowCount++;
            const tbody = document.getElementById('tableBody');
            const tr = document.createElement('tr');
            tr.className = "hover:bg-gray-50 transition-colors";
            
            // data.comment or blank editable field
            const commentValue = data.comment || "";

            tr.innerHTML = `
                <td class="p-2 text-center font-bold text-gray-400 border-r text-xs">${rowCount}</td>
                <td class="p-1 border-r">
                    <textarea oninput="adjustHeight(this); updateDashboard()" 
                    class="w-full p-1 border border-transparent focus:border-green-300 rounded outline-none auto-expand bg-transparent text-xs leading-relaxed" 
                    placeholder="Enter product...">${data.desc || ''}</textarea>
                </td>
                <td class="p-1 border-r text-center">
                    <select onchange="updateDashboard()" class="w-full p-1 border rounded bg-white text-[10px] font-semibold cursor-pointer">
                        <option value="">-</option>
                        <option value="Yes" ${data.pb === 'Yes' ? 'selected' : ''}>Yes</option>
                        <option value="No" ${data.pb === 'No' ? 'selected' : ''}>No</option>
                    </select>
                </td>
                <td class="p-1 border-r text-center">
                    <select onchange="updateDashboard()" class="w-full p-1 border rounded bg-white text-[10px] font-semibold cursor-pointer">
                        <option value="">-</option>
                        <option value="Yes" ${data.avail === 'Yes' ? 'selected' : ''}>Yes</option>
                        <option value="No" ${data.avail === 'No' ? 'selected' : ''}>No</option>
                    </select>
                </td>
                <td class="p-1 border-r text-center"><input type="checkbox" onchange="updateDashboard()" ${data.p ? 'checked' : ''}></td>
                <td class="p-1 border-r text-center"><input type="checkbox" onchange="updateDashboard()" ${data.e ? 'checked' : ''}></td>
                <td class="p-1 border-r text-center"><input type="checkbox" onchange="updateDashboard()" ${data.c ? 'checked' : ''}></td>
                <td class="p-1 border-r">
                    <textarea oninput="adjustHeight(this)" 
                    class="w-full p-1 border border-transparent focus:border-green-300 rounded outline-none auto-expand bg-transparent text-xs" 
                    placeholder="Click to add comment...">${commentValue}</textarea>
                </td>
                <td class="p-1 text-center no-print">
                    <button onclick="this.closest('tr').remove(); renumberRows(); updateDashboard()" class="text-red-400 hover:text-red-600 font-bold px-2 text-lg">×</button>
                </td>
            `;
            tbody.appendChild(tr);
            if (data.desc) adjustHeight(tr.querySelector('textarea'));
            updateDashboard();
        }

        function adjustHeight(el) {
            el.style.height = 'auto';
            el.style.height = el.scrollHeight + 'px';
        }

        function renumberRows() {
            let currentNum = 0;
            document.querySelectorAll('#tableBody tr').forEach((tr) => {
                currentNum++;
                tr.cells[0].innerText = currentNum;
            });
            rowCount = currentNum;
        }

        function updateDashboard() {
            const rows = document.querySelectorAll('#tableBody tr');
            let activeRows = 0, pbYes = 0, avYes = 0, displays = 0;

            rows.forEach(row => {
                const desc = row.querySelector('textarea').value.trim();
                const selects = row.querySelectorAll('select');
                const checks = row.querySelectorAll('input[type="checkbox"]');
                
                row.classList.remove('row-non-compliant');

                if (desc !== "") {
                    activeRows++;
                    if (selects[0].value === 'Yes') pbYes++;
                    if (selects[1].value === 'Yes') avYes++;
                    if(selects[0].value === 'No' || selects[1].value === 'No') row.classList.add('row-non-compliant');
                    if (checks[0].checked || checks[1].checked || checks[2].checked) displays++;
                }
            });

            document.getElementById('dash-total').innerText = activeRows;
            document.getElementById('dash-avail').innerText = activeRows ? Math.round((avYes / activeRows) * 100) + '%' : '0%';
            document.getElementById('dash-price').innerText = activeRows ? Math.round((pbYes / activeRows) * 100) + '%' : '0%';
            document.getElementById('dash-pec').innerText = displays;
        }

        function clearTable() {
            if(confirm('Are you sure? This will delete all rows.')) {
                document.getElementById('tableBody').innerHTML = '';
                rowCount = 0;
                addRow();
                updateDashboard();
            }
        }

        function handleExcel(input) {
            if (!input.files.length) return;
            const reader = new FileReader();
            reader.onload = (e) => {
                const data = new Uint8Array(e.target.result);
                const workbook = XLSX.read(data, { type: 'array' });
                const jsonRows = XLSX.utils.sheet_to_json(workbook.Sheets[workbook.SheetNames[0]], { header: 1 });
                
                // Clear existing and import
                document.getElementById('tableBody').innerHTML = '';
                rowCount = 3;
                
                jsonRows.forEach((row, i) => {
                    // Start from second row to skip header
                    if (i > 0 && (row[0] || row[1])) {
                        addRow({ desc: row[1] || row[0] }); 
                    }
                });
                input.value = ""; // Reset input
            };
            reader.readAsArrayBuffer(input.files[0]);
        }

        function saveAsNewPage() {
            document.querySelectorAll('input[type="text"], input[type="date"]').forEach(el => el.setAttribute('value', el.value));
            document.querySelectorAll('textarea').forEach(el => el.innerHTML = el.value);
            document.querySelectorAll('select').forEach(el => {
                el.querySelectorAll('option').forEach(opt => {
                    if (opt.value === el.value) opt.setAttribute('selected', 'selected');
                    else opt.removeAttribute('selected');
                });
            });
            document.querySelectorAll('input[type="checkbox"]').forEach(el => {
                if (el.checked) el.setAttribute('checked', 'checked');
                else el.removeAttribute('checked');
            });

            const htmlContent = "<!DOCTYPE html>\n" + document.documentElement.outerHTML;
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `Compliance_Audit_${new Date().toISOString().slice(0,10)}.html`;
            link.click();
        }

        window.onload = () => { if(rowCount === 0) for(let i=0; i<0; i++) addRow(); };
    </script>
</body>

</html>
