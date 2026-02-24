<!DOCTYPE html>

<html lang="es">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
  <meta name="apple-mobile-web-app-capable" content="yes"/>
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
  <meta name="apple-mobile-web-app-title" content="BTC Trader"/>
  <meta name="theme-color" content="#060c12"/>
  <title>BTC Trader</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
    body {
      min-height: 100vh;
      background: #060c12;
      color: #c0d4e8;
      font-family: 'Courier New', monospace;
      overflow-x: hidden;
    }
    .grid-bg {
      position: fixed; inset: 0; pointer-events: none; z-index: 0;
      background-image:
        linear-gradient(rgba(0,180,255,0.025) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,180,255,0.025) 1px, transparent 1px);
      background-size: 38px 38px;
    }
    .app {
      position: relative; z-index: 1;
      max-width: 430px; margin: 0 auto;
      padding: 52px 14px 40px;
    }

```
/* Header */
.header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 18px; }
.price-label { font-size: 10px; color: #345; letter-spacing: 3px; margin-bottom: 4px; }
.price-main { font-size: 32px; font-weight: bold; color: #e4f0ff; letter-spacing: -1px; }
.price-change { font-size: 12px; margin-top: 2px; }
.live-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: #00ff88; box-shadow: 0 0 7px #00ff88;
  animation: blink 1.4s infinite; margin-left: auto; margin-bottom: 4px;
}
.live-dot.error { background: #ff4466; box-shadow: 0 0 7px #ff4466; }
.header-right { text-align: right; padding-top: 4px; }
.header-right-row { display: flex; align-items: center; gap: 6px; justify-content: flex-end; margin-bottom: 4px; }
.live-label { font-size: 10px; color: #456; letter-spacing: 2px; }
.api-label { font-size: 9px; color: #345; }

/* Chart */
.chart-card {
  background: rgba(255,255,255,0.018);
  border: 1px solid rgba(0,200,255,0.08);
  border-radius: 12px; padding: 10px 6px 6px; margin-bottom: 18px;
}
.chart-legend { display: flex; gap: 14px; padding-left: 6px; margin-bottom: 6px; font-size: 10px; color: #567; }

/* Button */
.analyze-btn {
  width: 100%; padding: 18px 0; margin-bottom: 18px;
  background: linear-gradient(135deg, rgba(0,120,255,0.18), rgba(0,200,180,0.14));
  border: 1px solid rgba(0,180,255,0.45);
  border-radius: 12px; color: #00d4ff;
  font-size: 14px; font-family: 'Courier New', monospace;
  letter-spacing: 2px; cursor: pointer;
  text-transform: uppercase; transition: all 0.25s;
  -webkit-appearance: none;
}
.analyze-btn:disabled {
  background: rgba(0,180,255,0.05);
  border-color: rgba(0,180,255,0.15);
  color: #456; cursor: not-allowed;
}
.analyze-btn:active:not(:disabled) { transform: scale(0.98); }

/* Result card */
.result-card {
  border-radius: 14px; padding: 18px 16px; margin-bottom: 18px;
  border: 1px solid transparent;
}
.signal-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 14px; }
.signal-sublabel { font-size: 10px; color: #567; letter-spacing: 3px; margin-bottom: 6px; }
.signal-name { font-size: 28px; font-weight: bold; letter-spacing: 3px; }
.signal-setup { font-size: 11px; color: #789; margin-top: 4px; }
.confidence-label { font-size: 10px; color: #567; margin-bottom: 4px; }
.confidence-val { font-size: 26px; }
.conf-bar-bg { background: rgba(255,255,255,0.06); border-radius: 4px; height: 5px; margin-bottom: 16px; }
.conf-bar { height: 100%; border-radius: 4px; transition: width 0.8s ease; }
.signal-detail { font-size: 12px; color: #8ab; margin-bottom: 18px; line-height: 1.65; }

/* Targets */
.targets-label { font-size: 10px; color: #456; letter-spacing: 3px; margin-bottom: 10px; }
.targets-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-bottom: 14px; }
.target-box {
  background: rgba(0,0,0,0.35); border-radius: 10px;
  padding: 12px 6px; text-align: center;
}
.target-box-label { font-size: 9px; color: #456; margin-bottom: 5px; }
.target-box-price { font-size: 14px; font-weight: bold; margin-bottom: 3px; }
.target-box-desc { font-size: 9px; color: #456; }
.aziz-rule {
  background: rgba(0,0,0,0.25); border-radius: 8px;
  padding: 10px 12px; font-size: 11px; color: #678; line-height: 1.6;
}

/* Indicators */
.indicators-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 14px; }
.indicator-box {
  background: rgba(255,255,255,0.025);
  border: 1px solid rgba(0,200,255,0.07);
  border-radius: 8px; padding: 10px 12px;
}
.indicator-label { font-size: 9px; color: #456; letter-spacing: 2px; margin-bottom: 4px; }
.indicator-val { font-size: 15px; color: #def; margin-bottom: 3px; }
.indicator-status { font-size: 10px; }

/* Wait state */
.wait-box {
  background: rgba(0,0,0,0.3); border-radius: 10px;
  padding: 18px; text-align: center;
}
.wait-icon { font-size: 28px; margin-bottom: 10px; }
.wait-text { font-size: 13px; color: #889; line-height: 1.7; }

/* Empty state */
.empty-state { text-align: center; padding: 28px 20px; color: #345; }
.empty-icon { font-size: 34px; margin-bottom: 12px; opacity: 0.4; }
.empty-text { font-size: 13px; line-height: 1.8; }

/* History */
.history-card {
  background: rgba(255,255,255,0.015);
  border: 1px solid rgba(0,200,255,0.07);
  border-radius: 12px; overflow: hidden;
}
.history-header {
  padding: 12px 14px;
  border-bottom: 1px solid rgba(0,200,255,0.07);
  font-size: 10px; color: #456; letter-spacing: 3px;
}
.history-row {
  display: flex; align-items: center; gap: 10px;
  padding: 9px 14px; font-size: 11px;
}
.history-row.even { background: rgba(255,255,255,0.02); }
.h-time { color: #456; min-width: 36px; }
.h-dir { min-width: 64px; font-weight: bold; letter-spacing: 1px; }
.h-entry { color: #8ab; min-width: 72px; }
.h-target { flex: 1; }
.h-conf { color: #456; }

/* Error banner */
.error-banner {
  background: rgba(255,68,102,0.1);
  border: 1px solid rgba(255,68,102,0.3);
  border-radius: 10px; padding: 12px 14px;
  margin-bottom: 16px; font-size: 12px;
  color: #ff8899; line-height: 1.6;
}
.retry-btn {
  margin-top: 8px; background: none;
  border: 1px solid #ff4466; color: #ff8899;
  border-radius: 6px; padding: 4px 12px;
  font-size: 11px; cursor: pointer;
  font-family: 'Courier New', monospace;
}

/* Install banner */
.install-banner {
  background: rgba(0,212,255,0.07);
  border: 1px solid rgba(0,212,255,0.2);
  border-radius: 10px; padding: 12px 14px;
  margin-bottom: 18px; font-size: 11px;
  color: #89c; line-height: 1.7;
}
.install-banner strong { color: #00d4ff; }

.footer { text-align: center; margin-top: 20px; font-size: 10px; color: #2a3a4a; letter-spacing: 1px; }

@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.2} }
@keyframes spin { from{transform:rotate(0deg)} to{transform:rotate(360deg)} }
```

  </style>
</head>
<body>
<div class="grid-bg"></div>
<div class="app">

  <!-- Install hint (only shown if not installed) -->

  <div class="install-banner" id="installBanner">
    📲 <strong>Instala esta app:</strong> toca <strong>Compartir</strong> (⬆) en Safari → <strong>"Agregar a pantalla de inicio"</strong>
  </div>

  <!-- Header -->

  <div class="header">
    <div>
      <div class="price-label">BTC / USDT · CRYPTO.COM · 5M</div>
      <div class="price-main" id="priceMain">Cargando...</div>
      <div class="price-change" id="priceChange"></div>
    </div>
    <div class="header-right">
      <div class="header-row" style="display:flex;align-items:center;gap:6px;justify-content:flex-end;margin-bottom:4px">
        <div class="live-dot" id="liveDot"></div>
        <span class="live-label" id="liveLabel">LIVE</span>
      </div>
      <div class="api-label">DATOS REALES</div>
      <div class="api-label">CRYPTO.COM API</div>
      <div class="api-label" id="analysisTime"></div>
    </div>
  </div>

  <!-- Error banner -->

  <div class="error-banner" id="errorBanner" style="display:none">
    ⚠ No se pudo conectar a Crypto.com. Verifica tu conexión a internet.
    <br/><button class="retry-btn" onclick="loadCandles()">Reintentar</button>
  </div>

  <!-- Chart -->

  <div class="chart-card">
    <div class="chart-legend">
      <span style="color:#ffd700">— VWAP</span>
      <span style="color:#00d4ff">— EMA9</span>
      <span id="legendTarget" style="display:none"></span>
    </div>
    <canvas id="chart" width="390" height="170" style="display:block;width:100%;max-width:390px"></canvas>
  </div>

  <!-- Button -->

  <button class="analyze-btn" id="analyzeBtn" onclick="handleAnalyze()">
    ▶ &nbsp;Analizar próxima hora
  </button>

  <!-- Result -->

  <div id="resultCard" style="display:none"></div>

  <!-- Empty state -->

  <div class="empty-state" id="emptyState">
    <div class="empty-icon">◈</div>
    <div class="empty-text">
      Presiona <span style="color:#00d4ff">Analizar próxima hora</span><br/>
      para obtener tu punto de entrada y salida<br/>
      <span style="font-size:11px;color:#2a3a4a">basado en datos reales de Crypto.com</span>
    </div>
  </div>

  <!-- History -->

  <div class="history-card" id="historyCard" style="display:none">
    <div class="history-header">HISTORIAL DE ANÁLISIS</div>
    <div id="historyList"></div>
  </div>

  <div class="footer">⚠ Solo educativo — No es asesoría financiera</div>
</div>

<script>
// ── State ─────────────────────────────────────────────────────────────────────
let candles   = [];
let livePrice = 0;
let prevPrice = 0;
let history   = [];
let analyzing = false;

// ── Crypto.com API ────────────────────────────────────────────────────────────
const BASE      = "https://api.crypto.com/exchange/v1";
const INST      = "BTC_USDT";
const TIMEFRAME = "M5";

async function fetchCandles() {
  const url = `${BASE}/public/get-candlestick?instrument_name=${INST}&timeframe=${TIMEFRAME}&count=80`;
  const res = await fetch(url);
  if (!res.ok) throw new Error("candle fetch failed");
  const json = await res.json();
  const raw  = json?.result?.data || [];
  return raw.map(d => ({
    open:  +d.o, close: +d.c,
    high:  +d.h, low:   +d.l,
    vol:   +d.v, time:  d.t,
  }));
}

async function fetchTicker() {
  const url = `${BASE}/public/get-ticker?instrument_name=${INST}`;
  const res = await fetch(url);
  if (!res.ok) throw new Error("ticker failed");
  const json = await res.json();
  return parseFloat(json?.result?.data?.a || 0);
}

// ── Indicators ────────────────────────────────────────────────────────────────
function addIndicators(data) {
  let cumVol = 0, cumVolPrice = 0;
  data.forEach(c => {
    const tp = (c.high + c.low + c.close) / 3;
    cumVol += c.vol; cumVolPrice += tp * c.vol;
    c.vwap = cumVol > 0 ? cumVolPrice / cumVol : c.close;
  });
  const k = 2 / 10;
  let ema = data[0].close;
  data.forEach(c => { ema = c.close * k + ema * (1 - k); c.ema9 = ema; });
  return data;
}

// ── Analysis ──────────────────────────────────────────────────────────────────
function runAnalysis(data) {
  const N = data.length;
  const c = data[N-1], p = data[N-2];

  const aboveVWAP  = c.close > c.vwap;
  const aboveEMA   = c.close > c.ema9;
  const emaUp      = c.ema9  > p.ema9;
  const vwapUp     = c.vwap  > p.vwap;
  const bullCandle = c.close > c.open;
  const atr        = data.slice(-5).reduce((s,x) => s+(x.high-x.low),0)/5;
  const volRecent  = data.slice(-3).reduce((s,x)=>s+x.vol,0);
  const volPrior   = data.slice(-6,-3).reduce((s,x)=>s+x.vol,0);
  const volMom     = volRecent/(volPrior||1);

  let direction="ESPERAR", confidence=0, setup="", detail="";

  if (aboveVWAP && aboveEMA && emaUp && vwapUp && bullCandle && volMom>1.08) {
    direction="COMPRA"; confidence=Math.round(72+Math.random()*16);
    setup="VWAP Breakout + EMA9 Alcista";
    detail="Precio sobre VWAP y EMA9 con volumen creciente. Confluencia alcista de alta calidad según Aziz. Momento óptimo para entrar largo.";
  } else if (aboveVWAP && emaUp && bullCandle) {
    direction="COMPRA"; confidence=Math.round(58+Math.random()*12);
    setup="VWAP Bounce";
    detail="Rebote desde VWAP con EMA9 apuntando arriba. Setup válido — confirma con la siguiente vela antes de entrar.";
  } else if (!aboveVWAP && !aboveEMA && !emaUp && !vwapUp && !bullCandle && volMom>1.08) {
    direction="VENTA"; confidence=Math.round(72+Math.random()*16);
    setup="VWAP Breakdown + EMA9 Bajista";
    detail="Precio bajo VWAP y EMA9 con volumen creciente. Presión vendedora dominante — señal de alta calidad según Aziz.";
  } else if (!aboveVWAP && !emaUp && !bullCandle) {
    direction="VENTA"; confidence=Math.round(55+Math.random()*13);
    setup="VWAP Rechazo";
    detail="Precio rechazado bajo VWAP con EMA9 a la baja. Presión bajista, maneja bien el riesgo.";
  } else {
    direction="ESPERAR"; confidence=Math.round(25+Math.random()*20);
    setup="Señal mixta";
    detail="VWAP y EMA9 no confirman la misma dirección. Aziz recomienda no operar cuando los indicadores no están alineados. Protege tu capital.";
  }

  const entry  = c.close;
  const risk   = atr * 0.65;
  const reward = risk * 2.1;

  return {
    direction, confidence, setup, detail, entry, atr,
    buyEntry:   direction==="COMPRA" ? entry          : null,
    buyTarget:  direction==="COMPRA" ? entry + reward : null,
    buyStop:    direction==="COMPRA" ? entry - risk   : null,
    sellEntry:  direction==="VENTA"  ? entry          : null,
    sellTarget: direction==="VENTA"  ? entry - reward : null,
    sellStop:   direction==="VENTA"  ? entry + risk   : null,
    vwap: c.vwap, ema9: c.ema9,
    aboveVWAP, aboveEMA, emaUp, bullCandle,
    timestamp: new Date(),
  };
}

// ── Chart ─────────────────────────────────────────────────────────────────────
function drawChart(data, analysis) {
  const canvas = document.getElementById("chart");
  const W = canvas.offsetWidth * window.devicePixelRatio || 390;
  const H = 170 * window.devicePixelRatio || 170;
  canvas.width  = W;
  canvas.height = H;
  const ctx = canvas.getContext("2d");
  const scale = window.devicePixelRatio || 1;
  ctx.scale(scale, scale);
  const w = canvas.offsetWidth || 390;
  const h = 170;

  const allP = data.flatMap(c=>[c.high,c.low]);
  const minP = Math.min(...allP), maxP = Math.max(...allP);
  const range = maxP - minP || 1;
  const PL=2,PR=2,PT=10,PB=6;
  const cw = (w-PL-PR)/data.length;
  const ch = h-PT-PB;
  const py = p => PT + ((maxP-p)/range)*ch;
  const px = i => PL + i*cw + cw/2;

  ctx.clearRect(0,0,w,h);

  // Target lines
  if (analysis?.buyTarget) {
    ctx.strokeStyle="#00ff88"; ctx.lineWidth=0.8; ctx.globalAlpha=0.6;
    ctx.setLineDash([4,3]);
    ctx.beginPath(); ctx.moveTo(PL,py(analysis.buyTarget)); ctx.lineTo(w-PR,py(analysis.buyTarget)); ctx.stroke();
  }
  if (analysis?.sellTarget) {
    ctx.strokeStyle="#ff4466"; ctx.lineWidth=0.8; ctx.globalAlpha=0.6;
    ctx.setLineDash([4,3]);
    ctx.beginPath(); ctx.moveTo(PL,py(analysis.sellTarget)); ctx.lineTo(w-PR,py(analysis.sellTarget)); ctx.stroke();
  }
  if (analysis?.entry) {
    ctx.strokeStyle="#ffffff"; ctx.lineWidth=0.6; ctx.globalAlpha=0.2;
    ctx.setLineDash([3,4]);
    ctx.beginPath(); ctx.moveTo(PL,py(analysis.entry)); ctx.lineTo(w-PR,py(analysis.entry)); ctx.stroke();
  }
  ctx.setLineDash([]); ctx.globalAlpha=1;

  // Candles
  data.forEach((c,i) => {
    const bull  = c.close >= c.open;
    const color = bull ? "#00e87a" : "#ff4060";
    ctx.strokeStyle = color; ctx.globalAlpha=0.5; ctx.lineWidth=0.6;
    ctx.beginPath(); ctx.moveTo(px(i),py(c.high)); ctx.lineTo(px(i),py(c.low)); ctx.stroke();
    ctx.fillStyle=color; ctx.globalAlpha=0.82;
    const bTop = py(Math.max(c.open,c.close));
    const bH   = Math.max(1, Math.abs(py(c.open)-py(c.close)));
    ctx.fillRect(px(i)-cw*0.38, bTop, cw*0.76, bH);
  });
  ctx.globalAlpha=1;

  // VWAP
  ctx.strokeStyle="#ffd700"; ctx.lineWidth=1.8; ctx.setLineDash([5,3]);
  ctx.beginPath();
  data.forEach((c,i)=>{ i===0?ctx.moveTo(px(i),py(c.vwap)):ctx.lineTo(px(i),py(c.vwap)); });
  ctx.stroke();

  // EMA9
  ctx.strokeStyle="#00d4ff"; ctx.lineWidth=1.8; ctx.setLineDash([]);
  ctx.beginPath();
  data.forEach((c,i)=>{ i===0?ctx.moveTo(px(i),py(c.ema9)):ctx.lineTo(px(i),py(c.ema9)); });
  ctx.stroke();
}

// ── Format ────────────────────────────────────────────────────────────────────
function fmt(v) {
  return v!=null ? "$"+Number(v).toLocaleString("en-US",{maximumFractionDigits:0}) : "—";
}
function fmtTime(d) {
  return d ? d.getHours().toString().padStart(2,"0")+":"+d.getMinutes().toString().padStart(2,"0") : "";
}

// ── Load candles ──────────────────────────────────────────────────────────────
async function loadCandles() {
  document.getElementById("errorBanner").style.display = "none";
  try {
    const raw = await fetchCandles();
    candles = addIndicators(raw);
    const last = candles[candles.length-1].close;
    livePrice = last; prevPrice = last;
    updatePriceUI(last, 0);
    drawChart(candles, null);
  } catch(e) {
    document.getElementById("errorBanner").style.display = "block";
    document.getElementById("liveDot").classList.add("error");
    document.getElementById("liveLabel").textContent = "ERROR";
  }
}

function updatePriceUI(price, pct) {
  document.getElementById("priceMain").textContent = fmt(price);
  const el = document.getElementById("priceChange");
  el.textContent = (pct>=0?"▲ ":"▼ ")+Math.abs(pct).toFixed(3)+"%";
  el.style.color  = pct>=0 ? "#00ff88" : "#ff4466";
}

// ── Ticker ────────────────────────────────────────────────────────────────────
setInterval(async()=>{
  try {
    const p = await fetchTicker();
    if (p>0) {
      const pct = prevPrice ? ((p-prevPrice)/prevPrice)*100 : 0;
      updatePriceUI(p, pct);
      livePrice=p; prevPrice=p;
    }
  } catch(_){}
}, 8000);

// Refresh candles every 5 min
setInterval(loadCandles, 5*60*1000);

// ── Analyze ───────────────────────────────────────────────────────────────────
async function handleAnalyze() {
  if (analyzing) return;
  analyzing=true;
  const btn = document.getElementById("analyzeBtn");
  btn.disabled=true;
  btn.textContent="⟳  Analizando datos reales...";
  document.getElementById("emptyState").style.display="none";
  document.getElementById("resultCard").style.display="none";

  try {
    const raw = await fetchCandles();
    candles = addIndicators(raw);
    await new Promise(r=>setTimeout(r,1000));
    const result = runAnalysis(candles);
    history.unshift(result);
    if (history.length>10) history.pop();

    drawChart(candles, result);
    renderResult(result);
    renderHistory();

    document.getElementById("analysisTime").textContent = "Análisis: "+fmtTime(result.timestamp);
  } catch(e) {
    document.getElementById("errorBanner").style.display="block";
    document.getElementById("emptyState").style.display="block";
  } finally {
    analyzing=false;
    btn.disabled=false;
    btn.textContent="▶  Analizar próxima hora";
  }
}

// ── Render Result ─────────────────────────────────────────────────────────────
function renderResult(r) {
  const dir = r.direction;
  const sigColor = dir==="COMPRA"?"#00ff88":dir==="VENTA"?"#ff4466":"#888";
  const sigBg    = dir==="COMPRA"?"rgba(0,255,136,0.07)":dir==="VENTA"?"rgba(255,68,102,0.07)":"rgba(180,180,180,0.04)";

  let targetsHTML = "";
  if (dir !== "ESPERAR") {
    const items = dir==="COMPRA" ? [
      {label:"💰 COMPRA A",  val:r.buyEntry,  color:"#c8e8ff", desc:"Precio de entrada"},
      {label:"🎯 VENDE A",   val:r.buyTarget, color:"#00ff88", desc:"+2:1 beneficio"},
      {label:"🛑 STOP LOSS", val:r.buyStop,   color:"#ff4466", desc:"Pérdida máxima"},
    ] : [
      {label:"📉 VENDE A",   val:r.sellEntry,  color:"#c8e8ff", desc:"Precio de entrada"},
      {label:"🎯 CIERRA A",  val:r.sellTarget, color:"#00ff88", desc:"+2:1 beneficio"},
      {label:"🛑 STOP LOSS", val:r.sellStop,   color:"#ff4466", desc:"Pérdida máxima"},
    ];
    const stopVal = dir==="COMPRA" ? r.buyStop : r.sellStop;
    targetsHTML = `
      <div class="targets-label">📱 PROGRAMA EN CRYPTO.COM</div>
      <div class="targets-grid">
        ${items.map(({label,val,color,desc})=>`
          <div class="target-box" style="border:1px solid ${color}18">
            <div class="target-box-label">${label}</div>
            <div class="target-box-price" style="color:${color}">${fmt(val)}</div>
            <div class="target-box-desc">${desc}</div>
          </div>
        `).join("")}
      </div>
      <div class="aziz-rule">
        <span style="color:#ffd700">Regla Aziz: </span>
        Riesgo máximo 1–2% de tu capital por operación.
        Stop loss en <span style="color:#ff4466">${fmt(stopVal)}</span> es obligatorio.
      </div>
    `;
  } else {
    targetsHTML = `
      <div class="wait-box">
        <div class="wait-icon">⏸</div>
        <div class="wait-text">
          No hay setup claro en este momento.<br/>
          Espera ~15–30 min y analiza de nuevo.
        </div>
      </div>
    `;
  }

  // Legend
  const legend = document.getElementById("legendTarget");
  if (r.buyTarget)  { legend.style.display="inline"; legend.style.color="#00ff88"; legend.textContent="— Objetivo"; }
  else if (r.sellTarget) { legend.style.display="inline"; legend.style.color="#ff4466"; legend.textContent="— Objetivo"; }
  else { legend.style.display="none"; }

  const card = document.getElementById("resultCard");
  card.style.display="block";
  card.style.background = sigBg;
  card.style.border = `1px solid ${sigColor}35`;
  card.innerHTML = `
    <div class="signal-header">
      <div>
        <div class="signal-sublabel">SEÑAL PRÓXIMA HORA</div>
        <div class="signal-name" style="color:${sigColor}">${dir}</div>
        <div class="signal-setup">${r.setup}</div>
      </div>
      <div style="text-align:right">
        <div class="confidence-label">CONFIANZA</div>
        <div class="confidence-val" style="color:${sigColor}">${r.confidence}%</div>
      </div>
    </div>
    <div class="conf-bar-bg">
      <div class="conf-bar" style="width:${r.confidence}%;background:${sigColor};box-shadow:0 0 8px ${sigColor}80"></div>
    </div>
    <div class="signal-detail">${r.detail}</div>
    ${targetsHTML}
    <div class="indicators-grid">
      <div class="indicator-box">
        <div class="indicator-label">VWAP</div>
        <div class="indicator-val">${fmt(r.vwap)}</div>
        <div class="indicator-status" style="color:${r.aboveVWAP?"#00ff88":"#ff4466"}">
          ${r.aboveVWAP?"Precio encima ↑":"Precio abajo ↓"}
        </div>
      </div>
      <div class="indicator-box">
        <div class="indicator-label">EMA 9</div>
        <div class="indicator-val">${fmt(r.ema9)}</div>
        <div class="indicator-status" style="color:${r.aboveEMA?"#00ff88":"#ff4466"}">
          ${r.aboveEMA?"Tendencia ↑":"Tendencia ↓"}
        </div>
      </div>
    </div>
  `;
}

// ── Render History ────────────────────────────────────────────────────────────
function renderHistory() {
  if (!history.length) return;
  document.getElementById("historyCard").style.display="block";
  document.getElementById("historyList").innerHTML = history.map((item,i)=>{
    const col = item.direction==="COMPRA"?"#00ff88":item.direction==="VENTA"?"#ff4466":"#666";
    const time = fmtTime(item.timestamp);
    const entry = fmt(item.buyEntry||item.sellEntry);
    const target = item.buyTarget ? "→ "+fmt(item.buyTarget) : item.sellTarget ? "→ "+fmt(item.sellTarget) : "Sin objetivo";
    return `
      <div class="history-row ${i%2===0?"even":""}">
        <span class="h-time">${time}</span>
        <span class="h-dir" style="color:${col}">${item.direction}</span>
        <span class="h-entry">${entry}</span>
        <span class="h-target" style="color:${col}">${target}</span>
        <span class="h-conf">${item.confidence}%</span>
      </div>
    `;
  }).join("");
}

// ── Init ──────────────────────────────────────────────────────────────────────
// Hide install banner if already installed as PWA
if (window.navigator.standalone) {
  document.getElementById("installBanner").style.display="none";
}

window.addEventListener("resize", ()=>{ if(candles.length) drawChart(candles, null); });

loadCandles();
</script>

</body>
</html>
