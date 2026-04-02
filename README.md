<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>浪貓不浪 🐾 官方網站</title>
    <style>
        :root { --p: #ff8fab; --bg: #fff6f8; --h: #ffd1dc; --b: #a2d2ff; --dark: #555; }
        body { font-family: "Microsoft JhengHei", sans-serif; background: var(--bg); margin: 0; color: var(--dark); line-height: 1.6; }
        header { background: var(--h); padding: 40px 15px; text-align: center; border-radius: 0 0 40px 40px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
        h1 { margin: 0; color: #d63384; font-size: 2.2rem; letter-spacing: 2px; }
        .nav { margin-top: 20px; display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; }
        .btn { padding: 12px 24px; border-radius: 30px; border: none; cursor: pointer; font-weight: bold; transition: 0.3s; font-size: 15px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-m { background: var(--p); color: white; }
        .btn-s { background: var(--b); color: white; }
        .btn:hover { transform: translateY(-3px); filter: brightness(1.1); box-shadow: 0 6px 12px rgba(0,0,0,0.15); }
        .container { padding: 30px 15px; display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 25px; max-width: 1200px; margin: 0 auto; }
        .card { background: white; border-radius: 25px; overflow: hidden; box-shadow: 0 10px 25px rgba(0,0,0,0.08); transition: 0.3s; text-align: center; }
        .card img { width: 100%; height: 260px; object-fit: cover; cursor: pointer; border-bottom: 5px solid var(--h); }
        .card-body { padding: 20px; }
        .overlay { display: none; position: fixed; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.8); z-index: 1000; align-items: center; justify-content: center; backdrop-filter: blur(8px); }
        .modal { background: white; width: 90%; max-width: 480px; padding: 30px; border-radius: 30px; position: relative; max-height: 85vh; overflow-y: auto; }
        .close-btn { position: absolute; top: 15px; right: 20px; font-size: 30px; cursor: pointer; color: #ddd; }
        .form-group input, .form-group textarea { width: 100%; box-sizing: border-box; margin-bottom: 15px; padding: 14px; border-radius: 18px; border: 1px solid #eee; background: #fdfdfd; font-size: 15px; }
        footer { text-align: center; padding: 60px 20px; opacity: 0.7; font-size: 13px; }
        .loading { grid-column: 1/-1; text-align: center; padding: 50px; font-size: 1.2rem; color: var(--p); }
    </style>
</head>
<body>

<header>
    <h1>🐾 浪貓不浪</h1>
    <p>讓愛延續，讓每一隻貓咪都擁有溫暖的家</p>
    <div class="nav">
        <button class="btn btn-m" onclick="loadCats('waiting')">🏠 正在等家</button>
        <button class="btn btn-m" onclick="loadCats('adopted')">🎊 幸福回娘家</button>
        <button class="btn btn-s" onclick="openAuthModal()">🔐 系統登入</button>
    </div>
</header>

<div id="display-area" class="container">
    <div class="loading">正在讀取雲端檔案...</div>
</div>

<div id="modalOverlay" class="overlay">
    <div class="modal">
        <span class="close-btn" onclick="closeModal()">&times;</span>
        <h2 id="modalTitle" style="color: var(--p); text-align: center; margin-top: 0;"></h2>
        <div id="modalBody" class="form-group"></div>
    </div>
</div>

<footer>🐾 貓窩裏 到府寵物褓姆 💕</footer>

<script>
    /** --- 核心數據配置 --- **/
    const WAITING_CSV = "https://docs.google.com/spreadsheets/d/e/2PACX-1vTf9z00p3CAs7W9W3N34oO07uNfVcl4tVcl4vVcl/pub?output=csv"; 
    const ADOPTED_CSV = "https://docs.google.com/spreadsheets/d/e/2PACX-1vR_xX1L_O1X3_Y7W9N6P07_X9oO7P6J1_Jcl6ZJ/pub?output=csv";
    const GAS_URL = "在此填入你的GAS部署網址"; 
    const ADMIN_CODE = "715715";

    let catsData = [];

    async function loadCats(type) {
        const display = document.getElementById('display-area');
        display.innerHTML = '<div class="loading">同步最新紀錄中...</div>';
        const url = (type === 'waiting') ? WAITING_CSV : ADOPTED_CSV;

        try {
            const res = await fetch(url);
            const csv = await res.text();
            const rows = csv.split('\n').slice(1);
            catsData = [];
            let html = "";

            rows.forEach(row => {
                const col = row.split(',').map(c => c.trim());
                if (col.length < 2) return;
                
                // 針對兩份表結構做自動適應抓取
                const name = col[1] || "神秘貓咪";
                const age = col[2] || "不詳";
                const desc = col[4] || "還沒有自我介紹。";
                const img = col[5] || "https://placehold.co/400x300?text=圖片載入中";
                
                catsData.push({ name, age, desc, img });

                html += `
                    <div class="card">
                        <img src="${img}" onclick="viewDetails('${name}')" onerror="this.src='https://placehold.co/400x300?text=喵~照片迷路了'">
                        <div class="card-body">
                            <h3>${name}</h3>
                            <p>${age}</p>
                            <button class="btn btn-s" style="width:100%" onclick="viewDetails('${name}')">查看近況</button>
                        </div>
                    </div>`;
            });
            display.innerHTML = html || '<div class="loading">目前暫無貓咪紀錄。</div>';
        } catch (e) { 
            display.innerHTML = '<div class="loading">讀取失敗，請確認試算表已設為發佈 CSV。</div>'; 
        }
    }

    function openAuthModal() {
        showModal("系統登入", `
            <input type="text" id="loginUser" placeholder="帳號 (管理員或貓咪姓名)">
            <input type="password" id="loginPwd" placeholder="請輸入密碼">
            <button class="btn btn-m" style="width:100%" onclick="handleLogin()">進入後台</button>
        `);
    }

    function handleLogin() {
        const user = document.getElementById('loginUser').value.trim();
        const pwd = document.getElementById('loginPwd').value.trim();
        if (user === "admin" && pwd === ADMIN_CODE) { showAdminPanel(); } 
        else if (pwd === user + "715") { showOwnerPanel(user); } 
        else { alert("資訊不正確喔！"); }
    }

    function showAdminPanel() {
        showModal("管理員後台", `
            <input id="fName" placeholder="貓咪姓名">
            <input id="fAge" placeholder="年齡/性別">
            <input id="fImg" placeholder="主要照片 URL">
            <textarea id="fDesc" placeholder="故事內容..." rows="4"></textarea>
            <button class="btn btn-m" style="width:100%" onclick="sendData()">發佈新資訊</button>
        `);
    }

    function showOwnerPanel(name) {
        showModal(`${name} 家長專屬`, `
            <input id="fImg" placeholder="新照片網址 (URL)">
            <textarea id="fDesc" placeholder="跟大家分享 ${name} 的近況吧！" rows="4"></textarea>
            <button class="btn btn-s" style="width:100%" onclick="sendData('daily', '${name}')">送出回娘家分享</button>
        `);
    }

    async function sendData(type = 'new', name = "") {
        const payload = {
            action: type,
            name: name || document.getElementById('fName').value,
            img: document.getElementById('fImg').value,
            desc: document.getElementById('fDesc').value,
            age: document.getElementById('fAge')?.value || "",
            pwd: ADMIN_CODE
        };
        alert("資料同步中，請稍候...");
        try {
            await fetch(GAS_URL, { method: "POST", mode: "no-cors", body: JSON.stringify(payload) });
            alert("同步成功！雲端更新需約 1 分鐘。"); closeModal(); loadCats('waiting');
        } catch (e) { alert("發送失敗，請檢查網址。"); }
    }

    function showModal(t, b) {
        document.getElementById('modalOverlay').style.display = 'flex';
        document.getElementById('modalTitle').innerText = t;
        document.getElementById('modalBody').innerHTML = b;
    }
    function closeModal() { document.getElementById('modalOverlay').style.display = 'none'; }
    function viewDetails(name) {
        const cat = catsData.find(c => c.name === name);
        if(!cat) return;
        showModal(`${name} 的故事`, `
            <img src="${cat.img}" style="width:100%; border-radius:20px; margin-bottom:15px;" onerror="this.src='https://placehold.co/400x300?text=圖片載入中'">
            <p><b>年齡：</b>${cat.age}</p>
            <p><b>簡介：</b><br>${cat.desc}</p>
            <button class="btn btn-m" style="width:100%; margin-top:15px;" onclick="window.open('https://line.me/R/msg/text/?你好，我想詢問：${name}')">💬 透過 LINE 聯繫中途</button>
        `);
    }

    window.onload = () => loadCats('waiting');
</script>
</body>
</html>
