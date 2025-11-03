---
title: 随机封面图配置
createTime: 2025/01/27 18:38:13
permalink: /config/coverImageConfig-usage/
---
# 随机封面图配置

## 概述

随机封面图功能允许文章使用 API 自动获取随机图片作为封面图。当 API 请求失败时，系统会自动切换到备用图片，确保封面图始终能够正常显示。此功能特别适合想要快速为文章添加封面图的用户。

## 文件位置

```
src/config/coverImageConfig.ts
```

## 快速开始

### 在文章中使用随机封面图

在文章的 Frontmatter 中添加 `image: "api"` 即可：

```markdown
---
title: 我的文章标题
image: "api"
---
```

## 基础配置

```typescript
export const coverImageConfig: CoverImageConfig = {
  // 随机封面图功能开关
  enable: true,
  // 封面图API列表
  apis: [
    "https://t.alcy.cc/pc",
    "https://www.dmoe.cc/random.php",
    "https://uapis.cn/api/v1/random/image?category=acg&type=pc",
  ],
  // 备用图片路径
  fallback: "/assets/images/cover.webp",
  
  // 加载指示器配置
  loading: {
    image: "/assets/images/loading.gif",
    backgroundColor: "#fefefe",
  },
  
  // 水印配置
  watermark: {
    enable: true,
    text: "Random Cover",
    position: "bottom-right",
    opacity: 0.6,
    fontSize: "0.75rem",
    color: "#ffffff",
    backgroundColor: "rgba(0, 0, 0, 0.5)",
  },
};
```

## 配置选项详解

### 基础配置

| 选项 | 类型 | 说明 | 必填 | 默认值 |
|------|------|------|------|--------|
| `enable` | `boolean` | 随机封面图功能开关 | 是 | `true` |
| `apis` | `string[]` | 封面图API列表，系统会依次尝试 | 是 | `[]` |
| `fallback` | `string` | 备用图片路径（API全部失败时使用） | 否 | - |

### 功能开关说明

- **`enable: true`**：启用随机封面图功能，文章使用 `image: "api"` 时会尝试从 API 获取图片
- **`enable: false`**：禁用随机封面图功能，即使文章设置了 `image: "api"`，也不会显示封面图（也不会显示备用图）

### API 列表配置

系统会按照 `apis` 数组的顺序依次尝试每个 API：

```typescript
apis: [
  "https://api1.example.com/image",  // 首先尝试这个
  "https://api2.example.com/image",  // 如果失败，尝试这个
  "https://api3.example.com/image",  // 如果还失败，尝试这个
]
```

**API 选择逻辑：**
1. 系统按顺序尝试每个 API
2. 如果某个 API 失败，自动尝试下一个
3. 如果所有 API 都失败，使用备用图片（`fallback`）
4. 失败的 API 会被记录到 `localStorage`，避免下次重复请求（F5 刷新会清除记录）

### 备用图片配置

```typescript
fallback: "/assets/images/cover.webp"
```

- 路径相对于 `public` 目录
- 支持相对路径（如 `/assets/images/cover.webp`）
- 当所有 API 都失败时，使用此图片作为封面
- 使用备用图片时，水印文字会自动更新为 "Image API Error"

## 加载指示器配置

### 配置选项

| 选项 | 类型 | 说明 | 必填 | 默认值 |
|------|------|------|------|--------|
| `image` | `string` | 自定义加载图片路径（相对于 public 目录） | 否 | `"/assets/images/loading.gif"` |
| `backgroundColor` | `string` | 加载指示器背景颜色 | 否 | `"#fefefe"` |

### 使用示例

```typescript
loading: {
  image: "/assets/images/my-loading.gif",  // 自定义加载 GIF
  backgroundColor: "#ffffff",                // 白色背景（与 GIF 背景色一致）
}
```

### 注意事项

- **背景颜色匹配**：`backgroundColor` 应该与加载 GIF 的背景色一致，避免在暗色模式下显得突兀
- **图片路径**：路径相对于 `public` 目录，不需要包含 `public`
- **只对远程 API 图片生效**：本地图片不会显示加载指示器

## 水印配置

### 配置选项

| 选项 | 类型 | 说明 | 必填 | 默认值 |
|------|------|------|------|--------|
| `enable` | `boolean` | 水印开关 | 是 | `true` |
| `text` | `string` | 水印文本 | 否 | `"Random Cover"` |
| `position` | `string` | 水印位置 | 否 | `"bottom-right"` |
| `opacity` | `number` | 水印透明度（0-1） | 否 | `0.6` |
| `fontSize` | `string` | 字体大小 | 否 | `"0.75rem"` |
| `color` | `string` | 文字颜色 | 否 | `"#ffffff"` |
| `backgroundColor` | `string` | 背景颜色 | 否 | `"rgba(0, 0, 0, 0.5)"` |

### 水印位置选项

| 位置值 | 说明 | 移动端显示 | 桌面端显示 |
|--------|------|------------|------------|
| `"top-left"` | 左上角 | 左上角 | 左上角 |
| `"top-right"` | 右上角 | 右上角 | 右上角 |
| `"bottom-left"` | 左下角 | 左上角（避免被裁剪） | 左下角 |
| `"bottom-right"` | 右下角 | 右上角（避免被裁剪） | 右下角 |
| `"center"` | 居中 | 居中 | 居中 |

**注意**：`bottom-left` 和 `bottom-right` 在移动端会自动调整到顶部显示，避免水印被裁剪。

### 水印文字规则

- **API 成功时**：显示配置的 `text`（默认 "Random Cover"）
- **API 失败时**：自动更新为 "Image API Error"
- **仅对远程 API 图片显示**：本地图片不显示水印

### 使用示例

```typescript
watermark: {
  enable: true,
  text: "随机封面",           // 中文水印
  position: "bottom-right",   // 右下角
  opacity: 0.8,               // 更高透明度
  fontSize: "0.875rem",       // 稍大字体
  color: "#ff0000",           // 红色文字
  backgroundColor: "rgba(255, 255, 255, 0.9)", // 白色半透明背景
}
```

## 完整配置示例

### 基础配置

```typescript
export const coverImageConfig: CoverImageConfig = {
  enable: true,
  apis: [
    "https://t.alcy.cc/ycy",
    "https://www.dmoe.cc/random.php",
  ],
  fallback: "/assets/images/cover.webp",
  loading: {
    image: "/assets/images/loading.gif",
    backgroundColor: "#fefefe",
  },
  watermark: {
    enable: true,
    text: "Random Cover",
    position: "bottom-right",
    opacity: 0.6,
    fontSize: "0.75rem",
    color: "#ffffff",
    backgroundColor: "rgba(0, 0, 0, 0.5)",
  },
};
```

### 高级配置

```typescript
export const coverImageConfig: CoverImageConfig = {
  enable: true,
  // 多个 API 备用
  apis: [
    "https://api1.example.com/image",
    "https://api2.example.com/image",
    "https://api3.example.com/image",
  ],
  fallback: "/assets/images/custom-fallback.webp",
  
  // 自定义加载指示器
  loading: {
    image: "/assets/images/custom-loading.gif",
    backgroundColor: "#ffffff", // 与 GIF 背景色一致
  },
  
  // 自定义水印样式
  watermark: {
    enable: true,
    text: "随机封面图",        // 中文水印
    position: "top-right",     // 右上角
    opacity: 0.8,              // 更高透明度
    fontSize: "0.875rem",      // 稍大字体
    color: "#333333",          // 深色文字
    backgroundColor: "rgba(255, 255, 255, 0.9)", // 白色背景
  },
};
```

### 禁用功能

```typescript
export const coverImageConfig: CoverImageConfig = {
  enable: false, // 禁用随机封面图功能
  apis: [],
  fallback: "/assets/images/cover.webp",
};
```

## 使用流程

1. **配置 API 列表**：在 `apis` 数组中添加可用的随机图 API
2. **设置备用图片**：准备一个备用图片，放在 `public` 目录下
3. **在文章中使用**：在文章的 Frontmatter 中添加 `image: "api"`
4. **系统自动处理**：
   - 尝试从 API 获取图片
   - 显示加载指示器
   - 成功后显示图片和水印
   - 失败后使用备用图片并更新水印为 "Image API Error"

## 注意事项

### 1. API 可用性

- 确保配置的 API 可以正常访问
- 建议配置多个 API 作为备用
- API 返回的应该是直接的图片 URL，而不是 HTML 页面

### 2. 备用图片准备

- 建议使用 WebP 格式，文件更小
- 备用图片应该放在 `public` 目录下
- 路径要正确（相对于 `public` 目录）

### 3. 加载指示器

- 背景颜色应与加载 GIF 的背景色一致
- 只对远程 API 图片显示，本地图片不显示
- 加载 GIF 建议使用透明背景或与页面背景色一致的背景

### 4. 水印显示

- 只在随机 API 图片成功加载时显示配置的水印文字
- API 失败时会自动更新为 "Image API Error"
- 本地图片不显示水印

### 5. 缓存机制

- 失败的 API 会被记录到 `localStorage`
- 下次访问同一文章时，会直接使用备用图片（避免重复请求）
- F5 刷新会清除失败记录，重新尝试 API

## 常见问题

**Q: 如何启用随机封面图功能？**

A: 在 `coverImageConfig.ts` 中设置 `enable: true`，然后在文章的 Frontmatter 中添加 `image: "api"`。

**Q: 如何添加更多的 API？**

A: 在 `apis` 数组中添加 API URL，系统会按顺序尝试：

```typescript
apis: [
  "https://api1.com/image",
  "https://api2.com/image",
  "https://api3.com/image",
]
```

**Q: API 全部失败怎么办？**

A: 系统会自动使用 `fallback` 配置的备用图片，水印文字会自动更新为 "Image API Error"。

**Q: 如何禁用水印？**

A: 设置 `watermark.enable: false` 即可。

**Q: 如何自定义水印位置？**

A: 修改 `watermark.position` 的值，支持 `"top-left"`、`"top-right"`、`"bottom-left"`、`"bottom-right"`、`"center"`。

**Q: 为什么移动端水印位置不一样？**

A: `bottom-left` 和 `bottom-right` 在移动端会自动调整到顶部显示，避免水印被裁剪。这是设计特性，不是 bug。

**Q: 如何自定义加载 GIF？**

A: 在 `loading.image` 中设置自定义 GIF 路径，并确保 `loading.backgroundColor` 与 GIF 背景色一致。

**Q: 为什么本地图片不显示加载指示器？**

A: 加载指示器只对远程 API 图片显示，本地图片加载较快，不需要显示。

**Q: 如何清除 API 失败记录？**

A: 按 F5 刷新页面会自动清除 `localStorage` 中的失败记录，重新尝试 API。

**Q: 能否只使用一个 API？**

A: 可以，但建议配置多个 API 作为备用，提高可用性。

**Q: API 需要支持哪些参数？**

A: API 应该直接返回图片，支持 GET 请求。不需要任何特殊参数，系统会自动处理图片加载。

**Q: 如何测试 API 是否可用？**

A: 在浏览器中直接访问 API URL，应该能看到图片。如果可以，说明 API 可用。


