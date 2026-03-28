<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>毛孩守護者貓窩裏｜到府寵物保姆預約</title>
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
  background:linea
