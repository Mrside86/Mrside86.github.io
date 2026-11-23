<html lang="fr" class="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#050505">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>DOJO // S&C OS V11</title>
<style>
  :root {
    --bg: #050505;
    --surface: #111113;
    --surface2: #1a1a1e;
    --border: #27272a;
    --text: #f4f4f5;
    --muted: #a1a1aa;
    --accent: #ef4444;
    --accent-dim: rgba(239, 68, 68, 0.15);
    --green: #10b981;
    --green-dim: rgba(16, 185, 129, 0.15);
    --amber: #f59e0b;
    --amber-dim: rgba(245, 158, 11, 0.15);
    --blue: #3b82f6;
    --blue-dim: rgba(59, 130, 246, 0.16);
    --purple: #a855f7;
    --purple-dim: rgba(168, 85, 247, 0.16);
  }
  * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
  body {
    margin: 0;
    padding: 0;
    background-color: var(--bg);
    color: var(--text);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    overflow-x: hidden;
    user-select: none;
  }
  header {
    position: sticky;
    top: 0;
    z-index: 50;
    background: rgba(5, 5, 5, 0.92);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid var(--border);
    padding: 10px 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .brand {
    font-weight: 900;
    font-size: 16px;
    letter-spacing: 0.08em;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .brand span { color: var(--accent); }
  .header-controls { display: flex; gap: 6px; }
  .pill-btn {
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--muted);
    font-size: 11px;
    font-weight: 700;
    padding: 6px 10px;
    border-radius: 999px;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 4px;
    transition: all 0.15s;
  }
  .pill-btn.active {
    background: var(--green-dim);
    border-color: var(--green);
    color: var(--green);
  }
  main {
    padding: 14px 14px 90px 14px;
    max-width: 640px;
    margin: 0 auto;
  }
  nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 50;
    background: rgba(11, 11, 13, 0.96);
    backdrop-filter: blur(12px);
    border-top: 1px solid var(--border);
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    padding-bottom: env(safe-area-inset-bottom);
  }
  .nav-item {
    background: none;
    border: none;
    color: var(--muted);
    padding: 10px 4px;
    font-size: 11px;
    font-weight: 700;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    cursor: pointer;
  }
  .nav-item.active { color: var(--accent); }
  .nav-icon { font-size: 18px; }
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 14px;
    margin-bottom: 12px;
  }
  .card-title {
    font-size: 15px;
    font-weight: 800;
    margin: 0 0 4px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 8px;
  }
  .card-sub {
    font-size: 12px;
    color: var(--muted);
    margin: 0 0 10px 0;
  }
  .badge {
    display: inline-block;
    font-size: 10px;
    font-weight: 800;
    padding: 2px 7px;
    border-radius: 6px;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--muted);
    text-transform: uppercase;
    white-space: nowrap;
  }
  .badge.kb { border-color: #3b82f6; color: #60a5fa; }
  .badge.ds { border-color: #10b981; color: #34d399; }
  .badge.pl { border-color: #06b6d4; color: #22d3ee; }
  .badge.arme { border-color: #ef4444; color: #f87171; }
  .badge.vest { border-color: #f59e0b; color: #fbbf24; background: var(--amber-dim); }
  .badge.pnf { border-color: #a855f7; color: #c084fc; }
  .btn {
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    font-weight: 700;
    font-size: 13px;
    padding: 10px 14px;
    border-radius: 8px;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }
  .btn-primary { background: var(--accent); border-color: var(--accent); color: #fff; }
  .btn-green { background: var(--green); border-color: var(--green); color: #050505; }
  .btn-purple { background: var(--purple-dim); border-color: var(--purple); color: #e9d5ff; }
  .btn-danger { background: var(--accent-dim); border-color: var(--accent); color: #fca5a5; }
  .btn-sm { padding: 6px 10px; font-size: 12px; }
  .btn-block { width: 100%; }
  .filter-bar {
    display: flex;
    gap: 6px;
    overflow-x: auto;
    padding-bottom: 8px;
    margin-bottom: 10px;
    scrollbar-width: none;
  }
  .filter-bar::-webkit-scrollbar { display: none; }
  .chip {
    background: var(--surface);
    border: 1px solid var(--border);
    color: var(--muted);
    padding: 6px 12px;
    border-radius: 999px;
    font-size: 12px;
    font-weight: 700;
    white-space: nowrap;
    cursor: pointer;
  }
  .chip.active { background: var(--text); color: var(--bg); border-color: var(--text); }
  input[type="text"], input[type="number"], select {
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 10px;
    border-radius: 8px;
    font-size: 14px;
    width: 100%;
    outline: none;
  }
  input:focus, select:focus { border-color: var(--accent); }
  .status-banner {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 10px 12px;
    margin-bottom: 12px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 12px;
    font-weight: 700;
  }
  .status-banner.danger { background: var(--accent-dim); border-color: var(--accent); color: #fca5a5; }
  .status-banner.warning { background: var(--amber-dim); border-color: var(--amber); color: #fcd34d; }
  .mod-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    margin-top: 8px;
    padding: 6px 8px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 8px;
  }
  .seg-toggle {
    display: inline-flex;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 7px;
    overflow: hidden;
  }
  .seg-btn {
    background: none;
    border: none;
    color: var(--muted);
    font-size: 11px;
    font-weight: 800;
    padding: 5px 10px;
    cursor: pointer;
  }
  .seg-btn.active {
    background: var(--blue);
    color: #fff;
  }
  .vest-toggle {
    display: flex;
    align-items: center;
    gap: 6px;
    font-size: 12px;
    font-weight: 800;
    color: var(--muted);
    cursor: pointer;
  }
  .vest-toggle.on { color: var(--amber); }
  #runner-overlay {
    position: fixed;
    inset: 0;
    z-index: 100;
    background: var(--bg);
    display: none;
    flex-direction: column;
    justify-content: space-between;
    padding: 14px;
  }
  #runner-overlay.open { display: flex; }
  .runner-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid var(--border);
    padding-bottom: 10px;
  }
  .runner-timer {
    font-size: 68px;
    font-weight: 900;
    font-variant-numeric: tabular-nums;
    text-align: center;
    line-height: 1;
    margin: 8px 0;
  }
  .pnf-cue-box {
    border-radius: 12px;
    padding: 12px;
    text-align: center;
    font-weight: 900;
    font-size: 16px;
    letter-spacing: 0.04em;
    margin: 6px 0;
    transition: all 0.2s;
  }
  .pnf-contract { background: var(--accent-dim); border: 1px solid var(--accent); color: #fca5a5; }
  .pnf-relax { background: var(--green-dim); border: 1px solid var(--green); color: #6ee7b7; }
  .rep-adjust-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 18px;
    margin: 4px 0;
  }
  .rep-adj-btn {
    width: 48px;
    height: 48px;
    border-radius: 12px;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    font-size: 22px;
    font-weight: 900;
    cursor: pointer;
  }
  .rep-adj-btn:active { background: var(--accent-dim); border-color: var(--accent); }
  .giant-tap-zone {
    flex: 1;
    min-height: 145px;
    background: var(--surface2);
    border: 2px dashed var(--border);
    border-radius: 16px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 14px;
    cursor: pointer;
    margin-top: 8px;
    transition: transform 0.08s, background 0.15s;
  }
  .giant-tap-zone:active { transform: scale(0.98); background: var(--green-dim); border-color: var(--green); }
  .modal-backdrop {
    position: fixed;
    inset: 0;
    z-index: 80;
    background: rgba(0,0,0,0.85);
    display: none;
    align-items: flex-end;
    justify-content: center;
  }
  .modal-backdrop.open { display: flex; }
  .modal-sheet {
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-radius: 18px 18px 0 0;
    width: 100%;
    max-width: 640px;
    max-height: 88vh;
    overflow-y: auto;
    padding: 18px;
  }
  .demo-canvas-wrap {
    background: #08080a;
    border: 1px solid var(--border);
    border-radius: 10px;
    height: 125px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 8px 0;
    position: relative;
    overflow: hidden;
  }
  .demo-tag {
    position: absolute;
    bottom: 6px;
    right: 8px;
    font-size: 9px;
    font-weight: 800;
    color: var(--muted);
    background: rgba(0,0,0,0.65);
    padding: 2px 6px;
    border-radius: 4px;
    letter-spacing: 0.04em;
  }
  .cat-header {
    font-size: 13px;
    font-weight: 900;
    letter-spacing: 0.06em;
    color: var(--text);
    background: var(--surface2);
    border-left: 3px solid var(--accent);
    padding: 8px 12px;
    border-radius: 6px;
    margin: 16px 0 10px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .slide-wrap {
    background: #08080a;
    border: 1px solid var(--border);
    border-radius: 10px;
    height: 155px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 8px 0;
    position: relative;
    overflow: hidden;
  }
  .slide-wrap img {
    max-height: 100%;
    max-width: 100%;
    object-fit: contain;
    transition: opacity 0.2s;
  }
  .slide-dots {
    position: absolute;
    top: 6px;
    left: 8px;
    display: flex;
    gap: 4px;
    background: rgba(0,0,0,0.7);
    padding: 3px 7px;
    border-radius: 999px;
  }
  .slide-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #52525b;
  }
  .slide-dot.active { background: var(--accent); transform: scale(1.25); }
  .slide-phase-lbl {
    position: absolute;
    bottom: 6px;
    left: 8px;
    font-size: 9px;
    font-weight: 800;
    color: #f4f4f5;
    background: rgba(239, 68, 68, 0.25);
    border: 1px solid rgba(239, 68, 68, 0.5);
    padding: 2px 6px;
    border-radius: 4px;
  }
  .slide-cam-btn {
    position: absolute;
    top: 6px;
    right: 8px;
    background: rgba(24,24,27,0.88);
    border: 1px solid var(--border);
    color: var(--text);
    font-size: 10px;
    font-weight: 800;
    padding: 3px 7px;
    border-radius: 6px;
    cursor: pointer;
    z-index: 5;
  }

</style>
</head>
<body>

<header>
  <div class="brand">DOJO <span>//</span> S&C OS</div>
  <div class="header-controls">
    <button id="btn-voice" class="pill-btn active" onclick="toggleVoice()">🔊 VOIX</button>
    <button id="btn-wakelock" class="pill-btn" onclick="toggleWakeLock()">📱 ÉCRAN</button>
  </div>
</header>

<main id="app-content"></main>

<nav>
  <button class="nav-item active" data-tab="workouts" onclick="switchTab('workouts')">
    <span class="nav-icon">⚡</span><span>Séances</span>
  </button>
  <button class="nav-item" data-tab="builder" onclick="switchTab('builder')">
    <span class="nav-icon">🛠️</span><span>Créer A-Z</span>
  </button>
  <button class="nav-item" data-tab="library" onclick="switchTab('library')">
    <span class="nav-icon">🥋</span><span>Arsenal</span>
  </button>
  <button class="nav-item" data-tab="history" onclick="switchTab('history')">
    <span class="nav-icon">📊</span><span>Logs & Data</span>
  </button>
</nav>

<div id="runner-overlay">
  <div class="runner-top">
    <div>
      <div id="run-workout-name" style="font-size:12px; font-weight:800; color:var(--accent);">SÉANCE</div>
      <div id="run-global-clock" style="font-size:12px; color:var(--muted);">⏱ 00:00 • Tonnage: 0 kg</div>
    </div>
    <div style="display:flex; gap:8px;">
      <button class="pill-btn active" id="run-voice-btn" onclick="toggleVoice()">🔊</button>
      <button class="btn btn-sm" onclick="closeRunner()">Quitter</button>
    </div>
  </div>
  <div id="run-body" style="flex:1; display:flex; flex-direction:column; justify-content:space-between; overflow-y:auto; padding-top:8px;"></div>
</div>

<div id="modal" class="modal-backdrop" onclick="if(event.target===this) closeModal()">
  <div class="modal-sheet" id="modal-content"></div>
</div>

<script>
// ==================== INVENTAIRE MATÉRIEL & VESTE LESTÉE (1 KG À 24 KG) ====================
const UNIT_LOADS = [
  "Poids du corps",
  "8 kg",
  "12 kg",
  "16 kg",
  "20 kg",
  "24 kg",
  "28 kg",
  "32 kg",
  "Bo 4 kg",
  "Bokken"
];

const SINGLE_ONLY_KB = ["28 kg", "32 kg"];
const VEST_WEIGHTS = Array.from({ length: 24 }, (_, i) => i + 1);

const CATEGORIES = [
  { id: "KB", label: "Kettlebells (KB)", badge: "kb" },
  { id: "Dip Station", label: "Dip Station (86 cm)", badge: "ds" },
  { id: "Parallettes", label: "Parallettes (PL)", badge: "pl" },
  { id: "Armes", label: "Armes (Bo 4 kg & Bokken)", badge: "arme" },
  { id: "Kicks / PNF", label: "Kicks & Mobilité PNF", badge: "pnf" },
  { id: "Sol / Core", label: "Sol & Gainage", badge: "" }
];

const RIG_OPTIONS = [
  { id: "kb_swing", label: "Balistique KB (Swing / Clean)" },
  { id: "kb_snatch", label: "Snatch Overhead KB" },
  { id: "kb_press", label: "Développé Vertical / Halo KB" },
  { id: "kb_squat", label: "Squat KB" },
  { id: "kb_lunge", label: "Fente / Cossack KB" },
  { id: "kb_dl", label: "Charnière / Deadlift KB" },
  { id: "kb_row", label: "Tirage Horizontal KB (Row)" },
  { id: "kb_windmill", label: "Windmill / Turkish Get-Up" },
  { id: "kb_floorpress", label: "Floor Press au sol" },
  { id: "kb_carry", label: "Marche Chargée (Carry)" },
  { id: "kb_curl", label: "Curl Biceps KB" },
  { id: "ds_dips", label: "Dips sur barre 86 cm" },
  { id: "ds_supporthold", label: "Appui Tendu / Scapular (DS)" },
  { id: "ds_pushup", label: "Pompes sur Parallettes" },
  { id: "ds_pike", label: "Pike Push-Up (PL)" },
  { id: "ds_planche", label: "Planche Lean / Tuck (PL)" },
  { id: "ds_invrow", label: "Tirage Inversé sous barre (DS)" },
  { id: "ds_pullup", label: "Traction Jackknife (DS)" },
  { id: "core_lsit", label: "L-Sit / Compression (DS/PL)" },
  { id: "core_legraise", label: "Relevé de Jambes / Genoux" },
  { id: "core_hollow", label: "Hollow Body / Gainage Sol" },
  { id: "core_revplank", label: "Reverse Plank / Pont" },
  { id: "core_climber", label: "Mountain Climbers (PL)" },
  { id: "arme_bo_spin", label: "Bo 4 kg — Rotations / Flow" },
  { id: "arme_bo_strike", label: "Bo 4 kg — Estocs / Frappes" },
  { id: "arme_bokken", label: "Bokken — Coupes / Suburi" },
  { id: "kick_chamber", label: "Hold Kick (Chambre / Extension)" },
  { id: "pnf_bar", label: "Étirement PNF sur Barre 86 cm" }
];

// ==================== BASE D'EXERCICES UNIFIÉE & DÉDOUBLONNÉE ====================
const BASE_EXERCISES = [
  // KETTLEBELLS (KB)
  { id:"kb_swing", name:"Swing KB (Hardstyle)", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"24 kg", pushLoad:0, rig:"kb_swing", muscle:"Fessiers / Ischios / Core", tip:"Extension explosive des hanches, verrouillage abdos/fessiers en haut." },
  { id:"kb_clean", name:"Clean KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"20 kg", pushLoad:0, rig:"kb_swing", muscle:"Hanches / Dos / Avant-bras", tip:"Garder les coudes collés aux côtes, amortir en rack sans choc." },
  { id:"kb_snatch", name:"Snatch KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"16 kg", pushLoad:1, rig:"kb_snatch", muscle:"Chaîne postérieure / Épaules", tip:"Puncher le plafond à hauteur des yeux pour éviter le claquement." },
  { id:"kb_halfsnatch", name:"Half Snatch KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:true, defaultLoad:"16 kg", pushLoad:1, rig:"kb_snatch", muscle:"Dos / Épaules / Hanches", tip:"Montée en snatch, descente contrôlée en position rack." },
  { id:"kb_cp", name:"Clean & Press KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"16 kg", pushLoad:2, elbowWarn:true, rig:"kb_press", muscle:"Deltoïdes / Triceps / Core", tip:"Contrôler la descente du press pour protéger le tendon du triceps droit." },
  { id:"kb_cp2h", name:"Clean & Press (2 mains, 1 KB)", cat:"KB", type:"reps", allowDouble:false, defaultDouble:false, defaultLoad:"20 kg", pushLoad:1, rig:"kb_press", muscle:"Épaules / Haut Pecs", tip:"Prise par les cornes d'une seule KB, trajet strict devant le visage." },
  { id:"kb_cpsq", name:"Clean & Press & Squat KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:true, defaultLoad:"16 kg", pushLoad:2, elbowWarn:true, rig:"kb_squat", muscle:"Quadriceps / Épaules / Core", tip:"Complexe complet : 1 Clean + 1 Press + 1 Front Squat." },
  { id:"kb_pushpress", name:"Push Press KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"20 kg", pushLoad:1, rig:"kb_press", muscle:"Jambes / Épaules", tip:"Impulsion des jambes pour soulager le départ du triceps." },
  { id:"kb_halo", name:"Halo KB", cat:"KB", type:"reps", allowDouble:false, defaultDouble:false, defaultLoad:"12 kg", pushLoad:0, rig:"kb_press", muscle:"Coiffe rotateurs / Thoracique", tip:"Mobilité thoracique et échauffement coiffe des rotateurs." },
  { id:"kb_dl", name:"Soulevé de terre (Deadlift) KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"32 kg", pushLoad:0, rig:"kb_dl", muscle:"Ischios / Fessiers / Lombaires", tip:"Charnière de hanche pure, dos neutre, épaules basses." },
  { id:"kb_dlupright", name:"Deadlift to Upright Row KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:false, defaultLoad:"20 kg", pushLoad:0, rig:"kb_dl", muscle:"Trapèzes / Deltoïdes / Ischios", tip:"Tirer les coudes haut sans casser les poignets." },
  { id:"kb_shrugs", name:"Shrugs KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:true, defaultLoad:"24 kg", pushLoad:0, rig:"kb_dl", muscle:"Trapèzes supérieurs / Poigne", tip:"Maintien 2s en contraction haute des trapèzes." },
  { id:"kb_goblet", name:"Goblet Squat KB", cat:"KB", type:"reps", allowDouble:false, defaultDouble:false, defaultLoad:"24 kg", pushLoad:0, rig:"kb_squat", muscle:"Quadriceps / Fessiers / Core", tip:"Coudes à l'intérieur des genoux en bas du squat." },
  { id:"kb_racksq", name:"Rack Squat KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:true, defaultLoad:"20 kg", pushLoad:0, rig:"kb_squat", muscle:"Quadriceps / Gainage antérieur", tip:"Avant-bras verticaux, cage thoracique haute (1 KB asymétrique ou 2 KB)." },
  { id:"kb_cleanrack", name:"Clean Rack Squat KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:true, defaultLoad:"16 kg", pushLoad:0, rig:"kb_squat", muscle:"Jambes / Chaîne postérieure", tip:"Enchaîner chaque squat après un clean propre." },
  { id:"kb_snatchrack", name:"Snatch Rack Squat KB", cat:"KB", type:"reps", allowDouble:true, defaultDouble:true, defaultLoad:"12 kg", pushLoad:1, rig:"kb_snatch", mu
