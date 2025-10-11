---
title: 导航栏配置
createTime: 2025/10/11 18:38:14
permalink: /config/navBarConfig-usage/
---
# 导航栏配置

## 概述

`navBarConfig.ts` 文件用于配置网站顶部导航栏的链接结构，支持多级菜单和自定义链接。

## 文件位置

```
src/config/navBarConfig.ts
```

## 配置结构

```typescript
interface NavBarConfig {
  links: NavBarLink[];  // 导航链接数组
}

interface NavBarLink {
  name: string;                    // 链接显示名称
  url: string;                     // 链接地址
  icon?: string;                   // 图标名称
  external?: boolean;              // 是否外部链接
  children?: NavBarLink[];         // 子菜单链接
}
```

## 配置示例

```typescript
export const navBarConfig: NavBarConfig = {
  links: [
    LinkPreset.Home,              // 预设链接：首页
    LinkPreset.Archive,           // 预设链接：归档
    LinkPreset.Anime,             // 预设链接：追番
    {
      name: "链接",
      url: "/links/",
      icon: "material-symbols:link",
      children: [                 // 子菜单
        {
          name: "GitHub",
          url: "https://github.com/CuteLeaf/Firefly",
          external: true,
          icon: "fa6-brands:github",
        },
        {
          name: "Bilibili",
          url: "https://space.bilibili.com/38932988",
          external: true,
          icon: "fa6-brands:bilibili",
        },
      ],
    },
    {
      name: "关于",
      url: "/content/",
      icon: "material-symbols:info",
      children: [
        LinkPreset.About,         // 预设链接：关于
        LinkPreset.Friends,       // 预设链接：友链
      ],
    },
  ],
};
```

## 预设链接 (LinkPreset)

系统提供了一些常用的预设链接，可以直接使用：

```typescript
// 预设链接定义
export const LinkPreset = {
  Home: {
    name: "首页",
    url: "/",
    icon: "material-symbols:home",
  },
  Archive: {
    name: "归档",
    url: "/archive/",
    icon: "material-symbols:archive",
  },
  About: {
    name: "关于",
    url: "/about/",
    icon: "material-symbols:info",
  },
  Friends: {
    name: "友链",
    url: "/friends/",
    icon: "material-symbols:people",
  },
  Anime: {
    name: "追番",
    url: "/anime/",
    icon: "material-symbols:movie",
  },
} as const;
```

### 使用预设链接

```typescript
import { LinkPreset } from "../types/config";

// 直接使用预设
links: [
  LinkPreset.Home,
  LinkPreset.Archive,
  LinkPreset.About,
]

// 在子菜单中使用预设
{
  name: "导航",
  children: [
    LinkPreset.Home,
    LinkPreset.Archive,
  ]
}
```

## 自定义链接配置

### 基础链接

```typescript
{
  name: "首页",                    // 显示名称
  url: "/",                       // 链接地址
  icon: "material-symbols:home",  // 图标（可选）
  external: false,                // 内部链接
}
```

### 外部链接

```typescript
{
  name: "GitHub",
  url: "https://github.com/username",
  icon: "fa6-brands:github",
  external: true,                 // 外部链接，会在新标签页打开
}
```

### 多级菜单

```typescript
{
  name: "导航",
  url: "#",                       // 父级链接可以是 # 或不存在的路径
  icon: "material-symbols:menu",
  children: [                     // 子菜单
    {
      name: "首页",
      url: "/",
      icon: "material-symbols:home",
    },
    {
      name: "归档",
      url: "/archive/",
      icon: "material-symbols:archive",
    },
    {
      name: "外部链接",
      url: "https://example.com",
      external: true,
      icon: "material-symbols:link",
    },
  ],
}
```

## 图标系统

### 支持的图标库

1. **Material Symbols** (推荐)
   ```typescript
   icon: "material-symbols:home"
   icon: "material-symbols:info"
   icon: "material-symbols:archive"
   ```

2. **Font Awesome 6**
   ```typescript
   icon: "fa6-brands:github"
   icon: "fa6-brands:bilibili"
   icon: "fa6-solid:house"
   ```

3. **其他图标库**
   ```typescript
   icon: "lucide:home"
   icon: "heroicons:home"
   ```

### 图标命名规范

```typescript
// 格式：图标库:图标名称
"material-symbols:home"     // Material Symbols 的 home 图标
"fa6-brands:github"         // Font Awesome 6 Brands 的 github 图标
"fa6-solid:house"           // Font Awesome 6 Solid 的 house 图标
```

### 常用图标推荐

| 功能 | Material Symbols | Font Awesome 6 |
|------|------------------|----------------|
| 首页 | `material-symbols:home` | `fa6-solid:house` |
| 归档 | `material-symbols:archive` | `fa6-solid:box-archive` |
| 关于 | `material-symbols:info` | `fa6-solid:circle-info` |
| 友链 | `material-symbols:people` | `fa6-solid:users` |
| 项目 | `material-symbols:work` | `fa6-solid:briefcase` |
| 技能 | `material-symbols:psychology` | `fa6-solid:brain` |
| 时间线 | `material-symbols:timeline` | `fa6-solid:clock` |
| 链接 | `material-symbols:link` | `fa6-solid:link` |
| 更多 | `material-symbols:more-horiz` | `fa6-solid:ellipsis-horizontal` |

## 链接类型详解

### 内部链接

```typescript
{
  name: "首页",
  url: "/",                    // 以 / 开头，相对于网站根目录
  external: false,             // 或省略此属性
}
```

**特点：**
- 在当前标签页打开
- 支持路由跳转
- 加载速度快

### 外部链接

```typescript
{
  name: "GitHub",
  url: "https://github.com/username",
  external: true,              // 必须设置为 true
}
```

**特点：**
- 在新标签页打开
- 添加安全属性（noopener noreferrer）
- 显示外部链接图标

### 锚点链接

```typescript
{
  name: "回到顶部",
  url: "#top",                 // 页面内锚点
  external: false,
}
```

### 邮件链接

```typescript
{
  name: "联系我",
  url: "mailto:your@email.com",
  external: true,
  icon: "material-symbols:mail",
}
```

### 电话链接

```typescript
{
  name: "打电话",
  url: "tel:+1234567890",
  external: true,
  icon: "material-symbols:phone",
}
```

## 多级菜单配置

### 基础多级菜单

```typescript
{
  name: "导航",
  url: "#",                    // 父级链接
  icon: "material-symbols:menu",
  children: [
    {
      name: "首页",
      url: "/",
      icon: "material-symbols:home",
    },
    {
      name: "归档",
      url: "/archive/",
      icon: "material-symbols:archive",
    },
  ],
}
```

### 深层级菜单

```typescript
{
  name: "分类",
  url: "#",
  icon: "material-symbols:category",
  children: [
    {
      name: "技术",
      url: "/category/tech/",
      icon: "material-symbols:code",
      children: [               // 三级菜单
        {
          name: "前端",
          url: "/category/tech/frontend/",
          icon: "material-symbols:web",
        },
        {
          name: "后端",
          url: "/category/tech/backend/",
          icon: "material-symbols:storage",
        },
      ],
    },
    {
      name: "生活",
      url: "/category/life/",
      icon: "material-symbols:home",
    },
  ],
}
```

### 混合菜单

```typescript
{
  name: "其他",
  url: "#",
  icon: "material-symbols:more-horiz",
  children: [
    LinkPreset.About,          // 预设链接
    {
      name: "我的项目",
      url: "/projects/",
      icon: "material-symbols:work",
    },
    {
      name: "外部链接",
      url: "https://example.com",
      external: true,
      icon: "material-symbols:link",
    },
  ],
}
```

## 响应式配置

### 移动端适配

导航栏会自动适配移动端，多级菜单会转换为抽屉式菜单。

```typescript
// 移动端友好的配置
{
  name: "导航",                 // 简短名称
  url: "#",
  icon: "material-symbols:menu",
  children: [
    // 子菜单项
  ],
}
```

### 图标优先

在移动端，建议优先显示图标：

```typescript
{
  name: "首页",                 // 桌面端显示完整名称
  url: "/",
  icon: "material-symbols:home", // 移动端主要显示图标
}
```

## 最佳实践

### 1. 链接组织

```typescript
// 推荐：按重要性排序
links: [
  LinkPreset.Home,              // 最重要的链接在前
  LinkPreset.Archive,
  {
    name: "分类",
    children: [/* 分类链接 */]
  },
  {
    name: "其他",
    children: [/* 次要链接 */]
  },
]
```

### 2. 命名规范

```typescript
// 推荐：使用简洁明确的名称
{
  name: "首页",                 // 简洁
  name: "技术文章",             // 明确
  name: "关于我",               // 清晰
}

// 避免：使用过长的名称
{
  name: "这是一个非常长的导航链接名称", // 不推荐
}
```

### 3. 图标选择

```typescript
// 推荐：使用语义化的图标
{
  name: "首页",
  icon: "material-symbols:home",    // 语义明确
}

// 推荐：保持图标风格一致
{
  name: "GitHub",
  icon: "fa6-brands:github",        // 品牌图标
}
```

### 4. 外部链接处理

```typescript
// 推荐：明确标识外部链接
{
  name: "GitHub",
  url: "https://github.com/username",
  external: true,                   // 明确标识
  icon: "fa6-brands:github",
}
```

## 常见问题

### Q: 如何添加新的导航链接？

A: 在 `links` 数组中添加新对象：

```typescript
links: [
  // 现有链接...
  {
    name: "新链接",
    url: "/new-page/",
    icon: "material-symbols:new",
  },
]
```

### Q: 如何修改现有链接？

A: 直接修改对应的配置对象：

```typescript
// 修改链接地址
{
  name: "首页",
  url: "/new-home/",              // 修改URL
  icon: "material-symbols:home",
}
```

### Q: 如何删除某个链接？

A: 从 `links` 数组中移除对应项：

```typescript
links: [
  LinkPreset.Home,
  // LinkPreset.Archive,         // 注释或删除
  LinkPreset.About,
]
```

### Q: 如何调整链接顺序？

A: 调整 `links` 数组中的顺序：

```typescript
links: [
  LinkPreset.Home,
  LinkPreset.About,              // 调整顺序
  LinkPreset.Archive,
]
```

### Q: 图标不显示怎么办？

A: 检查以下项目：
1. 图标名称是否正确
2. 图标库是否支持
3. 是否安装了对应的图标库

### Q: 如何创建多级菜单？

A: 使用 `children` 属性：

```typescript
{
  name: "父菜单",
  url: "#",
  children: [
    {
      name: "子菜单1",
      url: "/sub1/",
    },
    {
      name: "子菜单2",
      url: "/sub2/",
    },
  ],
}
```

## 高级配置

### 动态链接生成

```typescript
// 根据条件生成链接
const generateLinks = () => {
  const baseLinks = [LinkPreset.Home, LinkPreset.Archive];
  
  // 根据环境添加不同链接
  if (process.env.NODE_ENV === 'development') {
    baseLinks.push({
      name: "开发工具",
      url: "/dev-tools/",
      icon: "material-symbols:build",
    });
  }
  
  return baseLinks;
};

export const navBarConfig: NavBarConfig = {
  links: generateLinks(),
};
```

### 条件显示链接

```typescript
// 根据用户权限显示不同链接
const getUserLinks = (userRole: string) => {
  const commonLinks = [LinkPreset.Home, LinkPreset.Archive];
  
  if (userRole === 'admin') {
    commonLinks.push({
      name: "管理后台",
      url: "/admin/",
      icon: "material-symbols:admin",
    });
  }
  
  return commonLinks;
};
```

### 国际化支持

```typescript
// 支持多语言的链接配置
const getLocalizedLinks = (locale: string) => {
  const translations = {
    'zh-CN': {
      home: '首页',
      archive: '归档',
      about: '关于',
    },
    'en': {
      home: 'Home',
      archive: 'Archive', 
      about: 'About',
    },
  };
  
  const t = translations[locale] || translations['zh-CN'];
  
  return [
    {
      name: t.home,
      url: "/",
      icon: "material-symbols:home",
    },
    // ... 其他链接
  ];
};
```
