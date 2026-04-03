<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>浪貓不浪 🐾 官方 App</title>
    <style>
        :root { --p: #ff8fab; --bg: #fffcfd; --card: #ffffff; }
        body { font-family: -apple-system, sans-serif; background: var(--bg); margin: 0; padding-bottom: 90px; color: #444; }
        header { background: white; padding: 20px; text-align: center; border-bottom: 1px solid #eee; position: sticky; top: 0; z-index: 100; }
        header h1 { margin: 0; font-size: 1.25rem; color: var(--p); letter-spacing: 2px; }
        
        .container { padding: 15px; display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .card { background: var(--card); border-radius: 20px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.05); border: 1px solid #f5f5f5; transition: 0.2s; }
        .card:active { transform: scale(0.96); }
        .card img { width: 100%; height: 150px; object-fit: cover; background: #eee; }
        .card-body { padding: 12px; text-align: center; }
        .card-body h3 { margin: 0; font-size: 0.95rem; font-weight: 600; }
        .card-body p { margin: 5px 0 0; font-size: 0.75rem; color: #999; }

        .nav { position: fixed; bottom: 0; left: 0; width: 100%; height: 75px; background: rgba(255,255,255,0.9); backdrop-filter: blur(10px); display: flex; justify-content: space-around; align-items: center; border-top: 1px solid #eee; z-index: 1000; }
        .nav-btn { background: none; border: none; color: #ccc; font-size: 0.7rem; display: flex; flex-direction: column; align-items: center; cursor: pointer; }
        .nav-btn.active { color: var(--p); font-weight: bold; }
        .nav-icon { font-size: 1.6rem; margin-bottom: 3px; }

        .overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 2000; align-items: flex-end; }
        .modal { background: white; width: 100%; border-radius: 30px 30px 0 0; padding: 30px 20px; box-sizing: border-box; animation: slideUp 0.3s; max-height: 85vh; overflow-y: auto; }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        
        input, textarea { width: 100%; padding: 15px; margin-bottom: 15px; border: 1px solid #eee; border-radius: 15px; box-sizing: border-box; font-size: 1rem; background: #f9f9f9; }
        .btn-action { width: 100%; padding: 16px; border-radius: 25px; border: none; background: var(--p); color: white; font-weight: bold; font-size: 1rem; box-shadow: 0 4px 10px rgba(255,143,171,0.3); }
        .loading { grid-column: 1/-1; text-align: center; padding: 80px 20px; color: var(--p); font-weight: 500; }
    </style>
</head>
<body>

<header><h1>🐾 浪貓不浪</h1></header>

<div id="display-area" class="container">
    <div class="loading">正在連線雲端資料庫...</div>
</div>

<nav class="nav">
    <button class="nav-btn active" onclick="switchTab('waiting', this)"><span class="nav-icon">🏠</span>等家孩子</button>
    <button class="nav-btn" onclick="switchTab('adopted', this)"><span class="nav-icon">🎊</span>幸福生活</button>
    <button class="nav-btn" onclick="openLogin()"><span class="nav-icon">⚙️</span>系統管理</button>
</nav>

<div id="overlay" class="overlay" onclick="closeModal()">
    <div class="modal" onclick="event.stopPropagation()" id="modal-content"></div>
</div>

<script>
    // 您的專屬 GAS 網址
    const GAS_URL = "https://script.google.com/macros/s/AKfycbxT_924TOVaiZc7-fEu0gITRgLZNvWmDwJn8xnTg75tcLmPD0eXOanYffdKBYphlvrX/exec";
    let catCache = [];

    async function loadData(type) {
        const area = document.getElementById('display-area');
        area.innerHTML = '<div class="loading">同步最新貓咪資訊...</div>';
        try {
            const res = await fetch(`${GAS_URL}?type=${type}`);
            catCache = await res.json();
            let html = "";
            catCache.forEach(cat => {
                html += `
                <div class="card" onclick="showInfo('${cat.name}')">
                    <img src="${cat.img}" onerror="this.src='https://placehold.co/400x300?text=照片讀取中'">
                    <div class="card-body">
                        <h3>${cat.name}</h3>
                        <p>${cat.age}</p>
                    </div>
                </div>`;
            });
            area.innerHTML = html || '<div class="loading">目前沒有資料喔！</div>';
        } catch (e) {
            area.innerHTML = '<div class="loading" style="color:red">連線失敗，請稍後再試。</div>';
        }
    }

    function switchTab(type, btn) {
        document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        loadData(type);
    }

    function showInfo(name) {
        const cat = catCache.find(c => c.name === name);
        document.getElementById('modal-content').innerHTML = `
            <h2 style="margin:0 0 15px; color:var(--p); text-align:center;">${cat.name}</h2>
            <img src="${cat.img}" style="width:100%; border-radius:20px; margin-bottom:15px;">
            <p style="color:#666; line-height:1.6; font-size:0.95rem;">${cat.desc || '這孩子還沒有詳細介紹。'}</p>
            <button class="btn-action" onclick="window.open('https://line.me/R/msg/text/?你好，我想詢問：${cat.name}')">💬 LINE 聯繫中途</button>
            <p style="text-align:center; color:#ccc; margin-top:20px; font-size:0.8rem;" onclick="closeModal()">點擊空白處關閉</p>
        `;
        document.getElementById('overlay').style.display = 'flex';
    }

    function openLogin() {
        document.getElementById('modal-content').innerHTML = `
            <h2 style="margin:0 0 20px; text-align:center;">後台管理</h2>
            <input type="text" id="u" placeholder="管理員帳號">
            <input type="password" id="p" placeholder="密碼">
            <button class="btn-action" onclick="doLogin()">確認進入</button>
        `;
        document.getElementById('overlay').style.display = 'flex';
    }

    function doLogin() {
        const u = document.getElementById('u').value;
        const p = document.getElementById('p').value;
        if(u === 'admin' && p === '715715') {
            document.getElementById('modal-content').innerHTML = `
                <h2 style="margin:0 0 20px; text-align:center;">新增貓咪</h2>
                <input id="n" placeholder="貓咪姓名"><input id="a" placeholder="年齡 / 性別"><input id="i" placeholder="照片 URL"><textarea id="d" placeholder="貓咪故事" rows="4"></textarea>
                <button class="btn-action" onclick="submitCat()">發佈到雲端</button>
            `;
        } else { alert('帳密錯誤'); }
    }

    async function submitCat() {
        const data = { action: 'new', pwd: '715715', name: document.getElementById('n').value, age: document.getElementById('a').value, img: document.getElementById('i').value, desc: document.getElementById('d').value };
        if(!data.name) return alert('姓名必填');
        alert('正在同步到試算表...');
        await fetch(GAS_URL, { method: 'POST', body: JSON.stringify(data) });
        alert('上傳成功！');
        location.reload();
    }

    function closeModal() { document.getElementById('overlay').style.display = 'none'; }
    window.onload = () => loadData('waiting');
</script>
</body>
</html>
