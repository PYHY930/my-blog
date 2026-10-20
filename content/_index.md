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
        <p>分享我喜欢的旋律</p>
    </a>
    <a href="/games/" class="nav-card">
        <div class="icon">🎮</div>
        <h2>游戏</h2>
        <p>把玩一下我制作的交互作品</p>
    </a>
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
</style>

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