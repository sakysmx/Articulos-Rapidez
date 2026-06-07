<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>El o La</title>
<style>
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #0d0d14;
  color: #e8e8f0;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 16px;
  touch-action: manipulation;
  -webkit-user-select: none;
  user-select: none;
}

.screen { display:none; width:100%; max-width:440px; }
.screen.active { display:flex; flex-direction:column; align-items:center; }

/* ── MENU ── */
.logo { font-size:72px; font-weight:900; text-align:center; line-height:1; margin-bottom:6px; }
.lg { color:#00e5a0; }
.lr { color:#ff3860; }
.logo-sub { font-size:11px; letter-spacing:5px; text-transform:uppercase; color:#44445a; margin-bottom:36px; }

.lbl { font-size:10px; letter-spacing:5px; text-transform:uppercase; color:#44445a; margin-bottom:12px; }

.grid {
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
  width:100%;
  margin-bottom:16px;
}
.card {
  background:#13131e;
  border:2px solid #1e1e30;
  border-radius:14px;
  padding:18px 14px;
  cursor:pointer;
  touch-action:manipulation;
  -webkit-appearance:none;
}
.card.sel { border-color:#00e5a0; background:rgba(0,229,160,0.07); }
.badge { font-size:26px; font-weight:900; display:block; margin-bottom:3px; }
.c1 .badge { color:#00e5a0; }
.c2 .badge { color:#a8e063; }
.c3 .badge { color:#ffd166; }
.c4 .badge { color:#ff7849; }
.c5 .badge { color:#ff3860; }
.cname { font-size:12px; font-weight:700; text-transform:uppercase; letter-spacing:1px; margin-bottom:2px; }
.ctime { font-size:11px; color:#44445a; }

.btn-go {
  width:100%; padding:20px;
  background:#00e5a0; color:#000;
  font-size:15px; font-weight:800; letter-spacing:2px; text-transform:uppercase;
  border:none; border-radius:14px; cursor:pointer;
  -webkit-appearance:none; touch-action:manipulation;
}
.btn-go:disabled { opacity:0.3; pointer-events:none; }

/* ── GAME ── */
.top-bar {
  display:flex;
  align-items:center;
  width:100%;
  gap:8px;
  margin-bottom:12px;
}
.back-btn {
  height:50px; min-width:50px;
  background:#13131e; border:2px solid #1e1e30; border-radius:12px;
  color:#e8e8f0; font-size:22px; cursor:pointer;
  display:flex; align-items:center; justify-content:center;
  flex-shrink:0;
  -webkit-appearance:none; touch-action:manipulation;
}
.stats { display:flex; gap:8px; flex:1; justify-content:flex-end; }
.stat {
  background:#13131e; border:1px solid #1e1e30; border-radius:10px;
  padding:8px 14px; text-align:center; min-width:62px;
}
.sv { font-size:26px; font-weight:900; line-height:1; }
.sl { font-size:9px; letter-spacing:2px; text-transform:uppercase; color:#44445a; margin-top:2px; }
.sv-ok  { color:#00e5a0; }
.sv-err { color:#ff3860; }

.lvl-tag {
  font-size:9px; letter-spacing:3px; text-transform:uppercase; color:#44445a;
  border:1px solid #1e1e30; border-radius:20px; padding:5px 10px;
  white-space:nowrap;
}

.bar-wrap {
  width:100%; height:6px; background:#1e1e30; border-radius:3px;
  overflow:hidden; margin-bottom:14px;
}
.bar-fill { height:100%; width:100%; background:#00e5a0; border-radius:3px; }

.card-word {
  width:100%; background:#13131e; border:2px solid #1e1e30; border-radius:20px;
  padding:32px 20px; text-align:center; margin-bottom:14px;
  min-height:120px; display:flex; flex-direction:column;
  align-items:center; justify-content:center;
}
.card-word.ok  { border-color:#00e5a0; background:rgba(0,229,160,0.07); }
.card-word.err { border-color:#ff3860; background:rgba(255,56,96,0.07); }

.word { font-size:44px; font-weight:300; margin-bottom:8px; line-height:1.1; }
.word .art { font-weight:900; color:#ffd166; }
.hint { font-size:11px; color:#44445a; letter-spacing:2px; text-transform:uppercase; }

.ans-row { display:grid; grid-template-columns:1fr 1fr; gap:12px; width:100%; }
.ans {
  height:88px; border:2px solid #1e1e30; border-radius:16px;
  background:#13131e; font-size:16px; font-weight:800;
  letter-spacing:1px; text-transform:uppercase; cursor:pointer;
  display:flex; align-items:center; justify-content:center;
  -webkit-appearance:none; touch-action:manipulation;
}
.ans-ok  { color:#00e5a0; }
.ans-err { color:#ff3860; }
.ans.hit-ok  { border-color:#00e5a0; background:rgba(0,229,160,0.15); }
.ans.hit-err { border-color:#ff3860; background:rgba(255,56,96,0.15); }
.ans.off { opacity:0.3; pointer-events:none; }

.qnum { font-size:10px; letter-spacing:3px; text-transform:uppercase; color:#44445a; margin-top:12px; }

/* ── CHIP ── */
.chip {
  position:fixed; top:50%; left:50%;
  transform:translate(-50%,-50%) scale(0.8);
  padding:12px 32px; border-radius:14px;
  font-size:38px; font-weight:900; letter-spacing:3px;
  opacity:0; pointer-events:none;
  transition:opacity .12s, transform .12s;
  z-index:999; white-space:nowrap;
}
.chip.ok  { background:#00e5a0; color:#000; }
.chip.err { background:#ff3860; color:#fff; }
.chip.show { opacity:1; transform:translate(-50%,-50%) scale(1); }

/* ── RESULTS ── */
#s-res { text-align:center; }
.rtitle { font-size:52px; font-weight:900; letter-spacing:3px; margin-bottom:4px; }
.rsub { font-size:11px; letter-spacing:4px; text-transform:uppercase; color:#44445a; margin-bottom:28px; }
.rgrid { display:grid; grid-template-columns:1fr 1fr 1fr; gap:10px; width:100%; margin-bottom:18px; }
.rtile { background:#13131e; border:1px solid #1e1e30; border-radius:14px; padding:16px 8px; }
.rv { font-size:38px; font-weight:900; line-height:1; margin-bottom:4px; }
.rl { font-size:9px; letter-spacing:3px; text-transform:uppercase; color:#44445a; }
.rv-g { color:#00e5a0; }
.rv-r { color:#ff3860; }
.rv-y { color:#ffd166; }
.rstreak { font-size:12px; color:#44445a; margin-bottom:24px; }
.rstreak b { color:#e8e8f0; }
.rbtns { display:flex; gap:10px; width:100%; }
.rbtn-back {
  flex:1; padding:18px; background:#13131e; border:1px solid #1e1e30;
  color:#e8e8f0; font-size:12px; font-weight:700; letter-spacing:2px;
  text-transform:uppercase; border-radius:12px; cursor:pointer;
  -webkit-appearance:none; touch-action:manipulation;
}
.rbtn-again {
  flex:2; padding:18px; background:#00e5a0; color:#000;
  font-size:14px; font-weight:800; letter-spacing:2px;
  text-transform:uppercase; border:none; border-radius:12px; cursor:pointer;
  -webkit-appearance:none; touch-action:manipulation;
}
</style>
</head>
<body>

<!-- MENU -->
<div id="s-menu" class="screen active">
  <div class="logo"><span class="lg">El</span> <span class="lr">La</span></div>
  <div class="logo-sub">articulos en espanol</div>
  <div class="lbl">Elige tu nivel</div>
  <div class="grid">
    <div class="card c1" data-lv="1"><span class="badge">N1</span><div class="cname">Nivel 1</div><div class="ctime">1.5 seg</div></div>
    <div class="card c2" data-lv="2"><span class="badge">N2</span><div class="cname">Nivel 2</div><div class="ctime">1.2 seg</div></div>
    <div class="card c3" data-lv="3"><span class="badge">N3</span><div class="cname">Nivel 3</div><div class="ctime">1.0 seg</div></div>
    <div class="card c4" data-lv="4"><span class="badge">N4</span><div class="cname">Nivel 4</div><div class="ctime">0.7 seg</div></div>
    <div class="card c5" data-lv="5"><span class="badge">N5</span><div class="cname">Nivel 5</div><div class="ctime">0.5 seg</div></div>
  </div>
  <button class="btn-go" id="btn-go" disabled>Comenzar</button>
</div>

<!-- GAME -->
<div id="s-game" class="screen">
  <div class="top-bar">
    <button class="back-btn" id="btn-back">&#8592;</button>
    <div class="stats">
      <div class="stat"><div class="sv sv-ok" id="g-ok">0</div><div class="sl">OK</div></div>
      <div class="stat"><div class="sv sv-err" id="g-err">0</div><div class="sl">ERR</div></div>
    </div>
    <div class="lvl-tag" id="g-lvl">N1</div>
  </div>

  <div class="bar-wrap"><div class="bar-fill" id="g-bar"></div></div>

  <div class="card-word" id="g-card">
    <div class="word" id="g-word"></div>
    <div class="hint" id="g-hint"></div>
  </div>

  <div class="ans-row">
    <button class="ans ans-ok"  id="b-si">Correcto</button>
    <button class="ans ans-err" id="b-no">Incorrecto</button>
  </div>

  <div class="qnum" id="g-qnum">1 / 30</div>
</div>

<!-- RESULTS -->
<div id="s-res" class="screen">
  <div class="rtitle" id="r-title">Bien!</div>
  <div class="rsub"   id="r-sub">—</div>
  <div class="rgrid">
    <div class="rtile"><div class="rv rv-g" id="r-ok">0</div><div class="rl">Correctas</div></div>
    <div class="rtile"><div class="rv rv-r" id="r-err">0</div><div class="rl">Errores</div></div>
    <div class="rtile"><div class="rv rv-y" id="r-pct">0%</div><div class="rl">Precision</div></div>
  </div>
  <div class="rstreak">Mejor racha: <b id="r-str">0</b> seguidas</div>
  <div class="rbtns">
    <button class="rbtn-back"  id="r-menu">Menu</button>
    <button class="rbtn-again" id="r-again">Otra vez</button>
  </div>
</div>

<div class="chip" id="chip"></div>

<script>
var WORDS = [
  // masculino normal
  {w:'zapato',  ok:true},  {w:'camino',  ok:true},  {w:'puente',  ok:true},
  {w:'cielo',   ok:true},  {w:'cuadro',  ok:true},  {w:'vuelo',   ok:true},
  {w:'museo',   ok:true},  {w:'viaje',   ok:true},  {w:'billete', ok:true},
  {w:'bolsillo',ok:true},  {w:'tejado',  ok:true},  {w:'mercado', ok:true},
  // masculino trampa -a
  {w:'programa', ok:true},  {w:'telegrama',ok:true}, {w:'enigma',  ok:true},
  {w:'dilema',  ok:true},  {w:'esquema', ok:true},  {w:'fantasma',ok:true},
  {w:'aroma',   ok:true},  {w:'diploma', ok:true},  {w:'panorama',ok:true},
  // femenino normal
  {w:'sombra',  ok:false}, {w:'playa',   ok:false}, {w:'calle',   ok:false},
  {w:'cumbre',  ok:false}, {w:'llave',   ok:false}, {w:'torre',   ok:false},
  {w:'mente',   ok:false}, {w:'fuente',  ok:false}, {w:'carne',   ok:false},
  {w:'sangre',  ok:false}, {w:'suerte',  ok:false}, {w:'nube',    ok:false},
  {w:'fiebre',  ok:false}, {w:'nieve',   ok:false}, {w:'nave',    ok:false},
  // femenino trampa -o  (abreviaturas y excepciones)
  {w:'tribu',   ok:false}, {w:'foto',    ok:false}, {w:'moto',    ok:false},
  {w:'mano',    ok:false}
];

var TIMES = {'1':1500,'2':1200,'3':1000,'4':700,'5':500};
var NAMES = {'1':'N1 1.5s','2':'N2 1.2s','3':'N3 1s','4':'N4 0.7s','5':'N5 0.5s'};

// Build deck: each word appears as "El X" (isCorrect = word.ok) and "La X" (isCorrect = !word.ok)
function buildDeck() {
  var deck = [];
  for (var i = 0; i < WORDS.length; i++) {
    var w = WORDS[i];
    var art_m = 'El';
    var art_f = 'La';
    // Card showing "El word" — correct only if masculine
    deck.push({
      html: '<span class="art">' + art_m + '</span> ' + w.w,
      correct: w.ok,
      hint: w.w + (w.ok ? ' = masculino' : ' = femenino')
    });
    // Card showing "La word" — correct only if feminine
    deck.push({
      html: '<span class="art">' + art_f + '</span> ' + w.w,
      correct: !w.ok,
      hint: w.w + (w.ok ? ' = masculino' : ' = femenino')
    });
  }
  return deck;
}

function shuffle(a) {
  var b = a.slice(), i, j, t;
  for (i = b.length-1; i>0; i--) {
    j = Math.floor(Math.random()*(i+1));
    t=b[i]; b[i]=b[j]; b[j]=t;
  }
  return b;
}

var level=null, queue=[], idx=0, score=0, errs=0, streak=0, best=0, locked=false, qnum=0;
var tOut=null, aFrm=null, tStart=0, tMs=0;

var sMenu  = document.getElementById('s-menu');
var sGame  = document.getElementById('s-game');
var sRes   = document.getElementById('s-res');
var gOk    = document.getElementById('g-ok');
var gErr   = document.getElementById('g-err');
var gLvl   = document.getElementById('g-lvl');
var gBar   = document.getElementById('g-bar');
var gCard  = document.getElementById('g-card');
var gWord  = document.getElementById('g-word');
var gHint  = document.getElementById('g-hint');
var gQnum  = document.getElementById('g-qnum');
var bSi    = document.getElementById('b-si');
var bNo    = document.getElementById('b-no');
var chip   = document.getElementById('chip');

function show(el) {
  sMenu.classList.remove('active');
  sGame.classList.remove('active');
  sRes.classList.remove('active');
  el.classList.add('active');
}

// Mode card selection
var cards = document.querySelectorAll('.card');
for (var i=0; i<cards.length; i++) {
  (function(c){
    c.addEventListener('touchstart', function(e){
      e.preventDefault();
      selectCard(c);
    }, {passive:false});
    c.addEventListener('click', function(){ selectCard(c); });
  })(cards[i]);
}
function selectCard(c) {
  for (var k=0; k<cards.length; k++) cards[k].classList.remove('sel');
  c.classList.add('sel');
  level = c.getAttribute('data-lv');
  document.getElementById('btn-go').disabled = false;
}

document.getElementById('btn-go').addEventListener('click', startGame);
document.getElementById('btn-back').addEventListener('click', function(){ stopGame(); show(sMenu); });
document.getElementById('r-menu').addEventListener('click', function(){ show(sMenu); });
document.getElementById('r-again').addEventListener('click', startGame);

function startGame() {
  if (!level) return;
  stopGame();
  queue = shuffle(buildDeck());
  idx=0; score=0; errs=0; streak=0; best=0; qnum=0; locked=false;
  gOk.textContent='0'; gErr.textContent='0';
  gLvl.textContent = NAMES[level];
  show(sGame);
  next();
}

function stopGame() {
  if (tOut)  { clearTimeout(tOut); tOut=null; }
  if (aFrm)  { cancelAnimationFrame(aFrm); aFrm=null; }
  locked = true;
}

function next() {
  locked = false;
  if (tOut)  { clearTimeout(tOut); tOut=null; }
  if (aFrm)  { cancelAnimationFrame(aFrm); aFrm=null; }

  if (idx >= queue.length) { queue = shuffle(buildDeck()); idx=0; }

  var q = queue[idx]; qnum++;
  gWord.innerHTML = q.html;
  gHint.textContent = q.hint;
  gQnum.textContent = qnum + ' / 30';

  gCard.classList.remove('ok','err');
  bSi.classList.remove('hit-ok','hit-err','off');
  bNo.classList.remove('hit-ok','hit-err','off');

  startTimer();
}

function startTimer() {
  tMs = TIMES[level]; tStart = performance.now();
  gBar.style.transition = 'none';
  gBar.style.width = '100%';
  gBar.style.background = '#00e5a0';
  requestAnimationFrame(function(){
    requestAnimationFrame(function(){
      gBar.style.transition = 'width '+tMs+'ms linear';
      gBar.style.width = '0%';
    });
  });
  function tick() {
    var f = (performance.now()-tStart)/tMs;
    if      (f >= 0.75) gBar.style.background = '#ff3860';
    else if (f >= 0.5)  gBar.style.background = '#ffd166';
    if (f < 1) aFrm = requestAnimationFrame(tick);
  }
  aFrm = requestAnimationFrame(tick);
  tOut = setTimeout(function(){ if(!locked) onTimeout(); }, tMs);
}

function onTimeout() {
  locked = true; errs++; streak = 0;
  gErr.textContent = errs;
  gCard.classList.add('err');
  showChip(false, 'Tiempo!');
  setTimeout(advance, 600);
}

function answer(yes) {
  if (locked) return;
  locked = true;
  if (tOut)  { clearTimeout(tOut); tOut=null; }
  if (aFrm)  { cancelAnimationFrame(aFrm); aFrm=null; }

  var q = queue[idx];
  var hit = yes ? bSi : bNo;

  if (yes === q.correct) {
    score++; streak++; if (streak>best) best=streak;
    gOk.textContent = score;
    gCard.classList.add('ok');
    hit.classList.add('hit-ok');
    showChip(true, 'Correcto!');
  } else {
    errs++; streak = 0;
    gErr.textContent = errs;
    gCard.classList.add('err');
    hit.classList.add('hit-err');
    showChip(false, 'Error!');
  }

  // disable answer buttons but NOT the back button
  bSi.classList.add('off');
  bNo.classList.add('off');

  setTimeout(advance, 480);
}

function advance() {
  idx++;
  if (qnum >= 30) showResults();
  else next();
}

function showChip(ok, txt) {
  chip.textContent = txt;
  chip.className = 'chip ' + (ok ? 'ok' : 'err') + ' show';
  setTimeout(function(){ chip.className = 'chip ' + (ok ? 'ok' : 'err'); }, 400);
}

function showResults() {
  stopGame();
  var total = score+errs, pct = total ? Math.round(score/total*100) : 0;
  var t = pct>=90 ? 'Perfecto!' : pct>=70 ? 'Muy bien!' : pct>=50 ? 'Bien!' : 'Sigue!';
  document.getElementById('r-title').textContent = t;
  document.getElementById('r-sub').textContent   = NAMES[level] + ' — ' + total + ' preguntas';
  document.getElementById('r-ok').textContent    = score;
  document.getElementById('r-err').textContent   = errs;
  document.getElementById('r-pct').textContent   = pct + '%';
  document.getElementById('r-str').textContent   = best;
  show(sRes);
}

// Answer buttons — touchstart for instant response, click fallback for desktop
function bindAns(btn, val) {
  var touched = false;
  btn.addEventListener('touchstart', function(e){
    e.preventDefault();
    touched = true;
    answer(val);
  }, {passive:false});
  btn.addEventListener('click', function(){
    if (touched) { touched=false; return; }
    answer(val);
  });
}
bindAns(bSi, true);
bindAns(bNo, false);

// Keyboard
document.addEventListener('keydown', function(e){
  if (!sGame.classList.contains('active')) return;
  if (e.key==='ArrowLeft'  || e.key==='1') answer(true);
  if (e.key==='ArrowRight' || e.key==='2') answer(false);
});
</script>
</body>
</html>
