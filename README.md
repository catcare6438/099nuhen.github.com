kground:linear-gradient(135deg,var(--p2),var(--p3));color:#fff;border:none;
  border-radius:16px;font-family:'Nunito',sans-serif;font-size:1rem;font-weight:900;
  cursor:pointer;letter-spacing:.06em;
  box-shadow:0 5px 16px rgba(224,80,112,.4),0 2px 0 rgba(160,30,60,.25);
  transition:transform .15s,box-shadow .15s;position:relative}
.submit-btn:hover{transform:translateY(-2px);box-shadow:0 8px 22px rgba(224,80,112,.5)}
.submit-btn:disabled{opacity:.6;cursor:not-allowed;transform:none}

/* 保姆 */
.team-hero{background:linear-gradient(135deg,var(--p1),var(--y1),var(--b1));
  border-radius:var(--r);padding:20px;margin-bottom:16px;text-align:center}
.team-hero h2{font-family:'Nunito',sans-serif;font-size:1.15rem;font-weight:900;color:var(--p3);margin-bottom:4px}
.team-hero p{font-size:.81rem;color:var(--mid);line-height:1.6}
.team-card{background:#fff;border-radius:var(--r);padding:17px;margin-bottom:11px;
  border:2px solid var(--p1);box-shadow:var(--shadow)}
.team-hdr{display:flex;gap:12px;align-items:flex-start;margin-bottom:10px}
.team-av{width:56px;height:56px;border-radius:15px;font-size:1.7rem;
  display:flex;align-items:center;justify-content:center;flex-shrink:0}
.team-name{font-family:'Nunito',sans-serif;font-size:.96rem;font-weight:900;color:var(--text);margin-bottom:3px}
.team-role{font-size:.68rem;font-weight:700;padding:2px 9px;border-radius:18px;display:inline-block;margin-bottom:4px}
.team-bio{font-size:.78rem;color:var(--mid);line-height:1.7}
.cert-row{display:flex;flex-wrap:wrap;gap:5px;margin-top:8px}
.cert{font-size:.66rem;padding:2px 8px;border-radius:11px;font-weight:600}

/* Modal */
.overlay{display:none;position:fixed;inset:0;background:rgba(60,20,40,.45);
  backdrop-filter:blur(6px);align-items:center;justify-content:center;z-index:300;padding:16px}
.overlay.show{display:flex}
.modal{background:#fff;border-radius:22px;padding:28px 22px;max-width:340px;width:100%;
  text-align:center;border:3px solid var(--p1);
  animation:popIn .28s cubic-bezier(.34,1.56,.64,1);max-height:88vh;overflow-y:auto}
@keyframes popIn{from{transform:scale(.82);opacity:0}to{transform:scale(1);opacity:1}}
.modal-icon{font-size:2.8rem;margin-bottom:8px}
.modal h2{font-family:'Nunito',sans-serif;font-size:1.1rem;font-weight:900;color:var(--p3);margin-bottom:8px}
.modal-inner{background:linear-gradient(135deg,rgba(255,183,197,.18),rgba(255,224,163,.12));
  border-radius:13px;padding:12px;margin-bottom:13px}
.modal-hi{font-size:.88rem;font-weight:700;color:var(--p3);margin-bottom:6px}
.modal-detail{font-size:.78rem;color:var(--mid);line-height:1.85;text-align:left}
.modal-btn{padding:10px 24px;background:linear-gradient(135deg,var(--p2),var(--p3));
  color:#fff;border:none;border-radius:13px;font-family:inherit;font-size:.88rem;font-weight:700;cursor:pointer}

@media(max-width:520px){
  .row2{grid-template-columns:1fr}
  .svc-grid{grid-template-columns:1fr 1fr}
  .urgent-row{grid-template-columns:1fr}
  .hero h1{font-size:1.5rem}
  .km-row{flex-direction:column}
  .gmap-btn{width:100%;justify-content:center}
  .pet-row{grid-template-columns:1fr 1fr}
}
</style>
</head>
<body>

<div class="hdr">
  <div class="logo">
    <div class="logo-circle">🐾</div>
    <div>
      <div class="logo-text">貓窩裏</div>
      <div class="logo-sub">到府寵物保姆</div>
    </div>
  </div>
  <div class="nav-tabs">
    <button class="ntab active" onclick="showTab('booking')">🗓 預約</button>
    <button class="ntab" onclick="showTab('team')">👩‍⚕️ 保姆</button>
  </div>
</div>

<!-- ══ 預約 ══ -->
<div class="sec active" id="tab-booking">
  <div class="hero">
    <span class="deco" style="top:14px;left:6%;font-size:1.3rem">🐱</span>
    <span class="deco" style="top:30px;right:8%;font-size:1.2rem">🐶</span>
    <span class="deco" style="bottom:6px;left:46%;font-size:1rem">🐾</span>
    <span class="hero-emoji">🏠💕</span>
    <h1>讓毛孩在家<br>也有人陪伴</h1>
    <p class="hero-sub">專業保姆到府服務 · 安心出門不擔心</p>
  </div>

  <!-- 基本資料 -->
  <div class="card">
    <div class="sec-lbl">📋 飼主資料</div>
    <div class="row2">
      <div class="fgroup">
        <label class="fl">姓名 *</label>
        <input type="text" id="name" placeholder="請輸入姓名">
        <div class="err" id="err-name">⚠ 請填寫姓名</div>
      </div>
      <div class="fgroup">
        <label class="fl">聯絡電話 *</label>
        <input type="tel" id="phone" placeholder="09XX-XXX-XXX">
        <div class="err" id="err-phone">⚠ 請填寫電話</div>
      </div>
    </div>
    <div class="fgroup">
      <label class="fl">服務地址 *</label>
      <input type="text" id="address" placeholder="請輸入完整地址">
      <div class="err" id="err-address">⚠ 請填寫地址</div>
    </div>
  </div>

  <!-- 日期 -->
  <div class="card">
    <div class="sec-lbl">📅 預約日期</div>
    <div class="cal-wrap">
      <div class="cal-header">
        <button class="cal-nav" onclick="calPrev()">‹</button>
        <div class="cal-title" id="cal-title"></div>
        <button class="cal-nav" onclick="calNext()">›</button>
      </div>
      <div class="cal-grid" id="cal-grid"></div>
    </div>
    <div class="cal-info" id="cal-info">請點選開始日期</div>
    <div class="err" id="err-date" style="margin-top:5px">⚠ 請選擇預約日期</div>
    <div class="fgroup" style="margin-top:13px">
      <label class="fl">每天服務次數</label>
      <div class="session-row">
        <button class="ssbtn active" onclick="setSess(this,1)">1次</button>
        <button class="ssbtn" onclick="setSess(this,2)">2次</button>
        <button class="ssbtn" onclick="setSess(this,3)">3次</button>
        <button class="ssbtn" onclick="setSess(this,4)">4次</button>
      </div>
    </div>
  </div>

  <!-- 急件 -->
  <div class="card">
    <div class="sec-lbl">⚡ 急件加收</div>
    <div class="urgent-row">
      <button class="urgbtn sel-none" onclick="setUrgent(this,'none',0)">
        <div class="urglbl">一般預約</div><div class="urgsub">48小時前</div>
        <div class="urgprice" style="color:#2d7a50">免加收</div>
      </button>
      <button class="urgbtn" onclick="setUrgent(this,'48',100)">
        <div class="urglbl">⚡ 急件</div><div class="urgsub">48小時內</div>
        <div class="urgprice" style="color:#8a5000">+NT$100</div>
      </button>
      <button class="urgbtn" onclick="setUrgent(this,'24',200)">
        <div class="urglbl">🔥 緊急</div><div class="urgsub">24小時內</div>
        <div class="urgprice" style="color:var(--p3)">+NT$200</div>
      </button>
    </div>
  </div>

  <!-- 寵物 -->
  <div class="card">
    <div class="sec-lbl">🐾 寵物資訊</div>
    <div class="fgroup">
      <label class="fl">寵物名字</label>
      <input type="text" id="petname" placeholder="例：小花、球球">
    </div>
    <div class="pet-row">
      <div class="petbox">
        <div class="pet-em">🐱</div><div class="pet-nm">貓咪</div>
        <div class="count-ctrl">
          <button class="cbtn" onclick="chgPet('cat',-1)">−</button>
          <div class="cnum" id="cnt-cat">0</div>
          <button class="cbtn" onclick="chgPet('cat',1)">+</button>
        </div>
      </div>
      <div class="petbox">
        <div class="pet-em">🐶</div><div class="pet-nm">狗狗</div>
        <div class="count-ctrl">
          <button class="cbtn" onclick="chgPet('dog',-1)">−</button>
          <div class="cnum" id="cnt-dog">0</div>
          <button class="cbtn" onclick="chgPet('dog',1)">+</button>
        </div>
      </div>
      <div class="petbox">
        <div class="pet-em">🐾</div><div class="pet-nm">其他</div>
        <div class="count-ctrl">
          <button class="cbtn" onclick="chgPet('other',-1)">−</button>
          <div class="cnum" id="cnt-other">0</div>
          <button class="cbtn" onclick="chgPet('other',1)">+</button>
        </div>
      </div>
    </div>
    <div id="extra-note" style="display:none;margin-top:9px;background:linear-gradient(135deg,#fff5f8,#ffe8ef);border:1.5px solid var(--p1);border-radius:11px;padding:8px 12px;font-size:.76rem;color:var(--p3);font-weight:600">
      🐾 第三隻起加收：<span id="extra-text"></span>
    </div>
  </div>

  <!-- 主要服務 -->
  <div class="card">
    <div class="sec-lbl">✨ 主要服務</div>
    <div class="svc-grid">
      <div class="svcbtn active" id="svc-companion" onclick="setSvc('companion')">
        <div class="svc-icon">🏠</div><div class="svc-name">到府陪伴</div><div class="svc-price">NT$300/次</div>
      </div>
      <div class="svcbtn" id="svc-walk" onclick="setSvc('walk')">
        <div class="svc-icon">🦮</div><div class="svc-name">散步服務</div><div class="svc-price">NT$200/次</div>
      </div>
      <div class="svcbtn" id="svc-both" onclick="setSvc('both')">
        <div class="svc-icon">🏠🦮</div><div class="svc-name">陪伴＋遛狗</div><div class="svc-price">NT$500/次</div>
      </div>
    </div>
    <div style="background:var(--cream);border-radius:11px;padding:10px 12px;font-size:.75rem;color:var(--mid);line-height:1.7">
      🏠 到府陪伴：餵食、清潔、陪玩、觀察身體狀況<br>🦮 散步服務：陪同外出散步、如廁
    </div>
  </div>

  <!-- 加購 -->
  <div class="card">
    <div class="sec-lbl">➕ 加購服務（每天計費）</div>
    <div class="addon-list">
      <div class="addon-item" onclick="togAddon(this,'medicine_oral')"><div class="addon-chk">✓</div><div class="addon-name">💊 餵藥（口服）</div><div class="addon-price">+NT$50/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'medicine_eye')"><div class="addon-chk">✓</div><div class="addon-name">👁 點藥（眼藥/耳藥）</div><div class="addon-price">+NT$50/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'massage')"><div class="addon-chk">✓</div><div class="addon-name">🤲 寵物舒緩按摩</div><div class="addon-price">+NT$100/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'nails')"><div class="addon-chk">✓</div><div class="addon-name">✂️ 剪指甲</div><div class="addon-price">+NT$80/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'mail')"><div class="addon-chk">✓</div><div class="addon-name">📬 收信</div><div class="addon-price">+NT$30/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'water')"><div class="addon-chk">✓</div><div class="addon-name">🌱 澆花</div><div class="addon-price">+NT$30/天</div></div>
      <div cla      
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>貓窩裏｜到府寵物保姆預約</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&family=Nunito:wght@700;800;900&display=swap" rel="stylesheet">
<style>
:root{
  --p1:#FFB7C5;--p2:#FF8FAB;--p3:#E05070;
  --y1:#FFE0A3;--y2:#FFD07A;
  --b1:#B8E4FF;--b2:#7DC8F5;
  --g1:#B8F0C8;--g2:#7DD99A;
  --lav:#D4B8FF;
  --cream:#FFF9F5;--warm:#FFF0F5;
  --text:#3D2B35;--mid:#7A5C68;--soft:#B08A9A;
  --shadow:0 4px 20px rgba(224,80,112,.1);
  --r:18px;
}
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Noto Sans TC',sans-serif;background:var(--warm);color:var(--text);min-height:100vh;overflow-x:hidden}
body::before{content:'';position:fixed;inset:0;background:
  radial-gradient(circle at 10% 20%,rgba(255,183,197,.15) 0%,transparent 50%),
  radial-gradient(circle at 90% 10%,rgba(184,228,255,.12) 0%,transparent 50%),
  radial-gradient(circle at 50% 90%,rgba(184,240,200,.1) 0%,transparent 50%);
  pointer-events:none;z-index:0}

.hdr{position:sticky;top:0;z-index:100;background:rgba(255,249,245,.93);backdrop-filter:blur(12px);
  border-bottom:3px dashed var(--p1);padding:12px 20px;
  display:flex;align-items:center;justify-content:space-between}
.logo{display:flex;align-items:center;gap:10px}
.logo-circle{width:42px;height:42px;border-radius:50%;background:linear-gradient(135deg,var(--p2),var(--p1));
  display:flex;align-items:center;justify-content:center;font-size:1.3rem;
  box-shadow:3px 3px 0 rgba(224,80,112,.2)}
.logo-text{font-family:'Nunito',sans-serif;font-size:1.05rem;font-weight:900;color:var(--p3);line-height:1.1}
.logo-sub{font-size:.58rem;color:var(--soft);font-weight:600;letter-spacing:.1em}
.nav-tabs{display:flex;gap:4px}
.ntab{padding:7px 13px;border-radius:20px;border:2px solid transparent;font-family:inherit;
  font-size:.74rem;font-weight:700;cursor:pointer;background:transparent;color:var(--mid);transition:all .2s}
.ntab.active{background:var(--p1);border-color:var(--p2);color:var(--p3)}

.sec{display:none;position:relative;z-index:1;max-width:760px;margin:0 auto;padding:20px 16px 80px}
.sec.active{display:block}

.hero{text-align:center;padding:28px 16px 22px;position:relative}
.hero-emoji{font-size:3.2rem;display:block;margin-bottom:8px}
.hero h1{font-family:'Nunito',sans-serif;font-size:1.75rem;font-weight:900;color:var(--p3);line-height:1.25;margin-bottom:6px}
.hero-sub{font-size:.84rem;color:var(--mid);line-height:1.6}
.deco{position:absolute;opacity:.2;pointer-events:none}

.card{background:#fff;border-radius:var(--r);padding:18px;margin-bottom:14px;
  box-shadow:var(--shadow);border:2px solid var(--p1);position:relative;overflow:hidden}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;
  background:linear-gradient(90deg,var(--p1),var(--y1),var(--b1),var(--g1))}
.sec-lbl{font-family:'Nunito',sans-serif;font-size:.92rem;font-weight:900;color:var(--p3);
  margin-bottom:13px;display:flex;align-items:center;gap:7px}
.sec-lbl::after{content:'';flex:1;border-bottom:2px dashed var(--p1)}

label.fl{display:block;font-size:.76rem;font-weight:700;color:var(--mid);margin-bottom:4px}
input[type=text],input[type=tel],input[type=number],textarea,select{
  width:100%;padding:10px 13px;border:2px solid var(--p1);border-radius:13px;
  font-family:inherit;font-size:.85rem;color:var(--text);background:var(--cream);
  outline:none;transition:border-color .2s;-webkit-appearance:none}
input:focus,textarea:focus,select:focus{border-color:var(--p2);box-shadow:0 0 0 3px rgba(255,143,171,.12)}
textarea{resize:vertical;min-height:68px}
.fgroup{margin-bottom:12px}.fgroup:last-child{margin-bottom:0}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:11px}
.err{font-size:.7rem;color:#d03;margin-top:3px;display:none}
.err-inp{border-color:#f88!important}

/* 日曆 */
.cal-wrap{background:var(--cream);border:2px solid var(--p1);border-radius:13px;padding:13px}
.cal-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:11px}
.cal-title{font-family:'Nunito',sans-serif;font-weight:900;font-size:.92rem;color:var(--p3)}
.cal-nav{width:28px;height:28px;border-radius:50%;border:2px solid var(--p1);background:#fff;
  font-size:.95rem;cursor:pointer;display:flex;align-items:center;justify-content:center;color:var(--p3)}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:2px;text-align:center}
.cal-dow{font-size:.62rem;font-weight:700;color:var(--soft);padding:2px 0}
.cal-day{padding:5px 2px;border-radius:9px;font-size:.78rem;cursor:pointer;transition:all .15s;
  border:2px solid transparent;font-weight:600;color:var(--mid)}
.cal-day:hover:not(.empty):not(.past){background:var(--p1);color:var(--p3)}
.cal-day.empty,.cal-day.past{cursor:default}
.cal-day.past{color:#ddd}
.cal-day.start{background:var(--p2);color:#fff;border-color:var(--p3)}
.cal-day.end{background:var(--p3);color:#fff}
.cal-day.inrange{background:var(--p1);color:var(--p3)}
.cal-day.today{border-color:var(--p2)}
.cal-info{margin-top:9px;background:linear-gradient(135deg,var(--p1),var(--y1));
  border-radius:10px;padding:8px 12px;font-size:.78rem;color:var(--p3);font-weight:700;text-align:center}

.session-row{display:flex;gap:7px;flex-wrap:wrap;margin-top:6px}
.ssbtn{padding:7px 15px;border-radius:18px;border:2px solid var(--p1);background:#fff;
  font-family:inherit;font-size:.78rem;font-weight:700;cursor:pointer;color:var(--mid);transition:all .2s}
.ssbtn.active{background:var(--p2);border-color:var(--p3);color:#fff}

.urgent-row{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px}
.urgbtn{padding:10px 6px;border-radius:13px;border:2px solid var(--p1);background:#fff;
  font-family:inherit;cursor:pointer;text-align:center;transition:all .2s}
.urgbtn.sel-none{border-color:var(--g2);background:#f0fff6}
.urgbtn.sel-48{border-color:var(--y2);background:#fffbf0}
.urgbtn.sel-24{border-color:var(--p2);background:#fff5f8}
.urglbl{font-size:.76rem;font-weight:700;color:var(--text)}
.urgsub{font-size:.64rem;color:var(--soft);margin:1px 0}
.urgprice{font-size:.72rem;font-weight:700}

.svc-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:9px;margin-bottom:11px}
.svcbtn{padding:13px 7px;border-radius:15px;border:2.5px solid var(--p1);background:#fff;
  cursor:pointer;text-align:center;transition:all .2s;font-family:inherit}
.svcbtn.active{border-color:var(--p2);background:linear-gradient(135deg,#fff5f8,#ffe8ef);
  box-shadow:0 3px 10px rgba(224,80,112,.15)}
.svc-icon{font-size:1.4rem;margin-bottom:3px}
.svc-name{font-size:.76rem;font-weight:700;color:var(--text);line-height:1.3}
.svc-price{font-size:.7rem;font-weight:700;color:var(--p2);margin-top:2px}

.pet-row{display:grid;grid-template-columns:1fr 1fr 1fr;gap:9px}
.petbox{background:var(--cream);border:2px solid var(--p1);border-radius:13px;padding:11px;text-align:center}
.pet-em{font-size:1.5rem;margin-bottom:3px}
.pet-nm{font-size:.7rem;font-weight:700;color:var(--mid);margin-bottom:5px}
.count-ctrl{display:flex;align-items:center;justify-content:center;
  border:2px solid var(--p1);border-radius:11px;overflow:hidden;width:fit-content;margin:0 auto}
.cbtn{width:30px;height:30px;border:none;background:var(--p1);color:var(--p3);
  font-size:1rem;cursor:pointer;font-weight:900;font-family:inherit}
.cnum{width:34px;height:30px;line-height:30px;text-align:center;font-weight:900;
  font-size:.92rem;color:var(--p3);background:#fff;border-left:2px solid var(--p1);border-right:2px solid var(--p1)}

.addon-list{display:flex;flex-direction:column;gap:7px}
.addon-item{display:flex;align-items:center;gap:10px;padding:10px 12px;
  border:2px solid var(--p1);border-radius:12px;cursor:pointer;background:#fff;
  transition:all .2s;user-select:none}
.addon-item.on{border-color:var(--g2);background:linear-gradient(135deg,#f0fff8,#e6fff2)}
.addon-chk{width:20px;height:20px;border-radius:6px;flex-shrink:0;
  border:2px solid var(--p1);background:#fff;display:flex;align-items:center;
  justify-content:center;color:#fff;font-size:.7rem;font-weight:700;transition:all .2s}
.addon-item.on .addon-chk{background:var(--g2);border-color:var(--g2)}
.addon-name{font-size:.84rem;font-weight:600;color:var(--text);flex:1}
.addon-price{font-size:.74rem;font-weight:700;color:var(--p2)}

.km-row{display:flex;gap:8px;align-items:flex-end}
.km-inp{flex:1}
.gmap-btn{padding:10px 12px;border:2px solid var(--b2);border-radius:13px;
  background:linear-gradient(135deg,var(--b1),var(--b2));color:#1a6fa8;
  font-family:inherit;font-size:.76rem;font-weight:700;cursor:pointer;
  white-space:nowrap;flex-shrink:0;text-decoration:none;display:inline-flex;align-items:center;gap:4px}
.km-res{margin-top:7px;border-radius:11px;padding:9px 12px;font-size:.78rem;line-height:1.6}
.km-free{background:#f0fff6;border:1.5px solid var(--g2);color:#2d7a50}
.km-fee{background:#fffbf0;border:1.5px solid var(--y2);color:#8a5000}

.price-box{background:linear-gradient(135deg,var(--p2),var(--p3) 55%,#c04060);
  border-radius:var(--r);padding:20px;margin-bottom:16px;color:#fff;
  box-shadow:0 6px 22px rgba(224,80,112,.3)}
.price-ttl{font-size:.8rem;opacity:.85;margin-bottom:13px;font-weight:700;letter-spacing:.06em}
.price-line{display:flex;justify-content:space-between;padding:5px 0;
  border-bottom:1px solid rgba(255,255,255,.13);font-size:.82rem}
.price-line.sub{padding-left:12px;font-size:.74rem;opacity:.76}
.price-total-row{display:flex;justify-content:space-between;align-items:center;
  padding-top:13px;margin-top:5px;border-top:2px solid rgba(255,255,255,.28)}
.price-total-lbl{font-weight:700;font-size:.9rem}
.price-total-num{font-family:'Nunito',sans-serif;font-size:1.9rem;font-weight:900;color:var(--y1)}

.note-box{background:rgba(255,183,197,.15);border:1.5px solid var(--p1);border-radius:13px;
  padding:10px 14px;font-size:.76rem;color:var(--mid);line-height:1.8;margin-bottom:16px}

.submit-btn{width:100%;padding:16px;
  background:linear-gradient(135deg,var(--p2),var(--p3));color:#fff;border:none;
  border-radius:16px;font-family:'Nunito',sans-serif;font-size:1rem;font-weight:900;
  cursor:pointer;letter-spacing:.06em;
  box-shadow:0 5px 16px rgba(224,80,112,.4),0 2px 0 rgba(160,30,60,.25);
  transition:transform .15s,box-shadow .15s;position:relative}
.submit-btn:hover{transform:translateY(-2px);box-shadow:0 8px 22px rgba(224,80,112,.5)}
.submit-btn:disabled{opacity:.6;cursor:not-allowed;transform:none}

/* 保姆 */
.team-hero{background:linear-gradient(135deg,var(--p1),var(--y1),var(--b1));
  border-radius:var(--r);padding:20px;margin-bottom:16px;text-align:center}
.team-hero h2{font-family:'Nunito',sans-serif;font-size:1.15rem;font-weight:900;color:var(--p3);margin-bottom:4px}
.team-hero p{font-size:.81rem;color:var(--mid);line-height:1.6}
.team-card{background:#fff;border-radius:var(--r);padding:17px;margin-bottom:11px;
  border:2px solid var(--p1);box-shadow:var(--shadow)}
.team-hdr{display:flex;gap:12px;align-items:flex-start;margin-bottom:10px}
.team-av{width:56px;height:56px;border-radius:15px;font-size:1.7rem;
  display:flex;align-items:center;justify-content:center;flex-shrink:0}
.team-name{font-family:'Nunito',sans-serif;font-size:.96rem;font-weight:900;color:var(--text);margin-bottom:3px}
.team-role{font-size:.68rem;font-weight:700;padding:2px 9px;border-radius:18px;display:inline-block;margin-bottom:4px}
.team-bio{font-size:.78rem;color:var(--mid);line-height:1.7}
.cert-row{display:flex;flex-wrap:wrap;gap:5px;margin-top:8px}
.cert{font-size:.66rem;padding:2px 8px;border-radius:11px;font-weight:600}

/* Modal */
.overlay{display:none;position:fixed;inset:0;background:rgba(60,20,40,.45);
  backdrop-filter:blur(6px);align-items:center;justify-content:center;z-index:300;padding:16px}
.overlay.show{display:flex}
.modal{background:#fff;border-radius:22px;padding:28px 22px;max-width:340px;width:100%;
  text-align:center;border:3px solid var(--p1);
  animation:popIn .28s cubic-bezier(.34,1.56,.64,1);max-height:88vh;overflow-y:auto}
@keyframes popIn{from{transform:scale(.82);opacity:0}to{transform:scale(1);opacity:1}}
.modal-icon{font-size:2.8rem;margin-bottom:8px}
.modal h2{font-family:'Nunito',sans-serif;font-size:1.1rem;font-weight:900;color:var(--p3);margin-bottom:8px}
.modal-inner{background:linear-gradient(135deg,rgba(255,183,197,.18),rgba(255,224,163,.12));
  border-radius:13px;padding:12px;margin-bottom:13px}
.modal-hi{font-size:.88rem;font-weight:700;color:var(--p3);margin-bottom:6px}
.modal-detail{font-size:.78rem;color:var(--mid);line-height:1.85;text-align:left}
.modal-btn{padding:10px 24px;background:linear-gradient(135deg,var(--p2),var(--p3));
  color:#fff;border:none;border-radius:13px;font-family:inherit;font-size:.88rem;font-weight:700;cursor:pointer}

@media(max-width:520px){
  .row2{grid-template-columns:1fr}
  .svc-grid{grid-template-columns:1fr 1fr}
  .urgent-row{grid-template-columns:1fr}
  .hero h1{font-size:1.5rem}
  .km-row{flex-direction:column}
  .gmap-btn{width:100%;justify-content:center}
  .pet-row{grid-template-columns:1fr 1fr}
}
</style>
</head>
<body>

<div class="hdr">
  <div class="logo">
    <div class="logo-circle">🐾</div>
    <div>
      <div class="logo-text">貓窩裏</div>
      <div class="logo-sub">到府寵物保姆</div>
    </div>
  </div>
  <div class="nav-tabs">
    <button class="ntab active" onclick="showTab('booking')">🗓 預約</button>
    <button class="ntab" onclick="showTab('team')">👩‍⚕️ 保姆</button>
  </div>
</div>

<!-- ══ 預約 ══ -->
<div class="sec active" id="tab-booking">
  <div class="hero">
    <span class="deco" style="top:14px;left:6%;font-size:1.3rem">🐱</span>
    <span class="deco" style="top:30px;right:8%;font-size:1.2rem">🐶</span>
    <span class="deco" style="bottom:6px;left:46%;font-size:1rem">🐾</span>
    <span class="hero-emoji">🏠💕</span>
    <h1>讓毛孩在家<br>也有人陪伴</h1>
    <p class="hero-sub">專業保姆到府服務 · 安心出門不擔心</p>
  </div>

  <!-- 基本資料 -->
  <div class="card">
    <div class="sec-lbl">📋 飼主資料</div>
    <div class="row2">
      <div class="fgroup">
        <label class="fl">姓名 *</label>
        <input type="text" id="name" placeholder="請輸入姓名">
        <div class="err" id="err-name">⚠ 請填寫姓名</div>
      </div>
      <div class="fgroup">
        <label class="fl">聯絡電話 *</label>
        <input type="tel" id="phone" placeholder="09XX-XXX-XXX">
        <div class="err" id="err-phone">⚠ 請填寫電話</div>
      </div>
    </div>
    <div class="fgroup">
      <label class="fl">服務地址 *</label>
      <input type="text" id="address" placeholder="請輸入完整地址">
      <div class="err" id="err-address">⚠ 請填寫地址</div>
    </div>
  </div>

  <!-- 日期 -->
  <div class="card">
    <div class="sec-lbl">📅 預約日期</div>
    <div class="cal-wrap">
      <div class="cal-header">
        <button class="cal-nav" onclick="calPrev()">‹</button>
        <div class="cal-title" id="cal-title"></div>
        <button class="cal-nav" onclick="calNext()">›</button>
      </div>
      <div class="cal-grid" id="cal-grid"></div>
    </div>
    <div class="cal-info" id="cal-info">請點選開始日期</div>
    <div class="err" id="err-date" style="margin-top:5px">⚠ 請選擇預約日期</div>
    <div class="fgroup" style="margin-top:13px">
      <label class="fl">每天服務次數</label>
      <div class="session-row">
        <button class="ssbtn active" onclick="setSess(this,1)">1次</button>
        <button class="ssbtn" onclick="setSess(this,2)">2次</button>
        <button class="ssbtn" onclick="setSess(this,3)">3次</button>
        <button class="ssbtn" onclick="setSess(this,4)">4次</button>
      </div>
    </div>
  </div>

  <!-- 急件 -->
  <div class="card">
    <div class="sec-lbl">⚡ 急件加收</div>
    <div class="urgent-row">
      <button class="urgbtn sel-none" onclick="setUrgent(this,'none',0)">
        <div class="urglbl">一般預約</div><div class="urgsub">48小時前</div>
        <div class="urgprice" style="color:#2d7a50">免加收</div>
      </button>
      <button class="urgbtn" onclick="setUrgent(this,'48',100)">
        <div class="urglbl">⚡ 急件</div><div class="urgsub">48小時內</div>
        <div class="urgprice" style="color:#8a5000">+NT$100</div>
      </button>
      <button class="urgbtn" onclick="setUrgent(this,'24',200)">
        <div class="urglbl">🔥 緊急</div><div class="urgsub">24小時內</div>
        <div class="urgprice" style="color:var(--p3)">+NT$200</div>
      </button>
    </div>
  </div>

  <!-- 寵物 -->
  <div class="card">
    <div class="sec-lbl">🐾 寵物資訊</div>
    <div class="fgroup">
      <label class="fl">寵物名字</label>
      <input type="text" id="petname" placeholder="例：小花、球球">
    </div>
    <div class="pet-row">
      <div class="petbox">
        <div class="pet-em">🐱</div><div class="pet-nm">貓咪</div>
        <div class="count-ctrl">
          <button class="cbtn" onclick="chgPet('cat',-1)">−</button>
          <div class="cnum" id="cnt-cat">0</div>
          <button class="cbtn" onclick="chgPet('cat',1)">+</button>
        </div>
      </div>
      <div class="petbox">
        <div class="pet-em">🐶</div><div class="pet-nm">狗狗</div>
        <div class="count-ctrl">
          <button class="cbtn" onclick="chgPet('dog',-1)">−</button>
          <div class="cnum" id="cnt-dog">0</div>
          <button class="cbtn" onclick="chgPet('dog',1)">+</button>
        </div>
      </div>
      <div class="petbox">
        <div class="pet-em">🐾</div><div class="pet-nm">其他</div>
        <div class="count-ctrl">
          <button class="cbtn" onclick="chgPet('other',-1)">−</button>
          <div class="cnum" id="cnt-other">0</div>
          <button class="cbtn" onclick="chgPet('other',1)">+</button>
        </div>
      </div>
    </div>
    <div id="extra-note" style="display:none;margin-top:9px;background:linear-gradient(135deg,#fff5f8,#ffe8ef);border:1.5px solid var(--p1);border-radius:11px;padding:8px 12px;font-size:.76rem;color:var(--p3);font-weight:600">
      🐾 第三隻起加收：<span id="extra-text"></span>
    </div>
  </div>

  <!-- 主要服務 -->
  <div class="card">
    <div class="sec-lbl">✨ 主要服務</div>
    <div class="svc-grid">
      <div class="svcbtn active" id="svc-companion" onclick="setSvc('companion')">
        <div class="svc-icon">🏠</div><div class="svc-name">到府陪伴</div><div class="svc-price">NT$300/次</div>
      </div>
      <div class="svcbtn" id="svc-walk" onclick="setSvc('walk')">
        <div class="svc-icon">🦮</div><div class="svc-name">散步服務</div><div class="svc-price">NT$200/次</div>
      </div>
      <div class="svcbtn" id="svc-both" onclick="setSvc('both')">
        <div class="svc-icon">🏠🦮</div><div class="svc-name">陪伴＋遛狗</div><div class="svc-price">NT$500/次</div>
      </div>
    </div>
    <div style="background:var(--cream);border-radius:11px;padding:10px 12px;font-size:.75rem;color:var(--mid);line-height:1.7">
      🏠 到府陪伴：餵食、清潔、陪玩、觀察身體狀況<br>🦮 散步服務：陪同外出散步、如廁
    </div>
  </div>

  <!-- 加購 -->
  <div class="card">
    <div class="sec-lbl">➕ 加購服務（每天計費）</div>
    <div class="addon-list">
      <div class="addon-item" onclick="togAddon(this,'medicine_oral')"><div class="addon-chk">✓</div><div class="addon-name">💊 餵藥（口服）</div><div class="addon-price">+NT$50/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'medicine_eye')"><div class="addon-chk">✓</div><div class="addon-name">👁 點藥（眼藥/耳藥）</div><div class="addon-price">+NT$50/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'massage')"><div class="addon-chk">✓</div><div class="addon-name">🤲 寵物舒緩按摩</div><div class="addon-price">+NT$100/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'nails')"><div class="addon-chk">✓</div><div class="addon-name">✂️ 剪指甲</div><div class="addon-price">+NT$80/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'mail')"><div class="addon-chk">✓</div><div class="addon-name">📬 收信</div><div class="addon-price">+NT$30/天</div></div>
      <div class="addon-item" onclick="togAddon(this,'water')"><div class="addon-chk">✓</div><div class="addon-name">🌱 澆花</div><div class="addon-price">+NT$30/天</div></div>
      <div cla
