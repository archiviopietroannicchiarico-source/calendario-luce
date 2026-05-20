[calendario_perpetuo_se_nella_luce.html](https://github.com/user-attachments/files/28070647/calendario_perpetuo_se_nella_luce.html)

<style>
  @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Cinzel:wght@400;600&display=swap');

  :root {
    --gold: #B8974A;
    --gold-light: #E8D5A3;
    --gold-dark: #7A6230;
    --ink: #1A1510;
    --parchment: #F7F3EC;
    --parchment-dark: #EDE6D8;
    --shadow-warm: rgba(90,60,20,0.12);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  .cal-wrap {
    font-family: 'Cormorant Garamond', serif;
    background: var(--parchment);
    color: var(--ink);
    min-height: 100vh;
    padding: 2rem 1.5rem 3rem;
    position: relative;
  }

  .cal-wrap::before {
    content: '';
    position: absolute;
    inset: 0;
    background: 
      radial-gradient(ellipse 80% 40% at 50% 0%, rgba(184,151,74,0.08) 0%, transparent 70%),
      radial-gradient(ellipse 60% 30% at 50% 100%, rgba(184,151,74,0.06) 0%, transparent 70%);
    pointer-events: none;
  }

  .cal-header {
    text-align: center;
    margin-bottom: 2rem;
    position: relative;
  }

  .cal-title {
    font-family: 'Cinzel', serif;
    font-size: clamp(18px, 4vw, 26px);
    font-weight: 600;
    letter-spacing: 0.15em;
    color: var(--gold-dark);
    text-transform: uppercase;
  }

  .cal-subtitle {
    font-size: 14px;
    font-style: italic;
    color: #7A6E5F;
    letter-spacing: 0.05em;
    margin-top: 4px;
  }

  .ornament {
    color: var(--gold);
    font-size: 18px;
    letter-spacing: 8px;
    display: block;
    margin: 6px 0;
  }

  .divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 1.2rem 0;
  }
  .divider::before, .divider::after {
    content: '';
    flex: 1;
    height: 0.5px;
    background: linear-gradient(to right, transparent, var(--gold), transparent);
  }
  .divider-dot {
    width: 5px; height: 5px;
    border-radius: 50%;
    background: var(--gold);
  }

  .nav-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1.5rem;
    margin-bottom: 1.5rem;
  }

  .nav-btn {
    background: none;
    border: 0.5px solid var(--gold);
    color: var(--gold-dark);
    font-family: 'Cormorant Garamond', serif;
    font-size: 18px;
    width: 36px; height: 36px;
    border-radius: 50%;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }
  .nav-btn:hover { background: var(--gold); color: var(--parchment); }

  .month-label {
    font-family: 'Cinzel', serif;
    font-size: clamp(15px, 3vw, 20px);
    font-weight: 600;
    color: var(--ink);
    letter-spacing: 0.1em;
    min-width: 220px;
    text-align: center;
  }

  .weekdays {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 2px;
    margin-bottom: 4px;
  }
  .wd {
    text-align: center;
    font-family: 'Cinzel', serif;
    font-size: 10px;
    letter-spacing: 0.08em;
    color: var(--gold-dark);
    padding: 4px 0;
    text-transform: uppercase;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 2px;
  }

  .day-cell {
    aspect-ratio: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    border-radius: 4px;
    position: relative;
    transition: all 0.2s;
    background: transparent;
    border: none;
    padding: 0;
  }
  .day-cell:hover .day-num { color: var(--gold); }
  .day-cell:hover { background: rgba(184,151,74,0.06); }

  .day-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(13px, 2.5vw, 18px);
    font-weight: 300;
    color: var(--ink);
    line-height: 1;
    transition: color 0.2s;
  }

  .day-cell.empty .day-num { color: transparent; cursor: default; }
  .day-cell.empty:hover { background: transparent; }

  .day-cell.today .day-num {
    color: var(--parchment);
  }
  .day-cell.today::before {
    content: '';
    position: absolute;
    width: 30px; height: 30px;
    border-radius: 50%;
    background: var(--gold-dark);
  }
  .day-cell.today .day-num { position: relative; z-index: 1; }

  .day-cell.selected {
    background: rgba(184,151,74,0.12);
    border-radius: 4px;
  }

  .chapter-dot {
    width: 3px; height: 3px;
    border-radius: 50%;
    background: var(--gold);
    margin-top: 2px;
    opacity: 0.7;
  }

  .insight-panel {
    margin-top: 1.8rem;
    background: var(--parchment-dark);
    border: 0.5px solid var(--gold-light);
    border-radius: 8px;
    padding: 1.4rem 1.6rem;
    position: relative;
    overflow: hidden;
    min-height: 160px;
  }

  .insight-panel::before {
    content: '';
    position: absolute;
    top: -20px; left: -20px;
    width: 100px; height: 100px;
    border-radius: 50%;
    border: 0.5px solid var(--gold-light);
    opacity: 0.4;
  }
  .insight-panel::after {
    content: '';
    position: absolute;
    bottom: -30px; right: -30px;
    width: 120px; height: 120px;
    border-radius: 50%;
    border: 0.5px solid var(--gold-light);
    opacity: 0.3;
  }

  .insight-chapter {
    font-family: 'Cinzel', serif;
    font-size: 10px;
    letter-spacing: 0.2em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .insight-date {
    font-size: 13px;
    color: #9A8E7A;
    font-style: italic;
    margin-bottom: 10px;
  }

  .insight-text {
    font-size: clamp(15px, 2.5vw, 19px);
    font-weight: 300;
    font-style: italic;
    line-height: 1.65;
    color: var(--ink);
    position: relative;
    z-index: 1;
  }

  .insight-ornament {
    font-size: 40px;
    color: var(--gold-light);
    line-height: 1;
    position: absolute;
    top: 8px; left: 14px;
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
  }

  .year-strip {
    display: flex;
    justify-content: center;
    gap: 8px;
    margin-top: 1.5rem;
    flex-wrap: wrap;
  }

  .year-btn {
    background: none;
    border: 0.5px solid rgba(184,151,74,0.4);
    color: var(--gold-dark);
    font-family: 'Cinzel', serif;
    font-size: 11px;
    padding: 4px 10px;
    border-radius: 20px;
    cursor: pointer;
    letter-spacing: 0.05em;
    transition: all 0.2s;
  }
  .year-btn:hover, .year-btn.active {
    background: var(--gold-dark);
    color: var(--parchment);
    border-color: var(--gold-dark);
  }
</style>

<div class="cal-wrap">
  <h2 class="sr-only">Calendario perpetuo Il Sé nella Luce — ogni giorno una riflessione di Pietro Annicchiarico</h2>

  <div class="cal-header">
    <div class="cal-title">Il Sé nella Luce</div>
    <span class="ornament">· · ·</span>
    <div class="cal-subtitle">Calendario perpetuo — in itinere</div>
  </div>

  <div class="divider"><div class="divider-dot"></div></div>

  <div class="nav-row">
    <button class="nav-btn" id="prevMonth" aria-label="Mese precedente">‹</button>
    <div class="month-label" id="monthLabel"></div>
    <button class="nav-btn" id="nextMonth" aria-label="Mese successivo">›</button>
  </div>

  <div class="weekdays">
    <div class="wd">Lu</div><div class="wd">Ma</div><div class="wd">Me</div>
    <div class="wd">Gi</div><div class="wd">Ve</div>
    <div class="wd" style="color:#B8974A">Sa</div>
    <div class="wd" style="color:#B8974A">Do</div>
  </div>

  <div class="grid" id="calGrid"></div>

  <div class="insight-panel" id="insightPanel">
    <div class="insight-ornament">"</div>
    <div class="insight-chapter" id="insightChapter"></div>
    <div class="insight-date" id="insightDate"></div>
    <div class="insight-text" id="insightText"></div>
  </div>

  <div class="year-strip" id="yearStrip"></div>

  <div class="divider" style="margin-top:2rem"><div class="divider-dot"></div></div>
  <div style="text-align:center; font-size:12px; font-style:italic; color:#9A8E7A; letter-spacing:0.05em">
    Pietro Annicchiarico · Grottaglie 2020–2026
  </div>
</div>

<script>
const MONTHS_IT = ['Gennaio','Febbraio','Marzo','Aprile','Maggio','Giugno',
  'Luglio','Agosto','Settembre','Ottobre','Novembre','Dicembre'];

const INSIGHTS = [
  { chapter: 'I · La Caduta', text: 'Ogni istante di vita è una fortuna e gioia.' },
  { chapter: 'I · La Caduta', text: 'La crisi è sacra, la guarigione è santa. Abbi fede.' },
  { chapter: 'I · La Caduta', text: 'Mi stupisco al mattino. Il cuore ha retto. Batte ancora.' },
  { chapter: 'I · La Caduta', text: 'La vita è un paradosso: è nel momento più buio che si vede una forte luce.' },
  { chapter: 'II · Il Vuoto', text: 'A cosa può appigliarsi il dolore, il rancore, la rabbia se la casa è vuota?' },
  { chapter: 'II · Il Vuoto', text: 'L\'Opera consiste nel togliere e sgombrare, fare spazio alla meraviglia.' },
  { chapter: 'II · Il Vuoto', text: 'Frena la mente, avvicinati un po\'. Sei nell\'unico posto possibile: la dimora.' },
  { chapter: 'II · Il Vuoto', text: 'Nella fonte interiore, luminosa e silenziosa, abbonda ogni ricchezza.' },
  { chapter: 'III · Il Perdono', text: 'Applica un perdono circolare, totale, sferico, che comprenda ogni dimensione.' },
  { chapter: 'III · Il Perdono', text: 'Il perdonare l\'altro è il dono più grande che puoi fare a te stesso.' },
  { chapter: 'III · Il Perdono', text: 'L\'altro, soprattutto il nemico, mi ha donato la capacità di amare incondizionatamente.' },
  { chapter: 'III · Il Perdono', text: 'Per farmi un regalo perdono e mi perdono.' },
  { chapter: 'IV · La Mente', text: 'Vinci la mente, sconfiggi l\'ego e il nemico smetterà di esistere.' },
  { chapter: 'IV · La Mente', text: 'Il passato non conta, il futuro non esiste e nel presente bisogna tenere a bada l\'ego.' },
  { chapter: 'IV · La Mente', text: 'Quando sei in ansia, fermati, respira, ascolta il respiro. Resta nel presente.' },
  { chapter: 'IV · La Mente', text: 'La pace attrae e vince.' },
  { chapter: 'V · Gli Errori Maestri', text: 'Gli errori sono i miei maestri. E non possono essere trasmessi.' },
  { chapter: 'V · Gli Errori Maestri', text: 'Ogni persona che incontro mi insegna qualcosa.' },
  { chapter: 'V · Gli Errori Maestri', text: 'Il raggiungimento della pace è il solitario attraversamento del proprio inferno.' },
  { chapter: 'V · Gli Errori Maestri', text: 'Accettare il disegno compiuto equivale a essere totalmente realizzati e responsabili.' },
  { chapter: 'VI · La Presenza', text: 'Importante è la presenza. Il qui e ora. L\'unica cosa che conta.' },
  { chapter: 'VI · La Presenza', text: 'Ogni momento è gioia. Il presente è il mio momento magico.' },
  { chapter: 'VI · La Presenza', text: 'Puoi vivere il presente in ogni luogo e in quel presente amare.' },
  { chapter: 'VI · La Presenza', text: 'Mi accorgo di essere tornato finalmente dove sono nato. In me. A casa.' },
  { chapter: 'VII · L\'Amore', text: 'Le anime s\'incontrano. Gli ego si scontrano.' },
  { chapter: 'VII · L\'Amore', text: 'L\'altro è il nostro specchio fedele: ha bisogno di essere amato per quello che è.' },
  { chapter: 'VII · L\'Amore', text: 'L\'eredità che lascio sta in ciò e in chi ho amato.' },
  { chapter: 'VII · L\'Amore', text: 'Da solo mi sento perfetto. Poi incontro l\'altro e capisco che sono appena a metà strada.' },
  { chapter: 'VIII · Il Silenzio', text: 'Ho imparato la lingua più preziosa: il silenzio.' },
  { chapter: 'VIII · Il Silenzio', text: 'Il più grande dono è il silenzio. O le parole che non feriscono.' },
  { chapter: 'VIII · Il Silenzio', text: 'Non si incide nel mondo ostentando la sensibilità. Essere sempre gentili è la via.' },
  { chapter: 'IX · La Luce', text: 'Vivo ogni istante come se fosse l\'ultimo, per questo non ho bisogno di sapere quando morirò.' },
  { chapter: 'IX · La Luce', text: 'Non contano i titoli. Conta solo la capacità di amare. Tutto il resto è inutile.' },
  { chapter: 'IX · La Luce', text: 'Io sono in pace. Spero che possa esserlo anche tu.' },
  { chapter: 'IX · La Luce', text: 'Del mio tempo salvo quando ho amato più di quando sono stato amato.' },
];

const today = new Date();
let curYear = today.getFullYear();
let curMonth = today.getMonth();
let selectedDay = today.getDate();
let selectedMonth = today.getMonth();
let selectedYear = today.getFullYear();

function getInsight(day, month, year) {
  const n = (day * 7 + month * 31 + year) % INSIGHTS.length;
  return INSIGHTS[Math.abs(n)];
}

function formatDateIT(day, month, year) {
  return `${day} ${MONTHS_IT[month]} ${year}`;
}

function render() {
  const grid = document.getElementById('calGrid');
  const label = document.getElementById('monthLabel');
  label.textContent = `${MONTHS_IT[curMonth]} ${curYear}`;

  const first = new Date(curYear, curMonth, 1).getDay();
  const startOffset = (first === 0) ? 6 : first - 1;
  const daysInMonth = new Date(curYear, curMonth + 1, 0).getDate();

  grid.innerHTML = '';

  for (let i = 0; i < startOffset; i++) {
    const e = document.createElement('div');
    e.className = 'day-cell empty';
    e.innerHTML = '<span class="day-num"> </span>';
    grid.appendChild(e);
  }

  for (let d = 1; d <= daysInMonth; d++) {
    const cell = document.createElement('div');
    cell.className = 'day-cell';
    const isToday = d === today.getDate() && curMonth === today.getMonth() && curYear === today.getFullYear();
    const isSelected = d === selectedDay && curMonth === selectedMonth && curYear === selectedYear;
    if (isToday) cell.classList.add('today');
    if (isSelected && !isToday) cell.classList.add('selected');

    const ins = getInsight(d, curMonth, curYear);
    cell.innerHTML = `<span class="day-num">${d}</span><span class="chapter-dot"></span>`;
    cell.addEventListener('click', () => {
      selectedDay = d; selectedMonth = curMonth; selectedYear = curYear;
      updateInsight(d, curMonth, curYear);
      render();
    });
    grid.appendChild(cell);
  }

  updateInsight(selectedDay, selectedMonth, selectedYear);
}

function updateInsight(d, m, y) {
  const ins = getInsight(d, m, y);
  document.getElementById('insightChapter').textContent = ins.chapter;
  document.getElementById('insightDate').textContent = formatDateIT(d, m, y);
  document.getElementById('insightText').textContent = ins.text;
}

function buildYearStrip() {
  const strip = document.getElementById('yearStrip');
  strip.innerHTML = '';
  const startY = today.getFullYear() - 2;
  for (let y = startY; y <= startY + 8; y++) {
    const btn = document.createElement('button');
    btn.className = 'year-btn' + (y === curYear ? ' active' : '');
    btn.textContent = y;
    btn.addEventListener('click', () => {
      curYear = y;
      document.querySelectorAll('.year-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      render();
    });
    strip.appendChild(btn);
  }
}

document.getElementById('prevMonth').addEventListener('click', () => {
  curMonth--; if (curMonth < 0) { curMonth = 11; curYear--; }
  render(); buildYearStrip();
});
document.getElementById('nextMonth').addEventListener('click', () => {
  curMonth++; if (curMonth > 11) { curMonth = 0; curYear++; }
  render(); buildYearStrip();
});

buildYearStrip();
render();
</script>
