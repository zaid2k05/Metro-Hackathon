[Diversions Without Disruption.html](https://github.com/user-attachments/files/33288804/Diversions.Without.Disruption.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Diversions Without Disruption · PS-10 City Public Transport</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:wght@500;600;700&family=Noto+Sans:wght@400;500;600&family=Noto+Sans+Devanagari:wght@400;500;600&family=Noto+Sans+Gujarati:wght@400;500;600&display=swap" rel="stylesheet">

<style>
  /* ───────── Design tokens ───────── */
  :root {
    --paper:   #F6F7F9;
    --surface: #FFFFFF;
    --ink:     #17283B;
    --ink-2:   #4A5B6D;
    --line:    #D9DEE5;
    --signal:  #FFC20E;   /* transit-sign yellow  */
    --closed:  #C8102E;   /* road closed          */
    --restrict:#E88A00;   /* lane restriction     */
    --detour:  #0B8A5B;   /* diversion route      */
    --bus:     #1F5FBF;   /* bus-route highlight  */
    --wa:      #DCF8C6;   /* WhatsApp bubble      */
    --wa-bg:   #EFE7DD;
    --radius:  10px;
    --font-body: "Noto Sans","Noto Sans Devanagari","Noto Sans Gujarati",system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
    --font-head: "Barlow Semi Condensed","Noto Sans","Noto Sans Devanagari","Noto Sans Gujarati",system-ui,sans-serif;
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    margin: 0; background: var(--paper); color: var(--ink);
    font-family: var(--font-body); font-size: 15px; line-height: 1.55;
  }
  h1,h2,h3 { font-family: var(--font-head); margin: 0; line-height: 1.15; }
  button, input, select, textarea { font: inherit; color: inherit; }
  :focus-visible { outline: 3px solid var(--bus); outline-offset: 2px; }

  /* ───────── Header (signage board) ───────── */
  header.board { background: var(--ink); color: #fff; border-bottom: 6px solid var(--signal); }
  .board-inner { max-width: 1240px; margin: 0 auto; padding: 22px 24px 20px; display: flex; gap: 22px; align-items: center; flex-wrap: wrap; }
  .ps-badge {
    background: var(--signal); color: var(--ink); font-family: var(--font-head); font-weight: 700;
    font-size: 26px; padding: 6px 14px; border-radius: 6px; letter-spacing: .5px;
  }
  .board h1 { font-size: clamp(26px, 4vw, 40px); font-weight: 700; letter-spacing: .2px; }
  .board p { margin: 2px 0 0; color: #C5D0DC; max-width: 70ch; }
  .board-meta { margin-left: auto; text-align: right; color: #C5D0DC; font-size: 13px; }
  .board-meta strong { color: #fff; font-weight: 600; }

  main { max-width: 1240px; margin: 0 auto; padding: 24px; display: grid; gap: 22px; }

  /* ───────── Panels ───────── */
  .panel { background: var(--surface); border: 1px solid var(--line); border-radius: var(--radius); }
  .panel > header { padding: 14px 18px; border-bottom: 1px solid var(--line); display: flex; align-items: center; gap: 12px; flex-wrap: wrap; }
  .panel > header h2 { font-size: 20px; }
  .panel > header .hint { color: var(--ink-2); font-size: 13px; }
  .panel .body { padding: 18px; }

  /* ───────── Input section ───────── */
  .input-grid { display: grid; grid-template-columns: minmax(0, 1.6fr) minmax(0, 1fr); gap: 18px; }
  label.field { display: grid; gap: 6px; font-weight: 600; font-size: 13px; color: var(--ink-2); }
  textarea, input[type="date"], select {
    width: 100%; border: 1px solid var(--line); border-radius: 8px; padding: 9px 11px; background: #fff; color: var(--ink);
  }
  textarea { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; font-size: 12.5px; line-height: 1.5; resize: vertical; min-height: 190px; white-space: pre; overflow: auto; }
  .controls { display: grid; gap: 14px; align-content: start; }
  .row { display: flex; gap: 10px; flex-wrap: wrap; align-items: center; }

  .btn {
    border: 1px solid var(--ink); background: var(--ink); color: #fff; padding: 9px 16px; border-radius: 8px;
    font-weight: 600; cursor: pointer; transition: background .15s, transform .05s;
  }
  .btn:hover { background: #24405d; }
  .btn:active { transform: translateY(1px); }
  .btn.ghost { background: #fff; color: var(--ink); border-color: var(--line); }
  .btn.ghost:hover { background: var(--paper); border-color: var(--ink-2); }
  .btn.signal { background: var(--signal); color: var(--ink); border-color: var(--signal); }
  .btn.signal:hover { background: #ffd24a; }
  .btn.small { padding: 5px 11px; font-size: 13px; }
  .btn.wa { background: #1FA855; border-color: #1FA855; }
  .btn.wa:hover { background: #178a45; }

  details { border: 1px dashed var(--line); border-radius: 8px; padding: 8px 12px; }
  details summary { cursor: pointer; font-weight: 600; font-size: 13px; color: var(--ink-2); }
  details textarea { margin-top: 10px; min-height: 150px; }

  .errors { background: #FDECEE; border: 1px solid #F3B7BF; color: #7D0A1B; border-radius: 8px; padding: 10px 14px; font-size: 13px; }
  .errors ul { margin: 4px 0 0 18px; padding: 0; }
  .errors[hidden] { display: none; }
  .csv-hint { font-size: 12.5px; color: var(--ink-2); margin: 0; }
  code { background: var(--paper); padding: 1px 5px; border-radius: 4px; font-size: 12px; }

  /* ───────── Summary strip ───────── */
  .summary { display: flex; gap: 0; flex-wrap: wrap; border: 1px solid var(--line); border-radius: var(--radius); background: var(--surface); overflow: hidden; }
  .stat { flex: 1 1 150px; padding: 14px 18px; border-right: 1px solid var(--line); }
  .stat:last-child { border-right: 0; }
  .stat b { display: block; font-family: var(--font-head); font-size: 32px; line-height: 1; }
  .stat span { color: var(--ink-2); font-size: 13px; }
  .stat.c b { color: var(--closed); } .stat.r b { color: var(--restrict); } .stat.b b { color: var(--bus); } .stat.d b { color: var(--detour); }

  /* ───────── Tabs & language switch ───────── */
  .toolbar { display: flex; gap: 14px; justify-content: space-between; align-items: center; flex-wrap: wrap; padding: 12px 18px; border-bottom: 1px solid var(--line); background: #FBFCFD; border-radius: var(--radius) var(--radius) 0 0; }
  .tabs { display: flex; gap: 4px; flex-wrap: wrap; }
  .tab { border: 0; background: transparent; padding: 8px 14px; border-radius: 8px; cursor: pointer; font-weight: 600; color: var(--ink-2); }
  .tab:hover { background: var(--paper); }
  .tab[aria-selected="true"] { background: var(--ink); color: #fff; }
  .seg { display: inline-flex; border: 1px solid var(--line); border-radius: 8px; overflow: hidden; background: #fff; }
  .seg button { border: 0; background: transparent; padding: 6px 12px; cursor: pointer; font-weight: 500; }
  .seg button + button { border-left: 1px solid var(--line); }
  .seg button[aria-pressed="true"] { background: var(--signal); font-weight: 600; }
  .tabpanel[hidden] { display: none; }

  /* ───────── Map ───────── */
  .map-wrap { display: grid; grid-template-columns: minmax(0, 1fr) 280px; }
  .map-canvas { background: #EEF2F6; border-right: 1px solid var(--line); min-height: 320px; }
  .map-canvas svg { display: block; width: 100%; height: auto; }
  .legend { padding: 18px; display: grid; gap: 12px; align-content: start; font-size: 13.5px; }
  .legend h3 { font-size: 17px; }
  .legend .item { display: flex; align-items: center; gap: 10px; }
  .swatch { width: 34px; height: 0; border-top: 6px solid; border-radius: 3px; flex: none; }
  .swatch.closed { border-color: var(--closed); }
  .swatch.restrict { border-color: var(--restrict); border-top-style: dashed; }
  .swatch.detour { border-color: var(--detour); border-top-style: dashed; }
  .swatch.bus { border-color: var(--bus); opacity: .5; }
  .legend .note { color: var(--ink-2); font-size: 12.5px; }
  .legend ul { list-style: none; margin: 0; padding: 0; display: grid; gap: 6px; }
  .legend li button { width: 100%; text-align: left; background: var(--paper); border: 1px solid var(--line); border-radius: 8px; padding: 6px 10px; cursor: pointer; }
  .legend li button[aria-pressed="true"] { background: var(--bus); color: #fff; border-color: var(--bus); }

  /* ───────── Advisory cards ───────── */
  .cards { display: grid; gap: 16px; padding: 18px; }
  .adv { border: 1px solid var(--line); border-left-width: 8px; border-radius: var(--radius); background: #fff; }
  .adv.closure { border-left-color: var(--closed); }
  .adv.restriction { border-left-color: var(--restrict); }
  .adv-head { display: flex; gap: 10px; align-items: baseline; flex-wrap: wrap; padding: 12px 16px 0; }
  .adv-head h3 { font-size: 22px; }
  .pill { font-size: 12px; font-weight: 600; padding: 2px 9px; border-radius: 999px; border: 1px solid var(--line); background: var(--paper); }
  .pill.active { background: #FDECEE; border-color: #F3B7BF; color: #8B1022; }
  .pill.upcoming { background: #FFF6DB; border-color: #F2DB8D; color: #7A5600; }
  .adv-langs { display: grid; gap: 0; }
  .adv-lang { padding: 12px 16px; border-top: 1px solid var(--line); margin-top: 12px; }
  .adv-lang:first-child { margin-top: 12px; }
  .adv-lang .lang-tag { font-size: 12px; color: var(--ink-2); font-weight: 600; margin-bottom: 4px; }
  .adv-lang p { margin: 4px 0; }
  .adv-lang .detour { color: var(--detour); font-weight: 600; }
  .adv-lang .warn { color: var(--closed); font-weight: 600; }
  .adv-actions { padding: 0 16px 14px; display: flex; gap: 8px; flex-wrap: wrap; }

  /* ───────── WhatsApp ───────── */
  .wa-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; padding: 18px; background: var(--wa-bg); border-radius: 0 0 var(--radius) var(--radius); }
  .wa-card { display: grid; gap: 8px; align-content: start; }
  .wa-card .cap { font-size: 12px; font-weight: 600; color: #54463a; }
  .bubble { background: var(--wa); border-radius: 10px 10px 2px 10px; padding: 10px 12px; box-shadow: 0 1px 1px rgba(0,0,0,.12); white-space: pre-wrap; word-break: break-word; font-size: 14px; line-height: 1.5; }
  .wa-card .row { gap: 6px; }

  /* ───────── Bus table ───────── */
  .table-wrap { overflow-x: auto; padding: 0; }
  table { border-collapse: collapse; width: 100%; min-width: 720px; }
  th, td { text-align: left; padding: 10px 16px; border-bottom: 1px solid var(--line); vertical-align: top; }
  th { font-family: var(--font-head); font-size: 15px; background: #FBFCFD; position: sticky; top: 0; }
  .route-no { display: inline-block; min-width: 44px; text-align: center; background: var(--bus); color: #fff; font-family: var(--font-head); font-weight: 700; font-size: 18px; padding: 1px 8px; border-radius: 6px; }
  .st { font-weight: 600; font-size: 12.5px; padding: 2px 8px; border-radius: 999px; }
  .st.diverted { background: #E3F5EC; color: #07613F; }
  .st.suspended { background: #FDECEE; color: #8B1022; }
  .st.delay { background: #FFF1D6; color: #7A4A00; }

  .empty { padding: 36px 18px; text-align: center; color: var(--ink-2); }
  footer { text-align: center; color: var(--ink-2); font-size: 12.5px; padding: 6px 24px 30px; }

  /* ───────── Responsive ───────── */
  @media (max-width: 900px) {
    .input-grid, .map-wrap { grid-template-columns: 1fr; }
    .map-canvas { border-right: 0; border-bottom: 1px solid var(--line); }
    .board-meta { margin-left: 0; text-align: left; }
    .stat { border-right: 0; border-bottom: 1px solid var(--line); }
  }
  @media print {
    header.board .board-meta, .input-section, .toolbar, .adv-actions, .wa-card .row, footer { display: none !important; }
    body { background: #fff; }
    .tabpanel[hidden] { display: block !important; }
    .panel { border: 0; }
  }
  @media (prefers-reduced-motion: reduce) { * { transition: none !important; scroll-behavior: auto !important; } }
</style>
</head>

<body>
<header class="board">
  <div class="board-inner">
    <div class="ps-badge">PS-10</div>
    <div>
      <h1>Diversions Without Disruption</h1>
      <p>Turn a construction schedule into ready-to-send diversion advisories: a map, multilingual text, WhatsApp messages and the list of bus routes affected.</p>
    </div>
    <div class="board-meta">
      <strong>City Public Transport</strong><br>
      DevFest · Offline operation not required
    </div>
  </div>
</header>

<main>

  <!-- ═════════ 1. INPUT ═════════ -->
  <section class="panel input-section" aria-labelledby="in-title">
    <header>
      <h2 id="in-title">Construction schedule</h2>
      <span class="hint">Paste CSV, upload a file, or edit the sample. Advisories regenerate as you change anything.</span>
    </header>
    <div class="body input-grid">
      <div style="display:grid; gap:10px;">
        <label class="field" for="csv">Schedule (CSV)
          <textarea id="csv" spellcheck="false" aria-describedby="csv-hint"></textarea>
        </label>
        <p class="csv-hint" id="csv-hint">
          Columns: <code>edge_id</code> <code>type</code> (closure | restriction) <code>start</code> <code>end</code> (YYYY-MM-DD)
          <code>time_window</code> <code>reason</code> and optional <code>reason_hi</code> <code>reason_gu</code> for translated reasons.
        </p>
        <details>
          <summary>Road network &amp; bus routes (JSON) – replace with your city's data</summary>
          <textarea id="net" spellcheck="false" aria-label="Road network and bus routes JSON"></textarea>
        </details>
      </div>

      <div class="controls">
        <label class="field" for="asof">Issue advisory for date
          <input type="date" id="asof">
        </label>
        <label class="field" for="horizon">Include works starting within
          <select id="horizon">
            <option value="0">Active today only</option>
            <option value="3">Next 3 days</option>
            <option value="7" selected>Next 7 days</option>
            <option value="14">Next 14 days</option>
            <option value="30">Next 30 days</option>
          </select>
        </label>
        <div class="row">
          <button class="btn signal" id="gen">Generate advisories</button>
          <button class="btn ghost" id="reset">Reset sample</button>
        </div>
        <div class="row">
          <label class="btn ghost small" for="file" style="cursor:pointer;">Upload CSV</label>
          <input type="file" id="file" accept=".csv,text/csv" hidden>
        </div>
        <div class="errors" id="errors" role="alert" hidden></div>
      </div>
    </div>
  </section>

  <!-- ═════════ 2. SUMMARY ═════════ -->
  <section class="summary" id="summary" aria-live="polite"></section>

  <!-- ═════════ 3. OUTPUT ═════════ -->
  <section class="panel" aria-label="Generated advisories">
    <div class="toolbar">
      <div class="tabs" role="tablist" aria-label="Output views">
        <button class="tab" role="tab" id="t-map"  aria-controls="p-map"  aria-selected="true">Diversion map</button>
        <button class="tab" role="tab" id="t-adv"  aria-controls="p-adv"  aria-selected="false">Advisories</button>
        <button class="tab" role="tab" id="t-wa"   aria-controls="p-wa"   aria-selected="false">WhatsApp</button>
        <button class="tab" role="tab" id="t-bus"  aria-controls="p-bus"  aria-selected="false">Bus routes</button>
      </div>
      <div class="row">
        <div class="seg" id="langseg" role="group" aria-label="Language">
          <button data-lang="en" aria-pressed="true">English</button>
          <button data-lang="hi" aria-pressed="false" lang="hi">हिन्दी</button>
          <button data-lang="gu" aria-pressed="false" lang="gu">ગુજરાતી</button>
          <button data-lang="all" aria-pressed="false">All</button>
        </div>
        <button class="btn ghost small" id="dl-txt">Download .txt</button>
        <button class="btn ghost small" id="print">Print</button>
      </div>
    </div>

    <div class="tabpanel" id="p-map" role="tabpanel" aria-labelledby="t-map">
      <div class="map-wrap">
        <div class="map-canvas" id="map"></div>
        <aside class="legend">
          <h3>Map key</h3>
          <div class="item"><span class="swatch closed"></span> Road closed</div>
          <div class="item"><span class="swatch restrict"></span> Lane restriction</div>
          <div class="item"><span class="swatch detour"></span> Suggested diversion</div>
          <div class="item"><span class="swatch bus"></span> Selected bus route</div>
          <p class="note">Faded markings are works that start within the selected window.</p>
          <h3>Show bus route</h3>
          <ul id="routepick"></ul>
          <button class="btn ghost small" id="dl-svg">Download map (SVG)</button>
        </aside>
      </div>
    </div>

    <div class="tabpanel" id="p-adv" role="tabpanel" aria-labelledby="t-adv" hidden>
      <div class="cards" id="cards"></div>
    </div>

    <div class="tabpanel" id="p-wa" role="tabpanel" aria-labelledby="t-wa" hidden>
      <div class="wa-grid" id="wagrid"></div>
    </div>

    <div class="tabpanel" id="p-bus" role="tabpanel" aria-labelledby="t-bus" hidden>
      <div class="table-wrap" id="bustable"></div>
    </div>
  </section>
</main>

<footer>
  Place names and any reasons without a translated column are shown exactly as entered. Review all advisories before public release.
</footer>

<script>
(() => {
  'use strict';

  /* ═════════════ CONFIG ═════════════ */
  const AUTHORITY = { en: 'City Transport Authority', hi: 'शहर परिवहन प्राधिकरण', gu: 'શહેર પરિવહન સત્તામંડળ' };

  /* ═════════════ SAMPLE DATA ═════════════ */
  const SAMPLE_NET = {
    nodes: [
      { id: 'N1',  name: 'Central Station',  x: 110, y: 280 },
      { id: 'N2',  name: 'Market Chowk',     x: 290, y: 165 },
      { id: 'N3',  name: 'University Gate',  x: 500, y: 110 },
      { id: 'N4',  name: 'Metro Hub',        x: 340, y: 320 },
      { id: 'N5',  name: 'Riverside',        x: 580, y: 270 },
      { id: 'N6',  name: 'Tech Park',        x: 730, y: 170 },
      { id: 'N7',  name: 'Old Town',         x: 150, y: 450 },
      { id: 'N8',  name: 'Stadium',          x: 410, y: 455 },
      { id: 'N9',  name: 'Airport Junction', x: 710, y: 420 },
      { id: 'N10', name: 'Hospital Circle',  x: 190, y: 85  }
    ],
    edges: [
      { id: 'E1',  name: 'Station Road',      a: 'N1',  b: 'N2'  },
      { id: 'E2',  name: 'Market Street',     a: 'N2',  b: 'N3'  },
      { id: 'E3',  name: 'Metro Avenue',      a: 'N2',  b: 'N4'  },
      { id: 'E4',  name: 'Central Link',      a: 'N1',  b: 'N4'  },
      { id: 'E5',  name: 'University Road',   a: 'N3',  b: 'N5'  },
      { id: 'E6',  name: 'Riverside Drive',   a: 'N4',  b: 'N5'  },
      { id: 'E7',  name: 'Tech Park Road',    a: 'N5',  b: 'N6'  },
      { id: 'E8',  name: 'Old Town Road',     a: 'N1',  b: 'N7'  },
      { id: 'E9',  name: 'Stadium Road',      a: 'N7',  b: 'N8'  },
      { id: 'E10', name: 'Ring Road South',   a: 'N4',  b: 'N8'  },
      { id: 'E11', name: 'Airport Road',      a: 'N8',  b: 'N9'  },
      { id: 'E12', name: 'Expressway',        a: 'N5',  b: 'N9'  },
      { id: 'E13', name: 'Hospital Road',     a: 'N10', b: 'N2'  },
      { id: 'E14', name: 'Hospital Link',     a: 'N10', b: 'N1'  },
      { id: 'E15', name: 'Campus Road',       a: 'N3',  b: 'N6'  }
    ],
    routes: [
      { no: '12', name: 'Central Station – Tech Park',      edges: ['E4','E6','E7'] },
      { no: '21', name: 'Old Town – University Gate',       edges: ['E8','E1','E2'] },
      { no: '34', name: 'Hospital Circle – Airport',        edges: ['E13','E3','E10','E11'] },
      { no: '45', name: 'Central Station – Airport',        edges: ['E4','E10','E11'] },
      { no: '52', name: 'Market Chowk – Tech Park',         edges: ['E2','E5','E7'] },
      { no: '60', name: 'Old Town – Stadium',               edges: ['E9'] },
      { no: '77', name: 'Central Station – Airport (Exp.)', edges: ['E4','E6','E12'] }
    ]
  };

  const pad = n => String(n).padStart(2, '0');
  const iso = d => `${d.getFullYear()}-${pad(d.getMonth() + 1)}-${pad(d.getDate())}`;
  const addDays = (d, n) => { const x = new Date(d); x.setDate(x.getDate() + n); return x; };
  const parseISO = s => { const m = /^(\d{4})-(\d{2})-(\d{2})$/.exec((s || '').trim()); return m ? new Date(+m[1], +m[2] - 1, +m[3]) : null; };

  function sampleCSV() {
    const t = new Date();
    const d = n => iso(addDays(t, n));
    return [
      'edge_id,type,start,end,time_window,reason,reason_hi,reason_gu',
      `E3,closure,${d(-2)},${d(12)},,Metro extension – pier casting,मेट्रो विस्तार – पियर निर्माण,મેટ્રો વિસ્તરણ – પિયર કામ`,
      `E6,restriction,${d(-1)},${d(6)},22:00–05:00,Utility line shifting,यूटिलिटी लाइन स्थानांतरण,યુટિલિટી લાઇન સ્થળાંતર`,
      `E10,closure,${d(1)},${d(5)},,Road resurfacing,सड़क की रीसर्फेसिंग,રસ્તાનું રીસરફેસિંગ`,
      `E2,closure,${d(3)},${d(9)},22:00–05:00,Girder launching for metro,मेट्रो गर्डर स्थापना,મેટ્રો ગર્ડર લોન્ચિંગ`,
      `E9,restriction,${d(-5)},${d(-1)},,Drainage work (completed),,`
    ].join('\n');
  }

  /* ═════════════ HELPERS ═════════════ */
  const $ = s => document.querySelector(s);
  const $$ = s => [...document.querySelectorAll(s)];
  const esc = s => String(s ?? '').replace(/[&<>"']/g, c => ({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;' }[c]));

  function parseCSV(text) {
    const rows = []; let row = [], cur = '', q = false;
    for (let i = 0; i < text.length; i++) {
      const c = text[i];
      if (q) { if (c === '"') { if (text[i + 1] === '"') { cur += '"'; i++; } else q = false; } else cur += c; }
      else if (c === '"') q = true;
      else if (c === ',') { row.push(cur); cur = ''; }
      else if (c === '\n' || c === '\r') {
        if (c === '\r' && text[i + 1] === '\n') i++;
        row.push(cur); cur = '';
        if (row.some(x => x.trim())) rows.push(row);
        row = [];
      } else cur += c;
    }
    row.push(cur); if (row.some(x => x.trim())) rows.push(row);
    if (!rows.length) return [];
    const head = rows.shift().map(h => h.trim().toLowerCase());
    return rows.map(r => Object.fromEntries(head.map((h, i) => [h, (r[i] || '').trim()])));
  }

  /* ═════════════ TRANSLATIONS ═════════════ */
  const LANGS = {
    en: {
      name: 'English', loc: 'en-IN',
      closedTitle: r => `Road closed: ${r}`,
      restrTitle:  r => `Lane restriction: ${r}`,
      closedBody:  (r, a, b, dates, win) => `${r} (${a} – ${b}) will be closed to traffic ${dates}${win ? ', daily ' + win : ''}.`,
      restrBody:   (r, a, b, dates, win) => `One lane of ${r} (${a} – ${b}) is restricted ${dates}${win ? ', daily ' + win : ''}. Expect slow-moving traffic.`,
      dates: (s, e) => `from ${s} to ${e}`,
      reason: x => `Reason: ${x}.`,
      useInstead: p => `Use instead: ${p}.`,
      noDiversion: 'No full alternative route is available. Expect heavy delays and plan extra time.',
      buses: l => `Bus routes affected: ${l}.`,
      noBuses: 'No bus routes affected.',
      digestTitle: 'Traffic diversion update',
      issuedBy: a => `Issued by ${a}`,
      statusDiverted: 'Diverted', statusSuspended: 'Suspended on this stretch', statusDelay: 'Delays expected',
      tagClosed: 'Road closed', tagRestr: 'Lane restriction',
      adviceDiv: p => `Runs via ${p}`, adviceSusp: 'No alternative – use nearby stops', adviceDelay: 'Allow extra 10–15 min'
    },
    hi: {
      name: 'हिन्दी', loc: 'hi-IN',
      closedTitle: r => `सड़क बंद: ${r}`,
      restrTitle:  r => `लेन प्रतिबंध: ${r}`,
      closedBody:  (r, a, b, dates, win) => `${r} (${a} – ${b}) ${dates}${win ? ', प्रतिदिन ' + win : ''} यातायात के लिए बंद रहेगी।`,
      restrBody:   (r, a, b, dates, win) => `${r} (${a} – ${b}) की एक लेन ${dates}${win ? ', प्रतिदिन ' + win : ''} प्रतिबंधित रहेगी। यातायात धीमा रहने की संभावना है।`,
      dates: (s, e) => `${s} से ${e} तक`,
      reason: x => `कारण: ${x}।`,
      useInstead: p => `वैकल्पिक मार्ग: ${p}।`,
      noDiversion: 'कोई पूर्ण वैकल्पिक मार्ग उपलब्ध नहीं है। भारी देरी की आशंका है, अतिरिक्त समय लेकर चलें।',
      buses: l => `प्रभावित बस मार्ग: ${l}।`,
      noBuses: 'कोई बस मार्ग प्रभावित नहीं है।',
      digestTitle: 'यातायात डायवर्जन अपडेट',
      issuedBy: a => `जारीकर्ता: ${a}`,
      statusDiverted: 'मार्ग परिवर्तित', statusSuspended: 'इस खंड पर सेवा बंद', statusDelay: 'देरी संभव',
      tagClosed: 'सड़क बंद', tagRestr: 'लेन प्रतिबंध',
      adviceDiv: p => `${p} के रास्ते चलेगी`, adviceSusp: 'विकल्प नहीं – पास के स्टॉप का उपयोग करें', adviceDelay: '10–15 मिनट अतिरिक्त रखें'
    },
    gu: {
      name: 'ગુજરાતી', loc: 'gu-IN',
      closedTitle: r => `રસ્તો બંધ: ${r}`,
      restrTitle:  r => `લેન પર નિયંત્રણ: ${r}`,
      closedBody:  (r, a, b, dates, win) => `${r} (${a} – ${b}) ${dates}${win ? ', દરરોજ ' + win : ''} વાહનવ્યવહાર માટે બંધ રહેશે.`,
      restrBody:   (r, a, b, dates, win) => `${r} (${a} – ${b}) ની એક લેન ${dates}${win ? ', દરરોજ ' + win : ''} પ્રતિબંધિત રહેશે. ટ્રાફિક ધીમો રહેવાની શક્યતા છે.`,
      dates: (s, e) => `${s} થી ${e} સુધી`,
      reason: x => `કારણ: ${x}.`,
      useInstead: p => `વૈકલ્પિક માર્ગ: ${p}.`,
      noDiversion: 'કોઈ સંપૂર્ણ વૈકલ્પિક માર્ગ ઉપલબ્ધ નથી. ભારે વિલંબની શક્યતા છે, વધારાનો સમય રાખો.',
      buses: l => `અસરગ્રસ્ત બસ રૂટ: ${l}.`,
      noBuses: 'કોઈ બસ રૂટ અસરગ્રસ્ત નથી.',
      digestTitle: 'ટ્રાફિક ડાયવર્ઝન અપડેટ',
      issuedBy: a => `જારી કરનાર: ${a}`,
      statusDiverted: 'રૂટ બદલાયો', statusSuspended: 'આ ભાગ પર સેવા બંધ', statusDelay: 'વિલંબની શક્યતા',
      tagClosed: 'રસ્તો બંધ', tagRestr: 'લેન પર નિયંત્રણ',
      adviceDiv: p => `${p} થઈને ચાલશે`, adviceSusp: 'વિકલ્પ નથી – નજીકના સ્ટોપનો ઉપયોગ કરો', adviceDelay: '10–15 મિનિટ વધારાના રાખો'
    }
  };
  const LANG_KEYS = ['en', 'hi', 'gu'];

  /* ═════════════ STATE ═════════════ */
  const state = { lang: 'en', tab: 'map', hl: null, items: [], routes: [], net: null, asOf: null, svg: '' };

  /* ═════════════ ROUTING (Dijkstra avoiding closed edges) ═════════════ */
  function shortestPath(net, from, to, blocked) {
    const nodes = Object.fromEntries(net.nodes.map(n => [n.id, n]));
    const adj = {};
    net.edges.forEach(e => {
      if (blocked.has(e.id)) return;
      const A = nodes[e.a], B = nodes[e.b];
      const w = Math.hypot(A.x - B.x, A.y - B.y);
      (adj[e.a] ||= []).push({ to: e.b, w, e });
      (adj[e.b] ||= []).push({ to: e.a, w, e });
    });
    const dist = { [from]: 0 }, prev = {}, done = new Set();
    while (true) {
      let u = null, best = Infinity;
      for (const k in dist) if (!done.has(k) && dist[k] < best) { best = dist[k]; u = k; }
      if (u === null) return null;
      if (u === to) break;
      done.add(u);
      (adj[u] || []).forEach(({ to: v, w, e }) => {
        if (dist[u] + w < (dist[v] ?? Infinity)) { dist[v] = dist[u] + w; prev[v] = { u, e }; }
      });
    }
    const nodeIds = [to], edges = [];
    let cur = to;
    while (cur !== from) { const p = prev[cur]; edges.unshift(p.e); nodeIds.unshift(p.u); cur = p.u; }
    return { nodeIds, edges };
  }

  /* ═════════════ BUILD MODEL ═════════════ */
  function build() {
    const errors = [];
    let net;
    try { net = JSON.parse($('#net').value); }
    catch (e) { errors.push('Road network JSON is invalid: ' + e.message); showErrors(errors); return; }

    const edgeById = Object.fromEntries(net.edges.map(e => [e.id, e]));
    const nodeById = Object.fromEntries(net.nodes.map(n => [n.id, n]));
    const asOf = parseISO($('#asof').value) || new Date(new Date().setHours(0, 0, 0, 0));
    const horizon = +$('#horizon').value;
    const rows = parseCSV($('#csv').value);
    const items = [];

    rows.forEach((r, i) => {
      const line = i + 2;
      const edge = edgeById[r.edge_id];
      if (!edge) { errors.push(`Row ${line}: unknown edge_id “${r.edge_id}”.`); return; }
      const s = parseISO(r.start), e = parseISO(r.end);
      if (!s || !e) { errors.push(`Row ${line}: start/end must be YYYY-MM-DD.`); return; }
      if (e < s) { errors.push(`Row ${line}: end date is before start date.`); return; }
      const type = (r.type || 'closure').toLowerCase().startsWith('r') ? 'restriction' : 'closure';
      let status;
      if (s <= asOf && asOf <= e) status = 'active';
      else if (s > asOf && s <= addDays(asOf, horizon)) status = 'upcoming';
      else return;
      items.push({
        edge, type, status, start: s, end: e,
        window: r.time_window || '',
        reason: { en: r.reason || '', hi: r.reason_hi || r.reason || '', gu: r.reason_gu || r.reason || '' },
        from: nodeById[edge.a], to: nodeById[edge.b]
      });
    });

    items.sort((a, b) => (a.status === b.status ? a.start - b.start : a.status === 'active' ? -1 : 1));

    const blocked = new Set(items.filter(i => i.type === 'closure').map(i => i.edge.id));
    items.forEach(it => {
      it.div = it.type === 'closure' ? shortestPath(net, it.edge.a, it.edge.b, blocked) : null;
      it.routes = (net.routes || []).filter(r => r.edges.includes(it.edge.id));
    });

    Object.assign(state, { items, net, asOf, routes: net.routes || [], nodeById, edgeById });
    if (state.hl && !state.routes.some(r => r.no === state.hl)) state.hl = null;
    showErrors(errors);
    renderAll();
  }

  function showErrors(list) {
    const box = $('#errors');
    if (!list.length) { box.hidden = true; box.innerHTML = ''; return; }
    box.hidden = false;
    box.innerHTML = `<strong>Check your input</strong><ul>${list.map(x => `<li>${esc(x)}</li>`).join('')}</ul>`;
  }

  /* ═════════════ TEXT GENERATION ═════════════ */
  const fmtDate = (d, L) => d.toLocaleDateString(L.loc, { day: 'numeric', month: 'short', year: 'numeric' });

  function divPathText(it) {
    return it.div ? it.div.edges.map(e => e.name).join(' → ') : '';
  }

  function advisory(it, lang) {
    const L = LANGS[lang];
    const road = it.edge.name, a = it.from.name, b = it.to.name;
    const dates = L.dates(fmtDate(it.start, L), fmtDate(it.end, L));
    const body = it.type === 'closure' ? L.closedBody(road, a, b, dates, it.window) : L.restrBody(road, a, b, dates, it.window);
    const title = it.type === 'closure' ? L.closedTitle(road) : L.restrTitle(road);
    const reason = it.reason[lang] ? L.reason(it.reason[lang]) : '';
    let detour = '', warn = '';
    if (it.type === 'closure') { if (it.div) detour = L.useInstead(divPathText(it)); else warn = L.noDiversion; }
    const nums = it.routes.map(r => r.no).join(', ');
    const buses = it.routes.length ? L.buses(nums) : L.noBuses;
    return { title, body, reason, detour, warn, buses, nums };
  }

  function waMessage(it, lang) {
    const L = LANGS[lang], A = advisory(it, lang);
    const icon = it.type === 'closure' ? '🚧' : '⚠️';
    const lines = [
      `${icon} *${A.title.toUpperCase()}*`,
      `📍 ${it.from.name} ↔ ${it.to.name}`,
      `📅 ${L.dates(fmtDate(it.start, L), fmtDate(it.end, L))}${it.window ? '  ⏰ ' + it.window : ''}`
    ];
    if (A.reason) lines.push(`ℹ️ ${A.reason}`);
    if (A.detour) lines.push(`↪️ ${A.detour}`);
    if (A.warn) lines.push(`❗ ${A.warn}`);
    if (it.routes.length) lines.push(`🚌 ${A.buses}`);
    lines.push('', `_${L.issuedBy(AUTHORITY[lang])} · ${fmtDate(state.asOf, L)}_`);
    return lines.join('\n');
  }

  function digest(lang) {
    const L = LANGS[lang];
    const lines = [`🚦 *${L.digestTitle} – ${fmtDate(state.asOf, L)}*`, ''];
    state.items.forEach(it => {
      const icon = it.type === 'closure' ? '🚧' : '⚠️';
      lines.push(`${icon} *${it.edge.name}* (${it.from.name} ↔ ${it.to.name})`);
      lines.push(`    ${L.dates(fmtDate(it.start, L), fmtDate(it.end, L))}${it.window ? ' · ' + it.window : ''}`);
      if (it.type === 'closure' && it.div) lines.push(`    ↪️ ${divPathText(it)}`);
    });
    const all = [...new Set(state.items.flatMap(i => i.routes.map(r => r.no)))];
    if (all.length) lines.push('', `🚌 ${L.buses(all.join(', '))}`);
    lines.push('', `_${L.issuedBy(AUTHORITY[lang])}_`);
    return lines.join('\n');
  }

  const langsToShow = () => state.lang === 'all' ? LANG_KEYS : [state.lang];
  const waCombined = (fn) => langsToShow().map(fn).join('\n\n──────────\n\n');

  function waHTML(text) {
    return esc(text)
      .replace(/\*(.+?)\*/g, '<b>$1</b>')
      .replace(/(^|\s)_(.+?)_(?=\s|$|[.,])/gm, '$1<i>$2</i>');
  }

  /* ═════════════ RENDER ═════════════ */
  function renderAll() { renderSummary(); renderMap(); renderCards(); renderWA(); renderBus(); }

  function renderSummary() {
    const closed = state.items.filter(i => i.type === 'closure').length;
    const restr = state.items.length - closed;
    const affected = new Set(state.items.flatMap(i => i.routes.map(r => r.no))).size;
    const diverted = state.items.filter(i => i.type === 'closure' && i.div).length;
    $('#summary').innerHTML = `
      <div class="stat c"><b>${closed}</b><span>Roads closed</span></div>
      <div class="stat r"><b>${restr}</b><span>Lane restrictions</span></div>
      <div class="stat d"><b>${diverted}</b><span>Diversions generated</span></div>
      <div class="stat b"><b>${affected}</b><span>Bus routes affected</span></div>`;
  }

  /* ─── Map ─── */
  function renderMap() {
    const { net, items, nodeById } = state;
    const pick = $('#routepick');
    pick.innerHTML = state.routes.map(r =>
      `<li><button data-route="${esc(r.no)}" aria-pressed="${state.hl === r.no}">Route ${esc(r.no)} · ${esc(r.name)}</button></li>`).join('');

    const P = id => nodeById[id];
    const line = (e, attrs) => `<line x1="${P(e.a).x}" y1="${P(e.a).y}" x2="${P(e.b).x}" y2="${P(e.b).y}" ${attrs}/>`;
    const mid = e => ({ x: (P(e.a).x + P(e.b).x) / 2, y: (P(e.a).y + P(e.b).y) / 2 });
    let s = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 840 540" role="img" aria-label="Schematic map of diversions" font-family="Noto Sans, system-ui, sans-serif">
      <rect width="840" height="540" fill="#EEF2F6"/>
      <path d="M0 360 C150 330 300 400 420 370 S700 330 840 380 L840 540 L0 540Z" fill="#DDE8F2" opacity=".65"/>`;

    /* base roads */
    net.edges.forEach(e => { s += line(e, 'stroke="#fff" stroke-width="13" stroke-linecap="round"'); });
    net.edges.forEach(e => { s += line(e, 'stroke="#B9C4D0" stroke-width="7" stroke-linecap="round"'); });

    /* highlighted bus route */
    const hl = state.routes.find(r => r.no === state.hl);
    if (hl) hl.edges.forEach(id => { const e = state.edgeById[id]; if (e) s += line(e, 'stroke="#1F5FBF" stroke-width="18" stroke-linecap="round" opacity=".35"'); });

    /* diversions */
    items.forEach(it => {
      if (!it.div) return;
      const op = it.status === 'upcoming' ? .55 : 1;
      it.div.edges.forEach(e => { s += line(e, `stroke="#0B8A5B" stroke-width="7" stroke-linecap="round" stroke-dasharray="2 11" opacity="${op}"`); });
      const pts = it.div.nodeIds.map(id => `${P(id).x},${P(id).y}`).join(' ');
      s += `<polyline points="${pts}" fill="none" stroke="#0B8A5B" stroke-width="3" stroke-linejoin="round" opacity="${op * .8}"/>`;
    });

    /* restrictions and closures */
    items.filter(i => i.type === 'restriction').forEach(it => {
      const op = it.status === 'upcoming' ? .55 : 1;
      s += `<g opacity="${op}"><title>${esc(it.edge.name)} – lane restriction</title>` +
           line(it.edge, 'stroke="#E88A00" stroke-width="8" stroke-linecap="round" stroke-dasharray="14 8"') + `</g>`;
    });
    items.filter(i => i.type === 'closure').forEach(it => {
      const op = it.status === 'upcoming' ? .55 : 1;
      const m = mid(it.edge);
      s += `<g opacity="${op}"><title>${esc(it.edge.name)} – road closed</title>` +
           line(it.edge, 'stroke="#C8102E" stroke-width="9" stroke-linecap="round"') +
           `<circle cx="${m.x}" cy="${m.y}" r="13" fill="#fff" stroke="#C8102E" stroke-width="3"/>` +
           `<path d="M${m.x - 6} ${m.y - 6}L${m.x + 6} ${m.y + 6}M${m.x + 6} ${m.y - 6}L${m.x - 6} ${m.y + 6}" stroke="#C8102E" stroke-width="3.5" stroke-linecap="round"/></g>`;
    });

    /* road labels */
    net.edges.forEach(e => {
      const A = P(e.a), B = P(e.b), m = mid(e);
      const dx = B.x - A.x, dy = B.y - A.y, len = Math.hypot(dx, dy) || 1;
      const nx = -dy / len, ny = dx / len, off = 17;
      const active = items.some(i => i.edge.id === e.id);
      s += `<text x="${m.x + nx * off}" y="${m.y + ny * off + 4}" text-anchor="middle" font-size="11.5" font-weight="${active ? 600 : 400}" fill="${active ? '#17283B' : '#5B6B7C'}" stroke="#EEF2F6" stroke-width="4" paint-order="stroke">${esc(e.name)}</text>`;
    });

    /* nodes */
    net.nodes.forEach(n => {
      s += `<circle cx="${n.x}" cy="${n.y}" r="8" fill="#fff" stroke="#17283B" stroke-width="3"/>`;
      s += `<text x="${n.x}" y="${n.y - 15}" text-anchor="middle" font-size="12.5" font-weight="600" fill="#17283B" stroke="#EEF2F6" stroke-width="4" paint-order="stroke">${esc(n.name)}</text>`;
    });

    s += `<text x="20" y="522" font-size="11" fill="#5B6B7C">Schematic – not to scale · ${esc(fmtDate(state.asOf, LANGS.en))}</text></svg>`;
    state.svg = s;
    $('#map').innerHTML = s;
  }

  /* ─── Advisory cards ─── */
  function renderCards() {
    const el = $('#cards');
    if (!state.items.length) { el.innerHTML = `<div class="empty">No active or upcoming works for this date. Try a different date or a longer window.</div>`; return; }
    el.innerHTML = state.items.map((it, idx) => {
      const langs = langsToShow().map(l => {
        const A = advisory(it, l);
        return `<div class="adv-lang" lang="${l}">
          ${state.lang === 'all' ? `<div class="lang-tag">${LANGS[l].name}</div>` : ''}
          <p><strong>${esc(A.title)}</strong></p>
          <p>${esc(A.body)} ${esc(A.reason)}</p>
          ${A.detour ? `<p class="detour">${esc(A.detour)}</p>` : ''}
          ${A.warn ? `<p class="warn">${esc(A.warn)}</p>` : ''}
          <p>${esc(A.buses)}</p>
        </div>`;
      }).join('');
      return `<article class="adv ${it.type}">
        <div class="adv-head">
          <h3>${esc(it.edge.name)}</h3>
          <span class="pill ${it.status}">${it.status === 'active' ? 'In effect' : 'Starts ' + esc(fmtDate(it.start, LANGS.en))}</span>
          <span class="pill">${it.type === 'closure' ? 'Road closed' : 'Lane restriction'}</span>
        </div>
        <div class="adv-langs">${langs}</div>
        <div class="adv-actions">
          <button class="btn ghost small" data-copy-adv="${idx}">Copy text</button>
        </div>
      </article>`;
    }).join('');
  }

  function advText(it) {
    return langsToShow().map(l => {
      const A = advisory(it, l);
      return [A.title, `${A.body} ${A.reason}`.trim(), A.detour, A.warn, A.buses].filter(Boolean).join('\n');
    }).join('\n\n');
  }

  /* ─── WhatsApp ─── */
  function renderWA() {
    const el = $('#wagrid');
    if (!state.items.length) { el.innerHTML = `<div class="empty" style="grid-column:1/-1">Nothing to send for this date.</div>`; return; }
    const digestTxt = waCombined(digest);
    let h = waCard('Daily digest · one message for all works', digestTxt, 'digest');
    state.items.forEach((it, i) => { h += waCard(`${it.edge.name} · ${it.type === 'closure' ? 'closure' : 'restriction'}`, waCombined(l => waMessage(it, l)), 'item' + i); });
    el.innerHTML = h;
  }
  function waCard(caption, text, key) {
    return `<div class="wa-card">
      <div class="cap">${esc(caption)}</div>
      <div class="bubble" data-key="${key}">${waHTML(text)}</div>
      <div class="row">
        <button class="btn ghost small" data-copy-wa="${key}">Copy message</button>
        <a class="btn wa small" style="text-decoration:none" target="_blank" rel="noopener" href="https://wa.me/?text=${encodeURIComponent(text)}">Open in WhatsApp</a>
      </div>
    </div>`;
  }
  const waTextByKey = key => key === 'digest' ? waCombined(digest) : waCombined(l => waMessage(state.items[+key.slice(4)], l));

  /* ─── Bus routes ─── */
  function busRows() {
    const out = [];
    state.routes.forEach(r => {
      const hits = state.items.filter(i => i.routes.includes(r));
      if (!hits.length) return;
      out.push({ r, hits });
    });
    return out;
  }
  function renderBus() {
    const rows = busRows();
    const el = $('#bustable');
    if (!rows.length) { el.innerHTML = `<div class="empty">No bus routes are affected for this date.</div>`; return; }
    const lang = state.lang === 'all' ? 'en' : state.lang;
    const L = LANGS[lang];
    el.innerHTML = `<table>
      <thead><tr><th>Route</th><th>Affected by</th><th>Status</th><th>Passenger advice</th></tr></thead>
      <tbody>${rows.map(({ r, hits }) => {
        const susp = hits.some(h => h.type === 'closure' && !h.div);
        const div = hits.filter(h => h.type === 'closure' && h.div);
        const cls = susp ? 'suspended' : div.length ? 'diverted' : 'delay';
        const label = susp ? L.statusSuspended : div.length ? L.statusDiverted : L.statusDelay;
        const advice = susp ? L.adviceSusp : div.length ? L.adviceDiv(divPathText(div[0])) : L.adviceDelay;
        return `<tr>
          <td><span class="route-no">${esc(r.no)}</span><div style="font-size:12.5px;color:var(--ink-2);margin-top:4px">${esc(r.name)}</div></td>
          <td>${hits.map(h => `${esc(h.edge.name)} <span style="color:var(--ink-2)">(${h.type === 'closure' ? L.tagClosed : L.tagRestr})</span>`).join('<br>')}</td>
          <td><span class="st ${cls}">${esc(label)}</span></td>
          <td lang="${lang}">${esc(advice)}<br><button class="btn ghost small" style="margin-top:6px" data-showroute="${esc(r.no)}">Show on map</button></td>
        </tr>`;
      }).join('')}</tbody></table>`;
  }

  /* ═════════════ EVENTS ═════════════ */
  function setTab(name) {
    state.tab = name;
    ['map', 'adv', 'wa', 'bus'].forEach(k => {
      $('#p-' + k).hidden = k !== name;
      $('#t-' + k).setAttribute('aria-selected', k === name);
    });
  }
  $$('.tab').forEach(b => b.addEventListener('click', () => setTab(b.id.slice(2))));

  $('#langseg').addEventListener('click', e => {
    const b = e.target.closest('button'); if (!b) return;
    state.lang = b.dataset.lang;
    $$('#langseg button').forEach(x => x.setAttribute('aria-pressed', x === b));
    renderCards(); renderWA(); renderBus();
  });

  document.addEventListener('click', e => {
    const t = e.target;
    const copyAdv = t.closest('[data-copy-adv]');
    if (copyAdv) return copy(advText(state.items[+copyAdv.dataset.copyAdv]), copyAdv);
    const copyWa = t.closest('[data-copy-wa]');
    if (copyWa) return copy(waTextByKey(copyWa.dataset.copyWa), copyWa);
    const rp = t.closest('#routepick button');
    if (rp) { state.hl = state.hl === rp.dataset.route ? null : rp.dataset.route; renderMap(); return; }
    const sr = t.closest('[data-showroute]');
    if (sr) { state.hl = sr.dataset.showroute; renderMap(); setTab('map'); window.scrollTo({ top: $('#map').offsetTop - 120, behavior: 'smooth' }); }
  });

  async function copy(text, btn) {
    try { await navigator.clipboard.writeText(text); }
    catch { const ta = document.createElement('textarea'); ta.value = text; document.body.appendChild(ta); ta.select(); document.execCommand('copy'); ta.remove(); }
    const old = btn.textContent; btn.textContent = 'Copied'; setTimeout(() => btn.textContent = old, 1400);
  }

  function download(name, mime, content) {
    const a = document.createElement('a');
    a.href = URL.createObjectURL(new Blob([content], { type: mime }));
    a.download = name; a.click(); URL.revokeObjectURL(a.href);
  }
  $('#dl-svg').addEventListener('click', () => download('diversion-map.svg', 'image/svg+xml', state.svg));
  $('#dl-txt').addEventListener('click', () => {
    const parts = [];
    LANG_KEYS.forEach(l => {
      parts.push(`==== ${LANGS[l].name} ====\n`);
      state.items.forEach(it => { const A = advisory(it, l); parts.push([A.title, `${A.body} ${A.reason}`.trim(), A.detour, A.warn, A.buses].filter(Boolean).join('\n') + '\n'); });
    });
    parts.push('==== WhatsApp digest ====\n', LANG_KEYS.map(digest).join('\n\n──────────\n\n'));
    download(`diversion-advisories-${iso(state.asOf)}.txt`, 'text/plain;charset=utf-8', parts.join('\n'));
  });
  $('#print').addEventListener('click', () => window.print());

  $('#gen').addEventListener('click', build);
  $('#asof').addEventListener('change', build);
  $('#horizon').addEventListener('change', build);
  let tm; $('#csv').addEventListener('input', () => { clearTimeout(tm); tm = setTimeout(build, 350); });
  $('#net').addEventListener('input', () => { clearTimeout(tm); tm = setTimeout(build, 500); });
  $('#file').addEventListener('change', e => {
    const f = e.target.files[0]; if (!f) return;
    const rd = new FileReader();
    rd.onload = () => { $('#csv').value = String(rd.result).trim(); build(); };
    rd.readAsText(f);
  });
  function init() {
    $('#csv').value = sampleCSV();
    $('#net').value = JSON.stringify(SAMPLE_NET, null, 2);
    $('#asof').value = iso(new Date());
    build();
  }
  $('#reset').addEventListener('click', init);
  init();
})();
</script>
</body>
</html>
