---
title: 许可证配置
createTime: 2025/01/27 18:38:13
permalink: /config/licenseConfig-usage/
---
# 许可证配置

## 概述

许可证配置用于在网站底部显示内容的使用许可信息，保护您的原创内容版权。

## 文件位置

```
src/config/licenseConfig.ts
```

## 基础配置

### 启用许可证功能

```typescript
export const licenseConfig: LicenseConfig = {
  enable: true, // 启用许可证显示
  name: "CC BY-NC-SA 4.0", // 许可证名称
  url: "https://creativecommons.org/licenses/by-nc-sa/4.0/", // 许可证链接
};
```

## 配置选项详解

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `enable` | `boolean` | 是否启用许可证显示 | `true` |
| `name` | `string` | 许可证名称 | `"CC BY-NC-SA 4.0"` |
| `url` | `string` | 许可证详情链接 | `"https://creativecommons.org/licenses/by-nc-sa/4.0/"` |

## 常用许可证类型

### 1. Creative Commons 许可证

#### CC BY（署名）
```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "CC BY 4.0",
  url: "https://creativecommons.org/licenses/by/4.0/",
};
```
- **允许**：商业使用、修改、分发
- **要求**：必须署名原作者

#### CC BY-NC（署名-非商业）
```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "CC BY-NC 4.0",
  url: "https://creativecommons.org/licenses/by-nc/4.0/",
};
```
- **允许**：修改、分发
- **要求**：必须署名原作者，不得用于商业用途

#### CC BY-NC-SA（署名-非商业-相同方式分享）
```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "CC BY-NC-SA 4.0",
  url: "https://creativecommons.org/licenses/by-nc-sa/4.0/",
};
```
- **允许**：修改、分发
- **要求**：必须署名原作者，不得用于商业用途，衍生作品必须使用相同许可证

#### CC BY-SA（署名-相同方式分享）
```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "CC BY-SA 4.0",
  url: "https://creativecommons.org/licenses/by-sa/4.0/",
};
```
- **允许**：商业使用、修改、分发
- **要求**：必须署名原作者，衍生作品必须使用相同许可证

### 2. 自定义许可证

```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "自定义许可证",
  url: "/license/", // 链接到您自己的许可证页面
};
```

### 3. 版权声明

```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "© 2024 您的姓名",
  url: "/copyright/",
};
```

## 许可证选择指南

### 根据使用目的选择

| 使用目的 | 推荐许可证 | 说明 |
|----------|------------|------|
| 开源项目 | CC BY 或 CC BY-SA | 允许商业使用，促进传播 |
| 个人博客 | CC BY-NC-SA | 保护原创，允许学习交流 |
| 商业内容 | 自定义版权 | 完全控制使用权限 |
| 教育内容 | CC BY | 鼓励学习和分享 |

### 根据内容类型选择

| 内容类型 | 推荐许可证 | 说明 |
|----------|------------|------|
| 技术教程 | CC BY | 鼓励技术分享 |
| 艺术作品 | CC BY-NC | 保护艺术价值 |
| 学术论文 | CC BY-SA | 促进学术交流 |
| 商业文档 | 自定义版权 | 保护商业利益 |

## 显示效果

许可证信息会在网站底部显示，格式如下：

```
本作品采用 [许可证名称] 进行许可
```

点击许可证名称会跳转到对应的许可证详情页面。

## 样式自定义

可以通过 CSS 自定义许可证的显示样式：

```css
/* 许可证容器 */
.license-container {
  text-align: center;
  padding: 1rem;
  font-size: 0.9rem;
  color: var(--text-secondary);
  border-top: 1px solid var(--border-color);
  margin-top: 2rem;
}

/* 许可证链接 */
.license-link {
  color: var(--primary);
  text-decoration: none;
  font-weight: 500;
}

.license-link:hover {
  text-decoration: underline;
}
```

## 多语言支持

许可证配置支持多语言显示：

```typescript
// 中文
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "CC BY-NC-SA 4.0",
  url: "https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh",
};

// 英文
export const licenseConfig: LicenseConfig = {
  enable: true,
  name: "CC BY-NC-SA 4.0",
  url: "https://creativecommons.org/licenses/by-nc-sa/4.0/",
};
```

## 注意事项

1. **法律效力**：许可证具有法律效力，请仔细阅读条款
2. **不可撤销**：一旦发布，许可证通常不可撤销
3. **兼容性**：确保许可证与您的内容使用方式兼容
4. **更新维护**：定期检查许可证链接是否有效

## 常见问题

**Q: 如何禁用许可证显示？**
A: 将 `enable` 设置为 `false`

**Q: 可以同时使用多个许可证吗？**
A: 目前只支持单个许可证，如需多个需要修改源码

**Q: 如何添加自定义许可证页面？**
A: 创建许可证页面，然后将 `url` 指向该页面

**Q: 许可证信息在哪里显示？**
A: 在网站底部的页脚区域显示

**Q: 如何更改许可证？**
A: 修改 `name` 和 `url` 字段即可，但要注意已发布内容的许可证变更问题
