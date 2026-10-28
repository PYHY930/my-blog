---
title: "Home"
layout: "single"
---

<style>
/* 1. 暴力去掉最外层丑陋的卡片框（背景、阴影、边框） */
.post-single {
    background: transparent !important;
    border: none !important;
    box-shadow: none !important;
    padding: 0 !important;
    margin-top: 0 !important;
}

/* 2. 隐藏上面多余的 "Home" 标题、日期、作者等 */
.post-header {
    display: none !important;
}

/* 3. 隐藏底部的分享按钮（叉叉、领英那些） */
.post-footer {
    display: none !important;
}

/* 4. 调整三个卡片的布局 */
.home-grid {
    display: flex;
    justify-content: center;
    gap: 25px;
    margin: 80px auto;
    max-width: 900px;
    flex-wrap: wrap; 
}

/* 卡片本身的样式（保持之前的毛玻璃效果） */
.nav-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 220px;
    padding: 40px 20px;
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    text-decoration: none !important;
    color: var(--primary);
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.nav-card:hover {
    transform: translateY(-10px);
    background: rgba(255, 255, 255, 0.1);
    border-color: var(--primary);
    box-shadow: 0 10px 25px rgba(255, 255, 255, 0.15);
}

.nav-card .icon {
    font-size: 48px;
    margin-bottom: 15px;
}

.nav-card h2 {
    margin: 0 0 10px 0;
    font-size: 24px;
    font-weight: bold;
}

.nav-card p {
    margin: 0;
    font-size: 14px;
    color: var(--secondary);
    text-align: center;
}
</style>

<div class="home-grid">
    <a href="/posts/" class="nav-card">
        <div class="icon">📝</div>
        <h2>文章</h2>
        <p>记录技术与生活的点滴</p>
    </a>
    <a href="/music/" class="nav-card">
        <div class="icon">🎵</div>
        <h2>音乐</h2>
        <p>放松一下</p>
    </a>
    <a href="/games/" class="nav-card">
        <div class="icon">🎮</div>
        <h2>游戏</h2>
        <p>把玩一下我们制作的交互作品</p>
    </a>
    <!-- 👇 新增的书单卡片 -->
    <a href="/study/" class="nav-card" onclick="return checkPassword(event)">
        <div class="icon" style="position: relative; display: inline-block;">
            📚
            <!-- 右上角悬浮一个锁图标 -->
            <span style="position: absolute; top: -10px; right: -15px; font-size: 24px; text-shadow: 0 0 10px rgba(255,0,0,0.5);">🔒</span>
        </div>
        <h2>资料</h2>
        <!-- 带锁的相册卡片 -->
    <a href="/photos/" class="nav-card" onclick="return checkPhotosPassword(event)">
        <div class="icon" style="position: relative; display: inline-block;">
            📷
            <!-- 右上角悬浮一个锁图标 -->
            <span style="position: absolute; top: -10px; right: -15px; font-size: 24px; text-shadow: 0 0 10px rgba(255,0,0,0.5);">🔒</span>
        </div>
        <h2>相册</h2>
        <p>一些抽象照片</p>
    </a>
</div>
<!-- 更新日志方框 -->
<div class="update-log-box">
    <h3>📅 更新日志</h3>
    <div class="log-content">
        <ul class="update-list">
            <li><span class="date">2026-10-23</span> 加入新板块：相册</li>
            <li><span class="date">2026-10-22</span> 加入AI助手（deepseek），但由于经费不足，AI目前无法正常使用</li>
            <li><span class="date">2026-10-21</span> 修改文章建立时间，作者等显示</li>
            <li><span class="date">2026-10-21</span> 增设新板块，并实现在线浏览文档</li>
            <li><span class="date">2026-10-21</span> 更新日志框改为固定高度，支持内部滚轮翻阅。</li>
            <li><span class="date">2026-10-21</span> 更新日志上线。</li>
            <li><span class="date">2026-10-20</span> 优化了主页 UI，增加了毛玻璃特效和三大导航版块。</li>
            <li><span class="date">2026-10-19</span> 成功部署上线！加入了俄罗斯方块小游戏和音乐播放器。</li>
            <li><span class="date">2026-10-18</span> 绑定专属域名</li>
            <li><span class="date">2026-10-18</span> 完成 Hugo 博客的基础搭建。</li>
            <li><span class="date">2026-10-18</span> 注册并购买了新域名。</li>
            <!-- 以后在这里继续添加新的 <li> 即可 -->
        </ul>
    </div>
</div>
</div>

<div style="text-align: right; margin: 50px 20px 20px 0;">
    <button id="danger-btn" style="background: transparent; border: none; color: #555; font-size: 12px; cursor: pointer; outline: none; transition: color 0.3s;" onmouseover="this.style.color='#ff3333'" onmouseout="this.style.color='#555'">别点我</button>
</div>

<div id="missile-modal" style="display: none; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background-color: rgba(0, 0, 0, 0.95); z-index: 9999; justify-content: center; align-items: center; flex-direction: column;">
    <img src="/images/missile.jpg" alt="敌导弹" style="max-width: 80vw; max-height: 70vh; animation: pulse 1s infinite alternate;">
    <p style="color: #00ff00; font-size: 20px; font-family: monospace; margin-top: 20px; text-shadow: 0 0 10px #00ff00; text-align: center;">⚠️ WARNING: MISSILE INBOUND ⚠️</p>
    <button id="close-btn" style="margin-top: 20px; padding: 8px 16px; background: #333; color: #fff; border: 2px solid #fff; cursor: pointer; border-radius: 5px;">解除警报</button>
</div>

<style>
    @keyframes pulse { 0% { transform: scale(0.95); opacity: 0.8; } 100% { transform: scale(1.05); opacity: 1; } }
   /* 更新日志方框外壳 */
.update-log-box {
    max-width: 900px;
    margin: 0 auto 50px auto;
    padding: 30px;
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
}

.update-log-box h3 {
    margin-top: 0;
    margin-bottom: 15px;
    font-size: 20px;
    color: var(--primary);
    text-align: center;
    border-bottom: 1px solid rgba(255,255,255,0.1);
    padding-bottom: 15px;
    flex-shrink: 0; /* 保证标题永远不会被压缩 */
}

/* 滚轮区域（关键部分） */
.log-content {
    height: 200px; /* 👈 这里控制方框的固定高度，你可以改成 150px 或 250px */
    overflow-y: auto; /* 纵向超出时显示滚动条 */
    padding-right: 10px; /* 给滚动条留一点空隙 */
}

/* 美化滚动条 (Webkit 内核浏览器，如 Chrome, Edge, Safari) */
.log-content::-webkit-scrollbar {
    width: 6px; /* 滚动条非常细 */
}
.log-content::-webkit-scrollbar-track {
    background: transparent; 
}
.log-content::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.2); /* 半透明的滚动条 */
    border-radius: 10px;
}
.log-content::-webkit-scrollbar-thumb:hover {
    background: rgba(255, 255, 255, 0.4);
}

.update-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.update-list li {
    margin-bottom: 15px;
    font-size: 15px;
    color: var(--secondary);
    display: flex;
    align-items: flex-start;
    line-height: 1.6;
}

.update-list li:last-child {
    margin-bottom: 0;
}

.update-list .date {
    font-family: monospace;
    background: rgba(0, 255, 0, 0.1);
    color: #00ff00; 
    padding: 2px 8px;
    border-radius: 4px;
    margin-right: 15px;
    font-size: 13px;
    white-space: nowrap;
}

/* 手机端适配 */
@media (max-width: 768px) {
    .update-log-box {
        margin: 20px;
        padding: 20px;
    }
    .log-content {
        height: 180px; /* 手机端高度稍微降低一点 */
    }
    .update-list li {
        flex-direction: column;
    }
    .update-list .date {
        margin-bottom: 5px;
    }
}
</style>
<script>
// 资料板块的密码验证
function checkPassword(e) {
    if (sessionStorage.getItem('studyUnlocked') === 'true') return true;
    const pwd = prompt("该资料区已加密，请输入密码解锁：");
    const correctPwd = "930308602"; // 你资料的真实密码
    if (pwd === correctPwd) { 
        sessionStorage.setItem('studyUnlocked', 'true');
        return true;
    } else {
        if (pwd !== null) alert("密码错误！禁止访问。");
        e.preventDefault(); return false;
    }
}

// 👇 新增：相册板块的密码验证
function checkPhotosPassword(e) {
    // 如果已经解锁过，直接放行
    if (sessionStorage.getItem('photosUnlocked') === 'true') return true;

    const pwd = prompt("请输入相册密码查看照片：");
    const correctPwd = "930308602"; // 👈 在这里设置你的相册密码

    if (pwd === correctPwd) { 
        sessionStorage.setItem('photosUnlocked', 'true');
        return true; 
    } else {
        if (pwd !== null) alert("密码错误！禁止访问。");
        e.preventDefault(); 
        return false;
    }
}
</script>
<script>
document.addEventListener("DOMContentLoaded", function() {
    const btn = document.getElementById('danger-btn'); const modal = document.getElementById('missile-modal'); const closeBtn = document.getElementById('close-btn'); let clickTimes = [];
    btn.addEventListener('click', function() { const now = Date.now(); clickTimes.push(now); clickTimes = clickTimes.filter(time => now - time <= 2000); if (clickTimes.length >= 5) { triggerMissile(); clickTimes = []; } });
    function triggerMissile() { modal.style.display = 'flex'; playSiren(); }
    closeBtn.addEventListener('click', function() { modal.style.display = 'none'; });
    function playSiren() {
        try {
            const AudioContext = window.AudioContext || window.webkitAudioContext; const ctx = new AudioContext(); const osc1 = ctx.createOscillator(); const osc2 = ctx.createOscillator(); const gainNode = ctx.createGain();
            osc1.type = 'sawtooth'; osc2.type = 'square'; gainNode.gain.setValueAtTime(0, ctx.currentTime); gainNode.gain.linearRampToValueAtTime(0.15, ctx.currentTime + 0.1);
            for (let i = 0; i < 5; i++) { osc1.frequency.setValueAtTime(400, ctx.currentTime + (i * 1.5)); osc1.frequency.linearRampToValueAtTime(800, ctx.currentTime + (i * 1.5) + 0.75); osc2.frequency.setValueAtTime(405, ctx.currentTime + (i * 1.5)); osc2.frequency.linearRampToValueAtTime(805, ctx.currentTime + (i * 1.5) + 0.75); }
            osc1.connect(gainNode); osc2.connect(gainNode); gainNode.connect(ctx.destination); osc1.start(); osc2.start(); setTimeout(() => { osc1.stop(); osc2.stop(); }, 5000);
        } catch (e) {}
    }
});
</script>