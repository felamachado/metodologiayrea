# modulo3.html — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Crear `metodologia/modulo3.html`, una página educativa interactiva de pestaña única que consolida los 4 bloques del Módulo 3 (EVA, Elementos, Tutor Virtual, Organización) con modales, videos embebidos, acordeones y recursos enlazados.

**Architecture:** Archivo HTML autocontenido con CSS y JS embebidos. Sistema de pestañas con JS vanilla (show/hide panels). Sistema de modales reutilizable con overlay. Sin dependencias externas excepto iframes de YouTube.

**Tech Stack:** HTML5, CSS3 (Grid, Flexbox, custom properties, transitions), JS vanilla (DOM API)

**Spec:** `docs/superpowers/specs/2026-05-13-modulo3-design.md`

---

### Task 1: Scaffold — Estructura base, CSS completo y sistema de tabs

**Files:**
- Create: `metodologia/modulo3.html`

- [ ] **Crear el archivo con doctype, head, y todas las CSS custom properties y estilos base**

```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Módulo 3: Construcción de un Curso en un EVA</title>
<style>
/* ── RESET & BASE ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --primary:      #1a237e;
  --primary-mid:  #283593;
  --primary-lt:   #1565c0;
  --accent:       #e65100;
  --accent-soft:  #fff8e1;
  --accent-border:#ffe082;
  --bg:           #f0f4f8;
  --card:         #ffffff;
  --border:       #e2e8f0;
  --text:         #1a1a2e;
  --muted:        #555;
  --radius-lg:    14px;
  --radius-md:    10px;
  --radius-sm:    8px;
  --shadow-sm:    0 2px 8px rgba(0,0,0,.06);
  --shadow-md:    0 4px 20px rgba(26,35,126,.12);
}
body {
  font-family: system-ui, -apple-system, 'Segoe UI', sans-serif;
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
  min-height: 100vh;
}

/* ── HEADER ── */
.page-header {
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-mid) 55%, var(--primary-lt) 100%);
  padding: 36px 24px 28px;
  color: #fff;
  position: relative;
  overflow: hidden;
}
.page-header::before {
  content: '';
  position: absolute;
  top: -40px; right: -40px;
  width: 200px; height: 200px;
  border-radius: 50%;
  background: rgba(255,255,255,.05);
  pointer-events: none;
}
.header-inner { max-width: 860px; margin: 0 auto; }
.header-badge {
  display: inline-block;
  background: rgba(255,255,255,.15);
  border: 1px solid rgba(255,255,255,.25);
  border-radius: 20px;
  padding: 4px 14px;
  font-size: .72rem;
  font-weight: 700;
  letter-spacing: .08em;
  text-transform: uppercase;
  color: #c5cae9;
  margin-bottom: 12px;
}
.page-header h1 {
  font-size: 1.65rem;
  font-weight: 800;
  line-height: 1.2;
  margin-bottom: 8px;
}
.page-header .lead {
  font-size: .92rem;
  color: #c5cae9;
  max-width: 600px;
  line-height: 1.65;
}

/* ── TAB BAR ── */
.tab-bar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--card);
  border-bottom: 2px solid var(--border);
  box-shadow: 0 2px 8px rgba(0,0,0,.08);
}
.tab-bar-inner {
  max-width: 860px;
  margin: 0 auto;
  display: flex;
}
.tab-btn {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 14px 10px;
  background: none;
  border: none;
  border-bottom: 3px solid transparent;
  font-size: .85rem;
  font-weight: 600;
  color: var(--muted);
  cursor: pointer;
  transition: color .2s, border-color .2s, background .2s;
  white-space: nowrap;
}
.tab-btn:hover { color: var(--primary); background: #f5f7ff; }
.tab-btn.active { color: var(--primary); border-bottom-color: var(--primary); }
.tab-btn .tab-icon { font-size: 1.1rem; }

/* ── TAB PANELS ── */
.tab-panels { max-width: 860px; margin: 0 auto; padding: 24px 20px 48px; }
.tab-panel { display: none; animation: fadeIn .3s ease; }
.tab-panel.active { display: block; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

/* ── SECTION HEADING ── */
.section-heading { margin: 28px 0 16px; }
.section-heading h2 {
  font-size: 1.2rem; font-weight: 700; color: var(--primary);
  margin-bottom: 4px;
}
.section-heading p { font-size: .85rem; color: var(--muted); }

/* ── CARDS GRID ── */
.card-grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin: 16px 0; }
.card-grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; margin: 16px 0; }
.card-grid-auto { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; margin: 16px 0; }

/* ── GENERIC CARD ── */
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 22px;
  box-shadow: var(--shadow-sm);
}

/* ── CLICKABLE CARD (opens modal) ── */
.card-clickable {
  cursor: pointer;
  transition: transform .2s, box-shadow .2s, border-color .2s;
  position: relative;
}
.card-clickable:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
  border-color: #bccfff;
}
.card-clickable .card-hint {
  position: absolute;
  bottom: 12px; right: 14px;
  font-size: .7rem;
  color: var(--primary-lt);
  font-weight: 600;
  opacity: 0;
  transition: opacity .2s;
}
.card-clickable:hover .card-hint { opacity: 1; }
.card-icon { font-size: 1.8rem; margin-bottom: 10px; }
.card h3 { font-size: .95rem; font-weight: 700; color: var(--primary); margin-bottom: 6px; }
.card p { font-size: .84rem; color: var(--muted); line-height: 1.55; }

/* ── NAV CARDS (Tab 1) ── */
.nav-card {
  text-align: center;
  padding: 28px 20px 22px;
  cursor: pointer;
}
.nav-card .nav-card-icon { font-size: 2.4rem; margin-bottom: 14px; display: block; }
.nav-card h3 { font-size: 1rem; margin-bottom: 8px; }
.nav-card .btn { margin-top: 14px; }

/* ── BUTTONS ── */
.btn {
  display: inline-block;
  padding: 9px 20px;
  background: var(--primary);
  color: #fff;
  border-radius: var(--radius-sm);
  text-decoration: none;
  font-size: .82rem;
  font-weight: 600;
  border: none;
  cursor: pointer;
  transition: background .15s;
}
.btn:hover { background: var(--primary-lt); }
.btn-outline {
  background: transparent;
  border: 2px solid var(--primary);
  color: var(--primary);
}
.btn-outline:hover { background: var(--primary); color: #fff; }
.btn-resource {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 18px;
  background: #f5f7ff;
  border: 1px solid #c5cae9;
  border-radius: var(--radius-sm);
  color: var(--primary);
  font-size: .84rem;
  font-weight: 600;
  text-decoration: none;
  transition: background .15s, border-color .15s;
}
.btn-resource:hover { background: #e8eaf6; border-color: var(--primary); }
.resource-links { display: flex; flex-wrap: wrap; gap: 10px; margin: 14px 0; }

/* ── HIGHLIGHT BOX ── */
.highlight-box {
  background: var(--accent-soft);
  border-left: 4px solid var(--accent);
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
  padding: 16px 20px;
  margin: 16px 0;
}
.highlight-box strong { color: var(--accent); }
.highlight-box p { font-size: .88rem; color: #444; line-height: 1.65; margin: 0; }

/* ── SEPARATOR (Recursos vs Actividades) ── */
.sep-wrap { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin: 16px 0; }
.sep-box { border-radius: var(--radius-md); padding: 18px; text-align: center; }
.sep-recursos { background: #e3f2fd; border: 2px solid #1565c0; }
.sep-actividades { background: #fce4ec; border: 2px solid #c62828; }
.sep-box h4 { font-size: .9rem; font-weight: 700; margin-bottom: 8px; }
.sep-recursos h4 { color: #1565c0; }
.sep-actividades h4 { color: #c62828; }
.sep-box ul { list-style: none; font-size: .81rem; color: #444; line-height: 1.9; }
.sep-box ul li::before { margin-right: 4px; }
.sep-recursos li::before { content: '📄'; }
.sep-actividades li::before { content: '✏️'; }

/* ── STRUCTURE DIAGRAM (Tab 2) ── */
.structure-diagram { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin: 16px 0; }
.struct-block { border-radius: var(--radius-md); padding: 18px; }
.struct-general { background: #e8f5e9; border: 2px solid #388e3c; }
.struct-desarrollo { background: #fff3e0; border: 2px solid #e65100; }
.struct-block h4 { font-size: .9rem; font-weight: 700; margin-bottom: 8px; }
.struct-general h4 { color: #2e7d32; }
.struct-desarrollo h4 { color: var(--accent); }
.struct-block ul { list-style: none; font-size: .82rem; color: #444; line-height: 1.85; }
.struct-block ul li::before { content: '▸ '; color: inherit; }

/* ── FUNCTION CARDS (2×2 grid, Tab 3) ── */
.func-card {
  background: #f8faff;
  border: 1px solid #dce8ff;
  border-radius: var(--radius-md);
  padding: 20px;
}
.func-card .func-icon { font-size: 1.8rem; margin-bottom: 10px; display: block; }
.func-card h3 { font-size: .95rem; font-weight: 700; color: var(--primary); margin-bottom: 6px; }
.func-card p { font-size: .83rem; color: var(--muted); line-height: 1.55; }

/* ── ACCORDION (5 roles, Tab 3) ── */
.accordion-list { margin: 16px 0; }
.acc-item {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  margin-bottom: 8px;
  overflow: hidden;
}
.acc-trigger {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 14px 18px;
  background: none;
  border: none;
  cursor: pointer;
  text-align: left;
  font-size: .9rem;
  font-weight: 700;
  color: var(--text);
  transition: background .15s;
}
.acc-trigger:hover { background: #f5f7ff; }
.acc-num {
  width: 28px; height: 28px;
  background: var(--primary);
  color: #fff;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: .72rem; font-weight: 700; flex-shrink: 0;
}
.acc-arrow { margin-left: auto; font-size: .75rem; transition: transform .25s; }
.acc-item.open .acc-arrow { transform: rotate(180deg); }
.acc-body {
  max-height: 0;
  overflow: hidden;
  transition: max-height .3s ease;
}
.acc-body-inner {
  padding: 0 18px 16px 60px;
  font-size: .86rem;
  color: var(--muted);
  line-height: 1.65;
}
.acc-item.open .acc-body { max-height: 200px; }

/* ── FOLDER CARDS (Tab 4) ── */
.folder-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 20px;
  display: flex;
  gap: 16px;
  align-items: flex-start;
  cursor: pointer;
  transition: transform .2s, box-shadow .2s;
}
.folder-card:hover { transform: translateY(-3px); box-shadow: var(--shadow-md); }
.folder-card .f-icon { font-size: 2.2rem; flex-shrink: 0; }
.folder-card h3 { font-size: .95rem; font-weight: 700; color: var(--primary); margin-bottom: 6px; }
.folder-card p { font-size: .84rem; color: var(--muted); line-height: 1.55; }
.folder-cards-col { display: flex; flex-direction: column; gap: 12px; margin: 16px 0; }

/* ── TIMELINE (Evaluación, Tab 4) ── */
.timeline { display: flex; gap: 0; margin: 20px 0; }
.timeline-step {
  flex: 1;
  background: #f3e5f5;
  border: 1px solid #ce93d8;
  padding: 18px 16px;
  text-align: center;
  position: relative;
}
.timeline-step:first-child { border-radius: var(--radius-md) 0 0 var(--radius-md); }
.timeline-step:last-child { border-radius: 0 var(--radius-md) var(--radius-md) 0; }
.timeline-step + .timeline-step::before {
  content: '▶';
  position: absolute;
  left: -12px; top: 50%;
  transform: translateY(-50%);
  color: #7b1fa2;
  font-size: .8rem;
  z-index: 1;
}
.timeline-step .step-num {
  font-size: 1.4rem; font-weight: 800; color: #7b1fa2;
  display: block; margin-bottom: 6px;
}
.timeline-step h4 { font-size: .82rem; font-weight: 700; color: #4a148c; margin-bottom: 4px; }
.timeline-step p { font-size: .76rem; color: #555; line-height: 1.45; }

/* ── VIDEO WRAPPER ── */
.video-section { margin: 20px 0; }
.video-label {
  font-size: .78rem; font-weight: 700; letter-spacing: .06em;
  text-transform: uppercase; color: var(--muted);
  margin-bottom: 8px; display: flex; align-items: center; gap: 6px;
}
.video-responsive {
  position: relative; padding-top: 56.25%;
  border-radius: var(--radius-md); overflow: hidden;
  background: #000; box-shadow: var(--shadow-sm);
}
.video-responsive iframe {
  position: absolute; top: 0; left: 0;
  width: 100%; height: 100%; border: none;
}

/* ── INTRO QUOTE ── */
.intro-quote {
  background: var(--card);
  border-left: 4px solid var(--primary);
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
  padding: 18px 22px;
  margin: 16px 0;
  box-shadow: var(--shadow-sm);
}
.intro-quote p { font-size: .92rem; color: #333; line-height: 1.75; font-style: italic; }
.intro-quote cite { font-size: .78rem; color: var(--muted); font-style: normal; display: block; margin-top: 8px; }

/* ── MODAL ── */
.modal-overlay {
  display: none;
  position: fixed; inset: 0;
  background: rgba(0,0,0,.55);
  z-index: 1000;
  align-items: center;
  justify-content: center;
  padding: 20px;
  animation: fadeOverlay .2s ease;
}
.modal-overlay.open { display: flex; }
@keyframes fadeOverlay { from { opacity: 0; } to { opacity: 1; } }
.modal-box {
  background: var(--card);
  border-radius: var(--radius-lg);
  max-width: 620px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 20px 60px rgba(0,0,0,.3);
  animation: scaleIn .25s ease;
}
@keyframes scaleIn { from { opacity: 0; transform: scale(.92); } to { opacity: 1; transform: scale(1); } }
.modal-header {
  display: flex; align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  padding: 22px 22px 16px;
  border-bottom: 1px solid var(--border);
  position: sticky; top: 0;
  background: var(--card);
  border-radius: var(--radius-lg) var(--radius-lg) 0 0;
}
.modal-header h2 { font-size: 1.05rem; font-weight: 700; color: var(--primary); }
.modal-close {
  background: none; border: none; cursor: pointer;
  font-size: 1.2rem; color: var(--muted);
  padding: 2px 6px; border-radius: 6px;
  transition: background .15s;
  flex-shrink: 0;
}
.modal-close:hover { background: var(--border); }
.modal-body { padding: 20px 22px 24px; }
.modal-body p { font-size: .9rem; color: #333; line-height: 1.7; margin-bottom: 12px; }
.modal-body ul { padding-left: 18px; font-size: .88rem; color: #444; line-height: 1.8; }
.modal-body h4 { font-size: .9rem; font-weight: 700; color: var(--primary); margin: 14px 0 6px; }

/* ── CHIP / TAG ── */
.chip {
  display: inline-block;
  background: #e3f2fd; color: var(--primary-lt);
  border-radius: 20px; padding: 3px 12px;
  font-size: .72rem; font-weight: 700; letter-spacing: .04em;
}
.chip-accent { background: #fff3e0; color: var(--accent); }

/* ── RESPONSIVE ── */
@media (max-width: 640px) {
  .page-header h1 { font-size: 1.25rem; }
  .card-grid-2, .card-grid-3, .structure-diagram, .sep-wrap { grid-template-columns: 1fr; }
  .tab-btn .tab-label { display: none; }
  .timeline { flex-direction: column; }
  .timeline-step { border-radius: var(--radius-sm) !important; }
  .timeline-step + .timeline-step::before { content: '▼'; left: 50%; top: -12px; transform: translateX(-50%); }
}
@media (max-width: 440px) {
  .tab-panels { padding: 16px 14px 40px; }
}
</style>
</head>
<body>
<!-- ═══════ HEADER ═══════ -->
<div class="page-header">
  <div class="header-inner">
    <span class="header-badge">📚 Profesorado de Informática · Metodología EaD</span>
    <h1>Módulo 3: Construcción de un Curso en un EVA y el Rol Docente</h1>
    <p class="lead">Explorá los componentes de un Entorno Virtual de Aprendizaje, el nuevo rol del tutor y la organización técnica de recursos educativos digitales.</p>
  </div>
</div>

<!-- ═══════ TAB BAR ═══════ -->
<nav class="tab-bar" role="tablist">
  <div class="tab-bar-inner">
    <button class="tab-btn active" onclick="switchTab('inicio')" role="tab" aria-selected="true">
      <span class="tab-icon">🏠</span><span class="tab-label">Inicio</span>
    </button>
    <button class="tab-btn" onclick="switchTab('elementos')" role="tab" aria-selected="false">
      <span class="tab-icon">🏗️</span><span class="tab-label">Elementos del EVA</span>
    </button>
    <button class="tab-btn" onclick="switchTab('tutor')" role="tab" aria-selected="false">
      <span class="tab-icon">🧑‍🏫</span><span class="tab-label">El Tutor Virtual</span>
    </button>
    <button class="tab-btn" onclick="switchTab('recursos')" role="tab" aria-selected="false">
      <span class="tab-icon">📁</span><span class="tab-label">Organización</span>
    </button>
  </div>
</nav>

<!-- ═══════ TAB PANELS (vacíos por ahora) ═══════ -->
<div class="tab-panels">
  <div id="panel-inicio"    class="tab-panel active"><!-- Task 2 --></div>
  <div id="panel-elementos" class="tab-panel"><!-- Task 3 --></div>
  <div id="panel-tutor"     class="tab-panel"><!-- Task 4 --></div>
  <div id="panel-recursos"  class="tab-panel"><!-- Task 5 --></div>
</div>

<!-- ═══════ MODAL OVERLAY ═══════ -->
<div id="modal-overlay" class="modal-overlay" onclick="closeModalOnOverlay(event)" role="dialog" aria-modal="true">
  <div class="modal-box">
    <div class="modal-header">
      <h2 id="modal-title"></h2>
      <button class="modal-close" onclick="closeModal()" aria-label="Cerrar">✕</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
  </div>
</div>

<script>
// ── TAB SYSTEM ──
function switchTab(name) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => {
    b.classList.remove('active');
    b.setAttribute('aria-selected', 'false');
  });
  document.getElementById('panel-' + name).classList.add('active');
  const btn = [...document.querySelectorAll('.tab-btn')]
    .find(b => b.getAttribute('onclick') === "switchTab('" + name + "')");
  if (btn) { btn.classList.add('active'); btn.setAttribute('aria-selected', 'true'); }
}

// ── MODAL SYSTEM ──
const MODAL_DATA = {}; // populated in Task 6

function openModal(key) {
  const data = MODAL_DATA[key];
  if (!data) return;
  document.getElementById('modal-title').textContent = data.title;
  document.getElementById('modal-body').innerHTML = data.body;
  document.getElementById('modal-overlay').classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeModal() {
  document.getElementById('modal-overlay').classList.remove('open');
  document.body.style.overflow = '';
}
function closeModalOnOverlay(e) {
  if (e.target === document.getElementById('modal-overlay')) closeModal();
}
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

// ── ACCORDION SYSTEM ──
function toggleAcc(el) {
  const item = el.closest('.acc-item');
  const isOpen = item.classList.contains('open');
  document.querySelectorAll('.acc-item.open').forEach(i => i.classList.remove('open'));
  if (!isOpen) item.classList.add('open');
}
</script>
</body>
</html>
```

- [ ] **Verificar en browser:** Abrir el archivo. Debe mostrar el header azul, la tab bar con 4 botones, y al hacer click entre tabs el contenido cambia (vacío pero sin errores JS).

- [ ] **Commit**
```bash
git add metodologia/modulo3.html
git commit -m "feat: scaffold modulo3.html — header, tab bar, modal system, all CSS"
```

---

### Task 2: Tab 1 — Inicio

**Files:**
- Modify: `metodologia/modulo3.html` — reemplazar `<!-- Task 2 -->` en `#panel-inicio`

- [ ] **Reemplazar el comentario en `#panel-inicio` con este HTML:**

```html
<div class="intro-quote">
  <p>Un Ambiente o Entorno Virtual de Aprendizaje (EVA) es un espacio interactivo, sincrónico y asincrónico, donde el docente cumple un papel de <strong>facilitador</strong>. La incorporación de las TIC ha propiciado un cambio de paradigma: el estudiante se convierte en el centro del proceso y protagonista en la construcción de sus propios saberes, <em>rompiendo las barreras tradicionales de espacio y tiempo</em>.</p>
  <cite>— Fundamentos de Metodología de la Educación a Distancia</cite>
</div>

<div class="highlight-box">
  <p><strong>¿Qué vas a encontrar en este módulo?</strong> Tres grandes bloques organizan el recorrido: la estructura técnica y pedagógica de un EVA, el nuevo rol del docente como tutor virtual, y la organización eficiente de archivos y la evaluación multimodal.</p>
</div>

<div class="section-heading">
  <h2>Navegá el módulo</h2>
  <p>Hacé click en una sección para explorarla</p>
</div>

<div class="card-grid-3">
  <div class="card nav-card card-clickable" onclick="switchTab('elementos')">
    <span class="nav-card-icon">🏗️</span>
    <h3>Elementos del EVA</h3>
    <p>Los 6 espacios fundamentales, la estructura visual de un aula virtual y la separación entre recursos y actividades.</p>
    <button class="btn" style="margin-top:14px;">Explorar →</button>
  </div>
  <div class="card nav-card card-clickable" onclick="switchTab('tutor')">
    <span class="nav-card-icon">🧑‍🏫</span>
    <h3>El Tutor Virtual</h3>
    <p>Las 4 áreas de función docente y los 5 roles específicos identificados por la investigación educativa actual.</p>
    <button class="btn" style="margin-top:14px;">Explorar →</button>
  </div>
  <div class="card nav-card card-clickable" onclick="switchTab('recursos')">
    <span class="nav-card-icon">📁</span>
    <h3>Organización y Recursos</h3>
    <p>Arquitectura de carpetas para cursos en línea y evaluación multimodal integrando TIC de forma transversal.</p>
    <button class="btn" style="margin-top:14px;">Explorar →</button>
  </div>
</div>
```

- [ ] **Verificar:** La Tab 1 muestra la quote, el highlight box y las 3 cards. Hacer click en una card navega a la tab correspondiente.

- [ ] **Commit**
```bash
git add metodologia/modulo3.html
git commit -m "feat: tab 1 inicio — intro quote, highlight box, nav cards"
```

---

### Task 3: Tab 2 — Elementos del EVA

**Files:**
- Modify: `metodologia/modulo3.html` — reemplazar `<!-- Task 3 -->` en `#panel-elementos`

- [ ] **Reemplazar el comentario en `#panel-elementos` con este HTML:**

```html
<div class="section-heading">
  <h2>Los 6 Espacios Fundamentales</h2>
  <p>Hacé click en cada espacio para ver más detalles</p>
</div>

<div class="card-grid-auto">
  <div class="card card-clickable" onclick="openModal('esp-avisos')">
    <div class="card-icon">📢</div>
    <h3>Avisos</h3>
    <p>Bienvenida institucional y recomendaciones generales.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card card-clickable" onclick="openModal('esp-info')">
    <div class="card-icon">📋</div>
    <h3>Información del Curso</h3>
    <p>Bienvenida del profesor, metodología y evaluación.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card card-clickable" onclick="openModal('esp-programa')">
    <div class="card-icon">🗓️</div>
    <h3>Programa</h3>
    <p>Organizador previo, cronograma y materiales de apoyo.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card card-clickable" onclick="openModal('esp-recursos')">
    <div class="card-icon">📚</div>
    <h3>Recursos de Apoyo</h3>
    <p>Accesos externos y concentrado de materiales.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card card-clickable" onclick="openModal('esp-herramientas')">
    <div class="card-icon">🔧</div>
    <h3>Herramientas</h3>
    <p>Elementos de la plataforma para la interacción.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card card-clickable" onclick="openModal('esp-equipo')">
    <div class="card-icon">👥</div>
    <h3>Equipo Docente</h3>
    <p>Datos del profesor titular, tutor y soporte técnico.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
</div>

<div class="section-heading">
  <h2>Estructura Visual del Aula Virtual</h2>
  <p>Cómo organizar la interfaz de Moodle, Schoology o CREA</p>
</div>

<div class="structure-diagram">
  <div class="struct-block struct-general">
    <h4>🟢 Sección General (Cabecera)</h4>
    <ul>
      <li>Banner o logotipo del curso</li>
      <li>Foro de Avisos (novedades)</li>
      <li>Foro de Cafetería (interacción social)</li>
      <li>Syllabus / Guía general</li>
      <li>Bibliografía transversal</li>
    </ul>
  </div>
  <div class="struct-block struct-desarrollo">
    <h4>🟠 Sección de Desarrollo (Módulos)</h4>
    <ul>
      <li>Fraccionar por temas, unidades o semanas</li>
      <li>Cada unidad con objetivos claros</li>
      <li>Etiquetas visuales separadoras</li>
      <li>Actividades de cierre por módulo</li>
    </ul>
  </div>
</div>

<div class="section-heading">
  <h2>⚖️ La Separación Clave</h2>
  <p>Regla de oro del diseño instruccional: separar siempre los recursos de las actividades</p>
</div>

<div class="sep-wrap">
  <div class="sep-box sep-recursos">
    <h4>📄 RECURSOS</h4>
    <ul>
      <li>Archivos PDF / Word</li>
      <li>Carpetas de material</li>
      <li>Videos explicativos</li>
      <li>Hipervínculos externos</li>
      <li>Presentaciones</li>
    </ul>
  </div>
  <div class="sep-box sep-actividades">
    <h4>✏️ ACTIVIDADES</h4>
    <ul>
      <li>Foros de debate</li>
      <li>Tareas con entregables</li>
      <li>Cuestionarios y tests</li>
      <li>Wikis colaborativas</li>
      <li>Glosarios participativos</li>
    </ul>
  </div>
</div>

<div class="section-heading"><h2>📺 Recursos Audiovisuales</h2></div>

<div class="video-section">
  <p class="video-label">▶ Video — Componentes o elementos de un curso en línea</p>
  <div class="video-responsive">
    <iframe src="https://www.youtube.com/embed/Vo9hgfltwPU" title="Componentes o elementos de un curso en línea" allowfullscreen loading="lazy"></iframe>
  </div>
</div>

<div class="video-section">
  <p class="video-label">▶ Video — Ejemplo de Elementos Básicos de un Curso Virtual</p>
  <div class="video-responsive">
    <iframe src="https://www.youtube.com/embed/6SHunbIQ-Lo" title="Ejemplo de Elementos Básicos de un Curso Virtual" allowfullscreen loading="lazy"></iframe>
  </div>
</div>
```

- [ ] **Verificar:** Las 6 cards se muestran. Los videos cargan. Los clicks en cards no abren modal aún (se llena en Task 6, no hay error JS).

- [ ] **Commit**
```bash
git add metodologia/modulo3.html
git commit -m "feat: tab 2 elementos EVA — 6 espacios, estructura visual, recursos vs actividades, 2 videos"
```

---

### Task 4: Tab 3 — El Tutor Virtual

**Files:**
- Modify: `metodologia/modulo3.html` — reemplazar `<!-- Task 4 -->` en `#panel-tutor`

- [ ] **Reemplazar el comentario en `#panel-tutor` con este HTML:**

```html
<div class="intro-quote">
  <p>En la enseñanza mediada por tecnología, el docente abandona el rol de mero transmisor de información. El <strong>tutor virtual</strong> orienta, enseña e integra al alumno en el sistema, incentivando el estudio independiente y mitigando las ansiedades que produce la distancia.</p>
</div>

<div class="section-heading">
  <h2>Las 4 Áreas de Función del Tutor</h2>
  <p>Hacé click en cada área para ver ejemplos prácticos</p>
</div>

<div class="card-grid-2">
  <div class="card func-card card-clickable" onclick="openModal('func-pedagogica')">
    <span class="func-icon">🎓</span>
    <h3>Pedagógica</h3>
    <p>Planificador, guía y moderador. Elabora materiales significativos y fomenta la construcción de saberes.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card func-card card-clickable" onclick="openModal('func-social')">
    <span class="func-icon">🤝</span>
    <h3>Social</h3>
    <p>Crea entornos cooperativos y colaborativos. Fomenta la empatía y mitiga el aislamiento del estudiante.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card func-card card-clickable" onclick="openModal('func-administrativa')">
    <span class="func-icon">📊</span>
    <h3>Administrativa</h3>
    <p>Establece normas, gestiona grupos de trabajo y evalúa los resultados y tiempos del curso.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
  <div class="card func-card card-clickable" onclick="openModal('func-tecnica')">
    <span class="func-icon">💻</span>
    <h3>Técnica</h3>
    <p>Domina las herramientas del entorno virtual para que la tecnología sea un puente, no un obstáculo.</p>
    <span class="card-hint">Ver más ›</span>
  </div>
</div>

<div class="section-heading">
  <h2>Los 5 Roles Específicos del Docente Virtual</h2>
  <p>Según Badia, Meneses y García (2017) — Hacé click para expandir cada rol</p>
</div>

<div class="accordion-list">
  <div class="acc-item">
    <button class="acc-trigger" onclick="toggleAcc(this)">
      <span class="acc-num">1</span>
      Diseño Instruccional
      <span class="acc-arrow">▼</span>
    </button>
    <div class="acc-body">
      <div class="acc-body-inner">
        Selección, diseño y adaptación de contenidos y actividades de aprendizaje. El tutor define la secuencia didáctica, elige los formatos más adecuados para cada objetivo y adapta los materiales al perfil de sus estudiantes.
      </div>
    </div>
  </div>
  <div class="acc-item">
    <button class="acc-trigger" onclick="toggleAcc(this)">
      <span class="acc-num">2</span>
      Gestión de la Interacción Social
      <span class="acc-arrow">▼</span>
    </button>
    <div class="acc-body">
      <div class="acc-body-inner">
        Promover relaciones de confianza, fomentar la participación activa y resolver conflictos dentro del grupo. El clima social del aula virtual depende en gran medida de la proactividad del tutor en los espacios de intercambio.
      </div>
    </div>
  </div>
  <div class="acc-item">
    <button class="acc-trigger" onclick="toggleAcc(this)">
      <span class="acc-num">3</span>
      Guía en el Uso de la Tecnología
      <span class="acc-arrow">▼</span>
    </button>
    <div class="acc-body">
      <div class="acc-body-inner">
        Orientar al estudiante en el uso adecuado del entorno virtual. Esto incluye responder consultas técnicas, elaborar tutoriales de uso y hacer que la plataforma resulte transparente para el proceso de aprendizaje.
      </div>
    </div>
  </div>
  <div class="acc-item">
    <button class="acc-trigger" onclick="toggleAcc(this)">
      <span class="acc-num">4</span>
      Evaluación del Aprendizaje
      <span class="acc-arrow">▼</span>
    </button>
    <div class="acc-body">
      <div class="acc-body-inner">
        Seguimiento continuo del progreso, corrección de trabajos y provisión de retroalimentación formativa y sumativa. La evaluación en entornos virtuales debe ser coherente con los objetivos y diversificar los instrumentos.
      </div>
    </div>
  </div>
  <div class="acc-item">
    <button class="acc-trigger" onclick="toggleAcc(this)">
      <span class="acc-num">5</span>
      Apoyo al Aprendizaje
      <span class="acc-arrow">▼</span>
    </button>
    <div class="acc-body">
      <div class="acc-body-inner">
        Regulación del proceso de estudio individual y el ritmo de los estudiantes. El tutor identifica a quienes se están quedando atrás, interviene a tiempo y ofrece estrategias personalizadas de organización y estudio autónomo.
      </div>
    </div>
  </div>
</div>

<div class="section-heading"><h2>📥 Fuentes Bibliográficas</h2></div>

<div class="resource-links">
  <a href="Modulo3/Recursos/Badia_Meneses_Garcia_ES_2017.pdf" target="_blank" rel="noopener" class="btn-resource">
    📄 Badia, Meneses y García (2017) — Roles docentes en EVA
  </a>
  <a href="Modulo3/Recursos/El_tutor.pdf" target="_blank" rel="noopener" class="btn-resource">
    📄 El Tutor Virtual — Funciones y competencias
  </a>
</div>

<div class="section-heading"><h2>📺 Recursos Audiovisuales</h2></div>

<div class="video-section">
  <p class="video-label">▶ Video — Procesos, estrategias y evaluación de la Educación Multimodal</p>
  <div class="video-responsive">
    <iframe src="https://www.youtube.com/embed/j3xqo3pabZM" title="Procesos, estrategias y evaluación de la Educación Multimodal" allowfullscreen loading="lazy"></iframe>
  </div>
</div>
```

- [ ] **Verificar:** Las 4 func-cards se muestran en grid 2×2. El acordeón abre/cierra al click. El video carga. Los links de PDF apuntan a las rutas correctas.

- [ ] **Commit**
```bash
git add metodologia/modulo3.html
git commit -m "feat: tab 3 tutor virtual — 4 func cards, 5 roles accordion, PDF links, video"
```

---

### Task 5: Tab 4 — Organización y Recursos

**Files:**
- Modify: `metodologia/modulo3.html` — reemplazar `<!-- Task 5 -->` en `#panel-recursos`

- [ ] **Reemplazar el comentario en `#panel-recursos` con este HTML:**

```html
<div class="section-heading">
  <h2>Arquitectura de Carpetas para Cursos Online</h2>
  <p>Hacé click en cada área para ver la estructura interna</p>
</div>

<div class="folder-cards-col">
  <div class="folder-card" onclick="openModal('folder-estandares')">
    <span class="f-icon">📦</span>
    <div>
      <h3>Estándares</h3>
      <p>Elementos reutilizables con el formato del curso: iconografía, fondos, audio y plantillas. Se usan en todos los módulos sin modificación.</p>
    </div>
  </div>
  <div class="folder-card" onclick="openModal('folder-recursos')">
    <span class="f-icon">🗂️</span>
    <div>
      <h3>Recursos</h3>
      <p>Archivos finales creados específicamente para cada lección. Replica la estructura de Estándares, pero fraccionada por módulo y lección.</p>
    </div>
  </div>
  <div class="folder-card" onclick="openModal('folder-misc')">
    <span class="f-icon">📎</span>
    <div>
      <h3>Misceláneos</h3>
      <p>Área de trabajo privado del desarrollador. Borradores, bibliografía de apoyo y materiales pendientes de adaptación.</p>
    </div>
  </div>
</div>

<div class="section-heading">
  <h2>🎯 Evaluación en la Educación Multimodal</h2>
  <p>La evaluación deja de ser un examen único e integra TIC de forma transversal en tres momentos clave</p>
</div>

<div class="timeline">
  <div class="timeline-step">
    <span class="step-num">1</span>
    <h4>Conocimientos Básicos</h4>
    <p>Verificar la comprensión conceptual de los contenidos del módulo mediante instrumentos asincrónicos.</p>
  </div>
  <div class="timeline-step">
    <span class="step-num">2</span>
    <h4>Aplicación Práctica</h4>
    <p>Transferir los conocimientos a contextos reales o simulados con proyectos, casos y actividades situadas.</p>
  </div>
  <div class="timeline-step">
    <span class="step-num">3</span>
    <h4>Demostración de Competencias</h4>
    <p>El estudiante evidencia el logro de competencias a través de estrategias sincrónicas y asincrónicas diversas.</p>
  </div>
</div>

<div class="highlight-box" style="margin-top:16px;">
  <p>Las plataformas LMS (Schoology, Moodle, CREA) permiten diseñar un entorno propicio donde el estudiante demuestra la consecución de estos niveles mediante <strong>diversas estrategias sincrónicas y asincrónicas</strong>: portfolios, foros evaluativos, rúbricas digitales, presentaciones en vivo y cuestionarios adaptativos.</p>
</div>

<div class="section-heading"><h2>📺 Recursos Audiovisuales</h2></div>

<div class="video-section">
  <p class="video-label">▶ Video — CFORMA: Estructura de elementos para cursos online</p>
  <div class="video-responsive">
    <iframe src="https://www.youtube.com/embed/ZJUNys88EEI" title="CFORMA - Estructura de elementos para cursos online" allowfullscreen loading="lazy"></iframe>
  </div>
</div>
```

- [ ] **Verificar:** Las 3 folder-cards se muestran en columna. El timeline de 3 pasos aparece horizontalmente. El video carga.

- [ ] **Commit**
```bash
git add metodologia/modulo3.html
git commit -m "feat: tab 4 organización — folder cards, evaluación multimodal timeline, video"
```

---

### Task 6: Contenido de Modales

**Files:**
- Modify: `metodologia/modulo3.html` — rellenar `const MODAL_DATA = {}` en el `<script>`

- [ ] **Reemplazar `const MODAL_DATA = {};` con el siguiente objeto completo:**

```javascript
const MODAL_DATA = {
  // ── ESPACIOS EVA ──
  'esp-avisos': {
    title: '📢 Espacio de Avisos',
    body: `<p>El espacio de Avisos es la <strong>puerta de entrada</strong> al curso. Concentra toda la comunicación institucional y del docente hacia los estudiantes.</p>
    <h4>Contenido típico</h4>
    <ul>
      <li>Mensaje de bienvenida institucional y del profesor</li>
      <li>Recomendaciones generales sobre la modalidad</li>
      <li>Título, código y período del curso</li>
      <li>Noticias urgentes o cambios en el cronograma</li>
      <li>Recordatorios de fechas de entrega</li>
    </ul>
    <h4>Buenas prácticas</h4>
    <p>Los avisos deben ser breves, frecuentes y con tono cercano. El foro de avisos no permite respuestas de estudiantes — es un canal unidireccional.</p>`
  },
  'esp-info': {
    title: '📋 Información del Curso',
    body: `<p>Este espacio responde a la pregunta del estudiante: <strong>"¿Cómo funciona este curso?"</strong>. Es la referencia permanente durante todo el período lectivo.</p>
    <h4>Elementos obligatorios</h4>
    <ul>
      <li>Video o carta de bienvenida del profesor</li>
      <li>Metodología de trabajo y modalidad de comunicación</li>
      <li>Esquema del temario y estructura del curso</li>
      <li>Sistema de evaluación y criterios de acreditación</li>
      <li>Políticas del curso: entregas tardías, plagios, netiqueta</li>
    </ul>`
  },
  'esp-programa': {
    title: '🗓️ Programa y Cronograma',
    body: `<p>El programa actúa como <strong>organizador previo</strong>: da al estudiante una visión global del recorrido antes de sumergirse en los contenidos específicos.</p>
    <h4>Componentes</h4>
    <ul>
      <li>Organizador gráfico o mapa conceptual del curso</li>
      <li>Cronograma detallado semana a semana o módulo a módulo</li>
      <li>Fechas de actividades evaluadas y entregas</li>
      <li>Materiales de apoyo transversales (guías de lectura, glosarios)</li>
    </ul>
    <h4>Recomendación</h4>
    <p>Publicar el cronograma en formato descargable (PDF) y también como tabla visual en la plataforma para facilitar su consulta rápida.</p>`
  },
  'esp-recursos': {
    title: '📚 Recursos de Apoyo',
    body: `<p>Concentra todos los materiales de consulta <strong>no ligados a un módulo específico</strong> sino al curso en su totalidad.</p>
    <h4>Tipos de recursos</h4>
    <ul>
      <li>Bibliografía general del curso (libros, artículos, leyes)</li>
      <li>Tutoriales de uso de la plataforma</li>
      <li>Repositorios externos recomendados</li>
      <li>Normativas institucionales y reglamentos</li>
      <li>Recursos de accesibilidad (subtítulos, versiones adaptadas)</li>
    </ul>`
  },
  'esp-herramientas': {
    title: '🔧 Herramientas de la Plataforma',
    body: `<p>Cada LMS ofrece herramientas de interacción que el docente debe <strong>seleccionar y configurar</strong> intencionalmente según los objetivos pedagógicos.</p>
    <h4>Herramientas comunes</h4>
    <ul>
      <li>Foros de debate (asincrónico, colaborativo)</li>
      <li>Chat o mensajería interna (sincrónico)</li>
      <li>Videoconferencia integrada (Zoom, Meet, BigBlueButton)</li>
      <li>Wikis y espacios de co-autoría</li>
      <li>Glosarios participativos</li>
      <li>Encuestas y cuestionarios</li>
    </ul>
    <p>La clave es que el docente las presente con instrucciones claras y no las active todas de golpe para no abrumar a los estudiantes.</p>`
  },
  'esp-equipo': {
    title: '👥 Equipo Docente',
    body: `<p>Presentar al equipo humaniza la experiencia virtual y reduce la sensación de anonimato que puede experimentar el estudiante a distancia.</p>
    <h4>Incluir para cada miembro</h4>
    <ul>
      <li>Nombre completo y foto profesional</li>
      <li>Rol en el curso (titular, tutor, soporte técnico)</li>
      <li>Formación y breve trayectoria</li>
      <li>Canales de contacto y horarios de disponibilidad</li>
      <li>Tiempo máximo de respuesta a consultas</li>
    </ul>`
  },

  // ── FUNCIONES TUTOR ──
  'func-pedagogica': {
    title: '🎓 Función Pedagógica',
    body: `<p>Es el núcleo de la tarea docente. El tutor virtual diseña y media el proceso de aprendizaje para que el conocimiento no se transmita sino que se <strong>construya</strong>.</p>
    <h4>Acciones concretas</h4>
    <ul>
      <li>Elaborar guías de estudio con objetivos claros y alcanzables</li>
      <li>Moderar foros promoviendo el pensamiento crítico</li>
      <li>Ofrecer retroalimentación formativa, no solo calificaciones</li>
      <li>Diseñar actividades que conecten el contenido con la práctica profesional</li>
      <li>Adaptar materiales a distintos estilos y ritmos de aprendizaje</li>
    </ul>
    <h4>Ejemplo</h4>
    <p>Un tutor en rol pedagógico no dice "lean el capítulo 3". Diseña una guía de lectura con preguntas disparadoras, propone un foro de análisis y da devolución individualizada a cada aporte.</p>`
  },
  'func-social': {
    title: '🤝 Función Social',
    body: `<p>La distancia física puede generar aislamiento, desmotivación y abandono. La función social del tutor crea el <strong>tejido humano</strong> que sostiene la comunidad de aprendizaje.</p>
    <h4>Acciones concretas</h4>
    <ul>
      <li>Dar la bienvenida personalizada a cada estudiante</li>
      <li>Fomentar el uso del Foro de Cafetería para la interacción informal</li>
      <li>Detectar estudiantes inactivos y contactarlos proactivamente</li>
      <li>Resolver conflictos grupales con empatía y ecuanimidad</li>
      <li>Celebrar los logros del grupo y los avances individuales</li>
    </ul>
    <h4>Indicador de éxito</h4>
    <p>Los estudiantes se conocen entre sí, se citan en los foros y colaboran más allá de las actividades obligatorias.</p>`
  },
  'func-administrativa': {
    title: '📊 Función Administrativa',
    body: `<p>El tutor también gestiona. Sin una buena administración, el curso pierde coherencia y los estudiantes pierden la orientación sobre qué hacer y cuándo.</p>
    <h4>Acciones concretas</h4>
    <ul>
      <li>Publicar y actualizar el cronograma del curso</li>
      <li>Establecer normas claras de participación y entrega</li>
      <li>Gestionar los grupos de trabajo y asignar roles</li>
      <li>Monitorear el progreso de los estudiantes con informes de la plataforma</li>
      <li>Registrar asistencia virtual y calificaciones en tiempo</li>
    </ul>
    <h4>Herramienta clave</h4>
    <p>Los LMS ofrecen dashboards de seguimiento: tasas de acceso, tiempo en plataforma, participación en foros. Usarlos es parte de la función administrativa del tutor.</p>`
  },
  'func-tecnica': {
    title: '💻 Función Técnica',
    body: `<p>El tutor debe dominar el entorno virtual con suficiente solvencia para que la tecnología sea <strong>invisible</strong> para el aprendizaje: cuando todo funciona, nadie la nota.</p>
    <h4>Acciones concretas</h4>
    <ul>
      <li>Configurar correctamente actividades, foros y cuestionarios</li>
      <li>Crear tutoriales en video o texto sobre el uso de la plataforma</li>
      <li>Responder consultas técnicas básicas de los estudiantes</li>
      <li>Conocer a quién escalar los problemas técnicos complejos</li>
      <li>Mantener actualizados los materiales y links del curso</li>
    </ul>
    <h4>Límite del rol</h4>
    <p>El tutor no necesita ser técnico informático. Sí necesita saber usar la plataforma con fluidez y tener el contacto del soporte técnico institucional para derivar problemas de infraestructura.</p>`
  },

  // ── CARPETAS ──
  'folder-estandares': {
    title: '📦 Carpeta: Estándares',
    body: `<p>Reservada para todos los elementos <strong>reutilizables</strong> que ya tienen el formato visual y sonoro del curso. Se crean una vez y se usan en todos los módulos sin modificación.</p>
    <h4>Subcarpetas sugeridas</h4>
    <ul>
      <li><strong>Iconografía:</strong> íconos, viñetas, separadores gráficos en PNG/SVG</li>
      <li><strong>Fondos:</strong> imágenes de fondo para pantallas de video o presentaciones</li>
      <li><strong>Audio:</strong> cortinas musicales, bases instrumentales, efectos de transición</li>
      <li><strong>Plantillas:</strong> documentos PDF/DOCX con el diseño institucional ya aplicado</li>
      <li><strong>Paleta de colores:</strong> archivo con los colores corporativos en HEX/RGB</li>
    </ul>
    <h4>Criterio de inclusión</h4>
    <p>Si el archivo se va a usar más de una vez en distintos módulos, va a Estándares. Si es específico de una lección, va a Recursos.</p>`
  },
  'folder-recursos': {
    title: '🗂️ Carpeta: Recursos',
    body: `<p>Contiene los elementos <strong>finales y publicables</strong> creados específicamente para cada lección del curso. Es el corazón de la producción de contenido.</p>
    <h4>Estructura interna recomendada</h4>
    <ul>
      <li><strong>Módulo1/</strong><ul style="padding-left:16px;margin-top:4px;">
        <li>Lección1/ → videos, PDFs, presentaciones</li>
        <li>Lección2/ → ídem</li>
      </ul></li>
      <li><strong>Módulo2/</strong> → misma estructura</li>
      <li><strong>ModuloN/</strong> → misma estructura</li>
    </ul>
    <h4>Ventaja</h4>
    <p>Esta organización permite localizar cualquier archivo en segundos, facilita las actualizaciones y hace el curso transferible a otro docente sin pérdida de información.</p>`
  },
  'folder-misc': {
    title: '📎 Carpeta: Misceláneos',
    body: `<p>Área de trabajo <strong>privada del desarrollador</strong>. No contiene materiales publicados en el curso, sino insumos de trabajo en proceso.</p>
    <h4>Contenido típico</h4>
    <ul>
      <li>Borradores y versiones previas de materiales</li>
      <li>Bibliografía de apoyo al diseño (no para los estudiantes)</li>
      <li>Artículos y referencias consultadas durante el diseño</li>
      <li>Materiales pendientes de revisión o adaptación</li>
      <li>Capturas de pantalla, notas de investigación, ideas</li>
    </ul>
    <h4>Regla de mantenimiento</h4>
    <p>Esta carpeta se limpia al finalizar el diseño del curso. Lo que no ingresó al curso como recurso final o estándar, se archiva o elimina para mantener el sistema limpio.</p>`
  }
};
```

- [ ] **Verificar:** Hacer click en cada card del Tab 2 y del Tab 3. El modal debe abrirse con título y contenido correcto. Cerrar con ✕, con click fuera, y con Escape.

- [ ] **Commit**
```bash
git add metodologia/modulo3.html
git commit -m "feat: modal data completo — 6 espacios EVA + 4 funciones tutor + 3 carpetas"
```

---

### Task 7: Self-review y pulido final

**Files:**
- Modify: `metodologia/modulo3.html` — ajustes menores de polish

- [ ] **Revisar en browser a 360px de ancho** (DevTools mobile). Verificar que:
  - Tab bar colapsa correctamente (solo íconos)
  - Grids colapsan a 1 columna
  - Timeline colapsa a columna
  - Modales no se cortan

- [ ] **Agregar el video de CFORMA al Tab 2 como referencia adicional** — no hay un video 4 en esa tab. El Tab 2 ya tiene sus 2 videos. Verificar que no falten videos en ningún tab.

- [ ] **Revisar todos los `onclick`** con DevTools Console abierta. No deben aparecer errores al abrir modales.

- [ ] **Commit final**
```bash
git add metodologia/modulo3.html
git commit -m "feat: modulo3.html completo — EVA interactivo, 4 tabs, modales, videos, acordeón"
```

---

## Self-Review del Plan

**Cobertura del spec:**
- ✅ Header gradiente con badge
- ✅ 4 tabs sticky con transición animada
- ✅ Tab 1: intro, cita, 3 nav cards
- ✅ Tab 2: 6 cards modales + estructura diagram + sep recursos/actividades + 2 videos
- ✅ Tab 3: 4 func cards modales + 5 roles accordion + PDF links + 1 video
- ✅ Tab 4: 3 folder cards modales + timeline evaluación + 1 video
- ✅ Sistema de modales con overlay, animación, cierre con Escape
- ✅ Accordion con max-height transition
- ✅ Responsive: grids colapsan, tab bar colapsa
- ✅ Videos siempre visibles como iframes de YouTube
- ✅ PDFs con rutas relativas `Modulo3/Recursos/`

**Sin placeholders:** Todo el código está presente en el plan.
