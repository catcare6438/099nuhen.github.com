<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>窩貓裏 | 後臺管理</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
:root {
  --pink: #FFB6C1;
  --pink-deep: #FF8FA3;
  --pink-light: #FFF0F3;
  --bg: #1A0F14;
  --bg2: #261520;
  --card: #32192A;
  --border: #4A2D3D;
  --text: #FFE8EF;
  --text-light: #C9939E;
  --green: #4ECDC4;
  --yellow: #FFE66D;
  --orange: #FF9F1C;
  --red: #FF6B6B;
}
* { box-sizing: border-box; margin:0; padding:0; }
body { font-family:'Noto Sans TC',sans-serif; background:var(--bg); color:var(--text); min-height:100vh; }
 
/* LOGIN */
#loginScreen {
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  background:linear-gradient(135deg,#1A0F14,#2D1020);
}
.login-box {
  background:var(--card);
  border:2px solid var(--border);
  border-radius:24px;
  padding:40px;
  text-align:center;
  width:340px;
  box-shadow:0 20px 60px rgba(0,0,0,.5);
}
.login-icon { font-size:3rem; margin-bottom:12px; }
.login-title { font-size:1.3rem; font-weight:700; color:var(--pink-deep); margin-bottom:6px; }
.login-sub { font-size:0.82rem; color:var(--text-light); margin-bottom:24px; }
.login-input {
  width:100%; padding:12px 16px;
  background:var(--bg2); border:2px solid var(--border);
  border-radius:12px; color:var(--text);
  font-size:0.95rem; font-family:inherit;
  outline:none; transition:border .2s; margin-bottom:14px;
  text-align:center; letter-spacing:4px;
}
.login-input:focus { border-color:var(--pink-deep); }
.login-btn {
  width:100%; padding:12px;
  background:linear-gradient(135deg,var(--pink-deep),#FF6B8A);
  color:white; border:none; border-radius:12px;
  font-size:1rem; font-weight:700; font-family:inherit;
  cursor:pointer; transition:all .2s;
}
.login-btn:hover { opacity:.9; transform:translateY(-1px); }
.login-err { color:var(--red); font-size:0.82rem; margin-top:8px; display:none; }
 
/* ADMIN */
#adminScreen { display:none; }
.top-bar {
  background:var(--bg2);
  border-bottom:2px solid var(--border);
  padding:14px 24px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  flex-wrap:wrap;
  gap:10px;
}
.top-title { font-weight:700; font-size:1.1rem; color:var(--pink-deep); }
.top-actions { display:flex; gap:10px; }
.btn {
  padding:8px 16px; border-radius:20px; border:none; cursor:pointer;
  font-size:0.82rem; font-weight:600; font-family:inherit; transition:all .2s;
}
.btn-pink { background:var(--pink-deep); color:white; }
.btn-out { background:transparent; border:2px solid var(--border); color:var(--text-light); }
.btn-out:hover { border-color:var(--pink); color:var(--pink); }
 
/* TABS */
.tabs {
  display:flex; gap:4px; padding:14px 24px;
  background:var(--bg2); border-bottom:1px solid var(--border);
  flex-wrap:wrap;
}
.tab {
  padding:7px 18px; border-radius:20px; cursor:pointer;
  font-size:0.82rem; font-weight:600; color:var(--text-light);
  transition:all .2s;
}
.tab.active { background:var(--pink-deep); color:white; }
 
/* CONTENT */
.content { padding:24px; max-width:1200px; margin:0 auto; }
 
/* STATS */
.stats-row { display:grid; grid-template-columns:repeat(auto-fit,minmax(160px,1fr)); gap:16px; margin-bottom:24px; }
.stat-card {
  background:var(--card); border:1px solid var(--border); border-radius:16px;
  padding:18px; text-align:center;
}
.stat-num { font-size:1.8rem; font-weight:700; color:var(--pink-deep); }
.stat-label { font-size:0.78rem; color:var(--text-light); margin-top:4px; }
 
/* TABLE */
.table-wrap { overflow-x:auto; }
table { width:100%; border-collapse:collapse; font-size:0.82rem; }
th {
  background:var(--bg2); color:var(--text-light);
  padding:12px 10px; text-align:left;
  border-bottom:2px solid var(--border); white-space:nowrap;
}
td { padding:12px 10px; border-bottom:1px solid var(--border); vertical-align:top; }
tr:hover td { background:rgba(255,143,163,0.05); }
.badge {
  display:inline-block; padding:3px 10px; border-radius:20px;
  font-size:0.72rem; font-weight:700;
}
.badge-wait { background:rgba(255,230,109,0.2); color:var(--yellow); border:1px solid var(--yellow); }
.badge-ok { background:rgba(78,205,196,0.2); color:var(--green); border:1px solid var(--green); }
.badge-done { background:rgba(200,200,200,0.1); color:#888; border:1px solid #555; }
 
/* ACTION BTNS */
.action-btns { display:flex; gap:6px; flex-wrap:wrap; }
.action-btn {
  padding:4px 10px; border-radius:10px; border:none; cursor:pointer;
  font-size:0.72rem; font-weight:600; font-family:inherit;
}
.ab-confirm { background:rgba(78,205,196,0.2); color:var(--green); border:1px solid var(--green); }
.ab-assign { background:rgba(255,159,28,0.2); color:var(--orange); border:1px solid var(--orange); }
.ab-done { background:rgba(200,200,200,0.1); color:#888; border:1px solid #555; }
.ab-del { background:rgba(255,107,107,0.15); color:var(--red); border:1px solid var(--red); }
 
/* SITTER SECTION */
.sitter-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr)); gap:16px; margin-bottom:24px; }
.sitter-card {
  background:var(--card); border:1px solid var(--border); border-radius:16px; padding:20px;
}
.sitter-head { display:flex; align-items:center; gap:12px; margin-bottom:14px; }
.sitter-avatar { font-size:2rem; }
.sitter-name { font-weight:700; color:var(--pink); font-size:1rem; }
.sitter-role { font-size:0.72rem; color:var(--text-light); }
.sitter-stat { display:flex; justify-content:space-between; font-size:0.82rem; padding:4px 0; border-bottom:1px solid var(--border); }
.sitter-stat:last-child { border:none; }
.sitter-stat .val { color:var(--pink-deep); font-weight:700; }
.export-btn {
  width:100%; margin-top:12px; padding:8px;
  background:transparent; border:1px solid var(--pink-deep); color:var(--pink-deep);
  border-radius:10px; font-size:0.78rem; cursor:pointer; font-family:inherit; transition:all .2s;
}
.export-btn:hover { background:var(--pink-deep); color:white; }
 
/* ASSIGN MODAL */
.modal-ov {
  display:none; position:fixed; inset:0;
  background:rgba(0,0,0,.6); z-index:999;
  align-items:center; justify-content:center;
}
.modal-ov.show { display:flex; }
.modal-box {
  background:var(--card); border:2px solid var(--border);
  border-radius:20px; padding:28px; width:360px; max-width:94vw;
}
.modal-box h3 { color:var(--pink-deep); margin-bottom:16px; }
.modal-box select, .modal-box input {
  width:100%; padding:10px 14px; margin-bottom:12px;
  background:var(--bg2); border:2px solid var(--border); border-radius:10px;
  color:var(--text); font-family:inherit; font-size:0.9rem; outline:none;
}
.modal-box select:focus, .modal-box input:focus { border-color:var(--pink-deep); }
.modal-row { display:flex; gap:10px; }
.modal-row .btn { flex:1; padding:10px; border-radius:10px; font-size:0.85rem; }
 
/* DETAIL MODAL */
.detail-modal {
  background:var(--card); border:2px solid var(--border);
  border-radius:20px; padding:28px; width:520px; max-width:96vw;
  max-height:85vh; overflow-y:auto;
}
.detail-row { display:flex; justify-content:space-between; padding:6px 0; border-bottom:1px solid var(--border); font-size:0.85rem; }
.detail-label { color:var(--text-light); }
.detail-val { font-weight:600; text-align:right; max-width:60%; }
.detail-total { color:var(--pink-deep); font-size:1.1rem; font-weight:700; }
</style>
</head>
<body>
 
<!-- LOGIN -->
<div id="loginScreen">
  <div class="login-box">
    <div class="login-icon">🔐</div>
    <div class="login-title">後臺管理系統</div>
    <div class="login-sub">窩貓裏 寵物褓姆</div>
    <input type="password" class="login-input" id="pwInput" placeholder="請輸入密碼" onkeydown="if(event.key==='Enter')doLogin()">
    <button class="login-btn" onclick="doLogin()">登入</button>
    <div class="login-err" id="loginErr">密碼錯誤，請再試一次 🐾</div>
  </div>
</div>
 
<!-- ADMIN -->
<div id="adminScreen">
  <div class="top-bar">
    <div class="top-title">🐾 窩貓裏後臺管理</div>
    <div class="top-actions">
      <button class="btn btn-pink" onclick="exportAll()">📥 匯出全部</button>
      <a href="index.html" class="btn btn-out">← 回前台</a>
      <button class="btn btn-out" onclick="doLogout()">登出</button>
    </div>
  </div>
  <div class="tabs">
    <div class="tab active" onclick="switchTab('orders',this)">📋 預約訂單</div>
    <div class="tab" onclick="switchTab('sitters',this)">👩 保母薪資</div>
  </div>
  <div class="content">
    <!-- STATS -->
    <div class="stats-row" id="statsRow"></div>
    <!-- ORDERS TAB -->
    <div id="tab-orders">
      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>#</th>
              <th>預約時間</th>
              <th>飼主</th>
              <th>電話</th>
              <th>地址</th>
              <th>日期</th>
              <th>天數</th>
              <th>次/天</th>
              <th>服務</th>
              <th>加購</th>
              <th>貓/狗</th>
              <th>公里</th>
              <th>費用</th>
              <th>負責保母</th>
              <th>狀態</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody id="bookingTbody"></tbody>
        </table>
      </div>
    </div>
    <!-- SITTERS TAB -->
    <div id="tab-sitters" style="display:none;">
      <div class="sitter-grid" id="sitterGrid"></div>
    </div>
  </div>
</div>
 
<!-- ASSIGN MODAL -->
<div class="modal-ov" id="assignModal">
  <div class="modal-box">
    <h3>指派保母</h3>
    <input type="hidden" id="assignId">
    <select id="assignSelect">
      <option value="">-- 選擇保母 --</option>
      <option>May</option>
      <option>Ying</option>
      <option>小汶</option>
      <option>菓菓</option>
      <option>小茹</option>
      <option>阿瑛</option>
    </select>
    <div class="modal-row">
      <button class="btn btn-pink" onclick="confirmAssign()">確認指派</button>
      <button class="btn btn-out" onclick="closeAssign()">取消</button>
    </div>
  </div>
</div>
 
<!-- DETAIL MODAL -->
<div class="modal-ov" id="detailModal">
  <div class="detail-modal">
    <h3 style="color:var(--pink-deep);margin-bottom:16px;">📋 訂單明細</h3>
    <div id="detailContent"></div>
    <button class="btn btn-pink" style="margin-top:18px;width:100%;" onclick="closeDetail()">關閉</button>
  </div>
</div>
 
<!-- EXPORT MODAL -->
<div class="modal-ov" id="exportModal">
  <div class="modal-box">
    <h3>匯出保母薪資明細</h3>
    <div id="exportContent" style="font-size:0.82rem;line-height:1.8;color:var(--text-light);white-space:pre-wrap;background:var(--bg2);border-radius:10px;padding:14px;max-height:320px;overflow-y:auto;margin-bottom:14px;"></div>
    <div class="modal-row">
      <button class="btn btn-pink" onclick="copyExport()">複製文字</button>
      <button class="btn btn-out" onclick="document.getElementById('exportModal').classList.remove('show')">關閉</button>
    </div>
  </div>
</div>
 
<script>
const PASSWORD = 'chch715715';
const SITTERS = ['May','Ying','小汶','菓菓','小茹','阿瑛'];
const SERVICE_NAMES = { companion:'到府陪伴', walk:'散步' };
const SERVICE_PRICE = { companion:300, walk:200 };
const ADDON_PRICE = { 餵藥:50,點藥:50,寵物舒緩按摩:100,剪指甲:80,協助排便導尿:80,收信:30,澆花:30,倒垃圾:50 };
 
function doLogin(){
  const pw = document.getElementById('pwInput').value;
  if(pw===PASSWORD){
    document.getElementById('loginScreen').style.display='none';
    document.getElementById('adminScreen').style.display='block';
    renderAll();
  } else {
    document.getElementById('loginErr').style.display='block';
    document.getElementById('pwInput').value='';
  }
}
function doLogout(){
  document.getElementById('loginScreen').style.display='flex';
  document.getElementById('adminScreen').style.display='none';
  document.getElementById('pwInput').value='';
  document.getElementById('loginErr').style.display='none';
}
 
function getBookings(){ return JSON.parse(localStorage.getItem('petBookings')||'[]'); }
function saveBookings(b){ localStorage.setItem('petBookings',JSON.stringify(b)); }
 
function calcBookingTotal(b){
  let basePerSession = (b.services||[]).reduce((s,k)=>s+(SERVICE_PRICE[k]||0),0);
  let addonPerSession = (b.addons||[]).reduce((s,a)=>s+(ADDON_PRICE[a]||0),0);
  const cats=b.catCount||1, dogs=b.dogCount||0;
  let extraPets = Math.max(0,cats-2)*30 + Math.max(0,dogs-2)*30;
  const perSession = basePerSession+addonPerSession+extraPets;
  const km = b.distance||0;
  let transport = 0;
  if(km>20) transport=150;
  else if(km>10) transport=100;
  else if(km>5) transport=50;
  const subtotal = perSession*(b.timesPerDay||1)*(b.days||0);
  return { basePerSession, addonPerSession, extraPets, perSession, subtotal, transport, total: subtotal+transport };
}
 
function renderAll(){ renderStats(); renderOrders(); renderSitters(); }
 
function renderStats(){
  const b = getBookings();
  const total = b.reduce((s,x)=>s+calcBookingTotal(x).total,0);
  const pending = b.filter(x=>x.status==='待確認').length;
  const confirmed = b.filter(x=>x.status==='已確認').length;
  document.getElementById('statsRow').innerHTML = `
    <div class="stat-card"><div class="stat-num">${b.length}</div><div class="stat-label">總預約數</div></div>
    <div class="stat-card"><div class="stat-num" style="color:var(--yellow)">${pending}</div><div class="stat-label">待確認</div></div>
    <div class="stat-card"><div class="stat-num" style="color:var(--green)">${confirmed}</div><div class="stat-label">已確認</div></div>
    <div class="stat-card"><div class="stat-num">$${total.toLocaleString()}</div><div class="stat-label">總營收</div></div>
  `;
}
 
function renderOrders(){
  const b = getBookings();
  const tbody = document.getElementById('bookingTbody');
  if(b.length===0){
    tbody.innerHTML='<tr><td colspan="16" style="text-align:center;padding:30px;color:var(--text-light);">尚無預約資料 🐾</td></tr>';
    return;
  }
  tbody.innerHTML = b.map((bk,i)=>{
    const {total} = calcBookingTotal(bk);
    const statusBadge = bk.status==='待確認'?'badge-wait':bk.status==='已確認'?'badge-ok':'badge-done';
    const svcNames = (bk.services||[]).map(s=>SERVICE_NAMES[s]||s).join('+');
    const addonStr = (bk.addons||[]).join('、')||'-';
    const dt = new Date(bk.timestamp).toLocaleString('zh-TW',{month:'2-digit',day:'2-digit',hour:'2-digit',minute:'2-digit'});
    return `<tr>
      <td>${i+1}</td>
      <td style="white-space:nowrap">${dt}</td>
      <td><strong>${bk.ownerName}</strong></td>
      <td>${bk.ownerPhone}</td>
      <td style="font-size:0.75rem;max-width:100px">${bk.ownerAddr}</td>
      <td style="white-space:nowrap;font-size:0.78rem">${bk.startDate}<br>至${bk.endDate}</td>
      <td>${bk.days}天</td>
      <td>${bk.timesPerDay}次</td>
      <td>${svcNames}</td>
      <td style="font-size:0.78rem">${addonStr}</td>
      <td>貓${bk.catCount||1}/狗${bk.dogCount||0}</td>
      <td>${bk.distance||0}km</td>
      <td style="color:var(--pink-deep);font-weight:700;">$${total}</td>
      <td>${bk.assignedTo||'<span style="color:#555">未指派</span>'}</td>
      <td><span class="badge ${statusBadge}">${bk.status}</span></td>
      <td>
        <div class="action-btns">
          <button class="action-btn ab-confirm" onclick="viewDetail(${bk.id})">明細</button>
          ${bk.status==='待確認'?`<button class="action-btn ab-confirm" onclick="confirmOrder(${bk.id})">確認</button>`:''}
          <button class="action-btn ab-assign" onclick="openAssign(${bk.id})">指派</button>
          ${bk.status!=='已完成'?`<button class="action-btn ab-done" onclick="doneOrder(${bk.id})">完成</button>`:''}
          <button class="action-btn ab-del" onclick="delOrder(${bk.id})">刪除</button>
        </div>
      </td>
    </tr>`;
  }).join('');
}
 
function confirmOrder(id){
  const b=getBookings(); const idx=b.findIndex(x=>x.id===id);
  if(idx>=0){ b[idx].status='已確認'; saveBookings(b); renderAll(); }
}
function doneOrder(id){
  const b=getBookings(); const idx=b.findIndex(x=>x.id===id);
  if(idx>=0){ b[idx].status='已完成'; saveBookings(b); renderAll(); }
}
function delOrder(id){
  if(!confirm('確定要刪除此筆預約？')) return;
  saveBookings(getBookings().filter(x=>x.id!==id)); renderAll();
}
 
function openAssign(id){
  document.getElementById('assignId').value=id;
  document.getElementById('assignModal').classList.add('show');
}
function closeAssign(){ document.getElementById('assignModal').classList.remove('show'); }
function confirmAssign(){
  const id=parseInt(document.getElementById('assignId').value);
  const sitter=document.getElementById('assignSelect').value;
  if(!sitter){ alert('請選擇保母'); return; }
  const b=getBookings(); const idx=b.findIndex(x=>x.id===id);
  if(idx>=0){ b[idx].assignedTo=sitter; saveBookings(b); renderAll(); closeAssign(); }
}
 
function viewDetail(id){
  const b=getBookings().find(x=>x.id===id); if(!b) return;
  const {basePerSession,addonPerSession,extraPets,perSession,subtotal,transport,total}=calcBookingTotal(b);
  const svcNames=(b.services||[]).map(s=>SERVICE_NAMES[s]||s).join('+');
  document.getElementById('detailContent').innerHTML=`
    <div class="detail-row"><span class="detail-label">飼主</span><span class="detail-val">${b.ownerName}</span></div>
    <div class="detail-row"><span class="detail-label">電話</span><span class="detail-val">${b.ownerPhone}</span></div>
    <div class="detail-row"><span class="detail-label">LINE</span><span class="detail-val">${b.ownerLine||'-'}</span></div>
    <div class="detail-row"><span class="detail-label">地址</span><span class="detail-val">${b.ownerAddr}</span></div>
    <div class="detail-row"><span class="detail-label">服務日期</span><span class="detail-val">${b.startDate} ~ ${b.endDate}（${b.days}天）</span></div>
    <div class="detail-row"><span class="detail-label">每天次數</span><span class="detail-val">${b.timesPerDay}次</span></div>
    <div class="detail-row"><span class="detail-label">主要服務</span><span class="detail-val">${svcNames}</span></div>
    <div class="detail-row"><span class="detail-label">加購服務</span><span class="detail-val">${(b.addons||[]).join('、')||'無'}</span></div>
    <div class="detail-row"><span class="detail-label">毛孩</span><span class="detail-val">貓${b.catCount||1}隻 / 狗${b.dogCount||0}隻</span></div>
    <div class="detail-row"><span class="detail-label">毛孩資訊</span><span class="detail-val">${b.petInfo||'-'}</span></div>
    <div class="detail-row"><span class="detail-label">備注</span><span class="detail-val">${b.notes||'-'}</span></div>
    <div class="detail-row"><span class="detail-label">距離</span><span class="detail-val">${b.distance||0}km</span></div>
    <div style="margin-top:12px;background:rgba(255,143,163,0.08);border-radius:10px;padding:12px;">
      <div class="detail-row"><span class="detail-label">主要服務/次</span><span class="detail-val">$${basePerSession}</span></div>
      <div class="detail-row"><span class="detail-label">加購/次</span><span class="detail-val">$${addonPerSession}</span></div>
      <div class="detail-row"><span class="detail-label">多寵物加收/次</span><span class="detail-val">$${extraPets}</span></div>
      <div class="detail-row"><span class="detail-label">每次費用</span><span class="detail-val">$${perSession}</span></div>
      <div class="detail-row"><span class="detail-label">×${b.timesPerDay}次×${b.days}天</span><span class="detail-val">$${subtotal}</span></div>
      <div class="detail-row"><span class="detail-label">車馬費</span><span class="detail-val">$${transport}</span></div>
      <div class="detail-row"><span class="detail-label detail-total">總費用</span><span class="detail-val detail-total">$${total}</span></div>
    </div>
    <div class="detail-row"><span class="detail-label">負責保母</span><span class="detail-val">${b.assignedTo||'未指派'}</span></div>
    <div class="detail-row"><span class="detail-label">狀態</span><span class="detail-val">${b.status}</span></div>
  `;
  document.getElementById('detailModal').classList.add('show');
}
function closeDetail(){ document.getElementById('detailModal').classList.remove('show'); }
 
// SITTERS
function renderSitters(){
  const b = getBookings();
  // Calculate per sitter
  const stats = {};
  SITTERS.forEach(s=>{ stats[s]={cases:0,days:0,revenue:0,details:[]}; });
  b.filter(x=>x.assignedTo&&stats[x.assignedTo]).forEach(bk=>{
    const s=bk.assignedTo;
    const {total}=calcBookingTotal(bk);
    stats[s].cases++;
    stats[s].days+=bk.days||0;
    stats[s].revenue+=total;
    stats[s].details.push(bk);
  });
  const avatars={May:'👩‍⚕️',Ying:'🐱',小汶:'🌟',菓菓:'🍎',小茹:'🐕',阿瑛:'🌺'};
  const roles={May:'首席顧問',Ying:'資深照護',小汶:'老年照護',菓菓:'中途志工',小茹:'中途志工',阿瑛:'中途志工'};
  document.getElementById('sitterGrid').innerHTML = SITTERS.map(s=>`
    <div class="sitter-card">
      <div class="sitter-head">
        <div class="sitter-avatar">${avatars[s]||'🐾'}</div>
        <div><div class="sitter-name">${s}</div><div class="sitter-role">${roles[s]}</div></div>
      </div>
      <div class="sitter-stat"><span>接案數</span><span class="val">${stats[s].cases} 件</span></div>
      <div class="sitter-stat"><span>服務天數</span><span class="val">${stats[s].days} 天</span></div>
      <div class="sitter-stat"><span>總服務費</span><span class="val">$${stats[s].revenue.toLocaleString()}</span></div>
      <button class="export-btn" onclick="exportSitter('${s}')">📄 匯出薪資明細</button>
    </div>
  `).join('');
}
 
function switchTab(tab, el){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('tab-orders').style.display=tab==='orders'?'block':'none';
  document.getElementById('tab-sitters').style.display=tab==='sitters'?'block':'none';
}
 
function exportSitter(name){
  const b=getBookings().filter(x=>x.assignedTo===name);
  if(b.length===0){ alert(`${name} 尚無接案紀錄`); return; }
  let text=`【窩貓裏寵物褓姆】薪資明細 - ${name}\n`;
  text+=`匯出時間：${new Date().toLocaleString('zh-TW')}\n`;
  text+=`${'='.repeat(40)}\n\n`;
  let grandTotal=0;
  b.forEach((bk,i)=>{
    const {basePerSession,addonPerSession,extraPets,perSession,subtotal,transport,total}=calcBookingTotal(bk);
    const svcNames=(bk.services||[]).map(s=>SERVICE_NAMES[s]||s).join('+');
    grandTotal+=total;
    text+=`【訂單 ${i+1}】${bk.ownerName} 飼主\n`;
    text+=`服務日期：${bk.startDate} ~ ${bk.endDate}（${bk.days}天）\n`;
    text+=`每天 ${bk.timesPerDay} 次\n`;
    text+=`服務：${svcNames}\n`;
    if(bk.addons?.length) text+=`加購：${bk.addons.join('、')}\n`;
    text+=`毛孩：貓${bk.catCount||1}隻 / 狗${bk.dogCount||0}隻\n`;
    text+=`主要服務/次：$${basePerSession}`;
    if(addonPerSession>0) text+=`，加購：$${addonPerSession}`;
    if(extraPets>0) text+=`，多寵加收：$${extraPets}`;
    text+=`\n每次費用：$${perSession} × ${bk.timesPerDay}次 × ${bk.days}天 = $${subtotal}\n`;
    if(transport>0) text+=`車馬費：$${transport}\n`;
    text+=`本單合計：$${total}\n\n`;
  });
  text+=`${'='.repeat(40)}\n`;
  text+=`總計接案：${b.length} 件\n`;
  text+=`總計服務天：${b.reduce((s,x)=>s+(x.days||0),0)} 天\n`;
  text+=`總計服務費：$${grandTotal.toLocaleString()}\n`;
  document.getElementById('exportContent').textContent=text;
  document.getElementById('exportModal').classList.add('show');
}
 
function copyExport(){
  navigator.clipboard.writeText(document.getElementById('exportContent').textContent)
    .then(()=>alert('已複製到剪貼簿 ✓'));
}
 
function exportAll(){
  const b=getBookings();
  if(b.length===0){ alert('尚無預約資料'); return; }
  let text='窩貓裏寵物褓姆 - 全部預約匯出\n';
  text+=`匯出時間：${new Date().toLocaleString('zh-TW')}\n${'='.repeat(50)}\n\n`;
  b.forEach((bk,i)=>{
    const {total}=calcBookingTotal(bk);
    const svcNames=(bk.services||[]).map(s=>SERVICE_NAMES[s]||s).join('+');
    text+=`[${i+1}] ${bk.ownerName} | ${bk.ownerPhone} | ${bk.startDate}~${bk.endDate} | ${svcNames} | $${total} | ${bk.assignedTo||'未指派'} | ${bk.status}\n`;
  });
  const blob=new Blob([text],{type:'text/plain'});
  const a=document.createElement('a');
  a.href=URL.createObjectURL(blob);
  a.download=`毛毛窩預約_${new Date().toLocaleDateString('zh-TW').replace(/\//g,'')}.txt`;
  a.click();
}
</script>
</body>
</html>
