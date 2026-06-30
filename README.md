# year4-learning-tools
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Old Man — Character Detective</title>
<style>
  :root{
    --paper:#f6efe1;        /* manila folder */
    --paper-2:#fffaf0;      /* card */
    --ink:#2b2a38;          /* main text */
    --ink-soft:#6c6a7d;     /* home-language scaffolding */
    --navy:#27405a;         /* detective ink */
    --teal:#1f7a6e;
    --orange:#e8730c;       /* TARGET English vocab */
    --orange-soft:#fff1e2;
    --green:#2e9b57;
    --green-soft:#e4f6e9;
    --red:#d65745;
    --gold:#f0b429;
    --line:#d9cdb6;
    --shadow:0 6px 18px rgba(43,42,56,.12);
  }
  *{box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
  html,body{margin:0;padding:0;}
  body{
    font-family:"Trebuchet MS","Segoe UI Rounded",system-ui,-apple-system,sans-serif;
    color:var(--ink);
    background:
      radial-gradient(circle at 12% 8%, #fbf6ea 0%, transparent 40%),
      repeating-linear-gradient(0deg,#f2eada,#f2eada 2px,#efe6d3 2px,#efe6d3 26px),
      var(--paper);
    line-height:1.45;
    padding:14px;
    min-height:100vh;
  }
  .wrap{max-width:880px;margin:0 auto;}

  /* ---------- Header ---------- */
  header{
    background:var(--navy);
    color:#fff;
    border-radius:18px;
    padding:18px 20px;
    box-shadow:var(--shadow);
    position:relative;
    overflow:hidden;
  }
  header h1{
    margin:0;font-size:1.5rem;letter-spacing:.3px;
    display:flex;align-items:center;gap:10px;flex-wrap:wrap;
  }
  header .sub{margin:4px 0 0;opacity:.85;font-size:.95rem;}
  .stamp{
    position:absolute;top:10px;right:-26px;rotate:14deg;
    border:3px solid #e6b3a6;color:#f4c3b6;border-radius:8px;
    padding:4px 30px;font-weight:bold;letter-spacing:2px;font-size:.8rem;opacity:.85;
  }
  .stars{display:flex;gap:6px;margin-top:10px;}
  .star{font-size:1.5rem;filter:grayscale(1) opacity(.45);transition:transform .4s, filter .4s;}
  .star.on{filter:none;transform:scale(1.15);}

  /* sound notice */
  .sound-note{
    margin:10px 0 0;font-size:.82rem;background:#fdf2e0;border:1px dashed var(--orange);
    color:#7a4a14;border-radius:12px;padding:8px 12px;
  }
  .sound-note a{color:var(--orange);font-weight:bold;}

  /* ---------- Tabs ---------- */
  nav.tabs{display:flex;gap:8px;margin:16px 0;flex-wrap:wrap;}
  .tab{
    flex:1 1 auto;min-width:120px;cursor:pointer;border:none;
    background:var(--paper-2);color:var(--navy);
    border:2px solid var(--line);border-radius:14px;
    padding:12px 8px;font-size:.98rem;font-weight:bold;font-family:inherit;
    transition:.15s;display:flex;flex-direction:column;align-items:center;gap:2px;
  }
  .tab .ic{font-size:1.4rem;}
  .tab.active{background:var(--orange);color:#fff;border-color:var(--orange);box-shadow:var(--shadow);}
  .tab .done{font-size:.7rem;color:var(--green);font-weight:bold;}
  .tab.active .done{color:#fff;}

  /* ---------- Panels ---------- */
  .panel{display:none;animation:fade .35s ease;}
  .panel.active{display:block;}
  @keyframes fade{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:none;}}

  .card{
    background:var(--paper-2);border:2px solid var(--line);border-radius:16px;
    padding:18px;box-shadow:var(--shadow);margin-bottom:14px;
  }
  .card h2{margin:0 0 4px;color:var(--navy);font-size:1.2rem;}
  .lead{color:var(--ink-soft);margin:0 0 14px;font-size:.95rem;}

  /* target English vocab styling */
  .vocab{color:var(--orange);font-weight:bold;}
  .home{display:block;color:var(--ink-soft);font-size:.82rem;font-weight:normal;margin-top:2px;}

  /* play (speaker) button */
  .say{
    border:none;background:var(--orange-soft);color:var(--orange);
    border:1.5px solid #f3c79a;border-radius:50%;width:38px;height:38px;min-width:38px;
    font-size:1.05rem;cursor:pointer;display:inline-flex;align-items:center;justify-content:center;
    transition:.12s;
  }
  .say:active{transform:scale(.88);}
  .say.big{width:44px;height:44px;font-size:1.2rem;}

  /* ---------- Mission / Story ---------- */
  .evidence{display:flex;flex-direction:column;gap:10px;}
  .evi{
    display:flex;align-items:center;gap:12px;background:#fffdf7;
    border:1.5px solid var(--line);border-left:6px solid var(--gold);
    border-radius:12px;padding:12px 14px;
  }
  .evi .tag{font-size:1.3rem;}
  .evi p{margin:0;font-size:1.02rem;}

  /* ---------- Match game ---------- */
  .match-grid{display:flex;gap:14px;}
  .col{flex:1;display:flex;flex-direction:column;gap:10px;}
  .col h3{margin:0 0 2px;font-size:.85rem;text-transform:uppercase;letter-spacing:1px;color:var(--ink-soft);}
  .wcard,.ccard{
    border:2px solid var(--line);border-radius:12px;background:#fffdf7;
    padding:12px;cursor:pointer;display:flex;gap:10px;align-items:flex-start;
    transition:.12s;text-align:left;font-family:inherit;color:var(--ink);
  }
  .wcard{align-items:center;}
  .wcard .txt{font-size:1.1rem;font-weight:bold;}
  .ccard .txt{font-size:.98rem;}
  .wcard.sel,.ccard.sel{border-color:var(--orange);background:var(--orange-soft);box-shadow:var(--shadow);}
  .matched{border-color:var(--green)!important;background:var(--green-soft)!important;cursor:default;}
  .matched .pairnum{margin-left:auto;font-weight:bold;color:var(--green);}
  .shake{animation:shake .4s;}
  @keyframes shake{0%,100%{transform:translateX(0);}25%{transform:translateX(-6px);}75%{transform:translateX(6px);}}
  .pairnum{font-weight:bold;color:var(--ink-soft);}

  /* ---------- Detective MCQ ---------- */
  .clue-box{
    background:var(--navy);color:#fff;border-radius:14px;padding:14px 16px;
    display:flex;gap:12px;align-items:center;margin-bottom:14px;
  }
  .clue-box .q{font-size:1.05rem;margin:0;}
  .opts{display:flex;flex-wrap:wrap;gap:10px;}
  .opt{
    flex:1 1 30%;min-width:130px;border:2px solid var(--line);background:#fffdf7;
    border-radius:14px;padding:12px;cursor:pointer;font-family:inherit;text-align:center;
    transition:.12s;
  }
  .opt .txt{font-size:1.1rem;font-weight:bold;color:var(--orange);}
  .opt:hover{border-color:var(--orange);}
  .opt.correct{border-color:var(--green);background:var(--green-soft);}
  .opt.wrong{border-color:var(--red);background:#fbe7e3;}
  .opt:disabled{cursor:default;}
  .feedback{margin-top:14px;border-radius:12px;padding:12px 14px;font-size:.98rem;display:none;}
  .feedback.show{display:block;}
  .feedback.good{background:var(--green-soft);border:1.5px solid var(--green);color:#1d6b3c;}
  .feedback.try{background:#fff3cf;border:1.5px solid var(--gold);color:#7a5a00;}
  .navrow{display:flex;justify-content:flex-end;margin-top:14px;}
  .btn{
    border:none;background:var(--orange);color:#fff;border-radius:12px;
    padding:11px 20px;font-size:1rem;font-weight:bold;cursor:pointer;font-family:inherit;
    box-shadow:var(--shadow);transition:.12s;
  }
  .btn:active{transform:scale(.96);}
  .btn.ghost{background:#fff;color:var(--navy);border:2px solid var(--line);box-shadow:none;}
  .btn:disabled{opacity:.4;cursor:default;}

  /* ---------- Prove it ---------- */
  .chip-row{display:flex;flex-wrap:wrap;gap:8px;margin:8px 0 4px;}
  .chip{
    border:2px solid var(--line);background:#fffdf7;border-radius:20px;
    padding:8px 14px;cursor:pointer;font-family:inherit;font-size:1rem;font-weight:bold;color:var(--orange);
    transition:.12s;
  }
  .chip.sel{background:var(--orange);color:#fff;border-color:var(--orange);}
  .frame{font-size:1.15rem;line-height:2.1;margin:14px 0;}
  .blank{
    display:inline-block;min-width:120px;border-bottom:3px dotted var(--orange);
    color:var(--orange);font-weight:bold;text-align:center;padding:0 6px;
  }
  textarea{
    width:100%;border:2px solid var(--line);border-radius:12px;padding:12px;
    font-family:inherit;font-size:1.05rem;color:var(--ink);resize:vertical;min-height:70px;background:#fffdf7;
  }
  textarea:focus{outline:none;border-color:var(--orange);}
  .clue-help{font-size:.85rem;color:var(--ink-soft);margin:6px 0 0;}
  .report{
    margin-top:16px;background:#fffdf7;border:2px dashed var(--navy);border-radius:14px;padding:16px;display:none;
  }
  .report.show{display:block;animation:fade .4s;}
  .report h3{margin:0 0 8px;color:var(--navy);}
  .report .rline{font-size:1.1rem;margin:6px 0;}
  .challenge{background:#fdf2e0;border:1px dashed var(--orange);border-radius:12px;padding:12px;margin-top:12px;font-size:.92rem;color:#7a4a14;}

  /* ---------- Celebration ---------- */
  .badge{
    text-align:center;background:linear-gradient(135deg,#fff7e6,#fdeccb);
    border:2px solid var(--gold);border-radius:16px;padding:18px;margin-top:14px;display:none;
  }
  .badge.show{display:block;animation:pop .5s;}
  @keyframes pop{0%{transform:scale(.7);opacity:0;}70%{transform:scale(1.08);}100%{transform:scale(1);opacity:1;}}
  .badge .seal{font-size:3rem;}
  .badge h2{margin:6px 0;color:var(--navy);}

  @media(max-width:560px){
    .match-grid{flex-direction:column;}
    header h1{font-size:1.25rem;}
    .opt{flex:1 1 100%;}
  }
</style>
</head>
<body>
<div class="wrap">

  <!-- ===== HEADER ===== -->
  <header>
    <div class="stamp">CASE FILE</div>
    <h1>🔍 The Old Man — Character Detective</h1>
    <p class="sub">Use clues from the story to prove what he is like.</p>
    <div class="stars" id="stars">
      <span class="star" data-s="0">★</span>
      <span class="star" data-s="1">★</span>
      <span class="star" data-s="2">★</span>
    </div>
    <p class="sound-note">🔊 Tap the speaker buttons to hear the words.
      If you can't hear sound inside Google Sites, <a href="#" target="_blank" id="fsLink">open full screen for sound</a>.</p>
  </header>

  <!-- ===== TABS ===== -->
  <nav class="tabs" id="tabs">
    <button class="tab active" data-tab="story"><span class="ic">📖</span>The Case</button>
    <button class="tab" data-tab="match"><span class="ic">🔗</span>Match the Clues<span class="done" id="d-match"></span></button>
    <button class="tab" data-tab="detect"><span class="ic">🕵️</span>Be the Detective<span class="done" id="d-detect"></span></button>
    <button class="tab" data-tab="prove"><span class="ic">✍️</span>Prove It!<span class="done" id="d-prove"></span></button>
  </nav>

  <!-- ===== 1. THE CASE (mission) ===== -->
  <section class="panel active" id="panel-story">
    <div class="card">
      <h2>🕵️ Your mission, detective</h2>
      <p class="lead">A good detective looks at <b>clues</b> and works out what a person is like.
        Here is the evidence about the old man. Read each clue. Tap 🔊 to listen.</p>
      <div class="evidence" id="evidenceList"></div>
      <div class="navrow"><button class="btn" onclick="goTab('match')">Start the case →</button></div>
    </div>
  </section>

  <!-- ===== 2. MATCH ===== -->
  <section class="panel" id="panel-match">
    <div class="card">
      <h2>🔗 Match the word to its clue</h2>
      <p class="lead">Tap a <span class="vocab">describing word</span>, then tap the clue that proves it.</p>
      <div class="match-grid">
        <div class="col">
          <h3>Describing word</h3>
          <div id="wordCol"></div>
        </div>
        <div class="col">
          <h3>Clue from the story</h3>
          <div id="clueCol"></div>
        </div>
      </div>
      <div class="badge" id="matchBadge">
        <div class="seal">🏅</div>
        <h2>Great detective work!</h2>
        <p>You matched every clue. ⭐ Star earned!</p>
        <button class="btn" onclick="goTab('detect')">Next: Be the Detective →</button>
      </div>
    </div>
  </section>

  <!-- ===== 3. BE THE DETECTIVE (MCQ) ===== -->
  <section class="panel" id="panel-detect">
    <div class="card">
      <h2>🕵️ Which word does the clue prove?</h2>
      <p class="lead">Read the clue. Choose the best <span class="vocab">describing word</span>.</p>
      <div id="qHost"></div>
    </div>
  </section>

  <!-- ===== 4. PROVE IT ===== -->
  <section class="panel" id="panel-prove">
    <div class="card">
      <h2>✍️ Prove it yourself</h2>
      <p class="lead">Pick a <span class="vocab">word</span>, then find your own clue from the story.</p>

      <p style="margin:0 0 4px;font-weight:bold;">1. The old man is…</p>
      <div class="chip-row" id="proveChips"></div>
      <div style="margin:6px 0 14px;">
        <input id="ownWord" placeholder="…or type your own describing word"
          style="width:100%;border:2px solid var(--line);border-radius:12px;padding:10px;font-family:inherit;font-size:1rem;background:#fffdf7;">
      </div>

      <p style="margin:0 0 4px;font-weight:bold;">2. I know this because in the story…</p>
      <textarea id="proveClue" placeholder="Write your clue here. What did the old man do?"></textarea>
      <p class="clue-help">💡 Need an idea? He lived alone… he built a forest from tin… he never gave up… a bird came to live there…</p>

      <div class="navrow" style="justify-content:flex-start;gap:10px;">
        <button class="btn" onclick="buildReport()">Make my report</button>
        <button class="btn ghost" onclick="sayReport()">🔊 Read it to me</button>
      </div>

      <div class="report" id="report">
        <h3>🗂️ Detective's Report</h3>
        <p class="rline">The old man is <span class="vocab" id="rWord">___</span>.</p>
        <p class="rline">I know this because in the story <span id="rClue">___</span>.</p>
      </div>

      <div class="challenge">
        ★ <b>Challenge:</b> Can you find a <b>second</b> clue for the same word?
        Or think of your <b>own</b> describing word that is not on this sheet!
      </div>

      <div class="badge" id="finalBadge">
        <div class="seal">🏆</div>
        <h2>Case closed, Detective!</h2>
        <p>You finished every part. You are a real Character Detective!</p>
      </div>
    </div>
  </section>

</div>

<script>
/* ---------------- DATA ---------------- */
const WORDS = [
  {en:"determined",  ko:"의지가 강한",  ja:"あきらめない",   clue:"D"},
  {en:"clever",      ko:"똑똑한",       ja:"かしこい",       clue:"C"},
  {en:"responsible", ko:"책임감 있는",  ja:"責任感がある",   clue:"A"},
  {en:"lonely",      ko:"외로운",       ja:"さびしい",       clue:"B"},
  {en:"hopeful",     ko:"희망찬",       ja:"希望に満ちた",   clue:"E"}
];
const CLUES = [
  {id:"A", text:"He looked after his forest and kept it going."},
  {id:"B", text:"He lived all alone among the rubbish."},
  {id:"C", text:"He made a whole forest out of tin and rubbish."},
  {id:"D", text:"He worked for a long time and never gave up."},
  {id:"E", text:"He dreamed of a real, living forest."}
];
const QS = [
  {
    clue:"A real bird came to live in his tin forest.",
    opts:[
      {en:"careless", ko:"부주의한", ja:"ふちゅういな"},
      {en:"proud",    ko:"자랑스러운", ja:"ほこらしい"},
      {en:"bored",    ko:"지루한",   ja:"たいくつな"}
    ],
    answer:"proud",
    why:"His tin forest was so good that a real, living bird wanted to live there. He would feel proud."
  },
  {
    clue:"He kept building even when it was hard.",
    opts:[
      {en:"determined", ko:"의지가 강한", ja:"あきらめない"},
      {en:"proud",      ko:"자랑스러운", ja:"ほこらしい"},
      {en:"clever",     ko:"똑똑한",     ja:"かしこい"},
      {en:"kind",       ko:"친절한",     ja:"やさしい"},
      {en:"patient",    ko:"인내심 있는", ja:"がまんづよい"},
      {en:"brave",      ko:"용감한",     ja:"ゆうかんな"}
    ],
    answer:"determined",
    almost:"patient",
    why:"He never gave up, even when it was hard. That makes him determined."
  }
];

/* ---------------- AUDIO ---------------- */
let voiceReady=false;
function pickVoice(){
  const vs = speechSynthesis.getVoices();
  return vs.find(v=>v.lang==="en-GB") || vs.find(v=>v.lang && v.lang.startsWith("en")) || null;
}
if('speechSynthesis' in window){ speechSynthesis.onvoiceschanged=()=>voiceReady=true; }
function say(text){
  if(!('speechSynthesis' in window)) return;
  speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(text);
  const v=pickVoice(); if(v) u.voice=v;
  u.lang="en-GB"; u.rate=.92; u.pitch=1.02;
  speechSynthesis.speak(u);
}

/* ---------------- TABS ---------------- */
function goTab(name){
  document.querySelectorAll('.tab').forEach(t=>t.classList.toggle('active',t.dataset.tab===name));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.getElementById('panel-'+name).classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
}
document.querySelectorAll('.tab').forEach(t=>t.addEventListener('click',()=>goTab(t.dataset.tab)));

/* full-screen link = current page URL in new tab */
document.getElementById('fsLink').href = window.location.href;

/* ---------------- STARS ---------------- */
const earned={match:false,detect:false,prove:false};
function award(key,starIndex,doneId){
  if(earned[key]) return;
  earned[key]=true;
  document.querySelector('.star[data-s="'+starIndex+'"]').classList.add('on');
  if(doneId) document.getElementById(doneId).textContent="✓ done";
  if(earned.match && earned.detect && earned.prove){
    document.getElementById('finalBadge').classList.add('show');
  }
}

/* ---------------- 1. EVIDENCE LIST ---------------- */
const tags=["🟡","🟠","🔵","🟢","🟣"];
const evHost=document.getElementById('evidenceList');
CLUES.slice().sort((a,b)=>a.id<b.id?-1:1).forEach((c,i)=>{
  const div=document.createElement('div'); div.className='evi';
  div.innerHTML=`<span class="tag">${tags[i]}</span><p>${c.text}</p>`;
  const b=document.createElement('button'); b.className='say'; b.textContent='🔊';
  b.onclick=()=>say(c.text); div.appendChild(b);
  evHost.appendChild(div);
});

/* ---------------- 2. MATCH GAME ---------------- */
const wordCol=document.getElementById('wordCol');
const clueCol=document.getElementById('clueCol');
const pairColors=["#fff3cf","#ffe2cf","#d8ecff","#dff5e3","#eddcff"];
let selWord=null, matchCount=0, pairIndex=0;

function shuffle(a){return a.map(x=>[Math.random(),x]).sort((m,n)=>m[0]-n[0]).map(x=>x[1]);}

shuffle(WORDS).forEach(w=>{
  const el=document.createElement('div'); el.className='wcard'; el.dataset.clue=w.clue;
  el.innerHTML=`<button class="say" onclick="event.stopPropagation();say('${w.en}')">🔊</button>
    <div class="txt"><span class="vocab">${w.en}</span>
    <span class="home">${w.ko} · ${w.ja}</span></div>`;
  el.onclick=()=>selectWord(el);
  wordCol.appendChild(el);
});
shuffle(CLUES).forEach(c=>{
  const el=document.createElement('div'); el.className='ccard'; el.dataset.id=c.id;
  el.innerHTML=`<button class="say" onclick="event.stopPropagation();say('${c.text.replace(/'/g,"\\'")}')">🔊</button>
    <div class="txt">${c.text}</div>`;
  el.onclick=()=>selectClue(el);
  clueCol.appendChild(el);
});

function selectWord(el){
  if(el.classList.contains('matched')) return;
  if(selWord===el){ el.classList.remove('sel'); selWord=null; return; }
  document.querySelectorAll('.wcard.sel').forEach(x=>x.classList.remove('sel'));
  el.classList.add('sel'); selWord=el;
  say(el.querySelector('.vocab').textContent);
}
function selectClue(el){
  if(el.classList.contains('matched')) return;
  say(el.querySelector('.txt').textContent);
  if(!selWord){ flash(el); return; }
  if(el.dataset.id===selWord.dataset.clue){
    const col=pairColors[pairIndex%pairColors.length]; pairIndex++;
    [selWord,el].forEach(n=>{
      n.classList.remove('sel'); n.classList.add('matched');
      n.style.background=col; n.style.borderColor='var(--green)';
      const num=document.createElement('span'); num.className='pairnum'; num.textContent='✓';
      n.appendChild(num);
    });
    selWord=null; matchCount++;
    if(matchCount===WORDS.length){
      document.getElementById('matchBadge').classList.add('show');
      award('match',0,'d-match');
    }
  } else {
    el.classList.add('shake'); selWord.classList.add('shake');
    setTimeout(()=>{ el.classList.remove('shake'); if(selWord)selWord.classList.remove('shake'); },420);
  }
}
function flash(el){ el.classList.add('shake'); setTimeout(()=>el.classList.remove('shake'),420); }

/* ---------------- 3. DETECTIVE MCQ ---------------- */
let qi=0;
const qHost=document.getElementById('qHost');
function renderQ(){
  const q=QS[qi];
  qHost.innerHTML='';
  const box=document.createElement('div'); box.className='clue-box';
  box.innerHTML=`<button class="say big" onclick="say('${q.clue.replace(/'/g,"\\'")}')">🔊</button>
    <p class="q"><b>Clue:</b> ${q.clue}<br>This shows he is…</p>`;
  qHost.appendChild(box);

  const opts=document.createElement('div'); opts.className='opts';
  q.opts.forEach(o=>{
    const b=document.createElement('button'); b.className='opt';
    b.innerHTML=`<div class="txt">${o.en}</div><div class="home">${o.ko} · ${o.ja}</div>`;
    b.onclick=()=>answer(b,o,q);
    opts.appendChild(b);
  });
  qHost.appendChild(opts);

  const fb=document.createElement('div'); fb.className='feedback'; fb.id='fb';
  qHost.appendChild(fb);

  const row=document.createElement('div'); row.className='navrow';
  const next=document.createElement('button'); next.className='btn'; next.id='nextBtn'; next.disabled=true;
  next.textContent = qi<QS.length-1 ? 'Next clue →' : 'Finish ✓';
  next.onclick=()=>{
    if(qi<QS.length-1){ qi++; renderQ(); }
    else { award('detect',1,'d-detect'); goTab('prove'); }
  };
  row.appendChild(next); qHost.appendChild(row);
}
function answer(btn,o,q){
  const fb=document.getElementById('fb');
  document.querySelectorAll('.opt').forEach(b=>b.disabled=true);
  if(o.en===q.answer){
    btn.classList.add('correct');
    fb.className='feedback good show'; fb.innerHTML=`✅ <b>Correct!</b> ${q.why}`;
    say("Correct! "+q.why);
    document.getElementById('nextBtn').disabled=false;
  } else if(q.almost && o.en===q.almost){
    btn.classList.add('correct');
    fb.className='feedback try show';
    fb.innerHTML=`👍 Good thinking — <b>${q.almost}</b> fits too! But the <b>best</b> word here is <span class="vocab">${q.answer}</span>. ${q.why}`;
    say("Good thinking. The best word is "+q.answer);
    document.getElementById('nextBtn').disabled=false;
  } else {
    btn.classList.add('wrong'); btn.disabled=true;
    document.querySelectorAll('.opt').forEach(b=>{ if(b!==btn) b.disabled=false; });
    fb.className='feedback try show'; fb.innerHTML=`🔎 Not quite — look at the clue again and try another word.`;
    say("Not quite. Try again.");
  }
}
renderQ();

/* ---------------- 4. PROVE IT ---------------- */
const proveWords=["determined","clever","responsible","lonely","hopeful","proud","patient","brave","kind"];
const chipHost=document.getElementById('proveChips');
let chosenWord="";
proveWords.forEach(w=>{
  const c=document.createElement('button'); c.className='chip'; c.textContent=w;
  c.onclick=()=>{
    document.querySelectorAll('.chip').forEach(x=>x.classList.remove('sel'));
    c.classList.add('sel'); chosenWord=w; document.getElementById('ownWord').value=''; say(w);
  };
  chipHost.appendChild(c);
});
document.getElementById('ownWord').addEventListener('input',e=>{
  if(e.target.value.trim()){ document.querySelectorAll('.chip').forEach(x=>x.classList.remove('sel')); chosenWord=''; }
});
function buildReport(){
  const own=document.getElementById('ownWord').value.trim();
  const word = own || chosenWord;
  const clue = document.getElementById('proveClue').value.trim();
  if(!word){ alert("First pick a describing word (or type your own)."); return; }
  if(!clue){ alert("Now write your clue from the story."); document.getElementById('proveClue').focus(); return; }
  document.getElementById('rWord').textContent=word;
  document.getElementById('rClue').textContent=clue;
  document.getElementById('report').classList.add('show');
  award('prove',2,'d-prove');
  sayReport();
}
function sayReport(){
  const w=document.getElementById('rWord').textContent;
  const c=document.getElementById('rClue').textContent;
  if(w==="___") return;
  say(`The old man is ${w}. I know this because in the story ${c}.`);
}
</script>
</body>
</html>
