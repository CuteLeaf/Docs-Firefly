---
title: 侧边栏配置
createTime: 2025/10/11 18:38:14
permalink: /config/sidebarConfig-usage/
---
# 侧边栏配置

## 概述

`sidebarConfig.ts` 文件用于配置网站侧边栏的布局、组件显示、排序、动画和响应式行为。

## 文件位置

```
src/config/sidebarConfig.ts
```

## 配置结构

```typescript
interface SidebarLayoutConfig {
  enable: boolean;                    // 是否启用侧边栏功能
  position: "left" | "right";        // 侧边栏位置
  components: SidebarComponent[];     // 侧边栏组件配置列表
  defaultAnimation: AnimationConfig; // 默认动画配置
  responsive: ResponsiveConfig;      // 响应式布局配置
}

interface SidebarComponent {
  type: string;                      // 组件类型
  enable: boolean;                   // 是否启用该组件
  order: number;                     // 显示顺序
  position: "top" | "sticky";        // 组件位置
  class: string;                     // CSS类名
  animationDelay: number;            // 动画延迟时间
  responsive?: ResponsiveOptions;    // 响应式配置
  configId?: string;                 // 配置ID（用于广告等组件）
}
```

## 基础配置

```typescript
export const sidebarLayoutConfig: SidebarLayoutConfig = {
  // 是否启用侧边栏功能
  enable: true,

  // 侧边栏位置：左侧或右侧
  position: "left",

  // 侧边栏组件配置列表
  components: [
    // 组件配置...
  ],

  // 默认动画配置
  defaultAnimation: {
    enable: true,
    baseDelay: 0,
    increment: 50,
  },

  // 响应式布局配置
  responsive: {
    breakpoints: {
      mobile: 768,
      tablet: 1024,
      desktop: 1280,
    },
    layout: {
      mobile: "sidebar",
      tablet: "sidebar", 
      desktop: "sidebar",
    },
  },
};
```

## 支持的组件类型

### 1. 用户资料组件 (profile)

```typescript
{
  type: "profile",
  enable: true,
  order: 1,
  position: "top",
  class: "onload-animation",
  animationDelay: 0,
}
```

**功能：**
- 显示用户头像、姓名、简介
- 显示社交链接
- 显示网站统计数据

### 2. 公告组件 (announcement)

```typescript
{
  type: "announcement",
  enable: true,
  order: 2,
  position: "top",
  class: "onload-animation",
  animationDelay: 50,
}
```

**功能：**
- 显示重要公告信息
- 支持关闭功能
- 支持链接跳转

### 3. 分类组件 (categories)

```typescript
{
  type: "categories",
  enable: true,
  order: 3,
  position: "sticky",
  class: "onload-animation",
  animationDelay: 150,
  responsive: {
    collapseThreshold: 5,  // 超过5个分类时自动折叠
  },
}
```

**功能：**
- 显示文章分类列表
- 自动折叠功能
- 显示分类文章数量

### 4. 标签组件 (tags)

```typescript
{
  type: "tags",
  enable: true,
  order: 5,
  position: "sticky",
  class: "onload-animation",
  animationDelay: 250,
  responsive: {
    collapseThreshold: 20,  // 超过20个标签时自动折叠
  },
}
```

**功能：**
- 显示文章标签云
- 自动折叠功能
- 显示标签使用频率

### 5. 广告组件 (advertisement)

```typescript
{
  type: "advertisement",
  enable: true,
  order: 6,
  position: "sticky",
  class: "onload-animation",
  animationDelay: 300,
  configId: "ad1",  // 对应 adConfig1
}
```

**功能：**
- 显示广告内容
- 支持图片和文字广告
- 支持关闭功能

## 组件配置详解

### 组件类型 (type)

| 类型 | 说明 | 必需配置 |
|------|------|----------|
| `profile` | 用户资料组件 | 无 |
| `announcement` | 公告组件 | 无 |
| `categories` | 分类组件 | 无 |
| `tags` | 标签组件 | 无 |
| `advertisement` | 广告组件 | `configId` |

### 显示顺序 (order)

```typescript
// 数字越小越靠前
components: [
  { type: "profile", order: 1 },      // 最前面
  { type: "announcement", order: 2 }, // 第二
  { type: "categories", order: 3 },   // 第三
  { type: "tags", order: 5 },         // 第四
  { type: "advertisement", order: 6 }, // 最后
]
```

### 组件位置 (position)

| 值 | 说明 | 使用场景 |
|----|------|----------|
| `"top"` | 固定在顶部 | 重要组件（资料、公告） |
| `"sticky"` | 粘性定位，可滚动 | 一般组件（分类、标签、广告） |

### 动画配置

```typescript
{
  class: "onload-animation",    // 动画CSS类
  animationDelay: 100,          // 延迟时间（毫秒）
}
```

**延迟时间建议：**
- 第一个组件：0ms
- 后续组件：递增50ms
- 避免动画重叠

### 响应式配置 (responsive)

```typescript
{
  responsive: {
    collapseThreshold: 5,  // 折叠阈值
  },
}
```

**折叠阈值：**
- 分类组件：建议5-10个
- 标签组件：建议15-25个
- 超过阈值时自动折叠

## 动画系统

### 默认动画配置

```typescript
defaultAnimation: {
  enable: true,        // 是否启用默认动画
  baseDelay: 0,        // 基础延迟时间
  increment: 50,       // 递增延迟时间
}
```

### 组件动画延迟

```typescript
// 推荐配置：递增延迟
components: [
  { animationDelay: 0 },    // 0ms
  { animationDelay: 50 },   // 50ms
  { animationDelay: 100 },  // 100ms
  { animationDelay: 150 },  // 150ms
  { animationDelay: 200 },  // 200ms
]
```

### 动画类名

```typescript
// 可用的动画类名
class: "onload-animation"     // 加载动画
class: "fade-in"             // 淡入动画
class: "slide-in-left"       // 从左滑入
class: "slide-in-right"      // 从右滑入
class: "bounce-in"           // 弹跳进入
```

## 响应式布局

### 断点配置

```typescript
responsive: {
  breakpoints: {
    mobile: 768,      // 移动端：< 768px
    tablet: 1024,     // 平板端：< 1024px
    desktop: 1280,    // 桌面端：< 1280px
  },
}
```

### 布局模式

```typescript
layout: {
  mobile: "sidebar",    // 移动端：显示侧边栏
  tablet: "sidebar",    // 平板端：显示侧边栏
  desktop: "sidebar",   // 桌面端：显示侧边栏
}
```

**布局模式说明：**
- `"hidden"`：不显示侧边栏
- `"drawer"`：抽屉模式（移动端不显示）
- `"sidebar"`：显示侧边栏

### 响应式组件配置

```typescript
{
  type: "categories",
  responsive: {
    collapseThreshold: 5,  // 超过5个时折叠
  },
}
```

## 完整配置示例

```typescript
export const sidebarLayoutConfig: SidebarLayoutConfig = {
  enable: true,
  position: "left",
  
  components: [
    // 用户资料 - 固定在顶部
    {
      type: "profile",
      enable: true,
      order: 1,
      position: "top",
      class: "onload-animation",
      animationDelay: 0,
    },
    
    // 公告 - 固定在顶部
    {
      type: "announcement",
      enable: true,
      order: 2,
      position: "top",
      class: "onload-animation",
      animationDelay: 50,
    },
    
    // 分类 - 粘性定位
    {
      type: "categories",
      enable: true,
      order: 3,
      position: "sticky",
      class: "onload-animation",
      animationDelay: 150,
      responsive: {
        collapseThreshold: 5,
      },
    },
    
    // 标签 - 粘性定位
    {
      type: "tags",
      enable: true,
      order: 5,
      position: "sticky",
      class: "onload-animation",
      animationDelay: 250,
      responsive: {
        collapseThreshold: 20,
      },
    },
    
    // 广告1 - 粘性定位
    {
      type: "advertisement",
      enable: true,
      order: 6,
      position: "sticky",
      class: "onload-animation",
      animationDelay: 300,
      configId: "ad1",
    },
    
    // 广告2 - 粘性定位（已禁用）
    {
      type: "advertisement",
      enable: false,  // 禁用
      order: 7,
      position: "sticky",
      class: "onload-animation",
      animationDelay: 350,
      configId: "ad2",
    },
  ],
  
  defaultAnimation: {
    enable: true,
    baseDelay: 0,
    increment: 50,
  },
  
  responsive: {
    breakpoints: {
      mobile: 768,
      tablet: 1024,
      desktop: 1280,
    },
    layout: {
      mobile: "sidebar",
      tablet: "sidebar",
      desktop: "sidebar",
    },
  },
};
```

## 组件管理

### 启用/禁用组件

```typescript
// 启用组件
{
  type: "categories",
  enable: true,  // 启用
}

// 禁用组件
{
  type: "advertisement",
  enable: false, // 禁用
}
```

### 调整组件顺序

```typescript
// 调整order值来改变显示顺序
components: [
  { type: "profile", order: 1 },      // 最前面
  { type: "categories", order: 2 },   // 第二
  { type: "tags", order: 3 },         // 第三
  { type: "advertisement", order: 4 }, // 最后
]
```

### 添加新组件

```typescript
// 在components数组中添加新组件
components: [
  // 现有组件...
  {
    type: "custom-component",  // 新组件类型
    enable: true,
    order: 8,                  // 新的顺序
    position: "sticky",
    class: "onload-animation",
    animationDelay: 400,
  },
]
```

## 最佳实践

### 1. 组件顺序规划

```typescript
// 推荐顺序
components: [
  { type: "profile", order: 1 },        // 用户信息最重要
  { type: "announcement", order: 2 },   // 公告次重要
  { type: "categories", order: 3 },     // 导航功能
  { type: "tags", order: 4 },           // 导航功能
  { type: "advertisement", order: 5 },  // 广告最后
]
```

### 2. 动画延迟设置

```typescript
// 推荐：递增延迟，避免重叠
animationDelay: 0,    // 第一个组件
animationDelay: 50,   // 第二个组件
animationDelay: 100,  // 第三个组件
animationDelay: 150,  // 第四个组件
```

### 3. 响应式考虑

```typescript
// 移动端友好的配置
responsive: {
  breakpoints: {
    mobile: 768,    // 合理的断点
  },
  layout: {
    mobile: "sidebar",  // 移动端也显示侧边栏
  },
}
```

### 4. 性能优化

```typescript
// 禁用不必要的组件
{
  type: "advertisement",
  enable: false,  // 如果不需要广告，直接禁用
}
```

## 常见问题

### Q: 如何禁用整个侧边栏？

A: 设置 `enable: false`：

```typescript
export const sidebarLayoutConfig: SidebarLayoutConfig = {
  enable: false,  // 禁用整个侧边栏
  // ... 其他配置
};
```

### Q: 如何调整侧边栏位置？

A: 修改 `position` 配置：

```typescript
{
  position: "right",  // 改为右侧
}
```

### Q: 如何添加新的组件类型？

A: 需要先实现对应的组件，然后在配置中添加：

```typescript
{
  type: "new-component",  // 新组件类型
  enable: true,
  order: 10,
  position: "sticky",
  class: "onload-animation",
  animationDelay: 500,
}
```

### Q: 如何调整组件显示顺序？

A: 修改 `order` 值：

```typescript
// 将分类组件移到最前面
{
  type: "categories",
  order: 1,  // 改为1，会显示在最前面
}
```

### Q: 动画不生效怎么办？

A: 检查以下项目：
1. `defaultAnimation.enable` 是否为 `true`
2. 组件是否设置了正确的 `class`
3. CSS动画类是否已定义

### Q: 如何自定义动画延迟？

A: 修改 `animationDelay` 值：

```typescript
{
  type: "categories",
  animationDelay: 200,  // 自定义延迟时间
}
```

## 高级配置

### 条件显示组件

```typescript
// 根据环境显示不同组件
const getComponents = () => {
  const baseComponents = [
    { type: "profile", enable: true, order: 1 },
    { type: "categories", enable: true, order: 2 },
  ];
  
  // 开发环境显示调试组件
  if (process.env.NODE_ENV === 'development') {
    baseComponents.push({
      type: "debug-info",
      enable: true,
      order: 10,
      position: "sticky",
      class: "onload-animation",
      animationDelay: 500,
    });
  }
  
  return baseComponents;
};
```

### 动态组件配置

```typescript
// 根据用户权限显示不同组件
const getUserComponents = (userRole: string) => {
  const components = [
    { type: "profile", enable: true, order: 1 },
    { type: "categories", enable: true, order: 2 },
  ];
  
  if (userRole === 'admin') {
    components.push({
      type: "admin-panel",
      enable: true,
      order: 5,
      position: "sticky",
      class: "onload-animation",
      animationDelay: 300,
    });
  }
  
  return components;
};
```

### 主题相关配置

```typescript
// 根据主题显示不同组件
const getThemeComponents = (theme: string) => {
  const components = [
    { type: "profile", enable: true, order: 1 },
  ];
  
  if (theme === 'minimal') {
    // 极简主题只显示必要组件
    components.push({ type: "categories", enable: true, order: 2 });
  } else {
    // 完整主题显示所有组件
    components.push(
      { type: "announcement", enable: true, order: 2 },
      { type: "categories", enable: true, order: 3 },
      { type: "tags", enable: true, order: 4 },
      { type: "advertisement", enable: true, order: 5 }
    );
  }
  
  return components;
};
```
