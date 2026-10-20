---
title: "Home"
layout: "list"
---

<!-- 极其隐蔽的触发文字（靠右对齐，暗灰色小字） -->
<div style="text-align: right; margin: 50px 20px 20px 0;">
    <button id="danger-btn" style="background: transparent; border: none; color: #555; font-size: 12px; cursor: pointer; outline: none; transition: color 0.3s;" onmouseover="this.style.color='#ff3333'" onmouseout="this.style.color='#555'">
        别点我
    </button>
</div>

<!-- 彩蛋全屏遮罩层 (默认隐藏) -->
<div id="missile-modal" style="display: none; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background-color: rgba(0, 0, 0, 0.95); z-index: 9999; justify-content: center; align-items: center; flex-direction: column;">
    <!-- 注意：如果图片是 jpg 结尾，请把这里的 png 改成 jpg -->
    <img src="/images/missile.jpg" alt="敌导弹" style="max-width: 80vw; max-height: 70vh; animation: pulse 1s infinite alternate;">
    <p style="color: #00ff00; font-size: 20px; font-family: monospace; margin-top: 20px; text-shadow: 0 0 10px #00ff00; text-align: center;">⚠️ WARNING: MISSILE INBOUND ⚠️</p>
    <button id="close-btn" style="margin-top: 20px; padding: 8px 16px; background: #333; color: #fff; border: 2px solid #fff; cursor: pointer; border-radius: 5px;">解除警报</button>
</div>

<!-- 动画效果 CSS -->
<style>
    @keyframes pulse {
        0% { transform: scale(0.95); opacity: 0.8; }
        100% { transform: scale(1.05); opacity: 1; }
    }
</style>

<!-- 点击逻辑与警报声 JavaScript -->
<script>
document.addEventListener("DOMContentLoaded", function() {
    const btn = document.getElementById('danger-btn');
    const modal = document.getElementById('missile-modal');
    const closeBtn = document.getElementById('close-btn');
    let clickTimes = []; // 记录点击的时间戳

    // 点击逻辑
    btn.addEventListener('click', function() {
        const now = Date.now();
        clickTimes.push(now);

        // 过滤掉 2 秒之前的点击记录
        clickTimes = clickTimes.filter(time => now - time <= 2000);

        // 如果 2 秒内点击了 5 次
        if (clickTimes.length >= 5) {
            triggerMissile();
            clickTimes = []; // 清空记录，防止重复触发
        }
    });

    // 触发彩蛋
    function triggerMissile() {
        modal.style.display = 'flex';
        playSiren();
    }

    // 关闭彩蛋
    closeBtn.addEventListener('click', function() {
        modal.style.display = 'none';
    });

    // 使用 Web Audio API 合成警报声
    function playSiren() {
        try {
            const AudioContext = window.AudioContext || window.webkitAudioContext;
            const ctx = new AudioContext();
            
            const osc1 = ctx.createOscillator();
            const osc2 = ctx.createOscillator();
            const gainNode = ctx.createGain();

            osc1.type = 'sawtooth';
            osc2.type = 'square';
            
            gainNode.gain.setValueAtTime(0, ctx.currentTime);
            gainNode.gain.linearRampToValueAtTime(0.15, ctx.currentTime + 0.1);

            // 频率变化模拟防空警报
            for (let i = 0; i < 5; i++) {
                osc1.frequency.setValueAtTime(400, ctx.currentTime + (i * 1.5));
                osc1.frequency.linearRampToValueAtTime(800, ctx.currentTime + (i * 1.5) + 0.75);
                osc2.frequency.setValueAtTime(405, ctx.currentTime + (i * 1.5)); 
                osc2.frequency.linearRampToValueAtTime(805, ctx.currentTime + (i * 1.5) + 0.75);
            }

            osc1.connect(gainNode);
            osc2.connect(gainNode);
            gainNode.connect(ctx.destination);

            osc1.start();
            osc2.start();

            setTimeout(() => {
                osc1.stop();
                osc2.stop();
            }, 5000);
        } catch (e) {
            console.log("浏览器不支持自动播放声音", e);
        }
    }
});
</script>