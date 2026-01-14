<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ניתוח יעילות תפעולית - דקות/ק"מ</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { font-family: system-ui, -apple-system, sans-serif; background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%); min-height: 100vh; }
        .upload-zone { border: 2px dashed #94a3b8; transition: all 0.3s; }
        .upload-zone:hover, .upload-zone.dragover { border-color: #3b82f6; background: #eff6ff; }
        .upload-zone.has-file { border-color: #22c55e; background: #f0fdf4; }
        
        .layout { display: grid; grid-template-columns: 320px 1fr; min-height: calc(100vh - 80px); }
        .sidebar { background: white; border-left: 1px solid #e2e8f0; padding: 24px; position: sticky; top: 80px; height: calc(100vh - 80px); overflow-y: auto; display: flex; flex-direction: column; gap: 16px; box-shadow: -5px 0 15px rgba(0,0,0,0.03); }
        .main { padding: 32px; overflow-y: auto; }
        
        .card { background: white; border-radius: 12px; padding: 16px; border: 1px solid #e2e8f0; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-val { font-size: 1.75rem; font-weight: 800; line-height: 1; margin-top: 4px; }
        .stat-lbl { font-size: 0.7rem; font-weight: 700; text-transform: uppercase; color: #64748b; }
        .stat-sub { font-size: 0.75rem; margin-top: 4px; }
        
        .compare-box { display: flex; gap: 8px; align-items: center; padding: 8px 12px; background: #f8fafc; border-radius: 8px; margin-top: 8px; }
        .compare-label { font-size: 0.65rem; color: #64748b; }
        .compare-val { font-size: 0.85rem; font-weight: 700; }
        
        .table-wrap { background: white; border-radius: 8px; border: 1px solid #e2e8f0; overflow: hidden; }
        .data-table { width: 100%; border-collapse: collapse; font-size: 0.8rem; }
        .data-table th { background: #f8fafc; color: #475569; font-weight: 700; text-align: right; padding: 10px 12px; border-bottom: 2px solid #e2e8f0; position: sticky; top: 0; white-space: nowrap; }
        .data-table td { padding: 8px 12px; border-bottom: 1px solid #f1f5f9; }
        .data-table tr:hover { background: #f8fafc; }
        .clickable { cursor: pointer; color: #2563eb; text-decoration: underline; }
        .clickable:hover { color: #1d4ed8; }
        
        .tabs-nav { display: flex; gap: 4px; border-bottom: 1px solid #e2e8f0; margin-bottom: 20px; overflow-x: auto; }
        .tab-btn { padding: 10px 14px; font-weight: 600; font-size: 0.85rem; color: #64748b; cursor: pointer; border-bottom: 3px solid transparent; white-space: nowrap; display: flex; align-items: center; gap: 6px; }
        .tab-btn.active { color: #2563eb; border-bottom-color: #2563eb; background: white; }
        .badge { background: #e2e8f0; color: #475569; font-size: 0.65rem; padding: 2px 6px; border-radius: 8px; }
        .tab-btn.active .badge { background: #dbeafe; color: #1e40af; }
        
        .status-ok { background: #dcfce7; color: #166534; padding: 2px 8px; border-radius: 4px; font-size: 0.7rem; font-weight: 700; }
        .status-warn { background: #fef3c7; color: #92400e; padding: 2px 8px; border-radius: 4px; font-size: 0.7rem; font-weight: 700; }
        .status-bad { background: #fee2e2; color: #991b1b; padding: 2px 8px; border-radius: 4px; font-size: 0.7rem; font-weight: 700; }
        
        .modal { position: fixed; inset: 0; background: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center; z-index: 1000; }
        .modal-content { background: white; border-radius: 16px; max-width: 900px; width: 95%; max-height: 85vh; overflow: hidden; display: flex; flex-direction: column; }
        .modal-header { padding: 20px 24px; border-bottom: 1px solid #e2e8f0; display: flex; justify-content: space-between; align-items: center; }
        .modal-body { padding: 24px; overflow-y: auto; flex: 1; }
        .modal-close { cursor: pointer; color: #64748b; font-size: 1.5rem; }
        .modal-close:hover { color: #1e293b; }
        
        .breakdown-bar { height: 24px; border-radius: 4px; overflow: hidden; display: flex; }
        .breakdown-segment { height: 100%; display: flex; align-items: center; justify-content: center; font-size: 0.65rem; font-weight: 700; color: white; min-width: 30px; }
        
        .activity-row { display: grid; grid-template-columns: 100px 1fr 80px 80px; gap: 12px; padding: 8px 12px; border-bottom: 1px solid #f1f5f9; align-items: center; }
        .activity-row.with-duty { grid-template-columns: 100px 1fr 60px 50px 70px; }
        .activity-row:hover { background: #f8fafc; }
        .activity-pt { background: #dcfce7; }
        .activity-non-pt { background: #fef3c7; }
        
        .gap-card { background: white; border-radius: 12px; padding: 20px; border: 1px solid #e2e8f0; margin-bottom: 16px; }
        .gap-title { font-size: 1rem; font-weight: 700; color: #1e293b; margin-bottom: 12px; }
        .gap-breakdown { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 12px; }
        .gap-item { background: #f8fafc; border-radius: 8px; padding: 12px; text-align: center; }
        .gap-item-value { font-size: 1.5rem; font-weight: 800; }
        .gap-item-label { font-size: 0.7rem; color: #64748b; margin-top: 4px; }
        
        .hidden { display: none !important; }
        @media (max-width: 900px) { .layout { grid-template-columns: 1fr; } .sidebar { position: relative; height: auto; } }
    </style>
</head>
<body>
    <header class="bg-white shadow-sm border-b border-slate-200 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-gradient-to-br from-blue-500 to-blue-600 rounded-xl flex items-center justify-center">
                    <i class="fas fa-gauge-high text-white"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold text-slate-800">ניתוח יעילות תפעולית</h1>
                    <p class="text-xs text-slate-500">דקות/ק"מ | תכנון vs ביצוע | יעילות נהגים</p>
                </div>
            </div>
            <div id="status-indicator" class="text-sm text-slate-500"><i class="fas fa-circle-info ml-1"></i> טען קבצים להתחלה</div>
        </div>
    </header>

    <div id="upload-section" class="max-w-4xl mx-auto p-6">
        <div class="grid md:grid-cols-2 gap-6 mb-6">
            <div class="card">
                <h3 class="font-bold text-slate-700 mb-3 flex items-center gap-2">
                    <i class="fas fa-file-csv text-green-500"></i> קובץ ביצוע (סדרן) <span class="text-red-500">*</span>
                </h3>
                <div id="exec-zone" class="upload-zone rounded-lg p-6 text-center cursor-pointer" onclick="document.getElementById('exec-file').click()">
                    <i class="fas fa-cloud-upload-alt text-3xl text-slate-400 mb-2"></i>
                    <p class="text-sm text-slate-600">גרור קובץ CSV או לחץ לבחירה</p>
                    <p id="exec-filename" class="text-xs text-slate-400 mt-1"></p>
                </div>
                <input type="file" id="exec-file" class="hidden" accept=".csv" onchange="handleFile(this, 'exec')">
            </div>
            <div class="card">
                <h3 class="font-bold text-slate-700 mb-3 flex items-center gap-2">
                    <i class="fas fa-file-csv text-blue-500"></i> קובץ תכנון (אופטיבוס) <span class="text-slate-400 text-xs">(אופציונלי)</span>
                </h3>
                <div id="plan-zone" class="upload-zone rounded-lg p-6 text-center cursor-pointer" onclick="document.getElementById('plan-file').click()">
                    <i class="fas fa-cloud-upload-alt text-3xl text-slate-400 mb-2"></i>
                    <p class="text-sm text-slate-600">גרור קובץ CSV או לחץ לבחירה</p>
                    <p id="plan-filename" class="text-xs text-slate-400 mt-1"></p>
                </div>
                <input type="file" id="plan-file" class="hidden" accept=".csv" onchange="handleFile(this, 'plan')">
            </div>
        </div>
        <div class="card bg-blue-50 border-blue-200 mb-6">
            <h4 class="font-bold text-blue-800 mb-2"><i class="fas fa-info-circle ml-1"></i> מידע על הנוסחאות</h4>
            <div class="text-sm text-blue-700 space-y-1">
                <p><strong>דקות/ק"מ</strong> = (שעות תשלום נהג × 60) / ק"מ תח"צ</p>
                <p><strong>יעילות נהג</strong> = זמן תח"צ / זמן עבודה כולל (יעד: ≥75%)</p>
                <p><strong>תח"צ</strong> = נסיעות עם מספר קו (service_trip באופטיבוס)</p>
            </div>
        </div>
        <!-- Manual KM Input -->
        <div id="manual-km-section" class="card bg-amber-50 border-amber-200 mb-6 hidden">
            <h4 class="font-bold text-amber-800 mb-2"><i class="fas fa-exclamation-triangle ml-1"></i> לא נמצאה עמודת מרחק בקובץ הביצוע</h4>
            <p class="text-sm text-amber-700 mb-3">הזן ק"מ תח"צ ידנית או השאר ריק לשימוש בנתוני התכנון:</p>
            <div class="flex gap-4 items-center">
                <div class="flex-1">
                    <label class="text-xs text-amber-600">ק"מ תח"צ ביצוע (אופציונלי)</label>
                    <input type="number" id="manual-km" placeholder="לדוגמא: 30000" class="w-full p-2 border rounded-lg text-sm mt-1">
                </div>
                <div class="text-xs text-amber-600 mt-4">
                    <span id="planning-km-hint"></span>
                </div>
            </div>
        </div>

        <button id="analyze-btn" onclick="runAnalysis()" disabled class="w-full bg-gradient-to-r from-blue-600 to-blue-700 text-white py-4 rounded-xl text-lg font-bold hover:from-blue-700 hover:to-blue-800 disabled:opacity-50 disabled:cursor-not-allowed transition-all flex items-center justify-center gap-2">
            <i class="fas fa-calculator"></i> הפעל ניתוח
        </button>
    </div>

    <div id="results-section" class="hidden">
        <div class="layout">
            <aside class="sidebar">
                <div><h2 class="text-lg font-black text-slate-800 flex items-center gap-2"><i class="fas fa-chart-pie text-blue-600"></i> תוצאות</h2><p class="text-xs text-slate-400 mt-1" id="analysis-date"></p></div>
                <div class="card border-r-4 border-blue-500"><div class="stat-lbl">דקות/ק"מ ביצוע</div><div class="stat-val text-blue-600" id="kpi-min-km">-</div><div class="compare-box" id="compare-min-km"></div></div>
                <div class="card border-r-4 border-cyan-500"><div class="stat-lbl">ק"מ תח"צ ביצוע</div><div class="stat-val text-cyan-600" id="kpi-pt-km">-</div><div class="compare-box" id="compare-pt-km"></div></div>
                <div class="card border-r-4 border-green-500"><div class="stat-lbl">% תח"צ ביצוע</div><div class="stat-val" id="kpi-pt-pct">-</div><div class="compare-box" id="compare-pt-pct"></div></div>
                <div class="card border-r-4 border-red-500"><div class="stat-lbl">נהגים מתחת 75%</div><div class="stat-val text-red-500" id="kpi-low-count">-</div><div class="stat-sub text-slate-400" id="kpi-low-sub"></div></div>
                <div class="card border-r-4 border-purple-500"><div class="stat-lbl">סה"כ נהגים</div><div class="stat-val text-slate-700" id="kpi-total-drivers">-</div></div>
                <div class="mt-auto space-y-2">
                    <button onclick="exportExcel()" class="w-full bg-green-600 text-white py-2.5 rounded-lg text-sm font-bold hover:bg-green-700 flex items-center justify-center gap-2"><i class="fas fa-file-excel"></i> ייצוא Excel</button>
                    <button onclick="downloadHTML()" class="w-full bg-slate-700 text-white py-2.5 rounded-lg text-sm font-bold hover:bg-slate-800 flex items-center justify-center gap-2"><i class="fas fa-download"></i> שמור דוח HTML</button>
                    <button onclick="resetAnalysis()" class="w-full bg-slate-200 text-slate-700 py-2.5 rounded-lg text-sm font-bold hover:bg-slate-300 flex items-center justify-center gap-2"><i class="fas fa-redo"></i> ניתוח חדש</button>
                </div>
            </aside>
            <main class="main">
                <div class="mb-4"><input type="text" id="search" onkeyup="filterTable()" placeholder="חיפוש..." class="w-full p-2.5 pr-4 border rounded-lg text-sm"></div>
                <div class="tabs-nav">
                    <div class="tab-btn active" onclick="showTab('drivers', this)"><i class="fas fa-user"></i> נהגים <span class="badge" id="badge-drivers">0</span></div>
                    <div class="tab-btn" onclick="showTab('low', this)"><i class="fas fa-exclamation-triangle"></i> מתחת 75% <span class="badge" id="badge-low">0</span></div>
                    <div class="tab-btn" onclick="showTab('planning', this)"><i class="fas fa-clipboard-list"></i> תכנון <span class="badge" id="badge-planning">0</span></div>
                    <div class="tab-btn" onclick="showTab('gaps', this)"><i class="fas fa-chart-bar"></i> ניתוח פערים</div>
                </div>
                <div id="view-drivers" class="view"><div class="table-wrap" style="max-height: calc(100vh - 280px); overflow-y: auto;"><table class="data-table" id="table-drivers"><thead><tr><th>תאריך</th><th>נהג</th><th>סידור</th><th>התחלה</th><th>סיום</th><th>דקות כולל</th><th>דקות תח"צ</th><th>ק"מ תח"צ</th><th>דק/ק"מ</th><th>% תח"צ</th><th>סטטוס</th></tr></thead><tbody></tbody></table></div></div>
                <div id="view-low" class="view hidden"><div class="table-wrap" style="max-height: calc(100vh - 280px); overflow-y: auto;"><table class="data-table" id="table-low"><thead><tr><th>תאריך</th><th>נהג</th><th>התחלה</th><th>סיום</th><th>דקות כולל</th><th>דקות תח"צ</th><th>% תח"צ</th><th>פער מ-75%</th></tr></thead><tbody></tbody></table></div></div>
                <div id="view-planning" class="view hidden"><div class="table-wrap" style="max-height: calc(100vh - 280px); overflow-y: auto;"><table class="data-table" id="table-planning"><thead><tr><th>סידור</th><th>דקות כולל</th><th>דקות תח"צ</th><th>ק"מ תח"צ</th><th>דק/ק"מ</th><th>% תח"צ</th><th>נסיעות</th></tr></thead><tbody></tbody></table></div></div>
                <div id="view-gaps" class="view hidden"><div id="gaps-container"></div></div>
            </main>
        </div>
    </div>

    <div id="detail-modal" class="modal hidden" onclick="if(event.target===this)closeModal()">
        <div class="modal-content">
            <div class="modal-header"><h3 class="text-lg font-bold" id="modal-title">פירוט</h3><span class="modal-close" onclick="closeModal()"><i class="fas fa-times"></i></span></div>
            <div class="modal-body" id="modal-body"></div>
        </div>
    </div>

<script>
let STATE = { execData: null, planData: null, execResults: [], planResults: [], gaps: [], driverDetails: {}, dutyDetails: {}, hasExecKm: false, planPtKm: 0, isNegev: false };
const CATEGORY_COLORS = { 'תח"צ': '#22c55e', 'הכנת מכונה': '#f59e0b', 'נסיעה ריקה': '#ef4444', 'המתנה': '#8b5cf6', 'הפסקה': '#06b6d4', 'לרשות': '#ec4899', 'אחר': '#64748b' };
const MAX_TRIP_KM = 200; // סף מקסימלי לנסיעה (לסינון חריגים)

function isNegevCluster(filename, data) {
    // זיהוי אשכול נגב לפי שם קובץ
    const fn = (filename || '').toLowerCase();
    if (fn.includes('נגב') || fn.includes('negev')) return true;
    // זיהוי לפי תוכן - חיפוש תחנות אופייניות לנגב
    const negevStations = ['ב"ש', 'באר שבע', 'דימונה', 'ערד', 'ירוחם', 'מצפה רמון', 'אופקים', 'נתיבות', 'שדרות'];
    const sampleDescs = (data || []).slice(0, 100).map(r => String(r['תאור'] || r['Description'] || '')).join(' ');
    return negevStations.some(s => sampleDescs.includes(s));
}

function handleFile(input, type) {
    const file = input.files[0]; if (!file) return;
    document.getElementById(type + '-zone').classList.add('has-file');
    document.getElementById(type + '-filename').textContent = file.name;
    Papa.parse(file, { header: true, encoding: 'UTF-8', complete: r => { 
        const data = r.data.filter(row => Object.values(row).some(v => v));
        if (type === 'exec') {
            STATE.execData = data;
            // בדיקה אם יש עמודת מרחק
            const cols = Object.keys(data[0] || {});
            STATE.hasExecKm = cols.some(c => c.includes('מרחק'));
            // זיהוי אשכול נגב
            STATE.isNegev = isNegevCluster(file.name, data);
            if (!STATE.hasExecKm) {
                document.getElementById('manual-km-section').classList.remove('hidden');
            } else {
                document.getElementById('manual-km-section').classList.add('hidden');
            }
        } else {
            STATE.planData = data;
            // זיהוי אשכול נגב גם מתכנון
            if (!STATE.isNegev) STATE.isNegev = isNegevCluster(file.name, data);
            // חישוב ק"מ תח"צ מתכנון (עם סינון חריגים)
            STATE.planPtKm = data.filter(r => r['Event Type'] === 'service_trip').reduce((sum, r) => {
                const km = parseFloat(r['Distance']) || 0;
                // סינון ק"מ חריג אם לא נגב
                if (!STATE.isNegev && km > MAX_TRIP_KM) return sum;
                return sum + km;
            }, 0);
            document.getElementById('planning-km-hint').textContent = `ק"מ תח"צ מתכנון: ${STATE.planPtKm.toFixed(0)}`;
        }
        updateAnalyzeButton(); 
    }});
}

function updateAnalyzeButton() {
    const btn = document.getElementById('analyze-btn'), status = document.getElementById('status-indicator');
    if (STATE.execData) { btn.disabled = false; status.innerHTML = '<i class="fas fa-check-circle text-green-500 ml-1"></i> מוכן לניתוח'; }
    else { btn.disabled = true; status.innerHTML = '<i class="fas fa-circle-info ml-1"></i> טען קובץ ביצוע'; }
}

function parseTime(t) { if (!t) return null; const p = String(t).trim().replace('.', ':').split(':'); return (parseInt(p[0])||0)*60 + (parseInt(p[1])||0); }
function getHour(t) { if (!t) return null; return parseInt(String(t).split(':')[0]); }
function formatMinutes(m) { if (m == null) return ''; return `${String(Math.floor(m/60)).padStart(2,'0')}:${String(m%60).padStart(2,'0')}`; }

function detectMidnightCrossing(starts, ends) {
    const hours = starts.concat(ends).map(t => getHour(t)).filter(h => h !== null);
    return hours.some(h => h >= 22) && hours.some(h => h < 6);
}

function parseDriverTimes(starts, ends) {
    const hasMidnight = detectMidnightCrossing(starts, ends);
    return starts.map((s, i) => {
        const e = ends[i], sh = getHour(s);
        let dayOff = (hasMidnight && sh !== null && sh < 6) ? 1 : 0;
        let sm = parseTime(s), em = parseTime(e);
        if (sm !== null) sm += dayOff * 1440;
        if (em !== null) em += dayOff * 1440;
        if (sm !== null && em !== null && em < sm && (em + 1440 - sm) <= 720) em += 1440;
        return { startMin: sm, endMin: em };
    });
}

function categorizeActivity(desc, isPT) {
    if (isPT) return 'תח"צ';
    const d = String(desc || '').toLowerCase();
    if (d.includes('הכנת מכונה')) return 'הכנת מכונה';
    if (d.includes('יציאה מחניון') || d.includes('חזרה לחניון') || d.includes('נסיעה ריקה')) return 'נסיעה ריקה';
    if (d.includes('הפסקה')) return 'הפסקה';
    if (d.includes('המתנה') || d.includes('standby')) return 'המתנה';
    if (d.includes('לרשות')) return 'לרשות';
    if (d.includes('תדלוק')) return 'אחר';
    return 'אחר';
}

function analyzeExecution() {
    const results = []; STATE.driverDetails = {};
    const grouped = {};
    
    // קבלת ק"מ ידני או מתכנון
    const manualKm = parseFloat(document.getElementById('manual-km')?.value) || 0;
    const useKmSource = STATE.hasExecKm ? 'exec' : (manualKm > 0 ? 'manual' : (STATE.planPtKm > 0 ? 'plan' : 'none'));
    
    STATE.execData.forEach(row => {
        const date = row['תאריך ייחוס'] || '', driver = row['קוד נהג'];
        if (!driver) return;
        const key = `${date}|${driver}`;
        if (!grouped[key]) grouped[key] = [];
        grouped[key].push(row);
    });
    
    let totalExecPtTrips = 0;
    Object.values(grouped).forEach(rows => {
        totalExecPtTrips += rows.filter(r => r['קו - מק"ט'] && r['קו - מק"ט'] !== '').length;
    });
    
    Object.entries(grouped).forEach(([key, rows]) => {
        const [date, driver] = key.split('|');
        const starts = rows.map(r => r['שעת התחלה']), ends = rows.map(r => r['שעת סיום']);
        const parsedTimes = parseDriverTimes(starts, ends);
        const activities = [], breakdown = {};
        let ptMinutes = 0, ptKm = 0, tripCount = 0;
        
        // איסוף קודי סידורים ייחודיים
        const dutyIds = [...new Set(rows.map(r => r['קוד סידור תכנון']).filter(d => d && !isNaN(d)))];
        
        rows.forEach((row, i) => {
            const isPT = row['קו - מק"ט'] && row['קו - מק"ט'] !== '';
            const { startMin, endMin } = parsedTimes[i];
            const duration = (startMin !== null && endMin !== null && endMin > startMin) ? endMin - startMin : 0;
            const category = categorizeActivity(row['תאור'], isPT);
            
            // קריאת ק"מ מעמודה אם קיימת
            let km = 0;
            if (STATE.hasExecKm) {
                const kmCol = Object.keys(row).find(c => c.includes('מרחק'));
                km = parseFloat(row[kmCol]) || 0;
                // סינון ק"מ חריג (מעל 200) - למעט אשכול נגב
                if (!STATE.isNegev && km > MAX_TRIP_KM) {
                    console.warn(`סינון ק"מ חריג: ${km} ק"מ בקו ${row['קו - מק"ט']}`);
                    km = 0;
                }
            }
            
            activities.push({ startTime: row['שעת התחלה'], endTime: row['שעת סיום'], startMin, endMin, duration, isPT, category, line: row['קו - מק"ט'] || '', description: row['תאור'] || '', km, dutyId: row['קוד סידור תכנון'] });
            if (!breakdown[category]) breakdown[category] = { minutes: 0, km: 0 };
            breakdown[category].minutes += duration; breakdown[category].km += km;
            if (isPT) { ptMinutes += duration; ptKm += km; tripCount++; }
        });
        
        activities.sort((a, b) => (a.startMin || 0) - (b.startMin || 0));
        const allTimes = parsedTimes.flatMap(t => [t.startMin, t.endMin]).filter(t => t !== null);
        const workStart = Math.min(...allTimes), workEnd = Math.max(...allTimes);
        
        // ביצוע: זמן עבודה = max-min (כולל המתנות שלא מדווחות)
        const totalMinutes = workEnd - workStart;
        // שעות תשלום = זמן עבודה ללא הכנת מכונה
        const machineMinutes = breakdown['הכנת מכונה']?.minutes || 0;
        const paymentMinutes = totalMinutes - machineMinutes;
        const nonPtMinutes = totalMinutes - ptMinutes;
        
        // חישוב ק"מ לפי מקור
        let effectivePtKm = ptKm;
        if (useKmSource === 'manual') {
            effectivePtKm = (manualKm / totalExecPtTrips) * tripCount;
        } else if (useKmSource === 'plan') {
            effectivePtKm = (STATE.planPtKm / totalExecPtTrips) * tripCount;
        }
        
        // דקות/ק"מ = שעות תשלום / ק"מ תח"צ
        const minPerKm = effectivePtKm > 0 ? paymentMinutes / effectivePtKm : 0;
        const ptPercent = totalMinutes > 0 ? (ptMinutes / totalMinutes) * 100 : 0;
        let status = ptPercent >= 75 ? 'תקין' : ptPercent >= 65 ? 'נמוך' : 'חריג';
        
        // בדיקת שלמות סידור - האם כל הנסיעות של הסידור בוצעו
        let dutyStatus = '';
        if (dutyIds.length === 0) {
            dutyStatus = 'ללא סידור';
        } else if (dutyIds.length === 1) {
            dutyStatus = 'מלא';
            // בדיקה מול התכנון אם קיים
            if (STATE.planData) {
                const planDuty = STATE.planData.filter(r => parseInt(r['Duty id']) === parseInt(dutyIds[0]) && r['Event Type'] === 'service_trip');
                const execTrips = activities.filter(a => a.isPT).length;
                if (planDuty.length > 0 && execTrips < planDuty.length) {
                    dutyStatus = `חלקי (${execTrips}/${planDuty.length})`;
                }
            }
        } else {
            dutyStatus = `${dutyIds.length} סידורים`;
        }
        
        STATE.driverDetails[key] = { activities, breakdown, summary: { totalMinutes, ptMinutes, nonPtMinutes, ptKm: effectivePtKm, paymentMinutes }, dutyIds };
        results.push({ date, driver: parseInt(driver), totalMinutes: Math.round(totalMinutes), paymentMinutes: Math.round(paymentMinutes), ptMinutes: Math.round(ptMinutes), nonPtMinutes: Math.round(nonPtMinutes), ptKm: Math.round(effectivePtKm * 100) / 100, minPerKm: Math.round(minPerKm * 100) / 100, ptPercent: Math.round(ptPercent * 10) / 10, status, tripCount, startTime: formatMinutes(workStart), endTime: formatMinutes(workEnd), breakdown, dutyIds, dutyStatus });
    });
    
    // שמירת מקור ק"מ
    STATE.kmSource = useKmSource;
    
    return results;
}

function analyzePlanning() {
    if (!STATE.planData) return [];
    const results = []; STATE.dutyDetails = {};
    const grouped = {};
    // Event types that count as "payment hours" (exclude sign_on and post_trip)
    const paymentEvents = ['service_trip', 'deadhead', 'depot_pull_out', 'depot_pull_in', 'standby', 'split'];
    STATE.planData.forEach(row => { const d = row['Duty id']; if (!d) return; if (!grouped[d]) grouped[d] = []; grouped[d].push(row); });
    Object.entries(grouped).forEach(([dutyId, rows]) => {
        const activities = [], breakdown = {}, allTimes = [];
        let ptMinutes = 0, ptKm = 0, tripCount = 0, paymentMinutes = 0;
        rows.forEach(row => {
            const dayOff = parseInt(row['Day Offset']) || 0;
            let sm = parseTime(row['Start Time']), em = parseTime(row['End Time']);
            if (sm !== null) sm += dayOff * 1440; if (em !== null) em += dayOff * 1440;
            if (sm !== null && em !== null && em < sm && (em + 1440 - sm) <= 720) em += 1440;
            if (sm !== null) allTimes.push(sm); if (em !== null) allTimes.push(em);
            const duration = (sm !== null && em !== null && em > sm) ? em - sm : 0;
            const et = row['Event Type'] || '', isPT = et === 'service_trip';
            let km = parseFloat(row['Distance']) || 0;
            // סינון ק"מ חריג (מעל 200) - למעט אשכול נגב
            if (!STATE.isNegev && km > MAX_TRIP_KM) {
                console.warn(`סינון ק"מ חריג בתכנון: ${km} ק"מ בקו ${row['Route Id']}`);
                km = 0;
            }
            let category = 'אחר';
            if (isPT) category = 'תח"צ';
            else if (et === 'deadhead' || et === 'depot_pull_out' || et === 'depot_pull_in') category = 'נסיעה ריקה';
            else if (et === 'standby') category = 'המתנה';
            else if (et === 'sign_on' || et === 'post_trip') category = 'הכנת מכונה';
            else if (et === 'split') category = 'הפסקה';
            activities.push({ startTime: row['Start Time'], endTime: row['End Time'], startMin: sm, endMin: em, duration, isPT, category, eventType: et, routeId: row['Route Id'] || '', km, sign: row['Sign'] || '', origin: row['Origin Stop Name'] || '', destination: row['Destination Stop Name'] || '' });
            if (!breakdown[category]) breakdown[category] = { minutes: 0, km: 0 };
            breakdown[category].minutes += duration; breakdown[category].km += km;
            if (isPT) { ptMinutes += duration; ptKm += km; tripCount++; }
            // שעות תשלום - ללא sign_on ו-post_trip
            if (paymentEvents.includes(et)) paymentMinutes += duration;
        });
        activities.sort((a, b) => (a.startMin || 0) - (b.startMin || 0));
        const dutyStart = Math.min(...allTimes), dutyEnd = Math.max(...allTimes), totalMinutes = dutyEnd - dutyStart;
        // דקות/ק"מ = שעות תשלום / ק"מ תח"צ
        const minPerKm = ptKm > 0 ? paymentMinutes / ptKm : 0, ptPercent = totalMinutes > 0 ? (ptMinutes / totalMinutes) * 100 : 0;
        STATE.dutyDetails[dutyId] = { activities, breakdown, summary: { totalMinutes, ptMinutes, ptKm, paymentMinutes } };
        results.push({ dutyId: parseInt(dutyId), totalMinutes: Math.round(totalMinutes), paymentMinutes: Math.round(paymentMinutes), ptMinutes: Math.round(ptMinutes), ptKm: Math.round(ptKm * 100) / 100, minPerKm: Math.round(minPerKm * 100) / 100, ptPercent: Math.round(ptPercent * 10) / 10, tripCount, breakdown });
    });
    return results;
}

function analyzeGaps() {
    const totalBreakdown = {}; let totalMinutes = 0, totalPtMinutes = 0, totalPtKm = 0, totalPaymentMinutes = 0;
    STATE.execResults.forEach(r => {
        totalMinutes += r.totalMinutes; totalPtMinutes += r.ptMinutes; totalPtKm += r.ptKm;
        totalPaymentMinutes += r.paymentMinutes || r.totalMinutes;
        Object.entries(r.breakdown || {}).forEach(([cat, data]) => {
            if (!totalBreakdown[cat]) totalBreakdown[cat] = { minutes: 0, km: 0 };
            totalBreakdown[cat].minutes += data.minutes; totalBreakdown[cat].km += data.km;
        });
    });
    // חישוב דקות/ק"מ = שעות תשלום / ק"מ תח"צ
    const execAvgMinKm = totalPtKm > 0 ? totalPaymentMinutes / totalPtKm : 0;
    
    let planAvgMinKm = 0, planPaymentMin = 0, planPtKm = 0;
    if (STATE.planResults.length > 0) {
        planPaymentMin = STATE.planResults.reduce((a, b) => a + (b.paymentMinutes !== undefined ? b.paymentMinutes : b.totalMinutes), 0);
        planPtKm = STATE.planResults.reduce((a, b) => a + b.ptKm, 0);
        planAvgMinKm = planPtKm > 0 ? planPaymentMin / planPtKm : 0;
    }
    
    return { summary: { execAvgMinKm, planAvgMinKm, gap: execAvgMinKm - planAvgMinKm, totalMinutes, totalPtMinutes, totalPtKm, nonPtMinutes: totalMinutes - totalPtMinutes, execPaymentMin: totalPaymentMinutes, planPaymentMin }, breakdown: totalBreakdown, lowDrivers: STATE.execResults.filter(r => r.ptPercent < 75) };
}

function runAnalysis() {
    STATE.execResults = analyzeExecution(); STATE.planResults = analyzePlanning(); STATE.gaps = analyzeGaps();
    updateKPIs(); renderTables(); renderGapsDetailed();
    document.getElementById('upload-section').classList.add('hidden'); document.getElementById('results-section').classList.remove('hidden');
    document.getElementById('analysis-date').textContent = new Date().toLocaleDateString('he-IL') + ' ' + new Date().toLocaleTimeString('he-IL');
}

function updateKPIs() {
    // חישוב דקות/ק"מ = שעות תשלום / ק"מ תח"צ
    const totalPaymentMin = STATE.execResults.reduce((a, b) => a + (b.paymentMinutes || b.totalMinutes), 0);
    const totalPtKm = STATE.execResults.reduce((a, b) => a + b.ptKm, 0);
    const execAvgMinKm = totalPtKm > 0 ? totalPaymentMin / totalPtKm : 0;
    const execAvgPt = STATE.execResults.reduce((a, b) => a + b.ptPercent, 0) / STATE.execResults.length || 0;
    const lowCount = STATE.execResults.filter(r => r.ptPercent < 75).length;
    document.getElementById('kpi-min-km').textContent = execAvgMinKm.toFixed(2);
    document.getElementById('kpi-pt-km').textContent = totalPtKm.toLocaleString('he-IL');
    document.getElementById('kpi-pt-pct').textContent = execAvgPt.toFixed(1) + '%';
    document.getElementById('kpi-pt-pct').className = `stat-val ${execAvgPt >= 75 ? 'text-green-600' : 'text-red-500'}`;
    document.getElementById('kpi-low-count').textContent = lowCount;
    document.getElementById('kpi-low-sub').textContent = `מתוך ${STATE.execResults.length} נהגים`;
    document.getElementById('kpi-total-drivers').textContent = STATE.execResults.length;
    
    // הוספת הערה על מקור ק"מ
    let kmSourceNote = '';
    if (STATE.kmSource === 'plan') kmSourceNote = '<div class="text-xs text-amber-600 mt-1"><i class="fas fa-info-circle"></i> ק"מ מתכנון</div>';
    else if (STATE.kmSource === 'manual') kmSourceNote = '<div class="text-xs text-amber-600 mt-1"><i class="fas fa-info-circle"></i> ק"מ ידני</div>';
    else if (STATE.kmSource === 'none') kmSourceNote = '<div class="text-xs text-red-500 mt-1"><i class="fas fa-exclamation-triangle"></i> אין נתוני ק"מ</div>';
    
    if (STATE.planResults.length > 0) {
        // לתכנון: שימוש ב-paymentMinutes (ללא sign_on/post_trip)
        const planPaymentMin = STATE.planResults.reduce((a, b) => a + (b.paymentMinutes !== undefined ? b.paymentMinutes : b.totalMinutes), 0);
        const planTotalPtKm = STATE.planResults.reduce((a, b) => a + b.ptKm, 0);
        const planAvgMinKm = planTotalPtKm > 0 ? planPaymentMin / planTotalPtKm : 0;
        const planAvgPt = STATE.planResults.reduce((a, b) => a + b.ptPercent, 0) / STATE.planResults.length;
        document.getElementById('compare-min-km').innerHTML = `<div><div class="compare-label">תכנון</div><div class="compare-val">${planAvgMinKm.toFixed(2)}</div></div><div class="text-lg ${execAvgMinKm > planAvgMinKm ? 'text-red-500' : 'text-green-500'}">${execAvgMinKm > planAvgMinKm ? '↑' : '↓'} ${Math.abs(execAvgMinKm - planAvgMinKm).toFixed(2)}</div>${kmSourceNote}`;
        document.getElementById('compare-pt-km').innerHTML = `<div><div class="compare-label">תכנון</div><div class="compare-val">${planTotalPtKm.toLocaleString('he-IL')}</div></div>`;
        document.getElementById('compare-pt-pct').innerHTML = `<div><div class="compare-label">תכנון</div><div class="compare-val">${planAvgPt.toFixed(1)}%</div></div><div><div class="compare-label">יעד</div><div class="compare-val text-green-600">75%</div></div>`;
    } else {
        document.getElementById('compare-min-km').innerHTML = '<span class="text-slate-400 text-xs">אין תכנון</span>' + kmSourceNote;
        document.getElementById('compare-pt-km').innerHTML = '';
        document.getElementById('compare-pt-pct').innerHTML = `<div><div class="compare-label">יעד</div><div class="compare-val text-green-600">75%</div></div>`;
    }
    document.getElementById('badge-drivers').textContent = STATE.execResults.length;
    document.getElementById('badge-low').textContent = lowCount;
    document.getElementById('badge-planning').textContent = STATE.planResults.length;
}

function renderTables() {
    document.querySelector('#table-drivers tbody').innerHTML = STATE.execResults.map(r => {
        // עמודת סידורים - עם לחיצה לפרטים
        let dutyCell = '';
        if (r.dutyIds && r.dutyIds.length > 0) {
            const dutyLinks = r.dutyIds.map(d => `<span class="clickable text-blue-600" onclick="showDutyDetail(${parseInt(d)})">${parseInt(d)}</span>`).join(', ');
            const statusClass = r.dutyStatus === 'מלא' ? 'text-green-600' : r.dutyStatus.includes('חלקי') ? 'text-amber-600' : r.dutyIds.length > 1 ? 'text-purple-600' : '';
            dutyCell = `<div>${dutyLinks}</div><div class="text-xs ${statusClass}">${r.dutyStatus}</div>`;
        } else {
            dutyCell = '<span class="text-slate-400">-</span>';
        }
        return `<tr><td>${r.date}</td><td class="font-bold clickable" onclick="showDriverDetail('${r.date}', ${r.driver})">${r.driver}</td><td>${dutyCell}</td><td class="font-mono text-xs">${r.startTime}</td><td class="font-mono text-xs">${r.endTime}</td><td>${r.totalMinutes}</td><td>${r.ptMinutes}</td><td>${r.ptKm}</td><td class="font-bold">${r.minPerKm}</td><td class="font-bold ${r.ptPercent >= 75 ? 'text-green-600' : 'text-red-500'}">${r.ptPercent}%</td><td><span class="${r.status === 'תקין' ? 'status-ok' : r.status === 'נמוך' ? 'status-warn' : 'status-bad'}">${r.status}</span></td></tr>`;
    }).join('');
    document.querySelector('#table-low tbody').innerHTML = STATE.execResults.filter(r => r.ptPercent < 75).map(r => `<tr><td>${r.date}</td><td class="font-bold clickable" onclick="showDriverDetail('${r.date}', ${r.driver})">${r.driver}</td><td class="font-mono text-xs">${r.startTime}</td><td class="font-mono text-xs">${r.endTime}</td><td>${r.totalMinutes}</td><td>${r.ptMinutes}</td><td class="font-bold text-red-500">${r.ptPercent}%</td><td class="font-bold text-red-600">-${(75 - r.ptPercent).toFixed(1)}%</td></tr>`).join('');
    document.querySelector('#table-planning tbody').innerHTML = STATE.planResults.map(r => `<tr><td class="font-bold clickable" onclick="showDutyDetail(${r.dutyId})">${r.dutyId}</td><td>${r.totalMinutes}</td><td>${r.ptMinutes}</td><td>${r.ptKm}</td><td class="font-bold">${r.minPerKm}</td><td>${r.ptPercent}%</td><td>${r.tripCount}</td></tr>`).join('');
}

function renderGapsDetailed() {
    const gaps = STATE.gaps, c = document.getElementById('gaps-container');
    
    // Build planning breakdown
    const planBreakdown = {};
    let planTotalMin = 0, planTotalKm = 0;
    STATE.planResults.forEach(r => {
        Object.entries(r.breakdown || {}).forEach(([cat, data]) => {
            if (!planBreakdown[cat]) planBreakdown[cat] = { minutes: 0, km: 0 };
            planBreakdown[cat].minutes += data.minutes;
            planBreakdown[cat].km += data.km;
        });
        planTotalMin += r.totalMinutes;
    });
    Object.values(planBreakdown).forEach(d => planTotalKm += d.km);
    
    // All categories
    const allCats = [...new Set([...Object.keys(gaps.breakdown), ...Object.keys(planBreakdown)])];
    
    // Category descriptions
    const catDesc = {
        'תח"צ': 'נסיעות תחבורה ציבורית עם נוסעים (service_trip)',
        'נסיעה ריקה': 'יציאה מחניון, חזרה לחניון, נסיעות ריקות בין קווים (deadhead, depot_pull)',
        'הכנת מכונה': 'בדיקת רכב, sign_on, post_trip',
        'המתנה': 'זמן המתנה בין נסיעות (standby)',
        'הפסקה': 'הפסקות נהג (split)',
        'לרשות': 'זמן לרשות סדרן - המתנה להקצאה',
        'אחר': 'תדלוק, פעולות אחרות'
    };
    
    const barHtml = Object.entries(gaps.breakdown).sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => {
        const pct = (data.minutes / gaps.summary.totalMinutes * 100).toFixed(1), color = CATEGORY_COLORS[cat] || '#64748b';
        return `<div class="breakdown-segment" style="width:${pct}%; background:${color}" title="${cat}: ${Math.round(data.minutes)} דק">${pct > 5 ? pct + '%' : ''}</div>`;
    }).join('');
    
    c.innerHTML = `
        <div class="gap-card"><div class="gap-title"><i class="fas fa-chart-pie ml-2 text-blue-500"></i> סיכום דקות/ק"מ</div>
        <div class="gap-breakdown"><div class="gap-item"><div class="gap-item-value text-blue-600">${gaps.summary.execAvgMinKm.toFixed(2)}</div><div class="gap-item-label">דק/ק"מ ביצוע</div></div>
        ${STATE.planResults.length > 0 ? `<div class="gap-item"><div class="gap-item-value text-slate-600">${gaps.summary.planAvgMinKm.toFixed(2)}</div><div class="gap-item-label">דק/ק"מ תכנון</div></div><div class="gap-item"><div class="gap-item-value ${gaps.summary.gap > 0 ? 'text-red-500' : 'text-green-500'}">${gaps.summary.gap > 0 ? '+' : ''}${gaps.summary.gap.toFixed(2)}</div><div class="gap-item-label">פער</div></div>` : ''}</div></div>
        
        <!-- Comparison Table -->
        ${STATE.planResults.length > 0 ? `
        <div class="gap-card">
            <div class="gap-title"><i class="fas fa-balance-scale ml-2 text-indigo-500"></i> השוואת תכנון מול ביצוע לפי קטגוריה</div>
            <div class="overflow-x-auto">
                <table class="w-full text-sm border-collapse">
                    <thead>
                        <tr class="bg-slate-100">
                            <th class="p-3 text-right font-bold border-b-2">קטגוריה</th>
                            <th colspan="3" class="p-3 text-center font-bold border-b-2 bg-blue-50">תכנון</th>
                            <th colspan="3" class="p-3 text-center font-bold border-b-2 bg-green-50">ביצוע</th>
                            <th colspan="3" class="p-3 text-center font-bold border-b-2 bg-amber-50">פער (ביצוע - תכנון)</th>
                        </tr>
                        <tr class="bg-slate-50 text-xs">
                            <th class="p-2 text-right border-b"></th>
                            <th class="p-2 text-center border-b bg-blue-50">דקות</th>
                            <th class="p-2 text-center border-b bg-blue-50">ק"מ</th>
                            <th class="p-2 text-center border-b bg-blue-50">%</th>
                            <th class="p-2 text-center border-b bg-green-50">דקות</th>
                            <th class="p-2 text-center border-b bg-green-50">ק"מ</th>
                            <th class="p-2 text-center border-b bg-green-50">%</th>
                            <th class="p-2 text-center border-b bg-amber-50">דקות</th>
                            <th class="p-2 text-center border-b bg-amber-50">ק"מ</th>
                            <th class="p-2 text-center border-b bg-amber-50">%</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${allCats.sort((a,b) => {
                            const order = ['תח"צ', 'נסיעה ריקה', 'הכנת מכונה', 'המתנה', 'הפסקה', 'לרשות', 'אחר'];
                            return order.indexOf(a) - order.indexOf(b);
                        }).map(cat => {
                            const plan = planBreakdown[cat] || { minutes: 0, km: 0 };
                            const exec = gaps.breakdown[cat] || { minutes: 0, km: 0 };
                            const planPct = planTotalMin > 0 ? (plan.minutes / planTotalMin * 100) : 0;
                            const execPct = gaps.summary.totalMinutes > 0 ? (exec.minutes / gaps.summary.totalMinutes * 100) : 0;
                            const diffMin = exec.minutes - plan.minutes;
                            const diffKm = exec.km - plan.km;
                            const diffPct = execPct - planPct;
                            const color = CATEGORY_COLORS[cat] || '#64748b';
                            return `
                            <tr class="border-b hover:bg-slate-50">
                                <td class="p-3 font-bold" style="border-right: 4px solid ${color}">
                                    ${cat}
                                    <div class="text-xs text-slate-400 font-normal">${catDesc[cat] || ''}</div>
                                </td>
                                <td class="p-2 text-center bg-blue-50/30">${Math.round(plan.minutes).toLocaleString()}</td>
                                <td class="p-2 text-center bg-blue-50/30">${plan.km.toFixed(1)}</td>
                                <td class="p-2 text-center bg-blue-50/30 font-bold">${planPct.toFixed(1)}%</td>
                                <td class="p-2 text-center bg-green-50/30">${Math.round(exec.minutes).toLocaleString()}</td>
                                <td class="p-2 text-center bg-green-50/30">${exec.km.toFixed(1)}</td>
                                <td class="p-2 text-center bg-green-50/30 font-bold">${execPct.toFixed(1)}%</td>
                                <td class="p-2 text-center bg-amber-50/30 font-bold ${diffMin > 0 ? 'text-red-600' : diffMin < 0 ? 'text-green-600' : ''}">${diffMin > 0 ? '+' : ''}${Math.round(diffMin).toLocaleString()}</td>
                                <td class="p-2 text-center bg-amber-50/30 ${diffKm > 0 ? 'text-red-600' : diffKm < 0 ? 'text-green-600' : ''}">${diffKm > 0 ? '+' : ''}${diffKm.toFixed(1)}</td>
                                <td class="p-2 text-center bg-amber-50/30 font-bold ${diffPct > 0 ? 'text-red-600' : diffPct < 0 ? 'text-green-600' : ''}">${diffPct > 0 ? '+' : ''}${diffPct.toFixed(1)}%</td>
                            </tr>`;
                        }).join('')}
                        <tr class="bg-slate-200 font-bold">
                            <td class="p-3">סה"כ</td>
                            <td class="p-2 text-center">${Math.round(planTotalMin).toLocaleString()}</td>
                            <td class="p-2 text-center">${Object.values(planBreakdown).reduce((a,b) => a + b.km, 0).toFixed(1)}</td>
                            <td class="p-2 text-center">100%</td>
                            <td class="p-2 text-center">${Math.round(gaps.summary.totalMinutes).toLocaleString()}</td>
                            <td class="p-2 text-center">${Object.values(gaps.breakdown).reduce((a,b) => a + b.km, 0).toFixed(1)}</td>
                            <td class="p-2 text-center">100%</td>
                            <td class="p-2 text-center ${gaps.summary.totalMinutes - planTotalMin > 0 ? 'text-red-600' : 'text-green-600'}">${gaps.summary.totalMinutes - planTotalMin > 0 ? '+' : ''}${Math.round(gaps.summary.totalMinutes - planTotalMin).toLocaleString()}</td>
                            <td class="p-2 text-center">-</td>
                            <td class="p-2 text-center">-</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="mt-4 p-3 bg-indigo-50 rounded-lg text-sm text-indigo-700">
                <i class="fas fa-info-circle ml-1"></i> <strong>הסבר הקטגוריות:</strong><br>
                <span class="text-xs">
                • <strong>תח"צ</strong> - נסיעות שירות עם נוסעים<br>
                • <strong>נסיעה ריקה</strong> - יציאה/חזרה מחניון, מעברים בין קווים<br>
                • <strong>הכנת מכונה</strong> - בדיקות רכב בתחילת/סוף משמרת<br>
                • <strong>המתנה</strong> - זמן המתנה מתוכנן בין נסיעות<br>
                • <strong>הפסקה</strong> - הפסקות נהג<br>
                • <strong>לרשות</strong> - זמן לרשות סדרן (ביצוע בלבד)<br>
                • <strong>אחר</strong> - תדלוק, פעולות שונות
                </span>
            </div>
        </div>
        ` : ''}
        
        <div class="gap-card"><div class="gap-title"><i class="fas fa-clock ml-2 text-purple-500"></i> פילוח זמן ביצוע</div><div class="mb-4"><div class="breakdown-bar">${barHtml}</div></div>
        <div class="gap-breakdown">${Object.entries(gaps.breakdown).sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => {
            const pct = (data.minutes / gaps.summary.totalMinutes * 100).toFixed(1), color = CATEGORY_COLORS[cat], hours = (data.minutes / 60).toFixed(1);
            return `<div class="gap-item" style="border-right: 4px solid ${color}"><div class="gap-item-value" style="color:${color}">${Math.round(data.minutes)}</div><div class="gap-item-label">${cat}</div><div class="text-xs text-slate-500">${hours} שעות (${pct}%)</div></div>`;
        }).join('')}</div></div>
        
        <div class="gap-card"><div class="gap-title"><i class="fas fa-exclamation-triangle ml-2 text-amber-500"></i> השפעה על דקות/ק"מ לפי קטגוריה</div>
        <div class="space-y-3">${Object.entries(gaps.breakdown).filter(([cat]) => cat !== 'תח"צ').sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => {
            const color = CATEGORY_COLORS[cat], impact = gaps.summary.totalPtKm > 0 ? data.minutes / gaps.summary.totalPtKm : 0, pctNonPt = gaps.summary.nonPtMinutes > 0 ? (data.minutes / gaps.summary.nonPtMinutes * 100) : 0;
            return `<div class="flex items-center gap-4 p-3 bg-slate-50 rounded-lg"><div class="w-3 h-3 rounded-full" style="background:${color}"></div><div class="flex-1"><div class="font-bold text-slate-700">${cat}</div><div class="text-xs text-slate-500">${Math.round(data.minutes)} דקות (${pctNonPt.toFixed(1)}% מזמן לא-תח"צ)</div></div><div class="text-left"><div class="font-bold text-lg" style="color:${color}">+${impact.toFixed(2)}</div><div class="text-xs text-slate-500">דק/ק"מ</div></div></div>`;
        }).join('')}</div>
        <div class="mt-4 p-3 bg-blue-50 rounded-lg text-sm text-blue-700"><i class="fas fa-lightbulb ml-1"></i> <strong>הסבר:</strong> כל קטגוריה מוסיפה לדקות/ק"מ את הזמן שלה חלקי סה"כ ק"מ תח"צ (${gaps.summary.totalPtKm.toFixed(0)} ק"מ).</div></div>
        
        <div class="gap-card"><div class="gap-title"><i class="fas fa-users ml-2 text-red-500"></i> נהגים מתחת 75% תח"צ</div>
        <div class="gap-breakdown"><div class="gap-item"><div class="gap-item-value text-red-500">${gaps.lowDrivers.length}</div><div class="gap-item-label">נהגים</div></div>
        <div class="gap-item"><div class="gap-item-value text-slate-600">${gaps.lowDrivers.length > 0 ? (gaps.lowDrivers.reduce((a,b) => a + b.ptPercent, 0) / gaps.lowDrivers.length).toFixed(1) : 0}%</div><div class="gap-item-label">ממוצע % תח"צ</div></div>
        <div class="gap-item"><div class="gap-item-value text-amber-500">${gaps.lowDrivers.length > 0 ? (gaps.lowDrivers.reduce((a,b) => a + b.minPerKm, 0) / gaps.lowDrivers.length).toFixed(2) : 0}</div><div class="gap-item-label">ממוצע דק/ק"מ</div></div></div></div>`;
}

function showDriverDetail(date, driver) {
    const d = STATE.driverDetails[`${date}|${driver}`]; if (!d) return;
    document.getElementById('modal-title').innerHTML = `<i class="fas fa-user ml-2"></i> נהג ${driver} - ${date}`;
    const barHtml = Object.entries(d.breakdown).sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => {
        const pct = (data.minutes / d.summary.totalMinutes * 100).toFixed(1), color = CATEGORY_COLORS[cat];
        return `<div class="breakdown-segment" style="width:${pct}%; background:${color}" title="${cat}: ${Math.round(data.minutes)} דק">${pct > 8 ? cat : ''}</div>`;
    }).join('');
    
    // פירוט פעילויות עם מספר סידור
    const activitiesHtml = d.activities.map(a => {
        const dutyId = a.dutyId && !isNaN(a.dutyId) ? parseInt(a.dutyId) : null;
        const dutyCell = dutyId ? `<span class="clickable text-blue-600 text-xs" onclick="showDutyDetail(${dutyId})">${dutyId}</span>` : '<span class="text-slate-300">-</span>';
        return `<div class="activity-row with-duty ${a.isPT ? 'activity-pt' : 'activity-non-pt'}"><div class="font-mono text-xs">${a.startTime} - ${a.endTime}</div><div><span class="inline-block w-2 h-2 rounded mr-1" style="background:${CATEGORY_COLORS[a.category]}"></span>${a.isPT ? `<strong>קו ${parseInt(a.line)}</strong> - ` : ''}${a.description || a.category}</div><div class="font-bold">${a.duration} דק</div><div>${a.km > 0 ? a.km.toFixed(1) : '-'}</div><div>${dutyCell}</div></div>`;
    }).join('');
    
    document.getElementById('modal-body').innerHTML = `
        <div class="grid grid-cols-4 gap-4 mb-6">
            <div class="bg-blue-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-blue-600">${d.summary.totalMinutes}</div><div class="text-xs text-slate-500">דקות כולל</div></div>
            <div class="bg-green-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-green-600">${d.summary.ptMinutes}</div><div class="text-xs text-slate-500">דקות תח"צ</div></div>
            <div class="bg-amber-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-amber-600">${d.summary.nonPtMinutes}</div><div class="text-xs text-slate-500">דקות לא-תח"צ</div></div>
            <div class="bg-purple-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-purple-600">${d.summary.ptKm.toFixed(1)}</div><div class="text-xs text-slate-500">ק"מ תח"צ</div></div>
        </div>
        <div class="mb-6"><div class="text-sm font-bold text-slate-700 mb-2">פילוח זמן</div><div class="breakdown-bar">${barHtml}</div>
        <div class="flex flex-wrap gap-3 mt-2">${Object.entries(d.breakdown).sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => `<div class="flex items-center gap-1 text-xs"><div class="w-3 h-3 rounded" style="background:${CATEGORY_COLORS[cat]}"></div><span>${cat}: ${Math.round(data.minutes)} דק (${(data.minutes / d.summary.totalMinutes * 100).toFixed(1)}%)</span></div>`).join('')}</div></div>
        <div class="text-sm font-bold text-slate-700 mb-2">פירוט פעילויות</div>
        <div class="border rounded-lg overflow-hidden"><div class="activity-row with-duty bg-slate-100 font-bold text-xs"><div>שעה</div><div>תיאור</div><div>משך</div><div>ק"מ</div><div>סידור</div></div>
        <div style="max-height: 400px; overflow-y: auto;">${activitiesHtml}</div></div>`;
    document.getElementById('detail-modal').classList.remove('hidden');
}

function showDutyDetail(dutyId) {
    const d = STATE.dutyDetails[dutyId]; 
    if (!d) {
        // אם הסידור לא נמצא בתכנון, הצג הודעה
        document.getElementById('modal-title').innerHTML = `<i class="fas fa-clipboard-list ml-2"></i> סידור ${dutyId}`;
        document.getElementById('modal-body').innerHTML = `<div class="text-center py-8 text-slate-500"><i class="fas fa-info-circle text-4xl mb-4"></i><p>סידור ${dutyId} לא נמצא בקובץ התכנון</p></div>`;
        document.getElementById('detail-modal').classList.remove('hidden');
        return;
    }
    document.getElementById('modal-title').innerHTML = `<i class="fas fa-clipboard-list ml-2"></i> סידור ${dutyId}`;
    const barHtml = Object.entries(d.breakdown).sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => {
        const pct = (data.minutes / d.summary.totalMinutes * 100).toFixed(1), color = CATEGORY_COLORS[cat];
        return `<div class="breakdown-segment" style="width:${pct}%; background:${color}" title="${cat}: ${Math.round(data.minutes)} דק">${pct > 8 ? cat : ''}</div>`;
    }).join('');
    
    // פירוט אירועים עם תיאור מלא
    const activitiesHtml = d.activities.map(a => {
        let description = '';
        if (a.isPT) {
            // נסיעת תח"צ - הצג קו ומסלול
            const lineNum = a.sign || (a.routeId ? a.routeId.split('-')[0] : '');
            description = `<strong>קו ${lineNum}</strong>`;
            if (a.origin && a.destination) {
                description += `<br><span class="text-xs text-slate-500">${a.origin} → ${a.destination}</span>`;
            }
        } else if (a.eventType === 'deadhead' || a.eventType === 'depot_pull_out' || a.eventType === 'depot_pull_in') {
            // נסיעה ריקה
            const typeLabel = a.eventType === 'depot_pull_out' ? 'יציאה מחניון' : a.eventType === 'depot_pull_in' ? 'חזרה לחניון' : 'נסיעה ריקה';
            description = `<strong>${typeLabel}</strong>`;
            if (a.origin && a.destination && a.origin !== a.destination) {
                description += `<br><span class="text-xs text-slate-500">${a.origin} → ${a.destination}</span>`;
            }
        } else {
            // שאר האירועים
            const labels = { 'sign_on': 'הכנת מכונה', 'post_trip': 'סיום', 'standby': 'המתנה', 'split': 'הפסקה' };
            description = `<strong>${labels[a.eventType] || a.eventType}</strong>`;
            if (a.origin) description += `<br><span class="text-xs text-slate-500">${a.origin}</span>`;
        }
        return `<div class="activity-row ${a.isPT ? 'activity-pt' : 'activity-non-pt'}"><div class="font-mono text-xs">${a.startTime} - ${a.endTime}</div><div><span class="inline-block w-2 h-2 rounded mr-1" style="background:${CATEGORY_COLORS[a.category]}"></span>${description}</div><div class="font-bold">${a.duration} דק</div><div>${a.km > 0 ? a.km.toFixed(1) : '-'}</div></div>`;
    }).join('');
    
    document.getElementById('modal-body').innerHTML = `
        <div class="grid grid-cols-3 gap-4 mb-6">
            <div class="bg-blue-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-blue-600">${d.summary.totalMinutes}</div><div class="text-xs text-slate-500">דקות כולל</div></div>
            <div class="bg-green-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-green-600">${d.summary.ptMinutes}</div><div class="text-xs text-slate-500">דקות תח"צ</div></div>
            <div class="bg-purple-50 p-4 rounded-lg text-center"><div class="text-2xl font-bold text-purple-600">${d.summary.ptKm.toFixed(1)}</div><div class="text-xs text-slate-500">ק"מ תח"צ</div></div>
        </div>
        <div class="mb-6"><div class="text-sm font-bold text-slate-700 mb-2">פילוח זמן</div><div class="breakdown-bar">${barHtml}</div>
        <div class="flex flex-wrap gap-3 mt-2">${Object.entries(d.breakdown).sort((a,b) => b[1].minutes - a[1].minutes).map(([cat, data]) => `<div class="flex items-center gap-1 text-xs"><div class="w-3 h-3 rounded" style="background:${CATEGORY_COLORS[cat]}"></div><span>${cat}: ${Math.round(data.minutes)} דק (${(data.minutes / d.summary.totalMinutes * 100).toFixed(1)}%)</span></div>`).join('')}</div></div>
        <div class="text-sm font-bold text-slate-700 mb-2">פירוט אירועים</div>
        <div class="border rounded-lg overflow-hidden"><div class="activity-row bg-slate-100 font-bold text-xs"><div>שעה</div><div>תיאור</div><div>משך</div><div>ק"מ</div></div>
        ${activitiesHtml}</div>`;
    document.getElementById('detail-modal').classList.remove('hidden');
}

function closeModal() { document.getElementById('detail-modal').classList.add('hidden'); }
function showTab(id, btn) { document.querySelectorAll('.view').forEach(v => v.classList.add('hidden')); document.getElementById('view-' + id).classList.remove('hidden'); document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active')); btn.classList.add('active'); }
function filterTable() { const v = document.getElementById('search').value.toLowerCase(); document.querySelectorAll('tbody tr').forEach(r => r.style.display = r.innerText.toLowerCase().includes(v) ? '' : 'none'); }
function resetAnalysis() { STATE = { execData: null, planData: null, execResults: [], planResults: [], gaps: [], driverDetails: {}, dutyDetails: {}, hasExecKm: false, planPtKm: 0, isNegev: false }; ['exec','plan'].forEach(t => { document.getElementById(t+'-zone').classList.remove('has-file'); document.getElementById(t+'-filename').textContent = ''; document.getElementById(t+'-file').value = ''; }); document.getElementById('results-section').classList.add('hidden'); document.getElementById('upload-section').classList.remove('hidden'); document.getElementById('manual-km-section').classList.add('hidden'); if(document.getElementById('manual-km')) document.getElementById('manual-km').value = ''; updateAnalyzeButton(); }

function exportExcel() {
    const wb = XLSX.utils.book_new(), gaps = STATE.gaps;
    
    // Summary
    XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet([{ 'מדד': 'דק/ק"מ ביצוע', 'ערך': gaps.summary.execAvgMinKm.toFixed(2) }, { 'מדד': 'דק/ק"מ תכנון', 'ערך': gaps.summary.planAvgMinKm.toFixed(2) }, { 'מדד': 'פער', 'ערך': gaps.summary.gap.toFixed(2) }, { 'מדד': 'נהגים מתחת 75%', 'ערך': gaps.lowDrivers.length }]), 'סיכום');
    
    // Comparison table - Planning vs Execution
    if (STATE.planResults.length > 0) {
        const planBreakdown = {};
        let planTotalMin = 0;
        STATE.planResults.forEach(r => {
            Object.entries(r.breakdown || {}).forEach(([cat, data]) => {
                if (!planBreakdown[cat]) planBreakdown[cat] = { minutes: 0, km: 0 };
                planBreakdown[cat].minutes += data.minutes;
                planBreakdown[cat].km += data.km;
            });
            planTotalMin += r.totalMinutes;
        });
        
        const allCats = [...new Set([...Object.keys(gaps.breakdown), ...Object.keys(planBreakdown)])];
        const comparisonData = allCats.map(cat => {
            const plan = planBreakdown[cat] || { minutes: 0, km: 0 };
            const exec = gaps.breakdown[cat] || { minutes: 0, km: 0 };
            const planPct = planTotalMin > 0 ? (plan.minutes / planTotalMin * 100) : 0;
            const execPct = gaps.summary.totalMinutes > 0 ? (exec.minutes / gaps.summary.totalMinutes * 100) : 0;
            return {
                'קטגוריה': cat,
                'תכנון_דקות': Math.round(plan.minutes),
                'תכנון_קמ': plan.km.toFixed(1),
                'תכנון_%': planPct.toFixed(1) + '%',
                'ביצוע_דקות': Math.round(exec.minutes),
                'ביצוע_קמ': exec.km.toFixed(1),
                'ביצוע_%': execPct.toFixed(1) + '%',
                'פער_דקות': Math.round(exec.minutes - plan.minutes),
                'פער_קמ': (exec.km - plan.km).toFixed(1),
                'פער_%': (execPct - planPct).toFixed(1) + '%'
            };
        });
        XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(comparisonData), 'השוואה_תכנון_ביצוע');
    }
    
    // Breakdown
    XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(Object.entries(gaps.breakdown).map(([c, d]) => ({ 'קטגוריה': c, 'דקות': Math.round(d.minutes), 'שעות': (d.minutes/60).toFixed(1), '%': (d.minutes/gaps.summary.totalMinutes*100).toFixed(1)+'%', 'תוספת_דק_קמ': (d.minutes/gaps.summary.totalPtKm).toFixed(2) }))), 'פילוח_ביצוע');
    
    // Drivers
    XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(STATE.execResults.map(r => ({ 'תאריך': r.date, 'נהג': r.driver, 'דקות_כולל': r.totalMinutes, 'דקות_תחצ': r.ptMinutes, 'קמ_תחצ': r.ptKm, 'דקות_לקמ': r.minPerKm, '%_תחצ': r.ptPercent, 'סטטוס': r.status }))), 'נהגים');
    
    // Low efficiency
    XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(gaps.lowDrivers.map(r => ({ 'תאריך': r.date, 'נהג': r.driver, 'דקות_כולל': r.totalMinutes, 'דקות_תחצ': r.ptMinutes, '%_תחצ': r.ptPercent, 'פער': (75-r.ptPercent).toFixed(1) }))), 'מתחת_75');
    
    // Planning
    if (STATE.planResults.length > 0) XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(STATE.planResults.map(r => ({ 'סידור': r.dutyId, 'דקות_כולל': r.totalMinutes, 'דקות_תחצ': r.ptMinutes, 'קמ_תחצ': r.ptKm, 'דקות_לקמ': r.minPerKm, '%_תחצ': r.ptPercent }))), 'תכנון');
    
    XLSX.writeFile(wb, 'efficiency_analysis.xlsx');
}

function downloadHTML() { const a = document.createElement('a'); a.href = URL.createObjectURL(new Blob([document.documentElement.outerHTML], {type:'text/html'})); a.download = 'efficiency_report.html'; a.click(); }

['exec-zone', 'plan-zone'].forEach(id => { const z = document.getElementById(id), t = id.split('-')[0]; z.addEventListener('dragover', e => { e.preventDefault(); z.classList.add('dragover'); }); z.addEventListener('dragleave', () => z.classList.remove('dragover')); z.addEventListener('drop', e => { e.preventDefault(); z.classList.remove('dragover'); if (e.dataTransfer.files[0]) { document.getElementById(t+'-file').files = e.dataTransfer.files; handleFile(document.getElementById(t+'-file'), t); }}); });
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });
</script>
</body>
</html>
