<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>貓窩裏｜後台管理</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&family=Nunito:wght@700;800;900&display=swap" rel="stylesheet">
<style>
:root{--p1:#FFB7C5;--p2:#FF8FAB;--p3:#E05070;--y1:#FFE0A3;--b1:#B8E4FF;--b2:#7DC8F5;--g1:#B8F0C8;--g2:#7DD99A;--bg:#FFF0F5;--text:#3D2B35;--mid:#7A5C68;--soft:#B08A9A;--shadow:0 3px 14px rgba(224,80,112,.1);}
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Noto Sans TC',sans-serif;background:var(--bg);color:var(--text);min-height:100vh}
.login-wrap{display:flex;align-items:center;justify-content:center;min-height:100vh;padding:20px;background:linear-gradient(160deg,#ffe8f0,#fff5e8)}
.login-box{background:#fff;border-radius:22px;padding:36px 28px;max-width:320px;width:100%;text-align:center;border:2px solid var(--p1);box-shadow:var(--shadow)}
.login-logo{font-size:2.5rem;margin-bottom:7px}.login-title{font-family:'Nunito',sans-serif;font-size:1.1rem;font-weight:900;color:var(--p3);margin-bottom:2px}
.login-sub{font-size:.74rem;color:var(--soft);margin-bottom:18px}
.login-box input{width:100%;padding:10px 13px;border:2px solid var(--p1);border-radius:12px;font-family:inherit;font-size:.86rem;outline:none;margin-bottom:9px}
.login-box input:focus{border-color:var(--p2)}
.login-btn{width:100%;padding:11px;background:linear-gradient(135deg,var(--p2),var(--p3));color:#fff;border:none;border-radius:12px;font-family:inherit;font-size:.9rem;font-weight:700;cursor:pointer}
.login-err{font-size:.72rem;color:var(--p3);margin-top:6px;display:none}
.admin-wrap{display:none}
.admin-hdr{background:#fff;padding:12px 18px;display:flex;align-items:center;justify-content:space-between;box-shadow:0 2px 8px rgba(0,0,0,.06);position:sticky;top:0;z-index:50;flex-wrap:wrap;gap:7px;border-bottom:3px dashed var(--p1)}
.admin-logo{display:flex;align-items:center;gap:8px}
.alogo-ic{font-size:1.35rem}.alogo-nm{font-family:'Nunito',sans-serif;font-size:.94rem;font-weight:900;color:var(--p3)}.alogo-sb{font-size:.56rem;color:var(--soft);font-weight:600}
.hbtns{display:flex;gap:6px;flex-wrap:wrap}
.hbtn{padding:6px 12px;border-radius:10px;font-family:inherit;font-size:.7rem;font-weight:700;cursor:pointer;border:none}
.hbtn-pink{background:linear-gradient(135deg,var(--p1),var(--p2));color:var(--p3)}
.hbtn-blue{background:linear-gradient(135deg,var(--b1),var(--b2));color:#1a6fa8}
.hbtn-out{background:#fff;color:var(--soft);border:1.5px solid #e8d8dc}
.tab-nav{display:flex;gap:0;background:#fff;border-bottom:2px solid var(--p1);padding:0 14px;overflow-x:auto}
.tnav{padding:11px 16px;border:none;background:transparent;font-family:inherit;font-size:.76rem;font-weight:700;cursor:pointer;color:var(--soft);border-bottom:3px solid transparent;margin-bottom:-2px;white-space:nowrap;transition:all .2s}
.tnav.active{color:var(--p3);border-bottom-color:var(--p3)}
.admin-body{max-width:960px;margin:0 auto;padding:18px 13px 60px}
.page{display:none}.page.active{display:block}
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:9px;margin-bottom:16px}
.stat-box{background:#fff;border-radius:14px;padding:12px;text-align:center;border:2px solid var(--p1);box-shadow:var(--shadow)}
.stat-n{font-family:'Nunito',sans-serif;font-size:1.65rem;font-weight:900;margin-bottom:2px}
.stat-l{font-size:.66rem;color:var(--soft);font-weight:600}
.filter-row{display:flex;gap:7px;flex-wrap:wrap;align-items:center;margin-bottom:13px}
.fbtn{padding:6px 13px;border-radius:17px;border:2px solid var(--p1);background:#fff;font-family:inherit;font-size:.72rem;font-weight:700;cursor:pointer;color:var(--soft)}
.fbtn.on{background:var(--p1);color:var(--p3)}
.search-inp{flex:1;min-width:130px;padding:7px 12px;border:2px solid var(--p1);border-radius:17px;font-family:inherit;font-size:.78rem;outline:none;background:#fff}
.order-card{background:#fff;border-radius:15px;padding:14px;margin-bottom:9px;border:2px solid var(--p1);box-shadow:var(--shadow)}
.order-hdr{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:10px;gap:9px;flex-wrap:wrap}
.order-id{font-size:.66rem;color:var(--soft);font-weight:600}
.order-nm{font-family:'Nunito',sans-serif;font-size:.94rem;font-weight:900;color:var(--text);margin-bottom:2px}
.order-ph{font-size:.76rem;color:var(--mid)}
.sbadge{padding:3px 10px;border-radius:16px;font-size:.67rem;font-weight:700;cursor:pointer;border:none;font-family:inherit}
.s-wait{background:#fff5f8;color:var(--p3);border:1.5px solid var(--p1)}
.s-conf{background:#e8f4fd;color:#1a6fa8;border:1.5px solid var(--b2)}
.s-done{background:#e8f8ee;color:#2d7a4a;border:1.5px solid var(--g2)}
.s-cancel{background:#f5f5f5;color:#888;border:1.5px solid #ddd}
.order-body{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:10px}
.ofield{font-size:.76rem;color:var(--mid)}.ofield strong{color:var(--text);font-weight:600}
.sitter-sel{padding:5px 10px;border:2px solid var(--p1);border-radius:9px;font-family:inherit;font-size:.76rem;background:var(--bg);color:var(--text);outline:none;-webkit-appearance:none}
.order-total-row{background:linear-gradient(135deg,var(--p1),var(--y1));border-radius:10px;padding:8px 12px;display:flex;justify-content:space-between;align-items:center}
.otl-lbl{font-size:.76rem;color:var(--p3);font-weight:700}
.otl-num{font-family:'Nunito',sans-serif;font-size:1.2rem;font-weight:900;color:var(--p3)}
.order-notes{margin-top:8px;background:var(--bg);border-radius:9px;padding:8px 11px;font-size:.74rem;color:var(--mid);line-height:1.6;border-left:3px solid var(--p1)}
.order-acts{display:flex;gap:6px;margin-top:9px;flex-wrap:wrap}
.act-btn{padding:5px 11px;border-radius:8px;font-family:inherit;font-size:.68rem;font-weight:700;cursor:pointer;border:none}
.act-conf{background:#e8f4fd;color:#1a6fa8;border:1.5px solid var(--b2)}
.act-done{background:#e8f8ee;color:#2d7a4a;border:1.5px solid var(--g2)}
.act-cancel{background:#fff5f8;color:var(--p3);border:1.5px solid var(--p1)}
.act-del{background:#f5f5f5;color:#888;border:1.5px solid #ddd;margin-left:auto}
.salary-card{background:#fff;border-radius:15px;padding:15px;margin-bottom:11px;border:2px solid var(--p1);box-shadow:var(--shadow)}
.salary-name{font-family:'Nunito',sans-serif;font-size:.98rem;font-weight:900;color:var(--text);margin-bottom:2px}
.salary-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:7px;margin:9px 0}
.sal-box{background:var(--bg);border-radius:10px;padding:9px;text-align:center;border:1.5px solid var(--p1)}
.sal-n{font-family:'Nunito',sans-serif;font-size:1.25rem;font-weight:900;color:var(--p3)}
.sal-l{font-size:.64rem;color:var(--soft);font-weight:600}
.salary-total{background:linear-gradient(135deg,var(--p2),var(--p3));border-radius:10px;padding:10px 13px;display:flex;justify-content:space-between;align-items:center;color:#fff;margin-top:9px}
.sal-total-lbl{font-size:.8rem;font-weight:700}.sal-total-num{font-family:'Nunito',sans-serif;font-size:1.35rem;font-weight:900;color:var(--y1)}
.export-btn{padding:7px 15px;background:linear-gradient(135deg,var(--g1),var(--g2));color:#2d7a4a;border:none;border-radius:9px;font-family:inherit;font-size:.72rem;font-weight:700;cursor:pointer;margin-top:9px}
.month-row{display:flex;gap:8px;align-items:center;margin-bottom:14px;flex-wrap:wrap}
.month-inp{padding:7px 12px;border:2px solid var(--p1);border-radius:11px;font-family:inherit;font-size:.82rem;outline:none;background:#fff}
.calc-btn{padding:7px 16px;background:linear-gradient(135deg,var(--p2),var(--p3));color:#fff;border:none;border-radius:11px;font-family:inherit;font-size:.8rem;font-weight:700;cursor:pointer}
.empty-state{text-align:center;padding:48px 20px;color:var(--soft)}
@media(max-width:520px){.stats-row{grid-template-columns:repeat(2,1fr)}.order-body{grid-template-columns:1fr}.salary-stats{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>

<div class="login-wrap" id="login-wrap">
  <div class="login-box">
    <div class="login-logo">🐾</div>
    <div class="login-title">貓窩裏後台</div>
    <div class="login-sub">管理員請輸入密碼</div>
    <input type="password" id="pw" placeholder="密碼" onkeydown="if(event.key==='Enter')doLogin()">
    <button class="login-btn" onclick="doLogin()">🔐 登入</button>
    <div class="login-err" id="login-err">密碼錯誤，請再試一次</div>
  </div>
</div>

<div class="admin-wrap" id="admin-wrap">
  <div class="admin-hdr">
    <div class="admin-logo">
      <span class="alogo-ic">🐾</span>
      <div><div class="alogo-nm">貓窩裏後台</div><div class="alogo-sb">管理系統</div></div>
    </div>
    <div class="hbtns">
      <button class="hbtn hbtn-blue" onclick="window.open('index.html','_blank')">🌐 前台</button>
      <button class="hbtn" style="background:#fff;color:var(--soft);border:1.5px solid #e8d8dc" onclick="changePW()">🔑 改密碼</button>
      <button class="hbtn hbtn-out" onclick="doLogout()">登出</button>
    </div>
  </div>

  <div class="tab-nav">
    <button class="tnav active" onclick="showPage('orders')">📋 訂單管理</button>
    <button class="tnav" onclick="showPage('salary')">💰 薪水計算</button>
  </div>

  <div class="admin-body">
    <div class="page active" id="page-orders">
      <div class="stats-row">
        <div class="stat-box"><div class="stat-n" id="s-total" style="color:var(--p3)">0</div><div class="stat-l">總訂單</div></div>
        <div class="stat-box"><div class="stat-n" id="s-wait" style="color:#e07000">0</div><div class="stat-l">待處理</div></div>
        <div class="stat-box"><div class="stat-n" id="s-conf" style="color:#1a6fa8">0</div><div class="stat-l">已確認</div></div>
        <div class="stat-box"><div class="stat-n" id="s-done" style="color:#2d7a4a">0</div><div class="stat-l">已完成</div></div>
      </div>
      <div class="filter-row">
        <button class="fbtn on" onclick="setFilter(this,'all')">全部</button>
        <button class="fbtn" onclick="setFilter(this,'待處理')">⏳ 待處理</button>
        <button class="fbtn" onclick="setFilter(this,'已確認')">✅ 已確認</button>
        <button class="fbtn" onclick="setFilter(this,'已完成')">🎉 已完成</button>
        <button class="fbtn" onclick="setFilter(this,'已取消')">❌ 已取消</button>
        <input class="search-inp" id="search-inp" placeholder="🔍 搜尋姓名、電話…" oninput="renderOrders()">
        <button class="fbtn" style="color:var(--p3)" onclick="clearAll()">🗑 清除</button>
      </div>
      <div id="order-list"></div>
    </div>

    <div class="page" id="page-salary">
      <div class="month-row">
        <input type="month" id="salary-month" class="month-inp">
        <button class="calc-btn" onclick="renderSalary()">💰 計算薪水</button>
        <button class="export-btn" onclick="exportAllSalary()">📤 匯出全體薪水明細</button>
      </div>
      <div id="salary-list"></div>
    </div>
  </div>
</div>

<script>
var ADMIN_PW='chch715715';
var SITTERS=['Ying','小汶','菓菓','小茹','阿瑛','未指派'];
var SITTER_RATE={companion:200,walk:140,both:350};
var currentFilter='all';

function doLogin(){
  var pw=document.getElementById('pw').value;
  var saved=localStorage.getItem('ps_admin_pw')||ADMIN_PW;
  if(pw===saved){
    document.getElementById('login-wrap').style.display='none';
    document.getElementById('admin-wrap').style.display='block';
    renderOrders();
  }else{document.getElementById('login-err').style.display='block';}
}
function doLogout(){
  document.getElementById('login-wrap').style.display='flex';
  document.getElementById('admin-wrap').style.display='none';
  document.getElementById('pw').value='';
}
function changePW(){
  var np=prompt('請輸入新密碼（至少6位）');
  if(np&&np.length>=6){localStorage.setItem('ps_admin_pw',np);alert('✅ 密碼已更新！');}
  else if(np!==null)alert('密碼至少6位');
}
function getOrders(){return JSON.parse(localStorage.getItem('ps_orders')||'[]');}
function saveOrders(o){localStorage.setItem('ps_orders',JSON.stringify(o));}

function setFilter(btn,f){
  currentFilter=f;
  document.querySelectorAll('.fbtn').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');renderOrders();
}
function updateStatus(id,status){
  var o=getOrders();o.forEach(x=>{if(x.id===id)x.status=status;});saveOrders(o);renderOrders();
}
function assignSitter(id,sitter){
  var o=getOrders();o.forEach(x=>{if(x.id===id)x.sitter=sitter;});saveOrders(o);renderOrders();
}
function deleteOrder(id){
  if(!confirm('確定要刪除這筆訂單嗎？'))return;
  saveOrders(getOrders().filter(o=>o.id!==id));renderOrders();
}
function clearAll(){
  if(!confirm('確定清除全部訂單？'))return;
  localStorage.removeItem('ps_orders');renderOrders();
}
function cycleStatus(id){
  var cycle=['待處理','已確認','已完成','已取消'];
  var o=getOrders();
  o.forEach(x=>{if(x.id===id){var i=cycle.indexOf(x.status);x.status=cycle[(i+1)%cycle.length];}});
  saveOrders(o);renderOrders();
}

function renderOrders(){
  var orders=getOrders();
  var search=(document.getElementById('search-inp')||{value:''}).value.toLowerCase();
  document.getElementById('s-total').textContent=orders.length;
  document.getElementById('s-wait').textContent=orders.filter(o=>o.status==='待處理').length;
  document.getElementById('s-conf').textContent=orders.filter(o=>o.status==='已確認').length;
  document.getElementById('s-done').textContent=orders.filter(o=>o.status==='已完成').length;

  var filtered=orders.filter(o=>{
    var mf=currentFilter==='all'||o.status===currentFilter;
    var ms=!search||(o.name||'').toLowerCase().includes(search)||(o.phone||'').includes(search);
    return mf&&ms;
  });

  var sc={'待處理':'s-wait','已確認':'s-conf','已完成':'s-done','已取消':'s-cancel'};
  var sem={'待處理':'⏳','已確認':'✅','已完成':'🎉','已取消':'❌'};
  var container=document.getElementById('order-list');

  if(!filtered.length){
    container.innerHTML='<div class="empty-state"><div style="font-size:2.4rem">🐾</div><div style="margin-top:9px">目前沒有符合條件的訂單</div></div>';
    return;
  }

  container.innerHTML=filtered.map(o=>{
    var sc2=sc[o.status]||'s-wait';
    var addonH=o.addons&&o.addons!=='無'?'<div class="ofield"><strong>加購：</strong>'+o.addons+'</div>':'';
    var noteH=o.notes&&o.notes!=='無'?'<div class="order-notes">📝 '+o.notes+'</div>':'';
    var urgH=o.urgent&&o.urgent!=='一般預約'?'<div class="ofield"><strong>急件：</strong><span style="color:var(--p3);font-weight:700">'+o.urgent+'</span></div>':'';
    var sitterSel='<select class="sitter-sel" onchange="assignSitter('+o.id+',this.value)">'+
      SITTERS.map(s=>'<option value="'+s+'"'+(o.sitter===s?' selected':'')+'>'+s+'</option>').join('')+'</select>';
    return '<div class="order-card">'+
      '<div class="order-hdr">'+
        '<div><div class="order-id">訂單 #'+o.id+'　'+o.time+'</div>'+
        '<div class="order-nm">'+o.name+'</div><div class="order-ph">📞 '+o.phone+'</div></div>'+
        '<button class="sbadge '+sc2+'" onclick="cycleStatus('+o.id+')">'+sem[o.status]+' '+o.status+'</button>'+
      '</div>'+
      '<div class="order-body">'+
        '<div class="ofield"><strong>地址：</strong>'+o.address+'</div>'+
        '<div class="ofield"><strong>日期：</strong>'+o.dates+'</div>'+
        '<div class="ofield"><strong>服務：</strong>'+o.service+'，'+o.sessions+'</div>'+
        '<div class="ofield"><strong>寵物：</strong>貓'+o.cats+'隻 狗'+o.dogs+'隻 其他'+o.others+'隻</div>'+
        (o.km&&o.km!=='未填寫'?'<div class="ofield"><strong>距離：</strong>'+o.km+' 公里（車馬費 NT$'+o.travelFee+'）</div>':'')+
        urgH+addonH+
        '<div class="ofield"><strong>指派保姆：</strong>'+sitterSel+'</div>'+
      '</div>'+
      '<div class="order-total-row"><span class="otl-lbl">預估總金額</span><span class="otl-num">NT$'+o.total+'</span></div>'+
      noteH+
      '<div class="order-acts">'+
        '<button class="act-btn act-conf" onclick="updateStatus('+o.id+',\'已確認\')">✅ 確認</button>'+
        '<button class="act-btn act-done" onclick="updateStatus('+o.id+',\'已完成\')">🎉 完成</button>'+
        '<button class="act-btn act-cancel" onclick="updateStatus('+o.id+',\'已取消\')">❌ 取消</button>'+
        '<button class="act-btn act-del" onclick="deleteOrder('+o.id+')">🗑 刪除</button>'+
      '</div></div>';
  }).join('');
}

function getSessAndDays(o){
  var sess=parseInt((o.sessions||'1次').replace(/[^0-9]/g,''))||1;
  var days=parseInt((o.dates||'').match(/共\s*(\d+)\s*天/)?.[1])||1;
  return{sess,days};
}
function calcSitterSalary(name,orders){
  var mine=orders.filter(o=>o.sitter===name&&o.status==='已完成');
  var totalOrders=mine.length;
  var totalSessions=mine.reduce((s,o)=>{var{sess,days}=getSessAndDays(o);return s+sess*days;},0);
  var baseSalary=mine.reduce((s,o)=>{
    var k=o.service==='到府陪伴'?'companion':o.service==='散步服務'?'walk':'both';
    var{sess,days}=getSessAndDays(o);return s+(SITTER_RATE[k]||200)*sess*days;
  },0);
  return{name,orders:mine,totalOrders,totalSessions,baseSalary};
}

function renderSalary(){
  var month=document.getElementById('salary-month').value;
  var orders=getOrders();
  var filtered=month?orders.filter(o=>o.time&&o.time.includes(month.replace('-','/').replace(/^(\d{4})\/0?(\d)$/,'$1/$2'))):orders;
  var activeSitters=SITTERS.filter(s=>s!=='未指派');
  var container=document.getElementById('salary-list');
  var html='';
  activeSitters.forEach(sitter=>{
    var data=calcSitterSalary(sitter,filtered);
    html+='<div class="salary-card">'+
      '<div class="salary-name">'+sitter+'</div>'+
      '<div style="font-size:.72rem;color:var(--soft)">'+(month||'全部時間')+'</div>'+
      '<div class="salary-stats">'+
        '<div class="sal-box"><div class="sal-n" style="color:var(--p3)">'+data.totalOrders+'</div><div class="sal-l">完成訂單</div></div>'+
        '<div class="sal-box"><div class="sal-n" style="color:#1a6fa8">'+data.totalSessions+'</div><div class="sal-l">服務次數</div></div>'+
        '<div class="sal-box"><div class="sal-n" style="color:#2d7a4a">'+data.baseSalary+'</div><div class="sal-l">薪資(NT$)</div></div>'+
      '</div>'+
      '<div class="salary-total"><span class="sal-total-lbl">💰 本期薪水</span><span class="sal-total-num">NT$'+data.baseSalary+'</span></div>'+
      '<button class="export-btn" onclick="exportSalary(\''+sitter+'\',\''+month+'\')">📤 匯出 '+sitter+' 薪水明細</button>'+
    '</div>';
  });
  container.innerHTML=html||'<div class="empty-state"><div style="font-size:2rem">🐾</div><div style="margin-top:8px">請選擇月份後計算</div></div>';
}

function buildSalaryText(sitter,month){
  var orders=getOrders();
  var filtered=month?orders.filter(o=>o.time&&o.time.includes(month.replace('-','/').replace(/^(\d{4})\/0?(\d)$/,'$1/$2'))):orders;
  var data=calcSitterSalary(sitter,filtered);
  var lines=['貓窩裏 ｜ 薪水明細','保姆：'+sitter,'期間：'+(month||'全部'),'完成訂單：'+data.totalOrders+'筆','服務次數：'+data.totalSessions+'次','薪資總計：NT$'+data.baseSalary,''];
  lines.push('── 訂單明細 ──');
  data.orders.forEach((o,i)=>{
    var k=o.service==='到府陪伴'?'companion':o.service==='散步服務'?'walk':'both';
    var{sess,days}=getSessAndDays(o);
    var salPer=(SITTER_RATE[k]||200)*sess*days;
    lines.push('');
    lines.push((i+1)+'. 訂單 #'+o.id+' ('+o.time+')');
    lines.push('   客戶：'+o.name+'  電話：'+o.phone);
    lines.push('   日期：'+o.dates);
    lines.push('   服務：'+o.service+'，'+o.sessions);
    lines.push('   地址：'+o.address);
    if(o.addons&&o.addons!=='無')lines.push('   加購：'+o.addons);
    lines.push('   訂單金額：NT$'+o.total);
    lines.push('   保姆薪資：NT$'+salPer);
  });
  lines.push('');lines.push('本明細由貓窩裏系統自動產生');
  return lines.join('\n');
}
function exportSalary(sitter,month){
  var txt=buildSalaryText(sitter,month);
  var blob=new Blob(['\uFEFF'+txt],{type:'text/plain;charset=utf-8'});
  var url=URL.createObjectURL(blob);var a=document.createElement('a');
  a.href=url;a.download=sitter+'_薪水明細_'+(month||'全部')+'.txt';a.click();URL.revokeObjectURL(url);
}
function exportAllSalary(){
  var month=document.getElementById('salary-month').value;
  var activeSitters=SITTERS.filter(s=>s!=='未指派');
  var all=['貓窩裏 ｜ 全體薪水明細','期間：'+(month||'全部'),'產生時間：'+new Date().toLocaleString('zh-TW'),''];
  activeSitters.forEach(s=>{all.push(buildSalaryText(s,month));all.push('\n═══════════════════\n');});
  var blob=new Blob(['\uFEFF'+all.join('\n')],{type:'text/p.login-logo{font-size:2.5rem;margin-bottom:7px}.login-title{font-family:'Nunito',sans-serif;font-size:1.1rem;font-weight:900;color:var(--p3);margin-bottom:2px}
.login-sub{font-size:.74rem;color:var(--soft);margin-bottom:18px}
.login-box input{width:100%;padding:10px 13px;border:2px solid var(--p1);border-radius:12px;font-family:inherit;font-size:.86rem;outline:none;margin-bottom:9px}
.login-box input:focus{border-color:var(--p2)}
.login-btn{width:100%;padding:11px;background:linear-gradient(135deg,var(--p2),var(--p3));color:#fff;border:none;border-radius:12px;font-family:inherit;font-size:.9rem;font-weight:700;cursor:pointer}
.login-err{font-size:.72rem;color:var(--p3);margin-top:6px;display:none}
.admin-wrap{display:none}
.admin-hdr{background:#fff;padding:12px 18px;display:flex;align-items:center;justify-content:space-between;box-shadow:0 2px 8px rgba(0,0,0,.06);position:sticky;top:0;z-index:50;flex-wrap:wrap;gap:7px;border-bottom:3px dashed var(--p1)}
.admin-logo{display:flex;align-items:center;gap:8px}
.alogo-ic{font-size:1.35rem}.alogo-nm{font-family:'Nunito',sans-serif;font-size:.94rem;font-weight:900;color:var(--p3)}.alogo-sb{font-size:.56rem;color:var(--soft);font-weight:600}
.hbtns{display:flex;gap:6px;flex-wrap:wrap}
.hbtn{padding:6px 12px;border-radius:10px;font-family:inherit;font-size:.7rem;font-weight:700;cursor:pointer;border:none}
.hbtn-pink{background:linear-gradient(135deg,var(--p1),var(--p2));color:var(--p3)}
.hbtn-blue{background:linear-gradient(135deg,var(--b1),var(--b2));color:#1a6fa8}
.hbtn-out{background:#fff;color:var(--soft);border:1.5px solid #e8d8dc}
.tab-nav{display:flex;gap:0;background:#fff;border-bottom:2px solid var(--p1);padding:0 14px;overflow-x:auto}
.tnav{padding:11px 16px;border:none;background:transparent;font-family:inherit;font-size:.76rem;font-weight:700;cursor:pointer;color:var(--soft);border-bottom:3px solid transparent;margin-bottom:-2px;white-space:nowrap;transition:all .2s}
.tnav.active{color:var(--p3);border-bottom-color:var(--p3)}
.admin-body{max-width:960px;margin:0 auto;padding:18px 13px 60px}
.page{display:none}.page.active{display:block}
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:9px;margin-bottom:16px}
.stat-box{background:#fff;border-radius:14px;padding:12px;text-align:center;border:2px solid var(--p1);box-shadow:var(--shadow)}
.stat-n{font-family:'Nunito',sans-serif;font-size:1.65rem;font-weight:900;margin-bottom:2px}
.stat-l{font-size:.66rem;color:var(--soft);font-weight:600}
.filter-row{display:flex;gap:7px;flex-wrap:wrap;align-items:center;margin-bottom:13px}
.fbtn{padding:6px 13px;border-radius:17px;border:2px solid var(--p1);background:#fff;font-family:inherit;font-size:.72rem;font-weight:700;cursor:pointer;color:var(--soft)}
.fbtn.on{background:var(--p1);color:var(--p3)}
.search-inp{flex:1;min-width:130px;padding:7px 12px;border:2px solid var(--p1);border-radius:17px;font-family:inherit;font-size:.78rem;outline:none;background:#fff}
.order-card{background:#fff;border-radius:15px;padding:14px;margin-bottom:9px;border:2px solid var(--p1);box-shadow:var(--shadow)}
.order-hdr{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:10px;gap:9px;flex-wrap:wrap}
.order-id{font-size:.66rem;color:var(--soft);font-weight:600}
.order-nm{font-family:'Nunito',sans-serif;font-size:.94rem;font-weight:900;color:var(--text);margin-bottom:2px}
.order-ph{font-size:.76rem;color:var(--mid)}
.sbadge{padding:3px 10px;border-radius:16px;font-size:.67rem;font-weight:700;cursor:pointer;border:none;font-family:inherit}
.s-wait{background:#fff5f8;color:var(--p3);border:1.5px solid var(--p1)}
.s-conf{background:#e8f4fd;color:#1a6fa8;border:1.5px solid var(--b2)}
.s-done{background:#e8f8ee;color:#2d7a4a;border:1.5px solid var(--g2)}
.s-cancel{background:#f5f5f5;color:#888;border:1.5px solid #ddd}
.order-body{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:10px}
.ofield{font-size:.76rem;color:var(--mid)}.ofield strong{color:var(--text);font-weight:600}
.sitter-sel{padding:5px 10px;border:2px solid var(--p1);border-radius:9px;font-family:inherit;font-size:.76rem;background:var(--bg);color:var(--text);outline:none;-webkit-appearance:none}
.order-total-row{background:linear-gradient(135deg,var(--p1),var(--y1));border-radius:10px;padding:8px 12px;display:flex;justify-content:space-between;align-items:center}
.otl-lbl{font-size:.76rem;color:var(--p3);font-weight:700}
.otl-num{font-family:'Nunito',sans-serif;font-size:1.2rem;font-weight:900;color:var(--p3)}
.order-notes{margin-top:8px;background:var(--bg);border-radius:9px;padding:8px 11px;font-size:.74rem;color:var(--mid);line-height:1.6;border-left:3px solid var(--p1)}
.order-acts{display:flex;gap:6px;margin-top:9px;flex-wrap:wrap}
.act-btn{padding:5px 11px;border-radius:8px;font-family:inherit;font-size:.68rem;font-weight:700;cursor:pointer;border:none}
.act-conf{background:#e8f4fd;color:#1a6fa8;border:1.5px solid var(--b2)}
.act-done{background:#e8f8ee;color:#2d7a4a;border:1.5px solid var(--g2)}
.act-cancel{background:#fff5f8;color:var(--p3);border:1.5px solid var(--p1)}
.act-del{background:#f5f5f5;color:#888;border:1.5px solid #ddd;margin-left:auto}
.salary-card{background:#fff;border-radius:15px;padding:15px;margin-bottom:11px;border:2px solid var(--p1);box-shadow:var(--shadow)}
.salary-name{font-family:'Nunito',sans-serif;font-size:.98rem;font-weight:900;color:var(--text);margin-bottom:2px}
.salary-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:7px;margin:9px 0}
.sal-box{background:var(--bg);border-radius:10px;padding:9px;text-align:center;border:1.5px solid var(--p1)}
.sal-n{font-family:'Nunito',sans-serif;font-size:1.25rem;font-weight:900;color:var(--p3)}
.sal-l{font-size:.64rem;color:var(--soft);font-weight:600}
.salary-total{background:linear-gradient(135deg,var(--p2),var(--p3));border-radius:10px;padding:10px 13px;display:flex;justify-content:space-between;align-items:center;color:#fff;margin-top:9px}
.sal-total-lbl{font-size:.8rem;font-weight:700}.sal-total-num{font-family:'Nunito',sans-serif;font-size:1.35rem;font-weight:900;color:var(--y1)}
.export-btn{padding:7px 15px;background:linear-gradient(135deg,var(--g1),var(--g2));color:#2d7a4a;border:none;border-radius:9px;font-family:inherit;font-size:.72rem;font-weight:700;cursor:pointer;margin-top:9px}
.month-row{display:flex;gap:8px;align-items:center;margin-bottom:14px;flex-wrap:wrap}
.month-inp{padding:7px 12px;border:2px solid var(--p1);border-radius:11px;font-family:inherit;font-size:.82rem;outline:none;background:#fff}
.calc-btn{padding:7px 16px;background:linear-gradient(135deg,var(--p2),var(--p3));color:#fff;border:none;border-radius:11px;font-family:inherit;font-size:.8rem;font-weight:700;cursor:pointer}
.empty-state{text-align:center;padding:48px 20px;color:var(--soft)}
@media(max-width:520px){.stats-row{grid-template-columns:repeat(2,1fr)}.order-body{grid-template-columns:1fr}.salary-stats{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>

<div class="login-wrap" id="login-wrap">
  <div class="login-box">
    <div class="login-logo">🐾</div>
    <div class="login-title">毛孩守護者後台</div>
    <div class="login-sub">管理員請輸入密碼</div>
    <input type="password" id="pw" placeholder="密碼" onkeydown="if(event.key==='Enter')doLogin()">
    <button class="login-btn" onclick="doLogin()">🔐 登入</button>
    <div class="login-err" id="login-err">密碼錯誤，請再試一次</div>
  </div>
</div>

<div class="admin-wrap" id="admin-wrap">
  <div class="admin-hdr">
    <div class="admin-logo">
      <span class="alogo-ic">🐾</span>
      <div><div class="alogo-nm">毛孩守護者後台</div><div class="alogo-sb">管理系統</div></div>
    </div>
    <div class="hbtns">
      <button class="hbtn hbtn-blue" onclick="window.open('index.html','_blank')">🌐 前台</button>
      <button class="hbtn" style="background:#fff;color:var(--soft);border:1.5px solid #e8d8dc" onclick="changePW()">🔑 改密碼</button>
      <button class="hbtn hbtn-out" onclick="doLogout()">登出</button>
    </div>
  </div>

  <div class="tab-nav">
    <button class="tnav active" onclick="showPage('orders')">📋 訂單管理</button>
    <button class="tnav" onclick="showPage('salary')">💰 薪水計算</button>
  </div>

  <div class="admin-body">
    <div class="page active" id="page-orders">
      <div class="stats-row">
        <div class="stat-box"><div class="stat-n" id="s-total" style="color:var(--p3)">0</div><div class="stat-l">總訂單</div></div>
        <div class="stat-box"><div class="stat-n" id="s-wait" style="color:#e07000">0</div><div class="stat-l">待處理</div></div>
        <div class="stat-box"><div class="stat-n" id="s-conf" style="color:#1a6fa8">0</div><div class="stat-l">已確認</div></div>
        <div class="stat-box"><div class="stat-n" id="s-done" style="color:#2d7a4a">0</div><div class="stat-l">已完成</div></div>
      </div>
      <div class="filter-row">
        <button class="fbtn on" onclick="setFilter(this,'all')">全部</button>
        <button class="fbtn" onclick="setFilter(this,'待處理')">⏳ 待處理</button>
        <button class=
