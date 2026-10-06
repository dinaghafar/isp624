# isp624

<!doctype html><html><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Deep Blue vs Kasparov</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Work+Sans:wght@400;600&family=JetBrains+Mono:wght@500&display=swap">
<style>
/* Layout: a single column framed like a tournament scoresheet; checkerboard strip as the only ornament */
:root{
  --bg:#f3f5f8; --ink:#15202e; --muted:#5a6779; --line:#cfd6e0;
  --accent:#0b5cad; --accent-ink:#fff; --sq:#dde4ee; --ok:#1d7a3a; --no:#b3261e; --card:#ffffff;
  --display:"Playfair Display",Georgia,serif; --body:"Work Sans",system-ui,sans-serif; --mono:"JetBrains Mono",ui-monospace,monospace;
}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0f141c;--ink:#e6ebf2;--muted:#9aa7b8;--line:#2a3442;--accent:#7fb2ff;--accent-ink:#0a1830;--sq:#1b2330;--ok:#7fd99a;--no:#ff8a80;--card:#151c27;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#0f141c;--ink:#e6ebf2;--muted:#9aa7b8;--line:#2a3442;--accent:#7fb2ff;--accent-ink:#0a1830;--sq:#1b2330;--ok:#7fd99a;--no:#ff8a80;--card:#151c27;color-scheme:dark}
body{background:var(--bg);color:var(--ink);font-family:var(--body);font-size:16px;line-height:1.55}
.wrap{max-width:820px;margin:0 auto;padding:24px 16px 64px;display:grid;gap:26px}
.board{height:16px;background:repeating-linear-gradient(90deg,var(--ink) 0 16px,transparent 16px 32px);opacity:.85}
h1,h2{font-family:var(--display);margin:0;line-height:1.05;text-wrap:balance}
h1{font-size:clamp(40px,9vw,78px);font-weight:900}
h2{font-size:clamp(26px,5vw,36px)}
p{margin:0;max-width:65ch}
.eyebrow{font-family:var(--mono);font-size:12px;letter-spacing:.14em;text-transform:uppercase;color:var(--muted)}
.hook{font-size:clamp(19px,3.2vw,24px);font-weight:600;max-width:34ch}
.sheet{background:var(--card);border:1px solid var(--line);padding:20px;display:grid;gap:14px;min-width:0}
button{font:600 15px var(--body);cursor:pointer;border-radius:4px;padding:10px 14px;border:1px solid var(--accent);background:transparent;color:var(--accent)}
button.on,button.primary{background:var(--accent);color:var(--accent-ink)}
button:focus-visible{outline:3px solid var(--accent);outline-offset:2px}
.row{display:flex;flex-wrap:wrap;gap:10px}
.result{font-family:var(--mono);font-size:14px;color:var(--muted)}
.tl{display:flex;flex-wrap:wrap;gap:8px}
.tl button{font-family:var(--mono);font-size:14px;padding:8px 12px}
.tl-card{border-left:3px solid var(--accent);padding:4px 0 4px 14px;min-height:100px;display:grid;gap:6px}
.tl-card b{font-family:var(--display);font-size:24px}
.score{display:grid;grid-template-columns:repeat(6,1fr);gap:6px;font-family:var(--mono);text-align:center}
.score div{background:var(--sq);padding:8px 2px;font-size:13px}
.score strong{display:block;font-size:18px}
.race{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.race > div{background:var(--sq);padding:14px;min-width:0}
.big{font-family:var(--mono);font-size:clamp(22px,6vw,36px);font-variant-numeric:tabular-nums;overflow-wrap:anywhere}
.q{display:grid;gap:10px;padding-block:12px;border-top:1px dashed var(--line)}
.q:first-child{border-top:0}
.q blockquote{margin:0;font-family:var(--display);font-size:21px}
.fb{font-size:14px;font-weight:600}.fb.ok{color:var(--ok)}.fb.no{color:var(--no)}
.slide{aspect-ratio:16/9;max-width:100%;background:#15202e;color:#e6ebf2;padding:clamp(14px,3vw,28px);display:grid;grid-template-rows:auto 1fr auto;gap:10px;overflow:hidden}
.slide h3{font-family:"Playfair Display",Georgia,serif;font-size:clamp(20px,4.4vw,38px);margin:0}
.slide .grid{display:grid;grid-template-columns:1fr 1fr;gap:clamp(6px,1.4vw,14px)}
.slide span{display:block;font-family:var(--mono);font-size:clamp(9px,1.4vw,12px);letter-spacing:.12em;text-transform:uppercase;color:#7fb2ff}
.slide p{font-size:clamp(11px,1.9vw,16px);line-height:1.3}
.slide small{font-size:clamp(8px,1.2vw,11px);color:#9aa7b8}
ol.src{margin:0;padding-left:20px;font-size:14px;display:grid;gap:4px}
ol.src a{color:var(--accent);overflow-wrap:anywhere}
.note{font-size:13px;color:var(--muted)}
</style>

<div class="wrap">
<div class="board" aria-hidden="true"></div>
<header style="display:grid;gap:12px">
  <span class="eyebrow">AI History · Track A · New York, May 1997</span>
  <h1>Deep Blue vs Kasparov</h1>
  <p class="hook">In 1997, a computer beat the world chess champion in a full match for the first time.</p>
</header>

<section class="sheet">
  <span class="eyebrow">Step 1 · Predict</span>
  <h2>1997 rematch. Who wins?</h2>
  <div class="row"><button type="button" id="pH">Kasparov (human)</button><button type="button" id="pM">Deep Blue (machine)</button></div>
  <p class="result" id="pOut">Raise your hand, then tap.</p>
  <div class="score" id="score" hidden></div>
</section>

<section class="sheet">
  <span class="eyebrow">Step 2 · Explore the timeline</span>
  <h2>Tap a year</h2>
  <div class="tl" id="tl" role="group" aria-label="Timeline"></div>
  <div class="tl-card" id="tlCard" aria-live="polite"></div>
</section>

<section class="sheet">
  <span class="eyebrow">Step 3 · Speed challenge</span>
  <h2>Can you think as fast as Deep Blue?</h2>
  <p>Tap the button as many times as you can in 5 seconds. Each tap = 1 chess position.</p>
  <div class="row"><button type="button" class="primary" id="go">Start</button><button type="button" id="tap" disabled>Tap!</button></div>
  <div class="race">
    <div><span class="eyebrow">You</span><div class="big" id="you">0</div></div>
    <div><span class="eyebrow">Deep Blue (≈200 million/sec)</span><div class="big" id="db">0</div></div>
  </div>
  <p class="result" id="raceOut"></p>
</section>

<section class="sheet">
  <span class="eyebrow">Step 4 · Quiz</span>
  <h2>Fact or myth?</h2>
  <div id="quiz"></div>
  <p class="result" id="qs">Score: 0 / 3</p>
</section>

<section style="display:grid;gap:10px">
  <span class="eyebrow">1-slide summary</span>
  <div class="slide" role="img" aria-label="Summary slide">
    <h3>Deep Blue vs Kasparov (1997)</h3>
    <div class="grid">
      <div><span>Hook</span><p>A machine beat the world chess champion in a full match.</p></div>
      <div><span>Context</span><p>1996: Kasparov beat IBM's Deep Blue 4–2. IBM upgraded the machine.</p></div>
      <div><span>Turning point</span><p>May 1997: Deep Blue won 3½–2½. Kasparov suspected human help. IBM retired the machine.</p></div>
      <div><span>Why it matters today</span><p>Brute-force search beat human skill. Today's AI (AlphaZero, ChatGPT) learns from data instead.</p></div>
    </div>
    <small>Sources: IBM History; Britannica; Wikipedia "Deep Blue versus Garry Kasparov".</small>
  </div>
</section>

<section class="sheet">
  <span class="eyebrow">Sources (key facts checked in 2+ sources)</span>
  <ol class="src">
    <li>IBM History, "Deep Blue" — <a href="https://www.ibm.com/history/deep-blue">ibm.com/history/deep-blue</a></li>
    <li>Britannica, "Deep Blue" — <a href="https://www.britannica.com/topic/Deep-Blue">britannica.com</a></li>
    <li>Wikipedia, "Deep Blue versus Garry Kasparov" — <a href="https://en.wikipedia.org/wiki/Deep_Blue_versus_Garry_Kasparov">en.wikipedia.org</a></li>
    <li>The Conversation, "Twenty years on from Deep Blue vs Kasparov" — <a href="https://theconversation.com/twenty-years-on-from-deep-blue-vs-kasparov-how-a-chess-match-started-the-big-data-revolution-76882">theconversation.com</a></li>
  </ol>
  <p class="note">Built with help from an AI tool (Claude). No AI-generated images are used.</p>
</section>
<div class="board" aria-hidden="true"></div>
</div>

<script>
// predict
const res=['½','1','½','½','½','1'];
const games=[['G1','Kasparov'],['G2','Deep Blue'],['G3','Draw'],['G4','Draw'],['G5','Draw'],['G6','Deep Blue']];
function reveal(guess){
  const s=document.getElementById('score');s.hidden=false;
  s.innerHTML=games.map(g=>'<div>'+g[0]+'<strong>'+(g[1]==='Draw'?'=':g[1]==='Kasparov'?'K':'DB')+'</strong></div>').join('');
  document.getElementById('pOut').textContent=(guess==='M'?'Correct! ':'Surprise! ')+'Deep Blue won 3½–2½. K = Kasparov win, DB = Deep Blue win, = draw.';
}
document.getElementById('pH').onclick=()=>reveal('H');document.getElementById('pM').onclick=()=>reveal('M');

// timeline
const ev=[
 ['1985','The start','A project that becomes Deep Blue begins at Carnegie Mellon University. IBM later hires the team.'],
 ['Feb 1996','Round 1, Philadelphia','Deep Blue wins Game 1, the first game a computer wins against a world champion in normal tournament time. Kasparov wins the match 4–2.'],
 ['May 1997','Round 2, New York','An upgraded Deep Blue searches about 200 million positions per second. It wins the match 3½–2½.'],
 ['Game 6','19 moves','Kasparov loses the final game in only 19 moves.'],
 ['After','"Human help?"','Kasparov suspects people helped the machine during play. He asks for a rematch. IBM says no and retires Deep Blue.'],
 ['Today','From search to learning','Deep Blue used brute-force search and rules from experts. Modern AI, like AlphaZero (2017), learns by itself.']
];
const tl=document.getElementById('tl'),card=document.getElementById('tlCard');
function show(i){[...tl.children].forEach((b,j)=>b.classList.toggle('on',j===i));card.innerHTML='<b>'+ev[i][1]+'</b><p>'+ev[i][2]+'</p>'}
ev.forEach((e,i)=>{const b=document.createElement('button');b.type='button';b.textContent=e[0];b.onclick=()=>show(i);tl.appendChild(b)});show(2);

// race
let n=0,running=false;const you=document.getElementById('you'),db=document.getElementById('db'),tap=document.getElementById('tap'),out=document.getElementById('raceOut');
document.getElementById('go').onclick=()=>{
  if(running)return;running=true;n=0;you.textContent=0;tap.disabled=false;out.textContent='GO!';const t0=performance.now();
  (function tick(){const t=Math.min((performance.now()-t0)/1000,5);db.textContent=Math.floor(t*200e6).toLocaleString();
    if(t<5)requestAnimationFrame(tick);else{running=false;tap.disabled=true;out.textContent='You: '+n+'. Deep Blue: 1,000,000,000. It is '+(n?Math.round(1e9/n).toLocaleString():'∞')+' times faster than you.'}})();
};
tap.onclick=()=>{if(running){n++;you.textContent=n}};

// quiz
const qs=[
 ['Deep Blue won its first match against Kasparov in 1996.',false,'Myth. Kasparov won 1996 (4–2). Deep Blue won the 1997 rematch.'],
 ['Deep Blue learned chess by itself, like modern AI.',false,'Myth. It used fast search plus rules from human chess experts.'],
 ['IBM did not give Kasparov a second rematch.',true,'Fact. IBM retired Deep Blue after 1997.']
];
let sc=0;const qz=document.getElementById('quiz');
qs.forEach(q=>{const d=document.createElement('div');d.className='q';
 d.innerHTML='<blockquote>"'+q[0]+'"</blockquote><div class="row"><button type="button" data-a="1">Fact</button><button type="button" data-a="0">Myth</button></div><p class="fb" aria-live="polite"></p>';
 const fb=d.querySelector('.fb');
 d.querySelectorAll('button').forEach(b=>b.onclick=()=>{if(d.dataset.done)return;d.dataset.done=1;const ok=(b.dataset.a==='1')===q[1];if(ok)sc++;
  fb.className='fb '+(ok?'ok':'no');fb.textContent=(ok?'Correct. ':'Not quite. ')+q[2];b.classList.add('primary');document.getElementById('qs').textContent='Score: '+sc+' / 3'});
 qz.appendChild(d)});
</script>

</body></html>
