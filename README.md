# Index.html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>G&D — Shop</title>
<style>
:root{
  --bg-a:#ffecd2; --bg-b:#fcb69f; --bg-c:#c7f1ff;
  --accent-1:#7c3aed; --accent-2:#06b6d4;
  --card-bg: rgba(255,255,255,0.85);
  --glass: rgba(255,255,255,0.6);
  --muted:#48515a;
  --maxw:1100px;
}
/* Reset */
*{box-sizing:border-box}
html,body{height:100%;margin:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto; -webkit-font-smoothing:antialiased}
body{
  background: linear-gradient(120deg,var(--bg-a),var(--bg-b) 40%, var(--bg-c));
  overflow-x:hidden;
  color:#07232b;
  perspective:1200px;
}

/* Animated depth background layers */
.bg-layer{
  position:fixed; inset:-10% -20% auto -20%; width:140%; height:70%; z-index:0; transform-style:preserve-3d; pointer-events:none;
  background:
    radial-gradient(600px 300px at 10% 20%, rgba(124,58,237,0.14), transparent 10%),
    radial-gradient(500px 300px at 90% 80%, rgba(6,182,212,0.12), transparent 10%);
  filter: blur(30px);
  animation: bgMove 18s linear infinite;
}
@keyframes bgMove{0%{transform:translate3d(0,0,0)}50%{transform:translate3d(-30px,8px,0)}100%{transform:translate3d(0,0,0)}}

/* Layout */
.header{
  position:sticky; top:12px; z-index:40; margin: 10px auto; max-width:var(--maxw); padding:10px 18px; display:flex; gap:12px; align-items:center;
  background: linear-gradient(180deg, rgba(255,255,255,0.6), rgba(255,255,255,0.4));
  border-radius:16px; box-shadow: 0 6px 30px rgba(8,20,30,0.08);
  transform: translateZ(30px);
}
.brand{display:flex;gap:12px;align-items:center;font-weight:800}
.brand .logo-sq{width:48px;height:48px;border-radius:12px;display:grid;place-items:center;color:#fff;font-weight:900;
  background:linear-gradient(135deg,var(--accent-1),var(--accent-2)); box-shadow:0 8px 30px rgba(12,18,30,0.08)}
.search{flex:1}
.search input{width:100%;padding:12px 14px;border-radius:12px;border:1px solid rgba(8,18,30,0.06); outline:none;background:rgba(255,255,255,0.85)}

/* main grid */
.main{max-width:var(--maxw); margin:28px auto; padding:0 18px 80px; position:relative; z-index:20}
.grid{display:grid; grid-template-columns: repeat(auto-fill,minmax(220px,1fr)); gap:20px}

/* 3D card */
.card{
  background:var(--card-bg); border-radius:16px; overflow:hidden; border:1px solid rgba(255,255,255,0.6);
  box-shadow: 0 24px 60px rgba(8,20,30,0.08); transform-style:preserve-3d;
  transition: transform .25s ease, box-shadow .25s ease;
  will-change: transform;
  transform-origin:center;
}
.card:hover{ box-shadow: 0 36px 90px rgba(8,20,30,0.14); }
.card .media{height:160px; background:#fff}
.card img{width:100%;height:100%;object-fit:cover;display:block}
.card .body{padding:12px 14px}
.title{font-weight:800}
.muted{color:var(--muted);font-size:.95rem}
.price{font-weight:900;margin-top:6px}

/* 3D button */
.btn{
  display:inline-block;padding:10px 14px;border-radius:12px;border:0;color:#fff;font-weight:800;cursor:pointer;
  background:linear-gradient(90deg,var(--accent-1),var(--accent-2)); box-shadow: 0 10px 30px rgba(124,58,237,0.18); transform-style:preserve-3d;
  transition: transform .12s ease, box-shadow .12s ease;
}
.btn:active{ transform: translateY(2px) translateZ(8px) ; box-shadow:0 6px 18px rgba(0,0,0,0.12)}

/* WhatsApp FAB */
.whats{position:fixed; right:18px; bottom:18px; z-index:60; border-radius:999px; padding:12px 14px; color:#fff; font-weight:900;
  background:linear-gradient(90deg,#25D366,#06b6d4); box-shadow: 0 18px 60px rgba(6,22,36,0.18); transform:translateZ(80px)}

/* Splash modal (3D logo) */
#splash{position:fixed; inset:0; display:grid; place-items:center; z-index:200; background: linear-gradient(180deg, rgba(255,255,255,0.2), rgba(255,255,255,0.0));}
.splash-card{width:84%; max-width:520px; padding:28px; border-radius:18px; text-align:center;
  background: linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.88));
  border:1px solid rgba(255,255,255,0.75); box-shadow: 0 36px 120px rgba(12,18,30,0.12); transform-style:preserve-3d;
  animation: popIn 700ms cubic-bezier(.2,.9,.2,1) both;
}
@keyframes popIn{ from{ transform: translateZ(-80px) scale(.95) translateY(14px); opacity:0 } to{ transform: translateZ(0) scale(1) translateY(0); opacity:1 } }
.splash-logo{width:260px; height:auto; margin:0 auto 12px; transform: translateZ(70px); }

/* Modal (sign in/up) */
.modal-back{ position:fixed; inset:0; display:none; align-items:center; justify-content:center; z-index:250; background:rgba(2,6,23,0.5); }
.modal{ width:380px; border-radius:12px; padding:18px; background:linear-gradient(180deg, rgba(255,255,255,0.96), rgba(255,255,255,0.9)); box-shadow: 0 28px 80px rgba(2,6,23,0.5) }

/* small */
.muted-sm{color:var(--muted); font-size:.92rem}
.footer{ text-align:center; color:var(--muted); margin-top:28px; padding-bottom:28px}

/* tilt helper: ensure transform-style preserved */
.card-inner{ transform-style:preserve-3d; }
@media(max-width:600px){ .header{flex-direction:column; align-items:flex-start} .brand{margin-bottom:8px} .splash-card{width:92%} }
</style>
</head>
<body>
  <div class="bg-layer" aria-hidden="true"></div>

  <!-- SPLASH -->
  <div id="splash" role="dialog" aria-label="G&D Splash">
    <div class="splash-card">
      <img id="splashLogo" class="splash-logo" alt="G&D Logo" />
      <div style="font-weight:900; font-size:1.2rem">G&amp;D</div>
      <div class="muted-sm" style="margin-top:6px">Welcome — stylish shopping in 3D</div>
      <div style="margin-top:14px"><button id="skip" class="btn">Enter Shop</button></div>
    </div>
  </div>

  <!-- HEADER -->
  <div class="header" role="banner">
    <div class="brand">
      <div class="logo-sq">G&amp;D</div>
      <div>
        <div style="font-weight:900">G&amp;D Shop</div>
        <div class="muted-sm">Fresh • Colorful • 3D</div>
      </div>
    </div>
    <div class="search"><input id="search" placeholder="Search products..." /></div>
    <div style="margin-left:auto" id="authArea">
      <button id="openModal" class="btn" style="background:linear-gradient(90deg,#06b6d4,#7c3aed)">Sign In / Sign Up</button>
      <a href="login.html" style="margin-left:8px;text-decoration:none"><button class="btn" style="background:linear-gradient(90deg,#ffd166,#fb8b24)">Login Page</button></a>
    </div>
  </div>

  <!-- MAIN -->
  <main class="main" role="main">
    <div class="grid" id="grid" aria-live="polite"></div>
    <div class="footer">© <span id="yr"></span> G&amp;D — all rights reserved</div>
  </main>

  <a id="whats" class="whats" target="_blank" rel="noopener">Customer Care</a>

  <!-- Modal -->
  <div class="modal-back" id="modalBack" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true">
      <div style="display:flex;gap:8px;margin-bottom:10px">
        <button id="tabSignIn" class="btn" style="flex:1;background:linear-gradient(90deg,#06b6d4,#7c3aed)">Sign In</button>
        <button id="tabSignUp" class="btn" style="flex:1;background:linear-gradient(90deg,#ffd166,#fb8b24)">Sign Up</button>
      </div>

      <div id="formSignIn" style="display:none">
        <input id="siEmail" placeholder="Email" />
        <input id="siPassword" type="password" placeholder="Password" />
        <div style="display:flex;gap:8px;margin-top:8px">
          <button id="btnSignIn" class="btn" style="flex:1">Sign In</button>
          <button id="btnCloseModal" class="btn" style="flex:1;background:transparent;color:#07232b;border:1px solid rgba(8,18,30,0.06)">Close</button>
        </div>
      </div>

      <div id="formSignUp" style="display:none">
        <input id="suName" placeholder="Full name" />
        <input id="suEmail" placeholder="Email" />
        <input id="suPassword" type="password" placeholder="Password (6+ chars)" />
        <div style="display:flex;gap:8px;margin-top:8px">
          <button id="btnSignUp" class="btn" style="flex:1">Create Account</button>
          <button id="btnCloseModal2" class="btn" style="flex:1;background:transparent;color:#07232b;border:1px solid rgba(8,18,30,0.06)">Cancel</button>
        </div>
      </div>
    </div>
  </div>

<script>
/* CONFIG: paste your Base64 logo string here (data:image/...) */
const LOGO_DATA_URI = "PASTE_YOUR_BASE64_DATA_URI_HERE";
const WHATSAPP_NUMBER_INTL = "2347085187460";
const WHATS_DEFAULT_TEXT = encodeURIComponent("Hi G&D! I need help.");

/* Splash handling */
const splash = document.getElementById('splash');
const splashLogo = document.getElementById('splashLogo');
splashLogo.src = LOGO_DATA_URI;
const skipBtn = document.getElementById('skip');
let splashTimer = setTimeout(()=>{ hideSplash(); }, 10000);
skipBtn.addEventListener('click', ()=>{ clearTimeout(splashTimer); hideSplash(); });
function hideSplash(){ splash.style.display='none'; }

/* WhatsApp */
document.getElementById('whats').href = `https://wa.me/${WHATSAPP_NUMBER_INTL}?text=${WHATS_DEFAULT_TEXT}`;

/* Products storage */
const STORAGE_KEY = "gnd_products_v1";
const USERS_KEY = "gnd_users_v1";
const SESSION_KEY = "gnd_session_v1";
const DEFAULT_PRODUCTS = [
  { title:"Wireless Headphones", price:"₦25,000", category:"Electronics", image:"https://images.unsplash.com/photo-1518447514771-a67cba0f2c1a?q=80&w=800&auto=format&fit=crop" },
  { title:"Running Shoes", price:"₦15,000", category:"Fashion", image:"https://images.unsplash.com/photo-1608231387042-66d1773070a5?q=80&w=800&auto=format&fit=crop" }
];
function loadProducts(){ const raw = localStorage.getItem(STORAGE_KEY); if(!raw){ localStorage.setItem(STORAGE_KEY, JSON.stringify(DEFAULT_PRODUCTS)); return DEFAULT_PRODUCTS } try{return JSON.parse(raw)}catch{return DEFAULT_PRODUCTS} }
function saveProducts(a){ localStorage.setItem(STORAGE_KEY, JSON.stringify(a)); window.dispatchEvent(new StorageEvent('storage',{key:STORAGE_KEY,newValue:JSON.stringify(a)})); }

let PRODUCTS = loadProducts();

/* Render products and attach tilt behaviour */
const grid = document.getElementById('grid');
function renderProducts(){
  grid.innerHTML = "";
  const q = (document.getElementById('search').value||"").trim().toLowerCase();
  PRODUCTS.filter(p => !q || (p.title+p.category+p.price).toLowerCase().includes(q))
  .forEach((p,idx)=>{
    const el = document.createElement('div'); el.className = 'card';
    el.innerHTML = `<div class="card-inner"><div class="media"><img src="${p.image}" alt="${p.title}"></div><div class="body"><div class="title">${escapeHtml(p.title)}</div><div class="muted">${escapeHtml(p.category||'')}</div><div class="price">${escapeHtml(p.price||'')}</div></div></div>`;
    grid.appendChild(el);
    attachTilt(el, 18, 14); // tilt intensity
  });
}
function escapeHtml(s){ return String(s).replace(/[&<>"']/g,c=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }

/* simple tilt effect on mouse move */
function attachTilt(card, maxRotate=12, maxTranslate=10){
  const inner = card.querySelector('.card-inner');
  card.addEventListener('mousemove', (e)=>{
    const rect = card.getBoundingClientRect();
    const x = (e.clientX - rect.left) / rect.width - 0.5;
    const y = (e.clientY - rect.top) / rect.height - 0.5;
    const rotY = (-x) * maxRotate;
    const rotX = (y) * maxRotate;
    const tz = Math.max(8, Math.abs(x*maxTranslate)+Math.abs(y*maxTranslate));
    inner.style.transform = `rotateX(${rotX}deg) rotateY(${rotY}deg) translateZ(${tz}px)`;
    card.style.transform = `translateZ(${Math.max(tz/2,8)}px)`;
  });
  card.addEventListener('mouseleave', ()=>{
    inner.style.transform = `rotateX(0deg) rotateY(0deg) translateZ(0px)`;
    card.style.transform = `translateZ(0px)`;
  });
  card.addEventListener('mouseenter', ()=>{ card.style.willChange='transform'; });
}

/* search */
document.getElementById('search').addEventListener('input', renderProducts);
renderProducts();

/* Auth (localStorage / session) */
function loadUsers(){ try{return JSON.parse(localStorage.getItem(USERS_KEY)||'[]')}catch{return[]} }
function saveUsers(a){ localStorage.setItem(USERS_KEY, JSON.stringify(a)); }
function currentUser(){ return JSON.parse(sessionStorage.getItem(SESSION_KEY) || 'null'); }
function setCurrentUser(u){ sessionStorage.setItem(SESSION_KEY, JSON.stringify(u)); updateAuthArea(); }
function signOut(){ sessionStorage.removeItem(SESSION_KEY); updateAuthArea(); }

function updateAuthArea(){
  const area = document.getElementById('authArea');
  const user = currentUser();
  if(user){
    area.innerHTML = `<span style="margin-right:10px">Welcome, ${escapeHtml(user.name)}</span><button id="signOut" class="btn" style="background:linear-gradient(90deg,#ff6b6b,#ff9a6b)">Sign Out</button>`;
    document.getElementById('signOut').addEventListener('click', ()=>{ signOut(); });
  } else {
    area.innerHTML = `<button id="openModal" class="btn" style="background:linear-gradient(90deg,#06b6d4,#7c3aed)">Sign In / Sign Up</button><a href="login.html" style="margin-left:8px;text-decoration:none"><button class="btn" style="background:linear-gradient(90deg,#ffd166,#fb8b24)">Login Page</button></a>`;
    document.getElementById('openModal').addEventListener('click', openModal);
  }
}
updateAuthArea();

/* Modal controls */
const modalBack = document.getElementById('modalBack'), formSignIn = document.getElementById('formSignIn'), formSignUp = document.getElementById('formSignUp');
document.getElementById('tabSignIn').addEventListener('click', ()=>showTab('in'));
document.getElementById('tabSignUp').addEventListener('click', ()=>showTab('up'));
document.getElementById('btnCloseModal').addEventListener('click', closeModal);
document.getElementById('btnCloseModal2').addEventListener('click', closeModal);
function openModal(){ modalBack.style.display='flex'; showTab('in'); modalBack.setAttribute('aria-hidden','false'); }
function closeModal(){ modalBack.style.display='none'; modalBack.setAttribute('aria-hidden','true'); }
function showTab(which){ if(which==='in'){ formSignIn.style.display='block'; formSignUp.style.display='none'; } else { formSignIn.style.display='none'; formSignUp.style.display='block'; } }

/* Sign Up / Sign In */
document.getElementById('btnSignUp').addEventListener('click', ()=>{
  const name = document.getElementById('suName').value.trim();
  const email = document.getElementById('suEmail').value.trim().toLowerCase();
  const pw = document.getElementById('suPassword').value;
  if(!name || !email || pw.length < 6){ alert('Please fill name/email and a password of at least 6 chars.'); return; }
  const users = loadUsers();
  if(users.find(u=>u.email===email)){ alert('Email already exists'); return; }
  users.push({name, email, password: pw}); saveUsers(users); setCurrentUser({name,email}); closeModal(); alert('Account created & signed in.');
});
document.getElementById('btnSignIn').addEventListener('click', ()=>{
  const email = document.getElementById('siEmail').value.trim().toLowerCase();
  const pw = document.getElementById('siPassword').value;
  const users = loadUsers();
  const u = users.find(x=>x.email===email && x.password===pw);
  if(!u){ alert('Invalid email or password'); return; }
  setCurrentUser({name:u.name,email:u.email}); closeModal(); alert('Signed in');
});

/* reflect external product changes */
window.addEventListener('storage', e=>{ if(e.key===STORAGE_KEY){ PRODUCTS = loadProducts(); renderProducts(); } });

/* small util */
document.getElementById('yr').textContent = new Date().getFullYear();
</script>
</body>
</html>
