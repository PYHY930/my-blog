---
title: "相册"
layout: "list"
---
分享一些抽象图片
<script>
document.addEventListener("DOMContentLoaded", function() {
    if (sessionStorage.getItem('photosUnlocked') !== 'true') {
        alert("请先在主页输入密码！");
        window.location.href = "/"; // 强行踢回主页
    }
});
</script>