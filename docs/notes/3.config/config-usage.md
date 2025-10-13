---
title: 站点配置
createTime: 2025/10/11 18:38:13
permalink: /config/config-usage/
---
# 主配置文件

## 概述

`config.ts` 文件是 `Firefly` 的核心配置文件，集成了所有功能模块的配置，包括站点信息、主题设置、功能开关等。

## 文件位置

```
src/config.ts
```


## 站点基础配置 (siteConfig)

### 基本信息

```typescript
export const siteConfig: SiteConfig = {
  title: "Firefly",                    // 网站标题
  subtitle: "Demo site",               // 网站副标题
  keywords: [                          // SEO关键词
    "Firefly",
    "Fuwari", 
    "Astro",
    "ACGN",
    "博客",
    "技术博客",
    "静态博客",
  ],
  lang: "zh_CN",                       // 网站语言
};
```

### 主题颜色配置

```typescript
themeColor: {
  hue: 155,                    // 主题色相 (0-360)
  fixed: false,                // 是否固定主题色
  defaultMode: "system",       // 默认模式
}
```

**色相值参考：**
- 红色：0
- 橙色：30
- 黄色：60
- 绿色：120
- 青色：180
- 蓝色：240
- 紫色：300
- 粉色：330

**默认模式选项：**
- `"light"`：浅色模式
- `"dark"`：深色模式
- `"system"`：跟随系统

### 网站图标配置

```typescript
favicon: [
  {
    src: "/assets/images/favicon.ico",  // 图标文件路径
    theme: "light",                     // 主题类型
    sizes: "32x32",                     // 图标大小
  },
]
```

### Logo配置

```typescript
logoIcon: {
  type: "image",                       // 图标类型
  value: "/assets/images/LiuYingPure3.svg", // 图标路径
  alt: "🍀",                          // 替代文本
}
```

**支持的图标类型：**
- `"icon"`：Astro图标库
- `"image"`：本地或网络图片

**图标类型示例：**
```typescript
// Astro图标库
logoIcon: {
  type: "icon",
  value: "material-symbols:home-pin-outline"
}

// 本地图片
logoIcon: {
  type: "image",
  value: "/assets/images/logo.webp",
  alt: "Firefly Logo"
}

// 网络图片
logoIcon: {
  type: "image", 
  value: "https://example.com/logo.png",
  alt: "Firefly Logo"
}
```

## 背景壁纸配置

### 基础配置

```typescript
backgroundWallpaper: {
  enable: true,                        // 启用背景壁纸
  mode: "banner",                      // 壁纸模式
  src: {
    desktop: "/assets/images/d1.webp", // 桌面背景
    mobile: "/assets/images/m1.webp",  // 移动背景
  },
  position: "10% 20%",                 // 图片位置
}
```

### 壁纸模式

| 模式 | 说明 | 使用场景 |
|------|------|----------|
| `"banner"` | Banner壁纸模式 | 主页横幅 |
| `"overlay"` | 全屏透明覆盖 | 背景装饰 |

### 图片位置配置

```typescript
// 常用位置值
position: "center"           // 居中
position: "top"              // 顶部居中
position: "bottom"           // 底部居中
position: "left"             // 左侧居中
position: "right"            // 右侧居中
position: "10% 20%"          // 自定义位置
position: "left top"         // 左上角
position: "right bottom"     // 右下角
```

### Banner模式配置

```typescript
banner: {
  homeText: {
    enable: true,                     // 启用主页文本
    title: "Lovely firefly!",         // 主标题
    subtitle: [                       // 副标题数组
      "In Reddened Chrysalis, I Once Rest",
      "From Shattered Sky, I Free Fall",
      // ... 更多副标题
    ],
    typewriter: {
      enable: true,                   // 启用打字机效果
      speed: 100,                     // 打字速度(ms)
      deleteSpeed: 50,                // 删除速度(ms)
      pauseTime: 2000,                // 暂停时间(ms)
    },
  },
  credit: {
    enable: {
      desktop: false,                 // 桌面端显示来源
      mobile: false,                  // 移动端显示来源
    },
    text: {
      desktop: "Desktop Credit",      // 桌面端来源文本
      mobile: "Mobile Credit",        // 移动端来源文本
    },
    url: {
      desktop: "",                    // 桌面端来源链接
      mobile: "",                     // 移动端来源链接
    },
  },
  navbar: {
    transparentMode: "semifull",      // 导航栏透明模式
  },
  waves: {
    enable: {
      desktop: true,                  // 桌面端波浪效果
      mobile: true,                   // 移动端波浪效果
    },
  },
}
```

### 导航栏透明模式

| 模式 | 说明 |
|------|------|
| `"semi"` | 半透明加圆角 |
| `"full"` | 完全透明 |
| `"semifull"` | 动态透明 |

### 全屏覆盖模式配置

```typescript
overlay: {
  zIndex: -1,                         // 层级
  opacity: 0.8,                       // 透明度
  blur: 1,                            // 模糊程度
}
```

## 功能配置

### 目录功能
depth已经弃用
```typescript
toc: {
  enable: true,                       // 启用目录
  depth: 3,                          // 目录深度 (1-6)
}
```

### 文章编辑时间

```typescript
showLastModified: true,              // 显示上次编辑时间
```

### OpenGraph图片

```typescript
generateOgImages: false,             // 生成OG图片（影响构建时间）
```

### 追番配置

```typescript
bangumi: {
  userId: "1163581",                 // Bangumi用户ID
}
```

## 用户资料配置 (profileConfig)

```typescript
export const profileConfig: ProfileConfig = {
  avatar: "/assets/images/avatar.webp",  // 头像路径
  name: "Firefly",                      // 用户名
  bio: "Hello, I'm Firefly.",          // 个人简介
  links: [                              // 社交链接
    {
      name: "Bilibli",
      icon: "fa6-brands:bilibili",
      url: "https://space.bilibili.com/38932988",
    },
    {
      name: "GitHub", 
      icon: "fa6-brands:github",
      url: "https://github.com/CuteLeaf",
    },
  ],
};
```

## 许可证配置 (licenseConfig)

```typescript
export const licenseConfig: LicenseConfig = {
  enable: true,                       // 启用许可证
  name: "CC BY-NC-SA 4.0",           // 许可证名称
  url: "https://creativecommons.org/licenses/by-nc-sa/4.0/", // 许可证链接
};
```

## 代码高亮配置 (expressiveCodeConfig)

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  theme: "github-dark",               // 代码主题
};
```

**支持的主题：**
- `"github-dark"`
- `"github-light"`
- `"monokai"`
- `"dracula"`
- `"one-dark"`

## 评论配置 (commentConfig)

```typescript
export const commentConfig: CommentConfig = {
  enable: false,                      // 启用评论
  twikoo: {
    envId: "https://twikoo.vercel.app", // Twikoo环境ID
    lang: "en",                       // 评论语言
  },
};
```

## 公告配置 (announcementConfig)

```typescript
export const announcementConfig: AnnouncementConfig = {
  title: "公告",                      // 公告标题
  content: "欢迎来到我的博客！这是一则示例公告。", // 公告内容
  closable: true,                     // 可关闭
  link: {
    enable: true,                     // 启用链接
    text: "了解更多",                 // 链接文本
    url: "/about/",                   // 链接地址
    external: false,                  // 内部链接
  },
};
```

## 页脚配置 (footerConfig)

```typescript
export const footerConfig: FooterConfig = {
  enable: false,                      // 启用页脚HTML注入
};
```

## 樱花特效配置 (sakuraConfig)

```typescript
export const sakuraConfig: SakuraConfig = {
  enable: false,                      // 启用樱花特效
  sakuraNum: 21,                      // 樱花数量
  limitTimes: -1,                     // 越界限制次数 (-1为无限)
  size: {
    min: 0.5,                         // 最小尺寸倍数
    max: 1.1,                         // 最大尺寸倍数
  },
  speed: {
    horizontal: {
      min: -1.7,                      // 水平速度最小值
      max: -1.2,                      // 水平速度最大值
    },
    vertical: {
      min: 1.5,                       // 垂直速度最小值
      max: 2.2,                       // 垂直速度最大值
    },
    rotation: 0.03,                   // 旋转速度
  },
  zIndex: 100,                        // 层级
};
```

## 统计配置 (umamiConfig)

```typescript
export const umamiConfig = {
  enabled: false,                     // 启用Umami统计
  apiKey: "api_XXXXXXXXXX",          // API密钥
  baseUrl: "https://api.umami.is",   // API地址
  scripts: `                         // 统计脚本
<script defer src="XXXX.XXX" data-website-id="ABCD1234"></script>
  `.trim(),
};
```

