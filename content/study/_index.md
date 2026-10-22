---
title: "学习"
layout: "list"
---
这里是一些学习的资料
<script>
document.addEventListener("DOMContentLoaded", function() {
    if (sessionStorage.getItem('studyUnlocked') !== 'true') {
        alert("请先在主页输入密码！");
        window.location.href = "/"; // 强行踢回主页
    }
});
</script>