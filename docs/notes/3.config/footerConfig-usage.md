---
title: 页脚配置
createTime: 2025/10/11 18:38:13
permalink: /config/footerConfig-usage/
---
# 页脚配置

## 概述

页脚配置用于在网站底部注入自定义HTML内容，如备案号、版权信息、统计代码等。

## 文件位置

```
src/config/FooterConfig.html
```

## 配置结构

页脚配置分为两个部分：

1. **HTML内容文件**：`src/config/FooterConfig.html`
2. **配置开关**：`src/config/footerConfig.ts` 中的 `footerConfig`

## 基础配置

### 1. 启用页脚功能

在 `src/config/footerConfig.ts` 中：

```typescript
export const footerConfig: FooterConfig = {
  enable: true,  // 启用Footer HTML注入功能
};
```

### 2. 添加HTML内容

在 `src/config/FooterConfig.html` 中：

```html
<!-- 这里是HTML注入示例，你可以在这个文件中添加自定义的HTML内容 -->

</div>
```

## 使用场景

### 1. 版权信息

```html
<div class="copyright">
  <p>本网站内容采用 <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/" target="_blank" rel="noopener">CC BY-NC-SA 4.0</a> 协议</p>
</div>
```

### 2. 备案信息

```html
<div class="beian">
  <p>
    <a href="https://beian.miit.gov.cn/" target="_blank" rel="noopener">京ICP备12345678号-1</a>
  </p>
</div>
```

### 3. 统计代码

```html
<!-- 百度统计 -->
<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?your-id";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>

<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

