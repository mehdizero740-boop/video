# video
Bb
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Émotions Studio — Vidéo éducative depuis une image</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
:root{
--bg:#0a0a12;--bg2:#12121c;--bg3:#1a1a28;
--panel:#16161f;--border:#2a2a3a;
--ink:#e8e6e0;--dim:#8a8896;--faint:#4a4858;
--acc:#f5b23e;--acc2:#e87b35;--acc3:#6ac0d8;
--ok:#4a9d6a;--err:#c85a4a;--warn:#d4a017;
--r:8px;--fs:-apple-system,BlinkMacSystemFont,'Helvetica Neue',Arial,sans-serif;
--fm:ui-monospace,'SF Mono',Menlo,monospace;
}
html,body{background:var(--bg)}
body{font-family:var(--fs);background:var(--bg);color:var(--ink);min-height:100vh;padding:1.5rem 1rem 20rem;font-size:15px;line-height:1.55;max-width:980px;margin:0 auto}
header{margin-bottom:1.5rem;text-align:center;padding:1rem 0 1.4rem;position:relative}
header::after{content:'';position:absolute;bottom:0;left:50%;transform:translateX(-50%);width:180px;height:1px;background:linear-gradient(90deg,transparent,var(--acc),var(--acc3),transparent);opacity:.6}
h1{font-size:1.8rem;font-weight:400;margin-bottom:.35rem;background:linear-gradient(135deg,#f5b23e,#e87b35,#6ac0d8,#8b5fc4);-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;letter-spacing:-.02em}
.subtitle{font-size:.85rem;color:var(--dim);font-style:italic}
.toast{position:fixed;top:1.5rem;left:50%;transform:translateX(-50%) translateY(-120px);background:var(--bg3);color:var(--ink);border:1px solid var(--border);border-left:3px solid var(--acc);padding:.85rem 1.4rem;border-radius:var(--r);font-size:.85rem;box-shadow:0 8px 32px rgba(0,0,0,.6);z-index:1000;opacity:0;transition:transform .35s cubic-bezier(.2,.9,.3,1.2),opacity .35s;max-width:90vw;text-align:center;display:flex;align-items:center;gap:.6rem}
.toast.visible{transform:translateX(-50%) translateY(0);opacity:1}
.toast.success{border-left-color:var(--ok)}.toast.error{border-left-color:var(--err)}.toast.warn{border-left-color:var(--warn)}
.banner{background:linear-gradient(135deg,rgba(245,178,62,.06),rgba(106,192,216,.05));border:1px solid var(--border);border-left:3px solid var(--acc);padding:1rem 1.15rem;border-radius:var(--r);font-size:.82rem;color:var(--dim);margin-bottom:1.2rem;line-height:1.6}
.banner strong{color:var(--ink)}.banner .hl{color:var(--acc);font-weight:600}
.panel{background:var(--panel);border:1px solid var(--border);border-radius:var(--r);padding:1.2rem 1.3rem;margin-bottom:1rem}
.panel.ok{box-shadow:inset 3px 0 0 var(--ok)}
.label{display:block;font-size:.72rem;color:var(--dim);margin-bottom:.5rem;text-transform:uppercase;letter-spacing:.15em;font-weight:600}
input[type=password],input[type=text],textarea{width:100%;padding:.85rem 1rem;border-radius:var(--r);border:1px solid var(--border);background:var(--bg2);color:var(--ink);font-family:var(--fm);font-size:.78rem;margin-bottom:.6rem}
textarea{font-family:var(--fs);font-size:.88rem;line-height:1.55;resize:vertical;min-height:120px}
input:focus,textarea:focus{outline:none;border-color:var(--acc)}
.btn{width:100%;padding:.85rem 1.2rem;border-radius:var(--r);border:1px solid var(--border);background:var(--bg2);color:var(--ink);font-size:.85rem;font-weight:600;letter-spacing:.1em;text-transform:uppercase;cursor:pointer;margin-bottom:.7rem;transition:all .2s;font-family:inherit}
.btn:hover:not(:disabled){background:var(--bg3);border-color:var(--acc)}
.btn:disabled{opacity:.35;cursor:not-allowed}
.btn-primary{border-color:var(--acc);background:linear-gradient(135deg,rgba(245,178,62,.2),rgba(106,192,216,.15));color:var(--acc);font-size:1.05rem;padding:1.3rem;letter-spacing:.2em}
.btn-stop{border-color:var(--err);color:var(--err);background:transparent;display:none}
.btn-stop.visible{display:block}
.status{font-size:.75rem;padding:.6rem .9rem;border-radius:var(--r);margin-bottom:.5rem;display:flex;align-items:center;gap:.6rem;background:var(--bg2);color:var(--dim);border:1px solid var(--border)}
.status.ok{background:rgba(74,157,106,.08);color:var(--ok);border-color:rgba(74,157,106,.3)}
.dot{width:6px;height:6px;border-radius:50%;background:var(--faint);flex-shrink:0}
.status.ok .dot{background:var(--ok);box-shadow:0 0 8px var(--ok)}
.hint{font-size:.72rem;color:var(--dim);margin-top:.5rem}
.hint a{color:var(--acc);text-decoration:none}
.ref-drop{border:2px dashed var(--border);border-radius:var(--r);padding:1.5rem 1rem;background:var(--bg2);text-align:center;cursor:pointer;transition:all .2s;position:relative}
.ref-drop:hover{border-color:var(--acc);background:rgba(245,178,62,.04)}
.ref-drop.has-image{padding:0;border-style:solid;border-color:var(--acc)}
.ref-drop input[type=file]{position:absolute;inset:0;opacity:0;cursor:pointer}
.ref-drop .ref-icon{font-size:2.2rem;color:var(--acc);opacity:.7;margin-bottom:.5rem}
.ref-drop .ref-text{font-size:.85rem;color:var(--dim);line-height:1.5}
.ref-drop .ref-text strong{color:var(--acc)}
.ref-drop .ref-hint{font-size:.7rem;color:var(--faint);margin-top:.4rem;font-family:var(--fm)}
.ref-preview{position:relative;display:block;width:100%;max-height:360px;overflow:hidden}
.ref-preview img{width:100%;height:auto;display:block;max-height:360px;object-fit:contain;background:#000}
.ref-preview .ref-remove{position:absolute;top:.6rem;right:.6rem;background:rgba(200,90,74,.9);color:#fff;border:none;width:32px;height:32px;border-radius:50%;font-size:1rem;cursor:pointer;font-weight:700}
.ref-preview .ref-label{position:absolute;bottom:0;left:0;right:0;padding:.5rem .8rem;background:linear-gradient(transparent,rgba(10,10,18,.92));font-size:.72rem;font-family:var(--fm);color:var(--acc);letter-spacing:.05em}
.video-result{margin-top:1rem;border-radius:var(--r);overflow:hidden;border:1px solid var(--border);background:#000;animation:fadeIn .5s ease}
.video-result video{width:100%;display:block;aspect-ratio:16/9;object-fit:contain;background:#000}
.video-result .v-caption{padding:.7rem 1rem;background:var(--panel);font-size:.78rem;color:var(--dim);display:flex;justify-content:space-between;align-items:center;gap:.6rem;flex-wrap:wrap}
.video-result .v-caption a{color:var(--acc);text-decoration:none;font-weight:600}
@keyframes fadeIn{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.progress{width:100%;height:6px;background:var(--bg2);border-radius:3px;overflow:hidden;margin-top:.8rem;border:1px solid var(--border);display:none}
.progress.visible{display:block}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--acc2),var(--acc),var(--acc3));width:0%;transition:width .3s;border-radius:3px}
.progress-info{font-size:.75rem;color:var(--dim);font-family:var(--fm);display:none;margin-top:.5rem;justify-content:space-between;flex-wrap:wrap;gap:.4rem}
.progress-info.visible{display:flex}
.debug-panel{position:fixed;bottom:0;left:0;right:0;height:220px;background:#05050a;border-top:2px solid var(--acc);z-index:200;display:flex;flex-direction:column;font-family:var(--fm);box-shadow:0 -8px 32px rgba(0,0,0,.7);transition:height .3s ease}
.debug-panel.collapsed{height:38px}
.debug-header{display:flex;justify-content:space-between;align-items:center;padding:.5rem .8rem;background:linear-gradient(90deg,#0f0f18,#1a1a28);border-bottom:1px solid var(--border);flex-shrink:0;cursor:pointer;user-select:none}
.debug-title{font-size:.72rem;color:var(--acc);letter-spacing:.15em;text-transform:uppercase;font-weight:600;display:flex;align-items:center;gap:.5rem}
.debug-badge{font-size:.6rem;padding:.1rem .4rem;background:var(--acc);color:var(--bg);border-radius:2px;font-weight:700}
.debug-actions{display:flex;gap:.3rem}
.debug-actions button{background:transparent;border:1px solid var(--border);color:var(--dim);font-size:.62rem;padding:.25rem .55rem;border-radius:2px;cursor:pointer;font-family:inherit}
.debug-actions button:hover{color:var(--acc);border-color:var(--acc)}
.debug-body{flex:1;overflow-y:auto;padding:.5rem .7rem 1rem;font-size:.72rem;line-height:1.45;color:#c8c8d0}
.debug-entry{margin-bottom:.3rem;padding:.25rem .4rem;border-left:2px solid transparent;border-radius:2px;word-break:break-word}
.debug-entry.info{border-left-color:var(--faint)}
.debug-entry.success{border-left-color:var(--ok);background:rgba(74,157,106,.04)}
.debug-entry.warn{border-left-color:var(--warn);background:rgba(212,160,23,.04)}
.debug-entry.error{border-left-color:var(--err);background:rgba(200,90,74,.06);color:#f0a0a0}
.debug-entry.api{border-left-color:var(--acc)}
.debug-entry.response{border-left-color:var(--acc3)}
.debug-entry.ai{border-left-color:#8b5fc4;background:rgba(139,95,196,.04)}
.debug-time{color:var(--faint);margin-right:.5rem;font-size:.65rem}
.debug-cat{color:var(--acc);font-weight:600;margin-right:.4rem;font-size:.65rem}
.debug-msg{color:#d8d8e0}
.debug-data{margin-top:.3rem;padding:.4rem .5rem;background:#0a0a12;border:1px solid var(--border);border-radius:2px;font-size:.68rem;color:#a8d8b0;max-height:180px;overflow:auto;white-space:pre-wrap;word-break:break-all;line-height:1.4}
@media(max-width:480px){h1{font-size:1.4rem}body{padding-bottom:18rem}.debug-panel{height:200px}}
</style>
</head>
<body>

<header>
<h1>Émotions Studio</h1>
<p class="subtitle">Ton image → une vidéo éducative animée en 3D · Personnages préservés à l'identique</p>
</header>

<div class="banner">
<strong>Ton projet :</strong> tu fournis une <span class="hl">image de référence</span> (comme « Mes émotions et mon bien-être »),
l'IA l'utilise comme <span class="hl">première frame absolue</span> et génère une vidéo 3D animée de 10 à 15 secondes en
<span class="hl">conservant exactement les personnages, les visages, les couleurs et le style</span> — avec une animation
douce, éducative, pour enfants de 3 à 7 ans.
</div>

<!-- ═══════════════ API ═══════════════ -->
<div class="panel" id="api-panel">
<label class="label">🔑 Clé API Agnes</label>
<input type="password" id="api-key-input" placeholder="sk-..." autocomplete="off" spellcheck="false">
<button type="button" class="btn" id="api-save-btn">Enregistrer la clé</button>
<div class="status" id="api-status-line"><span class="dot"></span><span id="api-status-text">Aucune clé API enregistrée</span></div>
<div class="hint">Clé gratuite sur <a href="https://platform.agnes-ai.com" target="_blank" rel="noopener">platform.agnes-ai.com</a> → Settings → API Keys</div>
</div>

<!-- ═══════════════ IMAGE DE RÉFÉRENCE ═══════════════ -->
<div class="panel">
<label class="label">🖼️ Image de référence — définit TOUT le style</label>
<div class="ref-drop" id="ref-drop">
<input type="file" accept="image/*" id="ref-input">
<div class="ref-icon">🎨</div>
<div class="ref-text"><strong>Cliquez pour charger ton image</strong><br>Illustration enfantine, artwork 3D, photo stylisée…</div>
<div class="ref-hint">L'IA préservera les personnages, les visages, les couleurs et le style à l'identique.</div>
</div>
</div>

<!-- ═══════════════ DESCRIPTION DE L'ANIMATION ═══════════════ -->
<div class="panel">
<label class="label">✨ Décris ce que tu veux voir bouger</label>
<textarea id="animation-prompt" placeholder="Exemple : L'enfant sourit et regarde les personnages autour de lui...">L'enfant sourit doucement et regarde les personnages autour de lui. Le personnage jaune saute de joie, le personnage bleu exprime la tristesse, le personnage rouge se calme progressivement, le personnage violet retrouve son courage et le personnage vert ferme les yeux pour respirer paisiblement.

Ajoute de petits mouvements naturels, des expressions faciales fluides, une légère brise dans les arbres, des particules lumineuses et une caméra qui avance lentement vers les personnages.

Ambiance magique, chaleureuse, rassurante et éducative. Animation de haute qualité, format horizontal 16:9, adaptée aux enfants de 3 à 7 ans. Aucun changement d'apparence entre les personnages. Pas de déformation des visages ni de mouvements brusques.</textarea>
</div>

<!-- ═══════════════ RÉGLAGES ═══════════════ -->
<div class="panel">
<label class="label">⚙️ Réglages vidéo</label>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:.8rem;">
<div>
<label class="label" style="margin-top:0;">Durée</label>
<select id="duration-select" style="width:100%;padding:.7rem .9rem;border-radius:var(--r);border:1px solid var(--border);background:var(--bg2);color:var(--ink);font-size:.85rem;font-family:inherit;">
<option value="241">10 secondes (241 frames) — recommandé</option>
<option value="313">13 secondes (313 frames)</option>
<option value="361">15 secondes (361 frames)</option>
</select>
</div>
<div>
<label class="label" style="margin-top:0;">Format</label>
<select id="ratio-select" style="width:100%;padding:.7rem .9rem;border-radius:var(--r);border:1px solid var(--border);background:var(--bg2);color:var(--ink);font-size:.85rem;font-family:inherit;">
<option value="16:9" selected>16:9 — Paysage (horizontal)</option>
<option value="9:16">9:16 — Portrait</option>
<option value="1:1">1:1 — Carré</option>
</select>
</div>
</div>
</div>

<!-- ═══════════════ BOUTON PRINCIPAL ═══════════════ -->
<button type="button" class="btn btn-primary" id="generate-btn" disabled>
🎬 Générer la vidéo animée
</button>
<button type="button" class="btn btn-stop" id="stop-btn">⏹ Arrêter la génération</button>

<div class="progress" id="progress"><div class="progress-fill" id="progress-fill"></div></div>
<div class="progress-info" id="progress-info">
<span id="progress-label">En attente…</span>
<span id="progress-eta"></span>
</div>

<!-- ═══════════════ RÉSULTAT ═══════════════ -->
<div id="result-container"></div>

<div class="toast" id="toast"><span id="toast-icon">✓</span><span id="toast-text">Message</span></div>

<!-- ═══════════════ DEBUG ═══════════════ -->
<div class="debug-panel" id="debug-panel">
<div class="debug-header" id="debug-header">
<div class="debug-title">🖥️ Console <span class="debug-badge" id="debug-count">0</span></div>
<div class="debug-actions">
<button type="button" id="debug-copy-btn">Copier</button>
<button type="button" id="debug-clear-btn">Effacer</button>
<button type="button" id="debug-collapse-btn">−</button>
</div>
</div>
<div class="debug-body" id="debug-body"></div>
</div>

<script>
// ══════════════════════════════════════════════════════════════════
// CONFIGURATION — protocoles issus des codes sources validés
// ══════════════════════════════════════════════════════════════════
const API_BASE = 'https://apihub.agnes-ai.com/v1';
const POLL_BASE = 'https://apihub.agnes-ai.com/agnesapi';
const MODEL_VIDEO = 'agnes-video-v2.0';
const FRAME_RATE = 24;

const API_KEY_STORAGE = 'emotions_studio_api_key_v1';
const DEBUG_MAX = 600;
const REF_MAX_SIDE = 1280;

// Attente initiale + cadence de polling (validées dans tes codes sources)
const VIDEO_FIRST_POLL_DELAY_SEC = 80;
const VIDEO_POLL_INTERVALS = [8, 8, 12, 12, 20, 20, 25];
const VIDEO_MAX_POLL_ATTEMPTS = 120;

// ══════════════════════════════════════════════════════════════════
// STATE
// ══════════════════════════════════════════════════════════════════
const state = {
  apiKey: '',
  referenceImage: null,
  referenceImageBase64: null,
  isRunning: false,
  stopRequested: false,
  currentVideoId: null
};

// ══════════════════════════════════════════════════════════════════
// UTILS
// ══════════════════════════════════════════════════════════════════
function esc(s){return String(s==null?'':s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function sleep(ms){return new Promise(r=>setTimeout(r,ms))}
function formatEta(s){if(s<60)return Math.round(s)+'s';const m=Math.floor(s/60);const r=Math.round(s%60);return m+'m'+(r>0?' '+r+'s':'')}
function setStatus(text){
  // Pas de barre fixe ici — on utilise progress-info
  const lbl=document.getElementById('progress-label');
  if(lbl&&text)lbl.textContent=text;
}

// ══════════════════════════════════════════════════════════════════
// TOAST
// ══════════════════════════════════════════════════════════════════
let toastTimeout=null;
function showToast(message,type='success',duration=2800){
  const t=document.getElementById('toast');
  const i=document.getElementById('toast-icon');
  const x=document.getElementById('toast-text');
  if(!t||!i||!x)return;
  t.classList.remove('visible','success','error','warn');
  void t.offsetWidth;
  const icons={success:'✓',error:'✕',warn:'⚠'};
  i.textContent=icons[type]||'✓';
  x.textContent=message;
  t.classList.add(type);
  requestAnimationFrame(()=>t.classList.add('visible'));
  if(toastTimeout)clearTimeout(toastTimeout);
  toastTimeout=setTimeout(()=>t.classList.remove('visible'),duration);
}

// ══════════════════════════════════════════════════════════════════
// DEBUG CONSOLE
// ══════════════════════════════════════════════════════════════════
let debugCount=0,debugEntries=[],debugCollapsed=false;
function debugLog(level,category,message,data){
  const body=document.getElementById('debug-body');if(!body)return;
  const time=new Date().toLocaleTimeString('fr-FR',{hour12:false});
  const entry=document.createElement('div');
  entry.className='debug-entry '+level;
  let html='<span class="debug-time">'+time+'</span>';
  html+='<span class="debug-cat">['+esc(category)+']</span>';
  html+='<span class="debug-msg">'+esc(message)+'</span>';
  if(data!==undefined&&data!==null){
    let ds;
    if(typeof data==='string')ds=data;
    else{try{ds=JSON.stringify(data,null,2)}catch(e){ds=String(data)}}
    if(ds.length>3500)ds=ds.slice(0,3500)+'\n…[tronqué]';
    html+='<pre class="debug-data">'+esc(ds)+'</pre>';
  }
  entry.innerHTML=html;
  body.appendChild(entry);
  debugEntries.push({time,level,category,message});
  if(debugEntries.length>DEBUG_MAX)debugEntries.shift();
  while(body.children.length>DEBUG_MAX)body.removeChild(body.firstChild);
  body.scrollTop=body.scrollHeight;
  debugCount++;
  const c=document.getElementById('debug-count');
  if(c)c.textContent=debugCount;
}
function clearDebug(){
  const b=document.getElementById('debug-body');if(b)b.innerHTML='';
  debugEntries=[];debugCount=0;
  const c=document.getElementById('debug-count');if(c)c.textContent='0';
}
function copyDebug(){
  const lines=debugEntries.map(e=>e.time+' ['+e.category+'] '+e.message).join('\n');
  const finish=(ok)=>showToast(ok?'Console copiée':'Copie impossible',ok?'success':'error');
  try{
    if(navigator.clipboard&&window.isSecureContext){
      navigator.clipboard.writeText(lines).then(()=>finish(true)).catch(()=>legacyCopy(lines,finish));
      return;
    }
  }catch(e){}
  legacyCopy(lines,finish);
}
function legacyCopy(text,cb){
  const ta=document.createElement('textarea');
  ta.value=text;ta.style.position='fixed';ta.style.opacity='0';
  document.body.appendChild(ta);ta.focus();ta.select();
  let ok=false;try{ok=document.execCommand('copy')}catch(e){}
  document.body.removeChild(ta);cb(ok);
}
function toggleDebugCollapse(){
  const p=document.getElementById('debug-panel');
  const b=document.getElementById('debug-collapse-btn');
  if(!p||!b)return;
  debugCollapsed=!debugCollapsed;
  p.classList.toggle('collapsed',debugCollapsed);
  b.textContent=debugCollapsed?'+':'−';
}

// ══════════════════════════════════════════════════════════════════
// PROGRESS BAR
// ══════════════════════════════════════════════════════════════════
function showProgress(){
  document.getElementById('progress').classList.add('visible');
  document.getElementById('progress-info').classList.add('visible');
}
function hideProgress(){
  document.getElementById('progress').classList.remove('visible');
  document.getElementById('progress-info').classList.remove('visible');
}
function setProgress(pct,label,eta){
  const f=document.getElementById('progress-fill');
  if(f)f.style.width=Math.max(0,Math.min(100,pct))+'%';
  const l=document.getElementById('progress-label');
  if(l&&label!==undefined)l.textContent=label;
  const e=document.getElementById('progress-eta');
  if(e&&eta!==undefined)e.textContent=eta||'';
}

// ══════════════════════════════════════════════════════════════════
// API KEY
// ══════════════════════════════════════════════════════════════════
function getApiKey(){try{return(localStorage.getItem(API_KEY_STORAGE)||'').trim()}catch(e){return''}}
function saveApiKey(){
  const input=document.getElementById('api-key-input');if(!input)return;
  const key=input.value.trim();
  if(!key){
    try{localStorage.removeItem(API_KEY_STORAGE)}catch(e){}
    updateApiPanel();showToast('Clé supprimée','warn');return;
  }
  if(!key.startsWith('sk-')){if(!confirm('La clé ne commence pas par "sk-". Sauvegarder ?'))return;}
  try{
    localStorage.setItem(API_KEY_STORAGE,key);
    updateApiPanel();
    showToast('Clé enregistrée ✓','success');
    debugLog('success','API','Clé : '+key.slice(0,8)+'…'+key.slice(-4));
    input.blur();
  }catch(e){showToast('Erreur sauvegarde','error')}
}
function updateApiPanel(){
  const panel=document.getElementById('api-panel');
  const input=document.getElementById('api-key-input');
  const line=document.getElementById('api-status-line');
  const text=document.getElementById('api-status-text');
  const key=getApiKey();
  if(!panel||!input||!line||!text)return;
  state.apiKey=key;
  if(key){
    panel.classList.add('ok');line.classList.add('ok');
    text.textContent='Clé active · '+key.slice(0,8)+'…'+key.slice(-4);
    input.value=key;input.placeholder='';
  }else{
    panel.classList.remove('ok');line.classList.remove('ok');
    text.textContent='Aucune clé API enregistrée';
    input.value='';input.placeholder='sk-...';
  }
  updateGenerateBtn();
}

// ══════════════════════════════════════════════════════════════════
// BOUTON GÉNÉRER
// ══════════════════════════════════════════════════════════════════
function updateGenerateBtn(){
  const btn=document.getElementById('generate-btn');
  if(!btn)return;
  const hasKey=!!state.apiKey;
  const hasImage=!!state.referenceImageBase64;
  const hasPrompt=document.getElementById('animation-prompt').value.trim().length>10;
  btn.disabled=!hasKey||!hasImage||!hasPrompt||state.isRunning;
  if(state.isRunning)btn.innerHTML='⏳ Génération en cours…';
  else if(!hasKey)btn.innerHTML='🔑 Ajoutez votre clé API';
  else if(!hasImage)btn.innerHTML='🖼️ Chargez une image de référence';
  else if(!hasPrompt)btn.innerHTML='✍️ Décrivez l\'animation';
  else btn.innerHTML='🎬 Générer la vidéo animée';
}

// ══════════════════════════════════════════════════════════════════
// IMAGE — compression + affichage
// ══════════════════════════════════════════════════════════════════
function fileToDataUri(file){
  return new Promise((res,rej)=>{
    const r=new FileReader();
    r.onload=e=>res(e.target.result);
    r.onerror=()=>rej(new Error('Erreur lecture'));
    r.readAsDataURL(file);
  });
}
async function compressImage(dataUrl,maxSide){
  return new Promise((resolve)=>{
    const img=new Image();
    img.onload=()=>{
      let{width,height}=img;
      const scale=Math.min(1,maxSide/Math.max(width,height));
      width=Math.round(width*scale);
      height=Math.round(height*scale);
      const canvas=document.createElement('canvas');
      canvas.width=width;canvas.height=height;
      const ctx=canvas.getContext('2d');
      ctx.drawImage(img,0,0,width,height);
      resolve(canvas.toDataURL('image/jpeg',0.92));
    };
    img.onerror=()=>resolve(dataUrl);
    img.src=dataUrl;
  });
}
async function handleReferenceImage(file){
  if(!file)return;
  if(!file.type.startsWith('image/')){showToast('Fichier non image','error');return;}
  if(file.size>20*1024*1024){showToast('Image trop lourde (max 20 Mo)','error');return;}
  try{
    debugLog('info','REF','Chargement de '+file.name+' ('+Math.round(file.size/1024)+' Ko)');
    const raw=await fileToDataUri(file);
    const compressed=await compressImage(raw,REF_MAX_SIDE);
    state.referenceImage=file;
    state.referenceImageBase64=compressed;
    updateRefPreview();
    updateGenerateBtn();
    showToast('Image de référence prête ✓','success');
    debugLog('success','REF','Image compressée : '+Math.round(compressed.length/1024)+' Ko');
  }catch(e){
    showToast('Erreur chargement image','error');
    debugLog('error','REF',e.message);
  }
}
function updateRefPreview(){
  const drop=document.getElementById('ref-drop');
  if(!drop)return;
  if(state.referenceImageBase64){
    drop.classList.add('has-image');
    drop.innerHTML=
      '<div class="ref-preview">'+
        '<img src="'+state.referenceImageBase64+'" alt="Référence">'+
        '<div class="ref-label">✅ Image de référence — sera la première frame absolue de la vidéo</div>'+
        '<button type="button" class="ref-remove" id="ref-remove-btn">✕</button>'+
      '</div>';
    const btn=document.getElementById('ref-remove-btn');
    if(btn)btn.addEventListener('click',(e)=>{
      e.stopPropagation();
      state.referenceImage=null;
      state.referenceImageBase64=null;
      updateRefPreview();
      updateGenerateBtn();
      showToast('Image retirée','warn');
    });
  }else{
    drop.classList.remove('has-image');
    drop.innerHTML=
      '<input type="file" accept="image/*" id="ref-input">'+
      '<div class="ref-icon">🎨</div>'+
      '<div class="ref-text"><strong>Cliquez pour charger ton image</strong><br>Illustration enfantine, artwork 3D, photo stylisée…</div>'+
      '<div class="ref-hint">L\'IA préservera les personnages, les visages, les couleurs et le style à l\'identique.</div>';
    bindRefInput();
  }
}
function bindRefInput(){
  const input=document.getElementById('ref-input');
  if(!input)return;
  input.addEventListener('change',e=>{
    const f=e.target.files&&e.target.files[0];
    if(f)handleReferenceImage(f);
  });
}

// ══════════════════════════════════════════════════════════════════
// API FETCH — protocole validé (backoff, 429, 503, timeouts)
// ══════════════════════════════════════════════════════════════════
async function apiFetch(url,options={},label='API',maxAttempts=6){
  let lastErr=null;
  for(let attempt=0;attempt<maxAttempts;attempt++){
    if(state.stopRequested)throw new Error('Arrêt demandé');
    const method=options.method||'GET';
    // Réduction des bases64 volumineuses pour le log
    let bodyPreview=null;
    if(options.body){
      try{
        const p=JSON.parse(options.body);
        const c=JSON.parse(JSON.stringify(p));
        const redact=(o)=>{
          if(Array.isArray(o)){o.forEach(redact);return}
          if(o&&typeof o==='object'){
            for(const k in o){
              if(typeof o[k]==='string'&&o[k].length>140)o[k]=o[k].slice(0,100)+'…[len '+o[k].length+']';
              else if(typeof o[k]==='object')redact(o[k]);
            }
          }
        };
        redact(c);bodyPreview=c;
      }catch(e){bodyPreview=String(options.body).slice(0,400)}
    }
    debugLog('api','REQ '+label,method+' '+url+' (essai '+(attempt+1)+'/'+maxAttempts+')',bodyPreview);
    try{
      const t0=Date.now();
      const res=await fetch(url,options);
      const dt=Date.now()-t0;
      let retryAfter=0;
      try{retryAfter=parseInt(res.headers.get('Retry-After')||'0',10)||0}catch(e){}
      let errorText='';
      if(!res.ok){try{errorText=(await res.clone().text()).slice(0,1200)}catch(e){}}
      debugLog('response','RÉP '+label,'HTTP '+res.status+' en '+dt+'ms',errorText||undefined);
      if(res.ok)return res;
      if([400,401,403,404].includes(res.status)){
        throw new Error('HTTP '+res.status+' — '+errorText.slice(0,400));
      }
      if(res.status===429){
        const wait=retryAfter>0?retryAfter:Math.min(120,15+attempt*15);
        debugLog('warn','RATELIMIT','429 — attente '+wait+'s');
        setStatus('Limite API — nouvelle tentative dans '+wait+'s');
        await sleep(wait*1000);continue;
      }
      if([500,502,503,504,520,522,524].includes(res.status)){
        const wait=Math.min(60,8+attempt*6);
        debugLog('warn','SERVICE','HTTP '+res.status+' — attente '+wait+'s');
        setStatus('Service occupé — reprise dans '+wait+'s');
        await sleep(wait*1000);continue;
      }
      const wait=Math.min(60,6+attempt*5);
      debugLog('warn','HTTP','HTTP '+res.status+' — retry dans '+wait+'s');
      await sleep(wait*1000);
    }catch(e){
      if(e.message==='Arrêt demandé')throw e;
      if(/^HTTP (4\d\d)/.test(e.message))throw e;
      lastErr=e;
      const wait=Math.min(45,4+attempt*4);
      debugLog('warn','NETWORK',e.message+' — retry dans '+wait+'s');
      await sleep(wait*1000);
    }
  }
  throw lastErr||new Error('Tentatives épuisées pour '+label);
}

// ══════════════════════════════════════════════════════════════════
// CRÉATION DE LA TÂCHE VIDÉO
// ══════════════════════════════════════════════════════════════════
async function createVideoTask(imageBase64, prompt, numFrames, ratio){
  const body={
    model:MODEL_VIDEO,
    prompt:prompt,
    image:imageBase64,
    num_frames:numFrames,
    frame_rate:FRAME_RATE,
    ratio:ratio,
    aspect_ratio:ratio,
    size:ratio
  };
  debugLog('ai','PROMPT VIDÉO','Envoi ('+prompt.length+' chars · '+numFrames+' frames · '+ratio+')');
  const res=await apiFetch(
    API_BASE+'/videos',
    {
      method:'POST',
      headers:{
        'Authorization':'Bearer '+state.apiKey,
        'Content-Type':'application/json'
      },
      body:JSON.stringify(body)
    },
    'Video Task',
    4
  );
  const data=await res.json();
  debugLog('response','VIDÉO CRÉÉE','Réponse du POST /videos',data);
  const videoId=data.video_id||data.id||data.task_id;
  if(!videoId)throw new Error('Pas de video_id retourné');
  debugLog('success','VIDÉO','Tâche créée : '+String(videoId).slice(0,40)+'…');
  return videoId;
}

// ══════════════════════════════════════════════════════════════════
// POLLING
// ══════════════════════════════════════════════════════════════════
async function pollVideo(videoId, onProgress){
  // Attente initiale (protocole validé : 80 s)
  let remaining=VIDEO_FIRST_POLL_DELAY_SEC;
  debugLog('info','POLLING','Attente initiale '+remaining+'s avant premier poll');
  while(remaining>0){
    if(state.stopRequested)throw new Error('Arrêt demandé');
    onProgress('Préparation — '+remaining+'s');
    await sleep(1000);
    remaining--;
  }

  for(let attempt=0;attempt<VIDEO_MAX_POLL_ATTEMPTS;attempt++){
    if(state.stopRequested)throw new Error('Arrêt demandé');
    if(attempt>0){
      const idx=Math.min(attempt-1,VIDEO_POLL_INTERVALS.length-1);
      let r=VIDEO_POLL_INTERVALS[idx];
      while(r>0){
        if(state.stopRequested)throw new Error('Arrêt demandé');
        onProgress('Création — '+r+'s');
        await sleep(1000);
        r--;
      }
    }
    const url=POLL_BASE+'?video_id='+encodeURIComponent(videoId)+'&model_name='+encodeURIComponent(MODEL_VIDEO);
    try{
      const res=await apiFetch(
        url,
        {method:'GET',headers:{'Authorization':'Bearer '+state.apiKey}},
        'Polling',
        2
      );
      const d=await res.json();
      const status=d.status||'unknown';
      const progress=d.progress||0;
      onProgress('Création — '+progress+'%');
      debugLog('info','POLLING','status='+status+' progress='+progress+'%');
      if(status==='completed'||status==='succeeded'||status==='done'){
        const videoUrl=(d.metadata&&d.metadata.url)||d.url||(d.output&&d.output.url);
        if(!videoUrl)throw new Error('Terminé mais pas d\'URL');
        debugLog('success','POLLING','Terminé après '+(attempt+1)+' polls');
        return videoUrl;
      }
      if(status==='failed'||status==='error'||status==='cancelled'){
        throw new Error('Échec de la génération ('+status+')');
      }
    }catch(e){
      if(e.message==='Arrêt demandé')throw e;
      if(e.message.includes('Échec de la génération'))throw e;
      debugLog('warn','POLLING','Erreur transitoire : '+e.message);
    }
  }
  throw new Error('Délai maximal dépassé');
}

// ══════════════════════════════════════════════════════════════════
// CONSTRUCTION DU PROMPT — préserve TOUT, anime doucement
// ══════════════════════════════════════════════════════════════════
function buildAnimationPrompt(userDescription, ratio){
  const orientationRule = ratio==='16:9'
    ? 'FORMAT: horizontal 16:9 landscape, widescreen cinematic framing.'
    : ratio==='9:16'
    ? 'FORMAT: vertical 9:16 portrait, mobile-first framing.'
    : 'FORMAT: 1:1 square, centered composition.';

  return [
    '╔══════════════════════════════════════════════════════════════════╗',
    '║ STYLE REFERENCE — ABSOLUTE PRESERVATION (highest priority)         ║',
    '╚══════════════════════════════════════════════════════════════════╝',
    'The provided image is the EXACT first frame of this video. It is the authoritative visual anchor.',
    'You MUST preserve, without ANY modification:',
    '  • The exact same characters — same number, same species, same shapes.',
    '  • The exact same faces — same eyes, same mouth shapes, same expressions at start, same fur/skin, same colors.',
    '  • The exact same colors — same palette, same saturation, same lighting.',
    '  • The exact same style — same 3D rendering, same soft cartoon look, same level of detail.',
    '  • The exact same environment — same trees, same ground, same sky, same background elements.',
    '  • The exact same composition and framing — same positions of every character and object.',
    'NO character substitutions. NO appearance changes. NO face deformation. NO sudden body changes.',
    'NO style drift. NO cartoon-to-realistic shifts. NO color palette shifts.',
    '',
    '╔══════════════════════════════════════════════════════════════════╗',
    '║ ANIMATION — CHILDREN\'S 3D ANIMATION, SOFT AND MAGICAL              ║',
    '╚══════════════════════════════════════════════════════════════════╝',
    'A gentle, warm, reassuring, educational animation for children aged 3 to 7.',
    'Quality: high-end 3D animated feature film rendering, soft global illumination, cinematic depth of field.',
    '',
    'WHAT MOVES (following the user description below):',
    userDescription,
    '',
    'SUBTLE NATURAL MOTION (always present):',
    '  • Gentle blinking on all characters with smooth eyelids.',
    '  • Soft breathing on every character (chest and shoulders).',
    '  • Very slight facial micro-expressions: eyebrows, mouth corners.',
    '  • Soft wind in the grass and in the tree leaves (subtle, natural).',
    '  • Floating warm light particles drifting slowly through the frame (magical sparkles).',
    '  • Sunbeams filtering through the trees with gentle shimmer.',
    '',
    'CAMERA MOTION:',
    '  • A slow, smooth DOLLY-IN toward the characters, almost imperceptible.',
    '  • The camera glides forward gently, keeping all characters perfectly in frame.',
    '  • NO camera shake. NO fast pans. NO zoom. NO angle changes.',
    '  • Camera stays perpendicular and stable, like a breathing motion.',
    '',
    '╔══════════════════════════════════════════════════════════════════╗',
    '║ MOTION CONSTRAINTS — SAFETY FOR YOUNG CHILDREN                     ║',
    '╚══════════════════════════════════════════════════════════════════╝',
    '  • ALL movements must be SLOW, GENTLE and CALM.',
    '  • NO abrupt motions. NO fast jumps. NO sudden changes.',
    '  • NO character deformation, NO face distortion, NO limb stretching.',
    '  • NO morphing. NO character merging. NO disappearing elements.',
    '  • NO new characters entering the frame.',
    '  • NO extra objects appearing or disappearing.',
    '  • The animation must feel safe, warm and reassuring at every second.',
    '',
    '╔══════════════════════════════════════════════════════════════════╗',
    '║ AUDIO — NATURAL SOUNDS ONLY                                        ║',
    '╚══════════════════════════════════════════════════════════════════╝',
    'No music. No dialogue. No narration. Only soft natural ambient sounds:',
    'gentle wind, distant birds, soft leaves rustling, faint sparkle chimes.',
    '',
    orientationRule,
    '',
    'FINAL OUTPUT: high-quality 3D animation, natural gentle motion, soft warm lighting,',
    'stays 100% faithful to the reference image, perfect for young children 3 to 7 years old.',
    'No text overlays. No subtitles. No watermarks.'
  ].join('\n');
}

// ══════════════════════════════════════════════════════════════════
// PIPELINE PRINCIPAL
// ══════════════════════════════════════════════════════════════════
async function generateVideo(){
  if(state.isRunning)return;
  if(!state.apiKey){showToast('Ajoutez votre clé API','error');return;}
  if(!state.referenceImageBase64){showToast('Chargez une image de référence','error');return;}
  const userDescription=document.getElementById('animation-prompt').value.trim();
  if(userDescription.length<10){showToast('Décrivez l\'animation','error');return;}

  const numFrames=parseInt(document.getElementById('duration-select').value,10);
  const ratio=document.getElementById('ratio-select').value;
  const durationSec=Math.round(numFrames/FRAME_RATE);

  state.isRunning=true;
  state.stopRequested=false;
  updateGenerateBtn();
  document.getElementById('stop-btn').classList.add('visible');
  document.getElementById('result-container').innerHTML='';
  showProgress();
  setProgress(5,'Envoi de la tâche à Agnes…','');

  const startTime=Date.now();
  debugLog('state','GÉNÉRATION','Démarrage : '+numFrames+' frames ('+durationSec+'s) · '+ratio);

  try{
    // Prompt final
    const prompt=buildAnimationPrompt(userDescription, ratio);
    debugLog('ai','PROMPT CONSTRUIT','Longueur finale : '+prompt.length+' chars');

    // Création de la tâche
    setProgress(10,'Création de la tâche vidéo…','');
    const videoId=await createVideoTask(state.referenceImageBase64, prompt, numFrames, ratio);
    state.currentVideoId=videoId;

    // Attente + polling
    setProgress(15,'Tâche créée — attente de la génération…','≈ '+formatEta(VIDEO_FIRST_POLL_DELAY_SEC+60));
    const videoUrl=await pollVideo(videoId,(prog)=>{
      // Progression visuelle de 15 à 90%
      const pct=15+Math.min(75, Math.round((Date.now()-startTime)/300));
      const elapsed=Math.round((Date.now()-startTime)/1000);
      setProgress(
        Math.min(pct,90),
        prog,
        elapsed>5?('écoulé '+formatEta(elapsed)):''
      );
    });

    // Succès
    setProgress(100,'✦ Vidéo prête ✦','durée : '+formatEta((Date.now()-startTime)/1000));
    debugLog('success','GÉNÉRATION','Vidéo disponible : '+videoUrl.slice(0,80)+'…');

    // Affichage du résultat
    const container=document.getElementById('result-container');
    container.innerHTML=
      '<div class="video-result">'+
        '<video src="'+videoUrl+'" controls autoplay loop playsinline preload="metadata"></video>'+
        '<div class="v-caption">'+
          '<span>🎬 <strong>'+durationSec+'s</strong> · '+ratio+' · 24 fps</span>'+
          '<a href="'+videoUrl+'" target="_blank" rel="noopener" download="emotions-animation.mp4">⬇ Télécharger / ouvrir</a>'+
        '</div>'+
      '</div>';

    showToast('Vidéo générée ✓','success',3500);
    await sleep(2500);
    hideProgress();

  }catch(e){
    if(e.message==='Arrêt demandé'){
      setProgress(0,'Arrêté par l\'utilisateur','');
      showToast('Génération arrêtée','warn');
      debugLog('warn','STOP','Arrêt demandé');
    }else{
      setProgress(0,'Erreur : '+e.message.slice(0,60),'');
      showToast('Erreur : '+e.message.slice(0,60),'error',4500);
      debugLog('error','GÉNÉRATION',e.message);
    }
    await sleep(3000);
    hideProgress();
  }

  state.isRunning=false;
  state.stopRequested=false;
  state.currentVideoId=null;
  document.getElementById('stop-btn').classList.remove('visible');
  updateGenerateBtn();
}

// ══════════════════════════════════════════════════════════════════
// INIT
// ══════════════════════════════════════════════════════════════════
(function init(){
  // API
  document.getElementById('api-save-btn').addEventListener('click',saveApiKey);
  document.getElementById('api-key-input').addEventListener('keydown',e=>{
    if(e.key==='Enter'){e.preventDefault();saveApiKey()}
  });

  // Image de référence
  bindRefInput();

  // Prompt
  document.getElementById('animation-prompt').addEventListener('input',updateGenerateBtn);

  // Bouton générer
  document.getElementById('generate-btn').addEventListener('click',generateVideo);

  // Stop
  document.getElementById('stop-btn').addEventListener('click',()=>{
    state.stopRequested=true;
    debugLog('warn','STOP','Arrêt demandé par l\'utilisateur');
  });

  // Debug
  document.getElementById('debug-header').addEventListener('click',e=>{
    if(e.target.tagName==='BUTTON')return;
    toggleDebugCollapse();
  });
  document.getElementById('debug-collapse-btn').addEventListener('click',e=>{e.stopPropagation();toggleDebugCollapse()});
  document.getElementById('debug-clear-btn').addEventListener('click',e=>{e.stopPropagation();clearDebug()});
  document.getElementById('debug-copy-btn').addEventListener('click',e=>{e.stopPropagation();copyDebug()});

  // Récupère la clé sauvegardée
  const savedKey=getApiKey();
  if(savedKey)document.getElementById('api-key-input').value=savedKey;

  updateApiPanel();
  updateGenerateBtn();

  debugLog('success','INIT','Émotions Studio prêt');
  debugLog('info','INIT','Pipeline : IMAGE DE RÉFÉRENCE → PROMPT DE PRÉSERVATION ABSOLUE → VIDÉO 3D ANIMÉE');
  debugLog('info','INIT','Modèle : '+MODEL_VIDEO+' · cadence 24 fps · polling à 80s puis [8,8,12,12,20,20,25]');
  debugLog('info','INIT','Le prompt force la préservation totale des personnages, visages, couleurs et style');
  debugLog('info','INIT','Animations douces, éducatives, adaptées aux enfants de 3 à 7 ans');

  showToast('Chargez votre image puis cliquez sur Générer','success',3500);
})();
</script>
</body>
</html>