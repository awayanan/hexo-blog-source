---
title: 404 - Awayanan - RollBack
date: 2023-01-24 19:51:13
comments: false
permalink: /404.html
---

<!-- markdownlint-disable MD039 MD033 -->

## 这是一個不存在的页面

对不起，您所访问的页面不存在或者已删除。

预计将在约 <span id="timeout">10</span> 秒后返回首页。

当然，你可以 **[点这里](https://www.awayanan.wang/)** 直接返回首页。

<script>
let countTime = 10;

function count() {

  document.getElementById('timeout').textContent = countTime;
  countTime -= 1;
  if(countTime === 0){
    location.href = 'https://www.awayanan.wang/';
  }
  setTimeout(() => {
    count();
  }, 1000);
}

count();
</script>

