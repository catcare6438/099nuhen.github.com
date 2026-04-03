<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>浪貓不浪 🐾</title>
    <style>
        :root { --p: #ff8fab; --bg: #fffcfd; --text: #444; }
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background: var(--bg); margin: 0; padding-bottom: 85px; }
        header { background: white; padding: 20px; text-align: center; border-bottom: 1px solid #eee; position: sticky; top: 0; z-index: 100; }
        header h1 { margin: 0; font-size: 1.4rem; color: var(--p); letter-spacing: 1px; }
        
        /* 雙欄位貓咪列表 */
        .container { padding: 15px; display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; }
        .card { background: white; border-radius: 20px; overflow: hidden; box-shadow: 0 4px 12px rgba(0,0,0,0.05); border: 1px solid #f0f0f0; transition: 0.2s; }
        .card:active { transform: scale(0.95); }
        .card img { width: 100%; height: 160px; object-fit: cover; background: #f9f9f9; }
        .card-body { padding: 12px; text-align: center; }
        .card h3 { margin: 0; font-size: 1rem; color: #333; }
        .card p { font-size: 0.8rem; color: #999; margin-top: 4px; }
        /* 底部導覽列 */
        .bottom-nav { position: fixed; bottom: 0; left: 0; width: 100%; height: 70px; background: rgba(255,255,255,0.95); backdrop-filter: blur(10px); display: flex; justify-content: space-around; align-items: center; border-top: 1px solid #eee; z-index: 1000; }
        .nav-item { background: none; border: none; color: #bbb; font-size: 0.75rem; cursor: pointer; display: flex; flex-direction: column; align-items: center; width: 33%; transition: 0.3s; }
        .nav-item.active { color: var(--p); font-weight: bold; }
        .nav-icon { font-size: 1.5rem; margin-bottom: 2px; }
        /* 彈窗樣式 */
        .overlay { display: none; position: fixed; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.6); z-index: 2000; align-items: flex-end; }
        .modal { background: white; width: 100%; padding: 30px 20px; border-radius: 30px 30px 0 0; box-sizing: border-box; animation: slideUp 0.3s ease; }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        .btn-main { width: 100%; padding: 15px; border-radius: 25px; border: none; background: var(--p); color: white; font-weight: bold; font-size: 1rem; margin-top: 15px; }
        .loading { text-align: center; padding: 100px 0; color: var(--p); grid-column: 1/-1; }
    </style>
</head>
<body>
<header><h1>🐾 浪貓不浪</h1></header>
<div id="display-area" class="container">
    <div class="loading">正在同步雲端資料...</div>
</div>
<nav class="bottom-nav">
    <button class="nav-item active" onclick="switchTab('waiting', this)">
        <span class="nav-icon">🏠</span>等家孩子
    </button>
    <button class="nav-item" onclick="switchTab('adopted', this)">
        <span class="nav-icon">🎊</span>幸福生活
    </button>
    <button class="nav-item" onclick="openLogin()">
        <span class="nav-icon">🔐</span>系統登入
    </button>
</nav>
<div id="modalOverlay" class="overlay" onclick="closeModal()">
    <div class="modal" onclick="event.stopPropagation()">
        <div id="modalContent"></div>
    </div>
</div>
<script>
    // 請將這些替換成您自己的 Google Sheets "發佈到網路" 的 CSV 連結！
    // 範例：https://docs.google.com/spreadsheets/d/e/2PACX-1vR-your-long-id-here/pub?output=csv
    const WAITING_CSV = "https://docs.google.com/spreadsheets/d/e/2PACX-1vQf9OqXlWv4V8F0qS1J_Z-Y0R5L7L5X-3f_0T9J2C-2d3s7a0o7p2g8k4c6h1m9/pub?output=csv"; // 這是測試用的範例連結，請替換
    const ADOPTED_CSV = "https://docs.google.com/spreadsheets/d/e/2PACX-1vQf9OqXlWv4V8F0qS1J_Z-Y0R5L7L5X-3f_0T9J2C-2d3s7a0o7p2g8k4c6h1m9/pub?output=csv"; // 這是測試用的範例連結，請替換
    
    let allCats = [];

    async function loadData(type) {
        const display = document.getElementById('display-area');
        display.innerHTML = '<div class="loading">抓取最新檔案中...</div>';
        const url = (type === 'waiting') ? WAITING_CSV : ADOPTED_CSV;
        
        if (!url || url.includes("your-long-id-here")) { // 檢查是否還是預設的或無效的連結
            display.innerHTML = '<div class="loading" style="color:orange">請在程式碼中設定正確的 Google Sheet CSV 連結！</div>';
            return;
        }

        try {
            const response = await fetch(url + '&cache=' + Date.now());
            if (!response.ok) { // 檢查 HTTP 響應狀態
                throw new Error(`HTTP 錯誤狀態: ${response.status} - 連結可能無效`);
            }
            const csvText = await response.text();
            
            // 簡易 CSV 解析邏輯
            const rows = csvText.split(/\r?\n/).filter(row => row.trim() !== "");
            allCats = [];
            let html = "";

            if (rows.length <= 1) { // 只有標題行或完全空白
                display.innerHTML = '<div class="loading">目前沒有任何貓咪資料。</div>';
                return;
            }

            // 跳過第一行標題
            for (let i = 1; i < rows.length; i++) {
                // 處理可能包含引號或逗號的內容
                // 這個 regex 適用於 Google Sheet 導出的 CSV，如果內容有逗號會被雙引號包起來
                const cols = rows[i].split(/,(?=(?:(?:[^"]*"){2})*[^"]*$)/);
                
                // 檢查是否有足夠的列，防止索引超出範圍
                if (cols.length < 6) { // 至少需要 6 列 (時間戳, 姓名, 年齡, 性別, 介紹, 圖片網址)
                    console.warn(`跳過無效行: ${rows[i]}`);
                    continue; 
                }

                const cat = {
                    name: cols[1]?.replace(/"/g, "").trim() || "無名貓", // 姓名在第2列 (索引1)
                    age: cols[2]?.replace(/"/g, "").trim() || "未知年齡", // 年齡在第3列 (索引2)
                    desc: cols[4]?.replace(/"/g, "").trim() || "這孩子還沒有詳細介紹喔。", // 介紹在第5列 (索引4)
                    img: cols[5]?.replace(/"/g, "").trim() || "https://placehold.co/400x300?text=圖片載入中" // 圖片網址在第6列 (索引5)
                };
                allCats.push(cat);
                html += `
                    <div class="card" onclick="viewDetails('${cat.name.replace(/'/g, "\\'")}')">
                        <img src="${cat.img}" onerror="this.src='https://placehold.co/400x300?text=照片迷路了'">
                        <div class="card-body">
                            <h3>${cat.name}</h3>
                            <p>${cat.age}</p>
                        </div>
                    </div>`;
            }
            display.innerHTML = html || '<div class="loading">目前沒有資料。</div>';
        } catch (error) {
            console.error("載入資料失敗:", error);
            display.innerHTML = `<div class="loading" style="color:red">連線失敗或資料解析錯誤：<br>${error.message}</div>`;
        }
    }

    function switchTab(type, btn) {
        document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        btn.classList.add('active');
        loadData(type);
    }

    function viewDetails(name) {
        const cat = allCats.find(c => c.name === name);
        if(!cat) {
            alert('找不到該貓咪的詳細資料！');
            return;
        }
        document.getElementById('modalContent').innerHTML = `
            <h2 style="color:var(--p); text-align:center; margin-top:0;">${cat.name}</h2>
            <img src="${cat.img}" style="width:100%; border-radius:20px; margin-bottom:15px;" onerror="this.src='https://placehold.co/400x400?text=圖片載入中'">
            <p style="font-size:0.95rem; line-height:1.6; color:#666;">${cat.desc}</p>
            <button class="btn-main" onclick="window.open('https://line.me/R/msg/text/?你好，我想詢問貓咪：${cat.name}')">💬 LINE 聯繫中途</button>
        `;
        document.getElementById('modalOverlay').style.display = 'flex';
    }

    function openLogin() {
        document.getElementById('modalContent').innerHTML = `
            <h2 style="text-align:center; margin-top:0;">系統管理</h2>
            <input type="text" placeholder="管理員帳號" style="width:100%; padding:15px; margin-bottom:12px; border:1px solid #eee; border-radius:12px; box-sizing:border-box;">
            <input type="password" placeholder="密碼" style="width:100%; padding:15px; margin-bottom:12px; border:1px solid #eee; border-radius:12px; box-sizing:border-box;">
            <button class="btn-main" onclick="alert('請設定 GAS_URL 後啟用')">登入</button>
        `;
        document.getElementById('modalOverlay').style.display = 'flex';
    }

    function closeModal() { document.getElementById('modalOverlay').style.display = 'none'; }
    
    // 初始化讀取等家貓咪
    window.onload = () => loadData('waiting');
</script>
</body>
</html>
