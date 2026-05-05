[index (1).html](https://github.com/user-attachments/files/27383716/index.1.html)
<!doctype html>
<html lang="es">
<head><script>(function(){
  function makeStore(){
    var data = {};
    var api = {
      getItem: function(k){ return Object.prototype.hasOwnProperty.call(data, k) ? data[k] : null; },
      setItem: function(k, v){ data[k] = String(v); },
      removeItem: function(k){ delete data[k]; },
      clear: function(){ data = {}; },
      key: function(i){ return Object.keys(data)[i] || null; }
    };
    Object.defineProperty(api, 'length', { get: function(){ return Object.keys(data).length; } });
    return api;
  }
  function tryShim(name){
    var works = false;
    try { works = !!window[name] && typeof window[name].getItem === 'function'; void window[name].length; }
    catch (_) { works = false; }
    if (works) return;
    try { Object.defineProperty(window, name, { configurable: true, value: makeStore() }); }
    catch (_) { try { window[name] = makeStore(); } catch (__) {} }
  }
  tryShim('localStorage');
  tryShim('sessionStorage');
})();</script>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <title>Hospedia — El PMS mexicano para hoteles independientes</title>
  <meta name="description" content="Hospedia es el PMS hecho en México para hoteles boutique, casas de huéspedes y propiedades vacacionales. Reservas, pagos, huéspedes y operación en un solo lugar." />
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,500;0,600;0,700;1,400;1,500&family=Manrope:wght@400;500;600;700;800&display=swap');

    :root {
      /* Airbnb DS palette — bound verbatim */
      --bg:        #ffffff;       /* Canvas White */
      --surface:   #f7f7f7;       /* Soft Cloud */
      --fg:        #222222;       /* Ink Black */
      --fg-soft:   #3f3f3f;       /* Charcoal */
      --muted:     #6a6a6a;       /* Ash Gray */
      --muted-2:   #929292;       /* Mute Gray */
      --stone:     #c1c1c1;       /* Stone Gray */
      --border:    #dddddd;       /* Hairline Gray */
      --accent:    #ff385c;       /* Rausch */
      --accent-2:  #e00b41;       /* Deep Rausch */
      --plus:      #92174d;       /* Plus Magenta */
      --luxe:      #460479;       /* Luxe Purple */
      --error:     #c13515;
      --info:      #428bff;

      /* Type — user override: Cormorant Garamond + Manrope */
      --font-display: 'Cormorant Garamond', 'Iowan Old Style', Georgia, serif;
      --font-body:    'Manrope', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;

      /* Layout */
      --max-w: 1200px;
      --max-w-wide: 1320px;
      --pad-page: clamp(20px, 4vw, 56px);

      /* Airbnb signature 3-layer shadow */
      --shadow-card: rgba(0,0,0,0.02) 0 0 0 1px,
                     rgba(0,0,0,0.04) 0 2px 6px 0,
                     rgba(0,0,0,0.10) 0 4px 8px 0;

      /* Subtle button press */
      --shadow-press: rgba(0,0,0,0.08) 0 4px 12px;

      --radius-card: 14px;
      --radius-lg: 20px;
      --radius-pill: 999px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }
    body {
      margin: 0;
      background: var(--bg);
      color: var(--fg);
      font-family: var(--font-body);
      font-weight: 500;
      font-size: 16px;
      line-height: 1.5;
      letter-spacing: -0.005em;
      position: relative;
    }

    /* Subtle paper grain — very low opacity SVG noise */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 1000;
      opacity: 0.045;
      mix-blend-mode: multiply;
      background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='240' height='240'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0  0 0 0 0 0  0 0 0 0 0  0 0 0 0.5 0'/></filter><rect width='100%25' height='100%25' filter='url(%23n)'/></svg>");
    }

    img, svg { display: block; max-width: 100%; }
    a { color: inherit; text-decoration: none; }

    .container { max-width: var(--max-w); margin: 0 auto; padding: 0 var(--pad-page); }
    .container-wide { max-width: var(--max-w-wide); margin: 0 auto; padding: 0 var(--pad-page); }

    /* ========== TYPOGRAPHY ========== */
    h1, h2, h3, h4 { font-family: var(--font-display); font-weight: 600; color: var(--fg); margin: 0; letter-spacing: -0.018em; line-height: 1.06; }
    .display-xxl { font-size: clamp(48px, 7.2vw, 96px); font-weight: 500; letter-spacing: -0.025em; line-height: 1.02; }
    .display-xl  { font-size: clamp(40px, 5.6vw, 72px); font-weight: 500; letter-spacing: -0.022em; line-height: 1.04; }
    .display-l   { font-size: clamp(32px, 4.2vw, 52px); font-weight: 500; letter-spacing: -0.018em; }
    .display-m   { font-size: clamp(26px, 2.8vw, 36px); font-weight: 500; letter-spacing: -0.012em; }
    .display-s   { font-size: 22px; font-weight: 600; letter-spacing: -0.012em; line-height: 1.18; }

    .eyebrow {
      font-family: var(--font-body);
      font-weight: 700;
      font-size: 12px;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: var(--accent);
    }
    .eyebrow.muted { color: var(--muted); }
    .lede { font-size: clamp(17px, 1.4vw, 20px); color: var(--muted); line-height: 1.55; max-width: 56ch; font-weight: 500; }

    /* italic emphasis utility for the serif */
    .italic { font-style: italic; font-family: var(--font-display); font-weight: 500; }

    /* ========== BUTTONS ========== */
    .btn {
      display: inline-flex; align-items: center; justify-content: center; gap: 8px;
      font-family: var(--font-body);
      font-weight: 600; font-size: 16px; letter-spacing: -0.005em;
      padding: 14px 22px; border-radius: 10px; border: 1px solid transparent;
      cursor: pointer; transition: transform .12s ease, background .2s, color .2s, border-color .2s;
      white-space: nowrap;
    }
    .btn-primary { background: var(--accent); color: #fff; border-color: var(--accent); }
    .btn-primary:hover { background: var(--accent-2); border-color: var(--accent-2); }
    .btn-primary:active { transform: scale(0.96); }
    .btn-ghost { background: transparent; color: var(--fg); border-color: var(--border); }
    .btn-ghost:hover { border-color: var(--fg); }
    .btn-pill { border-radius: var(--radius-pill); padding: 12px 20px; }
    .btn-sm { padding: 10px 16px; font-size: 14px; }

    .icon-btn {
      width: 40px; height: 40px; border-radius: 50%;
      display: inline-flex; align-items: center; justify-content: center;
      background: #fff; border: 1px solid var(--border);
      cursor: pointer; transition: transform .12s ease;
    }
    .icon-btn:hover { box-shadow: var(--shadow-press); }
    .icon-btn:active { transform: scale(0.92); }

    /* ========== NAV ========== */
    .nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      transition: background .25s ease, border-color .25s ease, backdrop-filter .25s ease;
      background: rgba(255,255,255,0);
      border-bottom: 1px solid transparent;
    }
    .nav.scrolled {
      background: rgba(255,255,255,0.92);
      backdrop-filter: saturate(140%) blur(12px);
      -webkit-backdrop-filter: saturate(140%) blur(12px);
      border-bottom-color: var(--border);
    }
    .nav-inner {
      max-width: var(--max-w-wide); margin: 0 auto;
      padding: 18px var(--pad-page);
      display: grid; grid-template-columns: auto 1fr auto; align-items: center; gap: 24px;
    }
    .logo { display: inline-flex; align-items: baseline; gap: 8px; font-family: var(--font-display); font-weight: 600; font-size: 26px; letter-spacing: -0.02em; color: var(--fg); }
    .logo .dot { width: 8px; height: 8px; border-radius: 50%; background: var(--accent); display: inline-block; transform: translateY(-3px); }
    .logo small { font-family: var(--font-body); font-weight: 600; font-size: 11px; letter-spacing: 0.18em; text-transform: uppercase; color: var(--muted); margin-left: 4px; }
    .nav-links { display: flex; justify-content: center; gap: 28px; }
    .nav-links a { font-size: 14px; font-weight: 500; color: var(--fg); }
    .nav-links a:hover { color: var(--accent); }
    .nav-cta { display: flex; gap: 10px; align-items: center; }
    @media (max-width: 880px) {
      .nav-inner { grid-template-columns: 1fr auto; }
      .nav-links { display: none; }
    }

    /* ========== HERO ========== */
    .hero {
      padding: 140px var(--pad-page) 80px;
      max-width: var(--max-w-wide); margin: 0 auto;
      display: grid; grid-template-columns: 1.05fr 1fr; gap: 64px; align-items: center;
    }
    .hero-copy .eyebrow { display: inline-flex; align-items: center; gap: 8px; }
    .hero h1 { margin-top: 16px; }
    .hero h1 .accent { color: var(--accent); font-style: italic; font-weight: 500; }
    .hero p.lede { margin-top: 22px; }
    .hero-ctas { margin-top: 32px; display: flex; gap: 12px; flex-wrap: wrap; }
    .hero-meta { margin-top: 28px; display: inline-flex; align-items: center; gap: 14px; padding: 10px 16px; border: 1px solid var(--border); border-radius: var(--radius-pill); background: #fff; font-size: 13px; font-weight: 500; color: var(--fg); }
    .hero-meta .sep { width: 3px; height: 3px; border-radius: 50%; background: var(--stone); }
    .hero-meta .pin { width: 6px; height: 6px; border-radius: 50%; background: var(--accent); box-shadow: 0 0 0 4px rgba(255,56,92,0.16); }

    @media (max-width: 1000px) {
      .hero { grid-template-columns: 1fr; gap: 56px; padding-top: 120px; }
    }

    /* ========== DASHBOARD MOCK ========== */
    .dashboard {
      background: #fff;
      border: 1px solid var(--border);
      border-radius: var(--radius-lg);
      box-shadow: var(--shadow-card);
      overflow: hidden;
      transform: translateY(0);
    }
    .dash-titlebar {
      display: flex; align-items: center; gap: 10px;
      padding: 12px 16px;
      border-bottom: 1px solid var(--border);
      background: #fff;
    }
    .dash-dots { display: flex; gap: 6px; }
    .dash-dots span { width: 11px; height: 11px; border-radius: 50%; background: #e6e6e6; }
    .dash-dots span:nth-child(1) { background: #ff5f56; }
    .dash-dots span:nth-child(2) { background: #ffbd2e; }
    .dash-dots span:nth-child(3) { background: #27c93f; }
    .dash-title { flex: 1; text-align: center; font-size: 12px; font-weight: 600; color: var(--muted); letter-spacing: 0.02em; }
    .dash-title strong { color: var(--fg); }

    .dash-body {
      padding: 22px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 18px;
    }
    .dash-row { grid-column: 1 / -1; display: grid; grid-template-columns: 1.4fr 1fr 1fr; gap: 14px; }

    .dash-card {
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 16px;
      background: #fff;
    }
    .dash-card .label { font-size: 11px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; color: var(--muted); }
    .dash-card .value { font-family: var(--font-display); font-size: 36px; font-weight: 600; letter-spacing: -0.02em; line-height: 1; margin-top: 8px; color: var(--fg); }
    .dash-card .delta { display: inline-flex; align-items: center; gap: 4px; margin-top: 10px; font-size: 12px; font-weight: 600; color: #2e7d32; background: #ecf6ee; padding: 3px 8px; border-radius: 999px; }
    .dash-card .delta.down { color: var(--accent-2); background: #fdecef; }
    .dash-card .delta.flat { color: var(--muted); background: #f3f3f3; }

    /* Donut */
    .donut-card { display: flex; align-items: center; gap: 18px; }
    .donut-meta { flex: 1; }
    .donut {
      width: 96px; height: 96px; flex-shrink: 0;
      position: relative;
    }
    .donut svg { transform: rotate(-90deg); }
    .donut-label {
      position: absolute; inset: 0; display: flex; align-items: center; justify-content: center;
      flex-direction: column;
      font-family: var(--font-display); font-weight: 600;
    }
    .donut-label b { font-size: 26px; letter-spacing: -0.02em; line-height: 1; }
    .donut-label span { font-family: var(--font-body); font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; color: var(--muted); margin-top: 4px; }
    .donut .ring-bg { stroke: #f0f0f0; }
    .donut .ring-fg { stroke: var(--accent); transition: stroke-dashoffset 1.4s cubic-bezier(.2,.7,.2,1); }

    /* Room grid */
    .rooms-card { grid-column: 1 / -1; }
    .rooms-head { display: flex; align-items: center; justify-content: space-between; margin-bottom: 12px; }
    .rooms-title { font-size: 13px; font-weight: 700; color: var(--fg); }
    .rooms-legend { display: flex; gap: 12px; font-size: 11px; color: var(--muted); }
    .rooms-legend span { display: inline-flex; align-items: center; gap: 4px; }
    .rooms-legend i { width: 8px; height: 8px; border-radius: 2px; display: inline-block; }
    .rooms-grid {
      display: grid; grid-template-columns: repeat(8, 1fr); gap: 6px;
    }
    .room {
      aspect-ratio: 1.05;
      border-radius: 7px;
      display: flex; align-items: center; justify-content: center;
      font-size: 11px; font-weight: 700; color: var(--muted);
      background: #fafafa;
      border: 1px solid var(--border);
      transition: transform .2s ease;
    }
    .room.occ { background: var(--fg); color: #fff; border-color: var(--fg); }
    .room.in  { background: var(--accent); color: #fff; border-color: var(--accent); }
    .room.out { background: #fff7f0; color: var(--accent-2); border-color: #f7d8d8; }
    .room.cln { background: #f7f7f7; color: var(--muted); }
    .legend-occ { background: var(--fg); }
    .legend-in  { background: var(--accent); }
    .legend-out { background: #fff7f0; border: 1px solid #f7d8d8; box-sizing: border-box; }
    .legend-av  { background: #fafafa; border: 1px solid var(--border); box-sizing: border-box; }

    /* Reservations strip card */
    .res-card { grid-column: 1 / -1; }
    .res-row { display: grid; grid-template-columns: auto 1fr auto auto; gap: 14px; align-items: center; padding: 10px 0; border-top: 1px solid var(--border); }
    .res-row:first-of-type { border-top: 0; padding-top: 0; }
    .res-avatar { width: 32px; height: 32px; border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; font-size: 11px; font-weight: 700; color: #fff; }
    .res-name { font-size: 13px; font-weight: 600; color: var(--fg); }
    .res-sub { font-size: 11px; color: var(--muted); margin-top: 2px; }
    .res-amount { font-family: var(--font-display); font-size: 16px; font-weight: 600; }
    .pill { font-size: 10px; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; padding: 4px 8px; border-radius: 999px; }
    .pill-confirm { background: #ecf6ee; color: #2e7d32; }
    .pill-pend    { background: #fdf6e7; color: #8a6300; }
    .pill-arrive  { background: #fdecef; color: var(--accent-2); }

    /* ========== MARQUEE ========== */
    .marquee {
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      padding: 22px 0;
      overflow: hidden;
      background: var(--surface);
      mask-image: linear-gradient(90deg, transparent, #000 8%, #000 92%, transparent);
      -webkit-mask-image: linear-gradient(90deg, transparent, #000 8%, #000 92%, transparent);
    }
    .marquee-track {
      display: inline-flex; gap: 56px; white-space: nowrap;
      animation: scroll 38s linear infinite;
      padding-left: 56px;
    }
    .marquee-item {
      display: inline-flex; align-items: center; gap: 12px;
      font-family: var(--font-display); font-style: italic; font-weight: 500;
      font-size: 22px; color: var(--fg-soft);
    }
    .marquee-item::after {
      content: '·'; color: var(--stone); font-style: normal; margin-left: 56px; font-size: 24px;
    }
    .marquee-item:last-child::after { content: ''; margin: 0; }
    @keyframes scroll {
      0% { transform: translateX(0); }
      100% { transform: translateX(-50%); }
    }

    /* ========== SECTION FRAME ========== */
    section { padding: clamp(64px, 9vw, 120px) 0; }
    .section-head { max-width: 720px; margin-bottom: 56px; }
    .section-head .eyebrow { display: inline-block; margin-bottom: 18px; }
    .section-head h2 { margin-bottom: 18px; }
    .section-head .lede { color: var(--muted); }
    .section-head.center { margin-left: auto; margin-right: auto; text-align: center; }
    .section-head.center .lede { margin-left: auto; margin-right: auto; }

    /* ========== WHY ========== */
    .why { background: var(--bg); }
    .why-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0;
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      margin-bottom: 80px;
    }
    .why-card {
      padding: 36px 28px;
      border-right: 1px solid var(--border);
      display: flex; flex-direction: column; gap: 14px;
    }
    .why-card:last-child { border-right: 0; }
    .why-icon {
      width: 48px; height: 48px; border-radius: 12px;
      background: var(--surface); border: 1px solid var(--border);
      display: inline-flex; align-items: center; justify-content: center;
      color: var(--fg);
      flex-shrink: 0;
    }
    .why-card h3 { font-size: 22px; font-weight: 600; }
    .why-card p { color: var(--muted); font-size: 15px; line-height: 1.55; margin: 0; }

    @media (max-width: 920px) {
      .why-grid { grid-template-columns: repeat(2, 1fr); }
      .why-card { border-right: 1px solid var(--border); border-bottom: 1px solid var(--border); }
      .why-card:nth-child(2n) { border-right: 0; }
      .why-card:nth-last-child(-n+2) { border-bottom: 0; }
    }
    @media (max-width: 560px) {
      .why-grid { grid-template-columns: 1fr; }
      .why-card { border-right: 0; }
      .why-card:not(:last-child) { border-bottom: 1px solid var(--border); }
    }

    /* Comparison table */
    .compare {
      display: grid; grid-template-columns: 1fr 1fr; gap: 0;
      border: 1px solid var(--border); border-radius: var(--radius-lg);
      overflow: hidden;
      background: #fff;
    }
    .compare-col { padding: 32px; }
    .compare-col + .compare-col { border-left: 1px solid var(--border); }
    .compare-col.hospedia { background: linear-gradient(180deg, #fff 0%, #fffafb 100%); }
    .compare-col h4 {
      font-family: var(--font-body);
      font-size: 13px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase;
      color: var(--muted); margin-bottom: 18px;
    }
    .compare-col.hospedia h4 { color: var(--accent); }
    .compare-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 14px; }
    .compare-list li {
      display: grid; grid-template-columns: 22px 1fr; gap: 12px;
      font-size: 15px; line-height: 1.5; color: var(--fg);
    }
    .compare-list li.dim { color: var(--muted); }
    .compare-mark {
      width: 22px; height: 22px; border-radius: 50%;
      display: inline-flex; align-items: center; justify-content: center;
      font-size: 12px; font-weight: 700;
      flex-shrink: 0;
    }
    .compare-mark.x { background: #f4f4f4; color: var(--muted-2); }
    .compare-mark.v { background: var(--accent); color: #fff; }

    @media (max-width: 720px) {
      .compare { grid-template-columns: 1fr; }
      .compare-col + .compare-col { border-left: 0; border-top: 1px solid var(--border); }
    }

    /* ========== BEFORE / AFTER ========== */
    .ba { background: var(--bg); }
    .ba-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 16px;
      border-radius: var(--radius-lg); overflow: hidden;
    }
    .ba-panel {
      padding: clamp(28px, 4vw, 48px);
      border-radius: var(--radius-lg);
      min-height: 420px;
      display: flex; flex-direction: column; gap: 26px;
    }
    .ba-without {
      background: var(--fg); color: #fff;
      border: 1px solid var(--fg);
    }
    .ba-with {
      background: #fff;
      border: 1px solid var(--border);
    }
    .ba-panel .label { font-size: 12px; font-weight: 700; letter-spacing: 0.16em; text-transform: uppercase; opacity: 0.72; }
    .ba-with .label { color: var(--accent); opacity: 1; }
    .ba-panel h3 {
      font-family: var(--font-display); font-weight: 500;
      font-size: clamp(28px, 3.4vw, 40px); letter-spacing: -0.018em; line-height: 1.05;
    }
    .ba-without h3 { color: #fff; }
    .ba-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 14px; }
    .ba-list li { display: grid; grid-template-columns: 24px 1fr; gap: 14px; align-items: start; font-size: 15.5px; line-height: 1.5; }
    .ba-without .ba-list li { color: rgba(255,255,255,0.86); }
    .ba-mark {
      width: 24px; height: 24px; border-radius: 50%;
      display: inline-flex; align-items: center; justify-content: center;
      font-size: 13px; font-weight: 700;
      flex-shrink: 0;
    }
    .ba-without .ba-mark { background: rgba(255,255,255,0.08); color: rgba(255,255,255,0.7); }
    .ba-with .ba-mark { background: var(--accent); color: #fff; }

    @media (max-width: 820px) { .ba-grid { grid-template-columns: 1fr; } }

    /* ========== FEATURES ========== */
    .features { background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
    .feat-grid { display: grid; grid-template-columns: repeat(6, 1fr); gap: 18px; }
    .feat-card {
      grid-column: span 2;
      background: #fff;
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      padding: 28px 26px;
      display: flex; flex-direction: column; gap: 14px;
      transition: transform .25s ease, box-shadow .25s ease;
    }
    .feat-card:hover { transform: translateY(-3px); box-shadow: var(--shadow-card); }
    .feat-card:nth-child(4) { grid-column: 1 / span 3; }
    .feat-card:nth-child(5) { grid-column: 4 / span 3; }
    .feat-icon {
      width: 44px; height: 44px; border-radius: 50%;
      background: var(--surface); border: 1px solid var(--border);
      display: inline-flex; align-items: center; justify-content: center;
      color: var(--fg);
    }
    .feat-card h3 { font-size: 22px; font-weight: 600; }
    .feat-card p { color: var(--muted); font-size: 14.5px; line-height: 1.55; margin: 0; }
    .feat-badge {
      align-self: flex-start;
      font-size: 11px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase;
      color: var(--accent);
      padding: 4px 10px; border-radius: 999px;
      background: #fff5f7; border: 1px solid #ffd9e0;
    }
    @media (max-width: 980px) { .feat-grid { grid-template-columns: repeat(2, 1fr); } .feat-card, .feat-card:nth-child(4), .feat-card:nth-child(5) { grid-column: span 1; } }
    @media (max-width: 560px) { .feat-grid { grid-template-columns: 1fr; } }

    /* ========== FOR WHO ========== */
    .who { background: var(--bg); }
    .who-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 14px; }
    .who-card {
      background: #fff;
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      padding: 32px 24px;
      text-align: center;
      display: flex; flex-direction: column; align-items: center; gap: 14px;
      transition: transform .25s, border-color .25s;
    }
    .who-card:hover { transform: translateY(-3px); border-color: var(--accent); }
    .who-emoji { font-size: 42px; line-height: 1; }
    .who-card h3 { font-size: 18px; font-weight: 600; }
    .who-card p { font-size: 13px; color: var(--muted); margin: 0; line-height: 1.5; }
    @media (max-width: 1080px) { .who-grid { grid-template-columns: repeat(3, 1fr); } }
    @media (max-width: 640px) { .who-grid { grid-template-columns: repeat(2, 1fr); } }

    /* ========== RESULTS ========== */
    .results { background: var(--bg); border-top: 1px solid var(--border); }
    .results-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0; }
    .result-block {
      padding: 56px 32px 56px 0;
      border-right: 1px solid var(--border);
      display: flex; flex-direction: column; gap: 12px;
    }
    .result-block:last-child { border-right: 0; padding-right: 0; }
    .result-block + .result-block { padding-left: 32px; }
    .result-num {
      font-family: var(--font-display);
      font-size: clamp(60px, 8vw, 108px);
      font-weight: 500; line-height: 1; letter-spacing: -0.03em;
      color: var(--fg);
    }
    .result-num .unit { color: var(--accent); }
    .result-block h3 { font-size: 20px; font-weight: 600; margin-top: 8px; }
    .result-block p { color: var(--muted); font-size: 14.5px; line-height: 1.5; margin: 0; }
    @media (max-width: 820px) {
      .results-grid { grid-template-columns: 1fr; }
      .result-block { border-right: 0; border-bottom: 1px solid var(--border); padding: 36px 0; }
      .result-block + .result-block { padding-left: 0; }
      .result-block:last-child { border-bottom: 0; }
    }

    /* ========== TESTIMONIAL ========== */
    .quote {
      background: var(--fg); color: #fff;
      border-radius: var(--radius-lg);
      padding: clamp(40px, 6vw, 80px);
      position: relative; overflow: hidden;
    }
    .quote::before {
      content: '“';
      position: absolute; top: 6px; left: 36px;
      font-family: var(--font-display); font-size: 220px; line-height: 1; color: var(--accent);
      pointer-events: none;
    }
    .quote-body {
      position: relative;
      max-width: 900px;
      font-family: var(--font-display);
      font-weight: 500;
      font-size: clamp(22px, 2.6vw, 38px);
      letter-spacing: -0.012em;
      line-height: 1.18;
      color: #fff;
    }
    .quote-body em { font-style: italic; color: #ffb6c4; }
    .quote-stars { display: inline-flex; gap: 4px; margin-bottom: 20px; }
    .quote-stars span { color: var(--accent); }
    .quote-attr {
      display: flex; align-items: center; gap: 14px; margin-top: 32px;
      font-family: var(--font-body);
      color: rgba(255,255,255,0.78);
      font-size: 14px;
    }
    .quote-avatar {
      width: 44px; height: 44px; border-radius: 50%;
      background: linear-gradient(135deg, #fff 0%, #ffb6c4 100%);
      color: var(--fg); font-weight: 700; font-size: 14px;
      display: inline-flex; align-items: center; justify-content: center;
      flex-shrink: 0;
    }
    .quote-attr strong { color: #fff; font-weight: 700; }

    /* ========== CTA / FORM ========== */
    .cta { background: var(--bg); }
    .cta-grid {
      display: grid; grid-template-columns: 1.2fr 1fr; gap: 56px; align-items: start;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-lg);
      padding: clamp(36px, 5vw, 64px);
    }
    .cta-grid h2 { margin-bottom: 16px; }
    .cta-grid .lede { margin-bottom: 32px; max-width: 48ch; }
    .form { display: flex; flex-direction: column; gap: 14px; }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
    .field { display: flex; flex-direction: column; gap: 6px; }
    .field label { font-size: 12px; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; color: var(--muted); }
    .field input {
      font-family: var(--font-body); font-weight: 500;
      font-size: 15px; color: var(--fg);
      background: #fff;
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 14px 16px;
      transition: border-color .15s, box-shadow .15s;
    }
    .field input:focus {
      outline: none;
      border-color: var(--fg);
      box-shadow: 0 0 0 3px rgba(34,34,34,0.08);
    }
    .form .btn { margin-top: 6px; }
    .form-foot {
      margin-top: 14px; font-size: 13px; color: var(--muted);
      display: flex; gap: 6px; align-items: center; flex-wrap: wrap;
    }
    .form-foot a { color: var(--fg); text-decoration: underline; text-underline-offset: 3px; }

    .checklist-card {
      background: #fff;
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      padding: 28px 28px 24px;
    }
    .checklist-card h4 {
      font-family: var(--font-body);
      font-size: 12px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase;
      color: var(--muted); margin-bottom: 18px;
    }
    .checklist-card .item {
      display: grid; grid-template-columns: 22px 1fr; gap: 12px;
      padding: 12px 0; border-top: 1px solid var(--border);
      font-size: 15px; color: var(--fg);
    }
    .checklist-card .item:first-of-type { border-top: 0; padding-top: 0; }
    .check {
      width: 22px; height: 22px; border-radius: 50%;
      background: var(--accent); color: #fff;
      display: inline-flex; align-items: center; justify-content: center;
      font-size: 12px; font-weight: 700;
    }

    .form-success {
      display: none;
      flex-direction: column; gap: 18px;
      padding: 36px 0;
      text-align: left;
    }
    .form-success.show { display: flex; }
    .form-success .check-big {
      width: 64px; height: 64px; border-radius: 50%;
      background: var(--accent); color: #fff;
      display: inline-flex; align-items: center; justify-content: center;
      font-size: 26px; font-weight: 700;
    }
    .form-success h3 { font-family: var(--font-display); font-size: 32px; font-weight: 600; }
    .form-success p { color: var(--muted); font-size: 15px; max-width: 44ch; }

    @media (max-width: 920px) {
      .cta-grid { grid-template-columns: 1fr; gap: 36px; }
      .form-row { grid-template-columns: 1fr; }
    }

    /* ========== FOOTER ========== */
    footer { background: var(--bg); border-top: 1px solid var(--border); padding: 64px 0 36px; }
    .foot-top { display: grid; grid-template-columns: 1.2fr 1fr 1fr 1fr; gap: 48px; padding-bottom: 48px; border-bottom: 1px solid var(--border); }
    .foot-brand p { font-size: 14px; color: var(--muted); max-width: 36ch; margin: 12px 0 0; line-height: 1.55; }
    .foot-col h5 { font-family: var(--font-body); font-size: 12px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; color: var(--muted); margin-bottom: 16px; }
    .foot-col ul { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 12px; }
    .foot-col a { font-size: 14px; color: var(--fg); }
    .foot-col a:hover { color: var(--accent); }
    .foot-bot { display: flex; justify-content: space-between; align-items: center; padding-top: 28px; flex-wrap: wrap; gap: 14px; font-size: 13px; color: var(--muted); }
    .foot-mx { display: inline-flex; align-items: center; gap: 6px; font-weight: 600; color: var(--fg); }
    @media (max-width: 820px) { .foot-top { grid-template-columns: 1fr 1fr; gap: 32px; } }
    @media (max-width: 480px) { .foot-top { grid-template-columns: 1fr; } }

    /* ========== ANIMATIONS ========== */
    .reveal {
      opacity: 0;
      transform: translateY(18px);
      transition: opacity .8s cubic-bezier(.2,.7,.2,1), transform .8s cubic-bezier(.2,.7,.2,1);
    }
    .reveal.in { opacity: 1; transform: none; }
    .reveal.delay-1 { transition-delay: .08s; }
    .reveal.delay-2 { transition-delay: .16s; }
    .reveal.delay-3 { transition-delay: .24s; }
    .reveal.delay-4 { transition-delay: .32s; }

    @media (prefers-reduced-motion: reduce) {
      .reveal { opacity: 1; transform: none; transition: none; }
      .marquee-track { animation: none; }
    }

    /* numerics */
    .tnum { font-variant-numeric: tabular-nums; }
  </style>
</head>
<body>

  <!-- ============== NAV ============== -->
  <nav class="nav" id="nav">
    <div class="nav-inner">
      <a href="#" class="logo" aria-label="Hospedia">
        <span class="dot" aria-hidden="true"></span>
        Hospedia
        <small>PMS</small>
      </a>
      <div class="nav-links">
        <a href="#porque">Por qué</a>
        <a href="#funciones">Funciones</a>
        <a href="#hoteles">Hoteles</a>
        <a href="#resultados">Resultados</a>
        <a href="#demo">Contacto</a>
      </div>
      <div class="nav-cta">
        <a class="btn btn-ghost btn-sm btn-pill" href="#demo" style="display:none">Iniciar sesión</a>
        <a class="btn btn-primary btn-sm btn-pill" href="#demo">Solicitar demo</a>
      </div>
    </div>
  </nav>

  <!-- ============== HERO ============== -->
  <header class="hero">
    <div class="hero-copy">
      <span class="eyebrow reveal">
        <span class="dot" style="width:6px;height:6px;border-radius:50%;background:var(--accent);display:inline-block"></span>
        Hecho en México · Para hoteles boutique
      </span>
      <h1 class="display-xxl reveal delay-1">
        El PMS mexicano diseñado para hoteles <span class="accent">independientes</span>.
      </h1>
      <p class="lede reveal delay-2">
        Reservas, huéspedes, pagos y operación — todo en un solo lugar. Pensado para hoteles boutique, casas de huéspedes y propiedades vacacionales que prefieren sentirse acompañados, no atendidos por un call center.
      </p>
      <div class="hero-ctas reveal delay-3">
        <a class="btn btn-primary" href="#demo">Solicitar demo</a>
        <a class="btn btn-ghost" href="#funciones">Ver cómo funciona →</a>
      </div>
      <div class="hero-meta reveal delay-4">
        <span class="pin" aria-hidden="true"></span>
        <span>Soporte en español</span>
        <span class="sep" aria-hidden="true"></span>
        <span>Cobros en MXN</span>
        <span class="sep" aria-hidden="true"></span>
        <span>Sin complicaciones</span>
      </div>
    </div>

    <!-- HAND-BUILT DASHBOARD MOCK -->
    <aside class="dashboard reveal delay-2" aria-label="Vista previa del panel de Hospedia">
      <div class="dash-titlebar">
        <div class="dash-dots" aria-hidden="true"><span></span><span></span><span></span></div>
        <div class="dash-title">panel.<strong>hospedia.mx</strong> / hoy · martes 5 de mayo</div>
        <div style="width:48px"></div>
      </div>
      <div class="dash-body">

        <div class="dash-row">
          <!-- Donut: Occupancy -->
          <div class="dash-card donut-card">
            <div class="donut" aria-hidden="true">
              <svg viewBox="0 0 100 100" width="96" height="96">
                <circle cx="50" cy="50" r="42" stroke-width="8" fill="none" class="ring-bg"></circle>
                <circle cx="50" cy="50" r="42" stroke-width="8" fill="none" class="ring-fg"
                        stroke-linecap="round"
                        stroke-dasharray="263.89"
                        stroke-dashoffset="263.89"
                        id="donut-fg"></circle>
              </svg>
              <div class="donut-label"><b class="tnum" id="occVal">87%</b><span>Ocupación</span></div>
            </div>
            <div class="donut-meta">
              <div class="label">Hoy</div>
              <div class="value tnum">26<span style="font-size:18px;color:var(--muted)"> / 30</span></div>
              <span class="delta">▲ 12% vs sem. pasada</span>
            </div>
          </div>

          <!-- KPI: Check-ins -->
          <div class="dash-card">
            <div class="label">Check-ins</div>
            <div class="value tnum">14</div>
            <span class="delta">▲ 3 confirmados</span>
          </div>

          <!-- KPI: Check-outs -->
          <div class="dash-card">
            <div class="label">Check-outs</div>
            <div class="value tnum">6</div>
            <span class="delta flat">▸ a las 12:00</span>
          </div>
        </div>

        <!-- Reservations strip -->
        <div class="dash-card res-card">
          <div class="rooms-head" style="margin-bottom:14px">
            <div class="rooms-title">Llegadas de hoy</div>
            <div class="rooms-legend"><span style="color:var(--accent);font-weight:700">Ver todas →</span></div>
          </div>
          <div class="res-row">
            <div class="res-avatar" style="background:#5e7e8c">MR</div>
            <div>
              <div class="res-name">Mariana Rivas</div>
              <div class="res-sub">Hab. 204 · 3 noches · Booking.com</div>
            </div>
            <span class="pill pill-arrive">Llega 15:00</span>
            <div class="res-amount tnum">$8,420</div>
          </div>
          <div class="res-row">
            <div class="res-avatar" style="background:#a8755a">JT</div>
            <div>
              <div class="res-name">Jorge Treviño</div>
              <div class="res-sub">Suite 301 · 5 noches · Sitio directo</div>
            </div>
            <span class="pill pill-confirm">Confirmada</span>
            <div class="res-amount tnum">$22,100</div>
          </div>
          <div class="res-row">
            <div class="res-avatar" style="background:#7a6d8c">VL</div>
            <div>
              <div class="res-name">Valeria López</div>
              <div class="res-sub">Hab. 108 · 2 noches · Airbnb</div>
            </div>
            <span class="pill pill-pend">Por pagar</span>
            <div class="res-amount tnum">$4,950</div>
          </div>
        </div>

        <!-- Room grid -->
        <div class="dash-card rooms-card">
          <div class="rooms-head">
            <div class="rooms-title">Disponibilidad · 30 hab.</div>
            <div class="rooms-legend">
              <span><i class="legend-occ"></i>Ocupada</span>
              <span><i class="legend-in"></i>Llega hoy</span>
              <span><i class="legend-out"></i>Sale hoy</span>
              <span><i class="legend-av"></i>Libre</span>
            </div>
          </div>
          <div class="rooms-grid">
            <div class="room occ">101</div><div class="room occ">102</div><div class="room out">103</div><div class="room cln">104</div><div class="room occ">105</div><div class="room in">106</div><div class="room occ">107</div><div class="room cln">108</div>
            <div class="room occ">201</div><div class="room cln">202</div><div class="room occ">203</div><div class="room in">204</div><div class="room occ">205</div><div class="room out">206</div><div class="room occ">207</div><div class="room occ">208</div>
            <div class="room occ">301</div><div class="room in">302</div><div class="room occ">303</div><div class="room occ">304</div><div class="room out">305</div><div class="room cln">306</div><div class="room occ">307</div><div class="room occ">308</div>
            <div class="room occ">401</div><div class="room occ">402</div><div class="room occ">403</div><div class="room cln">404</div><div class="room in">405</div><div class="room occ">406</div>
          </div>
        </div>

      </div>
    </aside>
  </header>

  <!-- ============== MARQUEE ============== -->
  <div class="marquee" aria-label="Hoteles que usan Hospedia">
    <div class="marquee-track" id="marquee-track">
      <span class="marquee-item">Hotel Casa Lúa · San Miguel de Allende</span>
      <span class="marquee-item">Casa de Huéspedes Mariposa · Oaxaca</span>
      <span class="marquee-item">B&amp;B El Mirador · Valle de Bravo</span>
      <span class="marquee-item">Hotel Independiente Cuatro Vientos · CDMX</span>
      <span class="marquee-item">Hostería Bacalar · Quintana Roo</span>
      <span class="marquee-item">Casa Rural La Quinta · Puebla</span>
      <span class="marquee-item">Hotel Boutique Sayulita · Nayarit</span>
      <span class="marquee-item">Posada del Carmen · Mérida</span>
    </div>
  </div>

  <!-- ============== WHY ============== -->
  <section class="why" id="porque">
    <div class="container">
      <div class="section-head reveal">
        <span class="eyebrow">Por qué Hospedia</span>
        <h2 class="display-l">¿Por qué un PMS <em class="italic" style="color:var(--accent)">mexicano</em>?</h2>
        <p class="lede">Porque administrar un hotel boutique en Tulum no se parece a operar una cadena en Miami. Las herramientas que importas tampoco se sienten así.</p>
      </div>

      <div class="why-grid">
        <article class="why-card reveal">
          <div class="why-icon" aria-hidden="true">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M3 21V9l9-6 9 6v12"/><path d="M9 21v-7h6v7"/></svg>
          </div>
          <h3>Operación boutique</h3>
          <p>Diseñado para hoteles de 5 a 50 habitaciones. Sin módulos de cadena que estorban ni jerarquías corporativas que sobran.</p>
        </article>
        <article class="why-card reveal delay-1">
          <div class="why-icon" aria-hidden="true">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><circle cx="12" cy="12" r="9"/><path d="M3 12h18M12 3a14 14 0 0 1 0 18M12 3a14 14 0 0 0 0 18"/></svg>
          </div>
          <h3>Integración con reservas</h3>
          <p>Conecta Booking, Airbnb, Expedia y tu sitio directo en un solo calendario. Inventario sincronizado en tiempo real.</p>
        </article>
        <article class="why-card reveal delay-2">
          <div class="why-icon" aria-hidden="true">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><rect x="3" y="6" width="18" height="13" rx="2"/><path d="M3 10h18M7 15h2"/></svg>
          </div>
          <h3>Pagos en MXN</h3>
          <p>Cobra en pesos directo a tu cuenta, conectado con bancos y procesadores mexicanos. Stripe, OpenPay, Mercado Pago, Conekta.</p>
        </article>
        <article class="why-card reveal delay-3">
          <div class="why-icon" aria-hidden="true">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M21 12a9 9 0 1 1-3.5-7.1"/><path d="M21 4v5h-5"/></svg>
          </div>
          <h3>Soporte en español</h3>
          <p>Equipo en CDMX y Mérida. WhatsApp directo con humanos, no chatbots. Respondemos en minutos, en tu mismo huso horario.</p>
        </article>
      </div>

      <!-- Comparison -->
      <div class="compare reveal">
        <div class="compare-col">
          <h4>Otros PMS</h4>
          <ul class="compare-list">
            <li class="dim"><span class="compare-mark x">×</span> Diseñado para cadenas en EE. UU. y Europa</li>
            <li class="dim"><span class="compare-mark x">×</span> Soporte en inglés, en horario de Nueva York</li>
            <li class="dim"><span class="compare-mark x">×</span> Pagos enredados — primero USD, luego MXN</li>
            <li class="dim"><span class="compare-mark x">×</span> Contratos anuales y costos sorpresa</li>
            <li class="dim"><span class="compare-mark x">×</span> Onboarding de 90 días con consultor</li>
          </ul>
        </div>
        <div class="compare-col hospedia">
          <h4>Hospedia</h4>
          <ul class="compare-list">
            <li><span class="compare-mark v">✓</span> Hecho para hoteles boutique mexicanos</li>
            <li><span class="compare-mark v">✓</span> Soporte en español, mismo huso horario</li>
            <li><span class="compare-mark v">✓</span> Pagos en MXN, integraciones locales</li>
            <li><span class="compare-mark v">✓</span> Mes a mes, sin permanencia ni cláusulas raras</li>
            <li><span class="compare-mark v">✓</span> Te montamos en 7 días con tu equipo</li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- ============== BEFORE / AFTER ============== -->
  <section class="ba">
    <div class="container">
      <div class="section-head reveal">
        <span class="eyebrow">Antes y después</span>
        <h2 class="display-l">El lunes en la mañana, <em class="italic">antes</em> y <em class="italic" style="color:var(--accent)">después</em>.</h2>
        <p class="lede">Lo que cambia cuando dejas de orquestar tu hotel desde tres ventanas de Excel y un grupo de WhatsApp.</p>
      </div>

      <div class="ba-grid">
        <div class="ba-panel ba-without reveal">
          <span class="label">Sin Hospedia</span>
          <h3>Apagar incendios antes del primer café.</h3>
          <ul class="ba-list">
            <li><span class="ba-mark">×</span> Excel y WhatsApp para cuadrar las reservas del fin de semana</li>
            <li><span class="ba-mark">×</span> Overbooking porque dos canales no se hablaron</li>
            <li><span class="ba-mark">×</span> Cobros manuales y conciliación bancaria a fin de mes</li>
            <li><span class="ba-mark">×</span> Reportes que toman 3 horas cada lunes</li>
            <li><span class="ba-mark">×</span> Tu equipo de limpieza no sabe qué cuartos están listos</li>
          </ul>
        </div>
        <div class="ba-panel ba-with reveal delay-1">
          <span class="label">Con Hospedia</span>
          <h3>Tu equipo empieza el día <em class="italic" style="color:var(--accent)">sabiendo</em> qué hacer.</h3>
          <ul class="ba-list">
            <li><span class="ba-mark">✓</span> Calendario único que sincroniza todos los canales</li>
            <li><span class="ba-mark">✓</span> Cero overbooking — disponibilidad al segundo</li>
            <li><span class="ba-mark">✓</span> Pagos en MXN automatizados, conciliación en un click</li>
            <li><span class="ba-mark">✓</span> Reporte de ocupación en tu correo cada mañana</li>
            <li><span class="ba-mark">✓</span> Tablero de housekeeping con asignación por turno</li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- ============== FEATURES ============== -->
  <section class="features" id="funciones">
    <div class="container">
      <div class="section-head reveal">
        <span class="eyebrow">Funciones</span>
        <h2 class="display-l">Todo lo que tu hotel necesita, en <em class="italic">un solo</em> lugar.</h2>
        <p class="lede">Una plataforma completa que reemplaza cinco herramientas. Sin integraciones frágiles, sin pestañas abiertas, sin pretextos.</p>
      </div>

      <div class="feat-grid">
        <article class="feat-card reveal">
          <span class="feat-badge">Channel Manager</span>
          <div class="feat-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><rect x="3" y="5" width="18" height="16" rx="2"/><path d="M3 10h18M8 3v4M16 3v4"/></svg></div>
          <h3>Gestión de Reservas</h3>
          <p>Calendario unificado con vista mensual, semanal y por habitación. Drag-and-drop, sincronización en tiempo real con Booking, Airbnb, Expedia y tu sitio directo.</p>
        </article>
        <article class="feat-card reveal delay-1">
          <span class="feat-badge">CRM incluido</span>
          <div class="feat-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><circle cx="12" cy="8" r="4"/><path d="M4 21c0-4.4 3.6-8 8-8s8 3.6 8 8"/></svg></div>
          <h3>Huéspedes</h3>
          <p>Perfiles, historial, preferencias, alergias, comunicación automatizada por WhatsApp y correo. Vuelven y los recuerdas como un anfitrión, no como un sistema.</p>
        </article>
        <article class="feat-card reveal delay-2">
          <span class="feat-badge">Inteligencia diaria</span>
          <div class="feat-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M3 21h18"/><rect x="6" y="11" width="3" height="9"/><rect x="11" y="6" width="3" height="14"/><rect x="16" y="13" width="3" height="7"/></svg></div>
          <h3>Reportes</h3>
          <p>Ocupación, ADR, RevPAR y P&amp;L en tiempo real. Comparativos por mes, canal y temporada. Exporta en CSV o recibe el resumen en tu correo cada mañana.</p>
        </article>
        <article class="feat-card reveal delay-1">
          <span class="feat-badge">Stripe · OpenPay · Conekta</span>
          <div class="feat-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><rect x="3" y="6" width="18" height="13" rx="2"/><path d="M3 10h18M7 15h4"/></svg></div>
          <h3>Pagos</h3>
          <p>Cobra en MXN, divide por habitación, factura sin complicaciones. Liga de pago por WhatsApp, depósitos parciales, conciliación automática con tu banco.</p>
        </article>
        <article class="feat-card reveal delay-2">
          <span class="feat-badge">Equipo sincronizado</span>
          <div class="feat-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M9 11l3 3 5-5"/><circle cx="12" cy="12" r="9"/></svg></div>
          <h3>Operación</h3>
          <p>Asigna limpieza, mantenimiento y cambios de turno. Tu equipo abre la app y ve qué cuartos limpiar primero, qué arreglar y a qué hora. Adiós libreta.</p>
        </article>
      </div>
    </div>
  </section>

  <!-- ============== FOR WHO ============== -->
  <section class="who" id="hoteles">
    <div class="container">
      <div class="section-head reveal">
        <span class="eyebrow">Para quién</span>
        <h2 class="display-l">Diseñado para ti si tienes…</h2>
        <p class="lede">Hospedia escala desde una propiedad vacacional con cuatro cuartos hasta un hotel boutique de cincuenta. Si tu operación es más cálida que corporativa, te entendemos.</p>
      </div>

      <div class="who-grid">
        <article class="who-card reveal"><div class="who-emoji">🏨</div><h3>Hotel Boutique</h3><p>15 a 50 hab. Curaduría propia, equipo cercano.</p></article>
        <article class="who-card reveal delay-1"><div class="who-emoji">🏡</div><h3>Casa de Huéspedes</h3><p>5 a 15 hab. Trato familiar, anfitrión presente.</p></article>
        <article class="who-card reveal delay-2"><div class="who-emoji">🏛</div><h3>Hotel Independiente</h3><p>Sin franquicia. Marca propia, decisiones rápidas.</p></article>
        <article class="who-card reveal delay-3"><div class="who-emoji">🏖</div><h3>Propiedad Vacacional</h3><p>2 a 10 unidades. Corta y media estancia.</p></article>
        <article class="who-card reveal delay-4"><div class="who-emoji">☕</div><h3>B&amp;B</h3><p>Pequeño, cuidado, con desayuno casero incluido.</p></article>
      </div>
    </div>
  </section>

  <!-- ============== RESULTS ============== -->
  <section class="results" id="resultados">
    <div class="container">
      <div class="section-head reveal">
        <span class="eyebrow">Resultados</span>
        <h2 class="display-l">Lo que mejora desde el primer mes.</h2>
        <p class="lede">Promedios entre los hoteles que llevan al menos seis meses con Hospedia. Calculados a partir de su propia operación previa.</p>
      </div>
      <div class="results-grid">
        <div class="result-block reveal">
          <div class="result-num tnum">+23<span class="unit">%</span></div>
          <h3>Más ocupación</h3>
          <p>Por sincronización en tiempo real con todos los canales y precios dinámicos por temporada.</p>
        </div>
        <div class="result-block reveal delay-1">
          <div class="result-num tnum">−94<span class="unit">%</span></div>
          <h3>Menos errores</h3>
          <p>Overbookings, cobros duplicados y check-ins confusos prácticamente desaparecen al unificar canales.</p>
        </div>
        <div class="result-block reveal delay-2">
          <div class="result-num tnum">8<span class="unit"> hrs</span></div>
          <h3>Más tiempo para huéspedes</h3>
          <p>Por semana — el tiempo que tu equipo recupera de Excel y WhatsApp para dedicarlo a la experiencia del huésped.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- ============== TESTIMONIAL ============== -->
  <section style="padding-top: 0">
    <div class="container">
      <div class="quote reveal">
        <div class="quote-stars" aria-label="5 de 5 estrellas">
          <span>★</span><span>★</span><span>★</span><span>★</span><span>★</span>
        </div>
        <p class="quote-body">
          Hospedia simplificó completamente nuestra operación diaria. Antes vivíamos pegados al Excel y discutiendo overbookings con Booking; ahora todo está en un solo lugar y mi equipo tiene <em>tiempo</em> para los huéspedes.
        </p>
        <div class="quote-attr">
          <div class="quote-avatar">MR</div>
          <div>
            <strong>María Fernanda Rivas</strong> · Directora · Hotel Casa Lúa
            <div style="font-size:13px;opacity:.7;margin-top:2px">San Miguel de Allende, Guanajuato · Cliente desde 2024</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ============== CTA / FORM ============== -->
  <section class="cta" id="demo">
    <div class="container">
      <div class="cta-grid reveal">
        <div>
          <span class="eyebrow" style="display:inline-block;margin-bottom:18px">Solicita tu demo</span>
          <h2 class="display-l">Administra tu hotel con tecnología <em class="italic" style="color:var(--accent)">hecha para México</em>.</h2>
          <p class="lede">Demo personalizada de 30 minutos con un especialista. Te montamos un ambiente con datos de tu propiedad para que veas cómo se siente.</p>

          <form class="form" id="demo-form" novalidate>
            <div class="form-row">
              <div class="field">
                <label for="f-name">Nombre completo</label>
                <input id="f-name" name="name" type="text" placeholder="Tu nombre" required />
              </div>
              <div class="field">
                <label for="f-hotel">Nombre del hotel</label>
                <input id="f-hotel" name="hotel" type="text" placeholder="Ej. Hotel Casa Lúa" required />
              </div>
            </div>
            <div class="form-row">
              <div class="field">
                <label for="f-email">Correo</label>
                <input id="f-email" name="email" type="email" placeholder="tu@hotel.mx" required />
              </div>
              <div class="field">
                <label for="f-phone">Teléfono / WhatsApp</label>
                <input id="f-phone" name="phone" type="tel" placeholder="+52 ··· ··· ····" required />
              </div>
            </div>
            <button class="btn btn-primary" type="submit">Solicitar demo gratuita →</button>
            <div class="form-foot">
              <span>O escríbenos directo por</span>
              <a href="#">WhatsApp →</a>
              <span style="margin-left:auto">Sin spam · Sin compromiso</span>
            </div>
          </form>

          <div class="form-success" id="form-success">
            <div class="check-big" aria-hidden="true">✓</div>
            <h3>Listo. Te escribimos hoy mismo.</h3>
            <p>Un especialista de Hospedia te contactará en las próximas dos horas para agendar tu demo. Mientras tanto, puedes escribirnos por WhatsApp si prefieres adelantarlo.</p>
          </div>
        </div>

        <aside class="checklist-card">
          <h4>¿Qué incluye la demo?</h4>
          <div class="item"><span class="check">✓</span><div><strong>Recorrido personalizado</strong> de 30 min con un especialista mexicano.</div></div>
          <div class="item"><span class="check">✓</span><div><strong>Demo con datos de tu propiedad</strong> — habitaciones, tarifas y temporada real.</div></div>
          <div class="item"><span class="check">✓</span><div><strong>Plan de migración</strong> desde Excel u otro PMS, sin pérdida de datos.</div></div>
          <div class="item"><span class="check">✓</span><div><strong>Cotización clara en MXN</strong>, sin permanencia ni costos sorpresa.</div></div>
          <div class="item"><span class="check">✓</span><div><strong>Acceso a la red</strong> de hoteles boutique que ya usan Hospedia.</div></div>
        </aside>
      </div>
    </div>
  </section>

  <!-- ============== FOOTER ============== -->
  <footer>
    <div class="container">
      <div class="foot-top">
        <div class="foot-brand">
          <a href="#" class="logo" aria-label="Hospedia">
            <span class="dot" aria-hidden="true"></span>
            Hospedia
            <small>PMS</small>
          </a>
          <p>El sistema de gestión hotelera hecho en México para hoteles boutique, casas de huéspedes y propiedades vacacionales.</p>
        </div>
        <div class="foot-col">
          <h5>Producto</h5>
          <ul>
            <li><a href="#funciones">Funciones</a></li>
            <li><a href="#">Integraciones</a></li>
            <li><a href="#">Precios</a></li>
            <li><a href="#">Seguridad</a></li>
          </ul>
        </div>
        <div class="foot-col">
          <h5>Empresa</h5>
          <ul>
            <li><a href="#">Sobre Hospedia</a></li>
            <li><a href="#">Casos de éxito</a></li>
            <li><a href="#">Blog</a></li>
            <li><a href="#demo">Contacto</a></li>
          </ul>
        </div>
        <div class="foot-col">
          <h5>Recursos</h5>
          <ul>
            <li><a href="#">Centro de ayuda</a></li>
            <li><a href="#demo">Demo</a></li>
            <li><a href="#">Estado del sistema</a></li>
            <li><a href="#">Documentación API</a></li>
          </ul>
        </div>
      </div>
      <div class="foot-bot">
        <span>© 2026 Hospedia · Todos los derechos reservados.</span>
        <span class="foot-mx">Hecho en México <span aria-hidden="true">🇲🇽</span></span>
      </div>
    </div>
  </footer>

  <script>
    // ===== Sticky nav state =====
    (function () {
      const nav = document.getElementById('nav');
      const onScroll = () => {
        if (window.scrollY > 16) nav.classList.add('scrolled');
        else nav.classList.remove('scrolled');
      };
      window.addEventListener('scroll', onScroll, { passive: true });
      onScroll();
    })();

    // ===== Reveal on scroll =====
    (function () {
      const els = document.querySelectorAll('.reveal');
      if (!('IntersectionObserver' in window)) {
        els.forEach(el => el.classList.add('in'));
        return;
      }
      const io = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('in');
            io.unobserve(entry.target);
          }
        });
      }, { rootMargin: '0px 0px -8% 0px', threshold: 0.06 });
      els.forEach(el => io.observe(el));
    })();

    // ===== Donut animate to 87% =====
    (function () {
      const fg = document.getElementById('donut-fg');
      if (!fg) return;
      const C = 2 * Math.PI * 42; // 263.89
      const target = 87;
      requestAnimationFrame(() => {
        setTimeout(() => {
          fg.style.strokeDashoffset = String(C - (C * target / 100));
        }, 350);
      });
    })();

    // ===== Marquee duplicate for seamless loop =====
    (function () {
      const track = document.getElementById('marquee-track');
      if (!track) return;
      track.innerHTML = track.innerHTML + track.innerHTML;
    })();

    // ===== Form submit -> success state =====
    (function () {
      const form = document.getElementById('demo-form');
      const success = document.getElementById('form-success');
      if (!form || !success) return;
      form.addEventListener('submit', (e) => {
        e.preventDefault();
        const inputs = form.querySelectorAll('input[required]');
        let ok = true;
        inputs.forEach(i => {
          if (!i.value.trim()) {
            ok = false;
            i.style.borderColor = 'var(--error)';
            i.addEventListener('input', () => { i.style.borderColor = ''; }, { once: true });
          }
        });
        if (!ok) return;
        form.style.display = 'none';
        success.classList.add('show');
      });
    })();
  </script>

</body>
</html>
