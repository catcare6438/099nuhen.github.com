<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>毛孩守護者｜後台管理</title>
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
