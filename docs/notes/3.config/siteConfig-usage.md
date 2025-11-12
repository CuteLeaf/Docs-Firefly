---
title: 站点配置
createTime: 2025/01/27 18:38:13
permalink: /config/siteConfig-usage/
---
# 站点配置

## 概述

站点配置是 Firefly 的核心配置文件，包含网站的基本信息、主题设置、功能开关等所有基础配置。

## 文件位置

```
src/config/siteConfig.ts
```

## 基础配置

### 网站基本信息

```typescript
export const siteConfig: SiteConfig = {
  title: "Firefly", // 网站标题
  subtitle: "Demo site", // 网站副标题
  site_url: "https://firefly.cuteleaf.cn", // 网站URL
  description: "Firefly 是一款基于 Astro 框架开发的清新美观且现代化个人博客主题...", // 网站描述
  keywords: [ // SEO关键词
    "Firefly",
    "Fuwari", 
    "Astro",
    "ACGN",
    "博客",
    "技术博客",
    "静态博客",
  ],
  lang: "zh_CN", // 网站语言
};
```

## 配置选项详解

### 基础信息

| 选项 | 类型 | 说明 | 必填 |
|------|------|------|------|
| `title` | `string` | 网站标题 | 是 |
| `subtitle` | `string` | 网站副标题 | 是 |
| `site_url` | `string` | 网站URL | 是 |
| `description` | `string` | 网站描述（SEO用） | 否 |
| `keywords` | `string[]` | SEO关键词数组 | 否 |
| `lang` | `string` | 网站语言代码 | 是 |

### 支持的语言

| 语言代码 | 语言名称 | 说明 |
|----------|----------|------|
| `zh_CN` | 简体中文 | 默认语言 |
| `zh_TW` | 繁体中文 | 台湾地区 |
| `en` | 英文 | 国际通用 |
| `ja` | 日文 | 日本地区 |
| `ru` | 俄语 | 俄罗斯及其他俄语地区 |

## 主题颜色配置

### 主题色设置

```typescript
themeColor: {
  hue: 165, // 主题色的默认色相，范围从 0 到 360。例如：红色：0，青色：200，蓝绿色：250，粉色：345
  fixed: false, // 对访问者隐藏主题色选择器
  defaultMode: "system", // 默认模式："light" 亮色，"dark" 暗色，"system" 跟随系统
}
```

### 色相值参考

| 颜色 | 色相值 | 说明 |
|------|--------|------|
| 红色 | 0 | 热情、活力 |
| 橙色 | 30 | 温暖、友好 |
| 黄色 | 60 | 明亮、乐观 |
| 绿色 | 120 | 自然、清新 |
| 青色 | 180 | 冷静、专业 |
| 蓝色 | 240 | 稳重、可信 |
| 紫色 | 300 | 神秘、创意 |
| 粉色 | 330 | 温柔、浪漫 |
| 蓝绿色 | 165-200 | 清新、现代 |

### 默认模式选项

| 模式 | 说明 | 适用场景 |
|------|------|----------|
| `"light"` | 亮色模式 | 日间使用 |
| `"dark"` | 暗色模式 | 夜间使用 |
| `"system"` | 跟随系统 | 自动切换 |

## 网站图标配置

### Favicon 设置

```typescript
favicon: [
  {
    src: "/assets/images/favicon.ico", // 图标文件路径
    theme: "light", // 可选，指定主题 'light' | 'dark'
    sizes: "32x32", // 可选，图标大小
  },
]
```

### 支持的图标格式

- **ICO**：传统格式，兼容性好
- **PNG**：现代格式，支持透明
- **SVG**：矢量格式，可缩放
- **WebP**：现代格式，文件小

### 图标尺寸建议

| 尺寸 | 用途 | 说明 |
|------|------|------|
| 16x16 | 浏览器标签 | 最小尺寸 |
| 32x32 | 浏览器标签 | 标准尺寸 |
| 48x48 | 书签 | 中等尺寸 |
| 64x64 | 桌面快捷方式 | 较大尺寸 |
| 128x128 | 移动设备 | 高分辨率 |
| 192x192 | PWA | 应用图标 |
| 512x512 | PWA | 启动画面 |

## 导航栏Logo配置

### Logo 类型

#### 1. Astro 图标库

```typescript
navbarLogo: {
  type: "icon",
  value: "material-symbols:home-pin-outline" // 图标名称
}
```

#### 2. 本地图片

```typescript
navbarLogo: {
  type: "image",
  value: "/assets/images/logo.webp", // 图片路径
  alt: "Firefly Logo" // 替代文本
}
```

#### 3. 网络图片

```typescript
navbarLogo: {
  type: "image",
  value: "https://example.com/logo.png", // 图片URL
  alt: "Firefly Logo"
}
```

### 导航栏标题配置

```typescript
navbarTitle: "Firefly", // 导航栏标题，可以设置为与 title 不同的值，如果不设置则使用 title
```

### 常用图标示例

```typescript
// 首页图标
navbarLogo: {
  type: "icon",
  value: "material-symbols:home-pin-outline"
}

// 代码图标
navbarLogo: {
  type: "icon", 
  value: "material-symbols:code"
}

// 博客图标
navbarLogo: {
  type: "icon",
  value: "material-symbols:article"
}

// 自定义图片
navbarLogo: {
  type: "image",
  value: "/assets/images/logo.svg",
  alt: "我的博客"
}
```

## 背景壁纸配置

### 基础配置结构

```typescript
backgroundWallpaper: {
  // 壁纸模式："banner" 横幅壁纸，"overlay" 全屏壁纸，"none" 纯色背景无壁纸
  mode: "banner",
  // 是否允许用户通过导航栏切换壁纸模式，设为false可提升性能（只渲染当前模式）
  switchable: true,

  // 背景图片配置
  src: {
    // 桌面背景图片
    desktop: "/assets/images/d1.webp",
    // 移动背景图片
    mobile: "/assets/images/m1.webp",
  },

  // Banner模式特有配置
  banner: {
    // 图片位置配置
    position: "0% 20%",
    // ... 其他banner配置
  },

  // 全屏透明覆盖模式特有配置
  overlay: {
    zIndex: -1,
    opacity: 0.8,
    blur: 1,
  },
}
```

### 壁纸模式

| 模式 | 说明 | 使用场景 |
|------|------|----------|
| `"banner"` | 横幅壁纸 | 主页横幅，位于导航栏下方 |
| `"overlay"` | 全屏透明覆盖 | 整个页面背景，内容半透明显示 |
| `"none"` | 纯色背景 | 无壁纸，使用主题背景色 |

### 切换控制

```typescript
switchable: true  // 允许切换，会在导航栏显示切换按钮
switchable: false // 禁止切换，提升性能（只渲染当前模式）
```

### 图片源配置

```typescript
src: {
  desktop: "/assets/images/d1.webp", // 桌面背景图片
  mobile: "/assets/images/m1.webp",  // 移动背景图片
}
```

**说明**：
- 如果只配置 `desktop`，移动端也会使用桌面图片
- 如果只配置 `mobile`，桌面端也会使用移动图片
- 建议为桌面和移动端分别配置不同尺寸的图片以优化加载速度

## Banner模式配置

### 图片位置配置

`position` 选项位于 `backgroundWallpaper.banner.position`，用于控制横幅壁纸图片的显示位置，支持所有 CSS `object-position` 值。该配置会通过 `!important` 确保位置定位生效，不会被其他样式覆盖。

```typescript
backgroundWallpaper: {
  mode: "banner",
  banner: {
    // 图片位置
    // 支持所有CSS object-position值，如: 'top', 'center', 'bottom', 'left top', 'right bottom', '25% 75%', '10px 20px'..
    // 如果不知道怎么配置百分百之类的配置，推荐直接使用：'center'居中，'top'顶部居中，'bottom' 底部居中，'left'左侧居中，'right'右侧居中
    position: "0% 20%",
  }
}
```

#### 常用位置值

```typescript
// 基本位置
position: "center"           // 居中
position: "top"              // 顶部居中
position: "bottom"           // 底部居中
position: "left"             // 左侧居中
position: "right"            // 右侧居中

// 组合位置
position: "left top"         // 左上角
position: "right top"        // 右上角
position: "left bottom"      // 左下角
position: "right bottom"     // 右下角

// 百分比位置（推荐用于精细调整）
position: "0% 20%"           // 水平 0%，垂直 20%（左上区域）
position: "25% 75%"          // 水平 25%，垂直 75%
position: "50% 50%"          // 完全居中（等同于 "center"）
position: "center 30%"       // 水平居中，垂直 30%

// 像素位置
position: "10px 20px"        // 距离左边 10px，距离顶部 20px
position: "center 50px"      // 水平居中，距离顶部 50px
```

#### 位置值说明

| 位置类型 | 格式 | 示例 | 说明 |
|---------|------|------|------|
| **关键字** | `"center"`, `"top"`, `"bottom"`, `"left"`, `"right"` | `"center"` | 简单的定位，易于理解 |
| **组合关键字** | `"left top"`, `"right bottom"` 等 | `"right bottom"` | 两个关键字组合 |
| **百分比** | `"X% Y%"` | `"0% 20%"` | 精确控制，支持小数 |
| **像素值** | `"Xpx Ypx"` | `"10px 20px"` | 固定像素定位 |
| **混合** | `"center 30%"`, `"left 50px"` 等 | `"center 30%"` | 关键字与数值混合 |

#### 使用建议

1. **推荐使用百分比**：`"0% 20%"` 这种方式既精确又易于理解
2. **常用居中**：如果不确定，直接使用 `"center"` 即可
3. **精细调整**：使用百分比可以进行像素级别的微调
4. **响应式友好**：百分比值在不同屏幕尺寸下表现更一致

#### 注意事项

- `position` 使用 `!important` 确保不会被其他 CSS 覆盖
- 该配置位于 `backgroundWallpaper.banner.position`，只影响横幅壁纸（banner 模式）
- 图片会被 `object-fit: cover` 填充容器，`position` 控制图片在容器内的显示区域

### 主页文本配置

```typescript
banner: {
  homeText: {
    // 主页显示自定义文本（全局开关）
    enable: true,
    // 主页横幅主标题
    title: "Lovely firefly!",
    // 主页横幅副标题（支持数组，可以设置多个副标题）
    subtitle: [
      "In Reddened Chrysalis, I Once Rest",
      "From Shattered Sky, I Free Fall",
      "Amidst Silenced Stars, I Deep Sleep",
      "Upon Lighted Fyrefly, I Soon Gaze",
      "From Undreamt Night, I Thence Shine",
      "In Finalized Morrow, I Full Bloom",
    ],
    typewriter: {
      enable: true, // 启用副标题打字机效果
      speed: 100, // 打字速度（毫秒）
      deleteSpeed: 50, // 删除速度（毫秒）
      pauseTime: 2000, // 完全显示后的暂停时间（毫秒）
    },
  },
}
```

**说明**：
- `enable`: 控制是否在主页显示横幅文本
- `title`: 主标题文本，显示在横幅中央上方
- `subtitle`: 副标题，支持字符串或字符串数组
  - 如果是数组，会依次显示多个副标题
  - 如果 `typewriter.enable` 为 `true`，会以打字机效果显示
- `typewriter`: 打字机效果配置
  - `enable`: 是否启用打字机效果
  - `speed`: 每个字符的显示间隔（毫秒）
  - `deleteSpeed`: 删除字符的间隔（毫秒）
  - `pauseTime`: 显示完整文本后的暂停时间（毫秒）

### 图片来源标注配置

```typescript
banner: {
  credit: {
    enable: {
      desktop: true, // 桌面端显示横幅图片来源文本
      mobile: false, // 移动端显示横幅图片来源文本
    },
    text: {
      desktop: "Pixiv - 晚晚喵", // 桌面端要显示的来源文本
      mobile: "Mobile Credit", // 移动端要显示的来源文本
    },
    url: {
      desktop: "https://www.pixiv.net/artworks/135490046", // 桌面端原始艺术品或艺术家页面的 URL 链接
      mobile: "", // 移动端原始艺术品或艺术家页面的 URL 链接
    },
  },
}
```

**说明**：
- `enable`: 分别控制桌面端和移动端是否显示图片来源标注
- `text`: 显示的来源文本，可以分别设置桌面端和移动端的文本
- `url`: 图片来源链接，点击标注会跳转到该链接
  - 如果没有设置 `url` 或 `url` 为空，标注不可点击

### 导航栏透明模式配置

```typescript
banner: {
  navbar: {
    transparentMode: "semifull", // 导航栏透明模式
  },
}
```

**透明模式选项**：

| 模式 | 说明 |
|------|------|
| `"semi"` | 半透明加圆角 |
| `"full"` | 完全透明 |
| `"semifull"` | 动态透明（推荐）|

**说明**：
- `"semifull"` 会根据页面滚动动态调整导航栏透明度，提供更好的视觉效果

### 波浪动画效果配置

```typescript
banner: {
  waves: {
    enable: {
      desktop: true, // 桌面端启用波浪动画效果
      mobile: true, // 移动端启用波浪动画效果
    },
    performance: {
      quality: "high",
      hardwareAcceleration: true, // 是否启用硬件加速
    },
  },
}
```

**性能配置说明**：

| 选项 | 值 | 说明 |
|------|------|------|
| `quality` | `"high"` | 最佳视觉效果，但GPU占用较高，适合高性能设备 |
| | `"medium"` | 平衡性能和质量，适合中等性能设备 |
| | `"low"` | 最低GPU占用，动画更简单，适合低性能设备 |
| `hardwareAcceleration` | `true` | 启用GPU加速，提升性能但增加GPU占用 |
| | `false` | 禁用GPU加速，降低GPU占用但可能影响性能 |

**注意事项**：
- 开启波浪动画可能会影响页面性能，请根据实际情况开启
- 移动端设备建议使用 `quality: "medium"` 或 `quality: "low"`

## Overlay模式配置

### 全屏透明覆盖配置

```typescript
backgroundWallpaper: {
  mode: "overlay",
  overlay: {
    zIndex: -1, // 层级，确保壁纸在背景层
    opacity: 0.8, // 壁纸透明度（0-1）
    blur: 1, // 背景模糊程度（像素）
  },
}
```

**配置说明**：

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `zIndex` | `number` | 层级，确保壁纸在背景层 | `-1` |
| `opacity` | `number` | 壁纸透明度，范围 0-1 | `0.8` |
| `blur` | `number` | 背景模糊程度（像素） | `1` |

**使用建议**：
- `opacity` 建议设置在 0.6-0.9 之间，太低看不清，太高会遮挡内容
- `blur` 建议设置在 0-3 之间，过度模糊会影响图片清晰度

## 功能配置

### 追番配置

```typescript
bangumi: {
  userId: "1163581", // 在此处设置你的Bangumi用户ID
}
```

**说明**：
- 需要设置你的 Bangumi 用户 ID
- 可以在 Bangumi 个人页面找到你的用户 ID

### 文章页底部配置

```typescript
// 文章页底部的"上次编辑时间"卡片开关
showLastModified: true,
```

### OpenGraph图片

```typescript
// OpenGraph图片功能,注意开启后要渲染很长时间，不建议本地调试的时候开启
generateOgImages: false,
```

**说明**：
- 开启后会为每篇文章生成 OpenGraph 图片
- 会显著增加构建时间，不建议在本地开发时开启

### 页面开关配置

```typescript
// 页面开关配置 - 控制特定页面的访问权限，设为false会返回404
pages: {
  anime: true, // 追番页面开关
  sponsor: true, // 赞助页面开关
  guestbook: true, // 留言板页面开关，需要配置评论系统
}
```

**说明**：
- 当页面开关设置为 `false` 时，访问对应页面将返回 404 错误
- 导航栏中的页面链接会根据开关状态自动显示或隐藏

### 文章列表布局配置

```typescript
postListLayout: {
  // 默认布局模式："list" 列表模式（单列布局），"grid" 网格模式（双列布局）
  defaultMode: "list",
  // 是否允许用户切换布局
  allowSwitch: true,
}
```

#### 布局模式说明

| 模式 | 说明 | 特点 |
|------|------|------|
| `"list"` | 列表模式 | 单列布局，显示文章封面，适合详细阅读 |
| `"grid"` | 网格模式 | 双列布局，无封面，适合快速浏览 |

#### 响应式行为

- 屏幕宽度 < 1200px 时自动切换为列表模式
- 布局切换按钮在小屏幕时自动隐藏
- 用户偏好会保存到 localStorage

### 分页配置

```typescript
pagination: {
  // 每页显示的文章数量
  postsPerPage: 10,
}
```

### 目录功能

```typescript
toc: {
  // 目录功能开关
  enable: true,
  // 目录深度，1-3，1 表示只显示 h1 标题，2 表示显示 h1 和 h2 标题，依此类推
  // depth在新版已弃用
  depth: 3,
}
```

### 字体配置

```typescript
// 字体配置
// 在src/config/fontConfig.ts中配置具体字体
font: fontConfig,
```

**说明**：
- 字体配置在单独的 `fontConfig.ts` 文件中
- 详见字体配置文档

#

## 注意事项

1. **SEO优化**：合理设置标题、描述和关键词
2. **性能考虑**：大图片会影响加载速度，建议使用 WebP 格式并压缩
3. **响应式设计**：确保在不同设备上正常显示，建议为桌面和移动端分别配置图片
4. **语言支持**：选择正确的语言代码
5. **位置配置**：`position` 位于 `backgroundWallpaper.banner.position`，不要放在错误的位置

## 常见问题

**Q: 如何更换网站标题？**
A: 修改 `title` 和 `subtitle` 字段

**Q: 如何设置主题颜色？**
A: 修改 `themeColor.hue` 的值（0-360）

**Q: 如何更换Logo？**
A: 修改 `navbarLogo` 配置，支持图标和图片两种方式

**Q: 如何禁用某些页面？**
A: 在 `pages` 配置中将对应选项设为 `false`

**Q: 如何设置多语言？**
A: 修改 `lang` 字段，并配置对应的翻译文件

**Q: 如何优化SEO？**
A: 合理设置 `description` 和 `keywords` 字段

**Q: 如何设置文章列表布局？**
A: 修改 `postListLayout.defaultMode` 为 `"list"` 或 `"grid"`，设置 `allowSwitch` 控制是否允许用户切换

**Q: 如何调整每页显示的文章数量？**
A: 修改 `pagination.postsPerPage` 的值

**Q: 如何设置横幅图片位置？**
A: 修改 `backgroundWallpaper.banner.position` 的值，支持所有 CSS `object-position` 值

**Q: 为什么图片位置不生效？**
A: 确保 `position` 配置在 `backgroundWallpaper.banner.position` 中，而不是 `backgroundWallpaper.position`

**Q: 布局切换按钮在哪里？**
A: 在导航栏右侧，屏幕宽度大于1200px时显示

**Q: 为什么小屏幕上看不到布局切换按钮？**
A: 小屏幕（<1200px）会自动使用列表模式，因此隐藏切换按钮
