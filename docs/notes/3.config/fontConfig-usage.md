---
title: 字体配置
createTime: 2025/10/11 18:38:13
permalink: /config/fontConfig-usage/
---
# 字体配置

## 概述

`fontConfig.ts` 文件用于配置网站的自定义字体功能，支持多种字体来源和加载方式。

## 文件位置

```
src/config/fontConfig.ts
```

## 配置结构

```typescript
interface FontConfig {
  enable: boolean;                    // 是否启用自定义字体功能
  preload: boolean;                   // 是否预加载字体文件
  selected: string | string[];        // 当前选择的字体ID
  fonts: {                           // 字体定义对象
    [key: string]: FontDefinition;
  };
  fallback: string[];                // 全局字体回退列表
}

interface FontDefinition {
  id: string;                        // 字体唯一标识
  name: string;                      // 字体显示名称
  src: string;                       // 字体源地址
  family: string;                    // 字体族名称
  weight?: number;                   // 字体粗细
  style?: string;                    // 字体样式
  display?: "auto" | "block" | "swap" | "fallback" | "optional";
  unicodeRange?: string;             // Unicode范围
  format?: string;                   // 字体格式
}
```

## 配置选项详解

### 基础配置

```typescript
export const fontConfig = {
  enable: true,                      // 启用自定义字体功能
  preload: true,                     // 预加载字体文件以提高性能
  selected: ["misans-normal", "misans-semibold"], // 当前选择的字体
  // ... 其他配置
};
```

| 属性 | 类型 | 说明 |
|------|------|------|
| `enable` | boolean | 是否启用自定义字体功能 |
| `preload` | boolean | 是否预加载字体文件，提高加载性能 |
| `selected` | string\|string[] | 当前选择的字体ID，支持多个字体组合 |

### 字体定义 (fonts)

#### 1. 系统字体

```typescript
"system": {
  id: "system",
  name: "系统字体",
  src: "", // 系统字体无需 src
  family: "system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, sans-serif",
}
```

**特点：**
- 无需下载，加载速度快
- 在不同操作系统上显示不同字体
- 适合追求性能的场景

#### 2. Google Fonts

```typescript
"inter": {
  id: "inter",
  name: "Inter",
  src: "https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap",
  family: "Inter",
  display: "swap",
}
```

**特点：**
- 免费使用，质量较高
- 支持多种字重和样式
- 自动优化加载性能

#### 3. CDN 字体

```typescript
"misans-normal": {
  id: "misans-normal",
  name: "MiSans Normal",
  src: "https://unpkg.com/misans@4.1.0/lib/Normal/MiSans-Normal.min.css",
  family: "MiSans",
  weight: 400,
  display: "swap",
}
```

**特点：**
- 使用CDN加速加载
- 支持分包加载，按需下载
- 文件较小，性能较好

#### 4. 本地字体

```typescript
"custom-font": {
  id: "custom-font",
  name: "自定义字体",
  src: "/assets/fonts/custom-font.woff2",
  family: "CustomFont",
  weight: 400,
  display: "swap",
  format: "woff2",
}
```

**特点：**
- 完全控制字体文件
- 不依赖外部服务
- 需要自己管理字体文件

### 字体属性详解

#### src 属性

```typescript
// 外部链接（Google Fonts）
src: "https://fonts.googleapis.com/css2?family=Inter:wght@400;500&display=swap"

// 外部链接（CDN）
src: "https://unpkg.com/misans@4.1.0/lib/Normal/MiSans-Normal.min.css"

// 本地文件
src: "/assets/fonts/font.woff2"

// 相对路径
src: "./fonts/font.woff2"
```

#### display 属性

| 值 | 说明 | 使用场景 |
|----|------|----------|
| `"auto"` | 浏览器默认行为 | 一般情况 |
| `"block"` | 阻塞渲染直到字体加载完成 | 重要标题 |
| `"swap"` | 先显示回退字体，字体加载后替换 | 推荐使用 |
| `"fallback"` | 短暂阻塞后回退 | 平衡性能和体验 |
| `"optional"` | 字体加载失败也不影响 | 装饰性字体 |

#### weight 属性

```typescript
weight: 100,  // 极细
weight: 200,  // 超细
weight: 300,  // 细
weight: 400,  // 正常（默认）
weight: 500,  // 中等
weight: 600,  // 半粗
weight: 700,  // 粗
weight: 800,  // 超粗
weight: 900,  // 极粗
```

#### unicodeRange 属性

```typescript
// 只加载中文字符
unicodeRange: "U+4E00-9FFF"

// 只加载英文字符
unicodeRange: "U+0000-00FF"

// 只加载数字
unicodeRange: "U+0030-0039"

// 多个范围
unicodeRange: "U+0000-00FF, U+4E00-9FFF"
```

### 回退字体 (fallback)

```typescript
fallback: [
  "system-ui",           // 系统UI字体
  "-apple-system",       // 苹果系统字体
  "BlinkMacSystemFont",  // 苹果浏览器字体
  "Segoe UI",            // Windows系统字体
  "Roboto",              // Android系统字体
  "sans-serif"           // 通用无衬线字体
]
```

**作用：**
- 当自定义字体加载失败时使用
- 提供一致的字体体验
- 按优先级顺序尝试

## 使用方式

### 1. 选择单个字体

```typescript
selected: "misans-normal"
```

### 2. 选择多个字体

```typescript
selected: ["misans-normal", "misans-semibold"]
```

### 3. 在CSS中使用

```css
/* 自动应用选中的字体 */
body {
  font-family: var(--font-family-custom), var(--font-family-fallback);
}

/* 使用特定字体类 */
.font-misans-normal {
  font-family: "MiSans", var(--font-family-fallback) !important;
}
```

## 字体文件管理

### 本地字体文件结构

```
public/assets/fonts/
├── custom-font.woff2     # 主要字体文件
├── custom-font.woff      # 兼容性字体文件
└── custom-font.ttf       # 备用字体文件
```

### 字体格式选择

| 格式 | 文件大小 | 浏览器支持 | 推荐度 |
|------|----------|------------|--------|
| `woff2` | 最小 | 现代浏览器 | ⭐⭐⭐⭐⭐ |
| `woff` | 较小 | 较老浏览器 | ⭐⭐⭐⭐ |
| `ttf` | 较大 | 所有浏览器 | ⭐⭐⭐ |
| `otf` | 大 | 所有浏览器 | ⭐⭐ |

### 字体文件优化

```typescript
// 使用字体子集，只包含需要的字符
"optimized-font": {
  id: "optimized-font",
  name: "优化字体",
  src: "/assets/fonts/font-subset.woff2",
  family: "CustomFont",
  unicodeRange: "U+4E00-9FFF, U+0000-00FF", // 只包含中文和英文
}
```

## 性能优化

### 1. 预加载关键字体

```typescript
// 在 FontManager.astro 中自动处理
preload: true
```

### 2. 使用 font-display: swap

```typescript
display: "swap" // 避免字体加载阻塞渲染
```

### 3. 字体分包加载

```typescript
// MiSans 自动分包，只加载需要的字符集
"misans-normal": {
  src: "https://unpkg.com/misans@4.1.0/lib/Normal/MiSans-Normal.min.css",
  // 自动分包为多个 .woff2 文件
}
```

### 4. 减少字体数量

```typescript
// 只选择必要的字体
selected: ["misans-normal"] // 而不是多个字体
```

## 常见问题

### Q: 字体不显示怎么办？

A: 检查以下项目：
1. `enable` 是否设置为 `true`
2. `selected` 中的字体ID是否存在
3. 字体文件路径是否正确
4. 网络连接是否正常（外部字体）

### Q: 如何添加新字体？

A: 在 `fonts` 对象中添加新字体定义：

```typescript
fonts: {
  // 现有字体...
  "new-font": {
    id: "new-font",
    name: "新字体",
    src: "/assets/fonts/new-font.woff2",
    family: "NewFont",
    weight: 400,
    display: "swap",
  }
}
```

### Q: 如何更换当前字体？

A: 修改 `selected` 配置：

```typescript
// 从多个字体改为单个字体
selected: "inter"

// 从单个字体改为多个字体
selected: ["inter", "misans-normal"]
```

### Q: 字体加载很慢怎么办？

A: 尝试以下优化：
1. 使用本地字体文件
2. 启用预加载：`preload: true`
3. 使用字体子集
4. 选择文件更小的字体

### Q: 如何禁用字体功能？

A: 设置 `enable: false`：

```typescript
export const fontConfig = {
  enable: false, // 禁用字体功能
  // ... 其他配置
};
```

