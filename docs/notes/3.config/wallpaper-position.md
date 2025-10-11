---
title: 壁纸位置配置详解
createTime: 2025/10/11 18:38:13
permalink: /config/wallpaper-position/
---
# 壁纸位置配置详解

## 概述

`backgroundWallpaper.position` 配置现在支持所有 CSS `object-position` 属性值，提供更精确的壁纸定位控制。

## 支持的位置值类型

### 1. 关键词组合

#### 单关键词
- `"top"` - 顶部居中
- `"center"` - 居中（默认）
- `"bottom"` - 底部居中
- `"left"` - 左侧居中
- `"right"` - 右侧居中

#### 双关键词组合
- `"top left"` 或 `"left top"` - 左上角
- `"top center"` - 顶部居中
- `"top right"` 或 `"right top"` - 右上角
- `"center left"` 或 `"left center"` - 左侧居中
- `"center center"` - 正中央
- `"center right"` 或 `"right center"` - 右侧居中
- `"bottom left"` 或 `"left bottom"` - 左下角
- `"bottom center"` - 底部居中
- `"bottom right"` 或 `"right bottom"` - 右下角

### 2. 百分比值

#### 单值（应用于水平和垂直方向）
- `"25%"` - 水平和垂直都偏移25%
- `"50%"` - 居中（等同于 "center"）

#### 双值（水平 垂直）
- `"0% 0%"` - 左上角
- `"50% 0%"` - 顶部居中
- `"100% 0%"` - 右上角
- `"0% 50%"` - 左侧居中
- `"50% 50%"` - 正中央
- `"100% 50%"` - 右侧居中
- `"0% 100%"` - 左下角
- `"50% 100%"` - 底部居中
- `"100% 100%"` - 右下角
- `"25% 75%"` - 自定义位置

### 3. 像素值

#### 单值
- `"10px"` - 水平和垂直都偏移10像素

#### 双值
- `"10px 20px"` - 水平偏移10px，垂直偏移20px
- `"-10px 0px"` - 向左偏移10px，垂直居中
- `"0px -20px"` - 水平居中，向上偏移20px

### 4. 混合值

- `"left 25%"` - 左对齐，垂直25%位置
- `"right 10px"` - 右对齐，垂直偏移10像素
- `"25% top"` - 水平25%位置，顶部对齐
- `"10px bottom"` - 水平偏移10像素，底部对齐

## 配置示例

### 基本位置配置

```typescript
backgroundWallpaper: {
  enable: true,
  mode: "banner",
  src: {
    desktop: "/assets/desktop-banner/d1.webp",
    mobile: "/assets/mobile-banner/m1.webp",
  },
  position: "center", // 默认居中
}
```

### 精确位置控制

```typescript
// 示例1：右上角定位
position: "top right"

// 示例2：自定义百分比定位
position: "25% 75%" // 水平25%，垂直75%

// 示例3：像素偏移
position: "10px 20px" // 右偏移10px，下偏移20px

// 示例4：混合定位
position: "left 25%" // 左对齐，垂直25%位置

// 示例5：负值偏移（裁剪效果）
position: "-50px 0px" // 向左裁剪50px
```

### 常用场景配置

#### 人物肖像壁纸（突出主体）
```typescript
position: "center top" // 保持人物头部在可见区域
```

#### 风景壁纸（突出远景）
```typescript
position: "center 25%" // 突出天空和远景
```

#### 建筑壁纸（突出建筑主体）
```typescript
position: "50% 40%" // 根据建筑位置调整
```

#### 动漫壁纸（角色居中）
```typescript
position: "center" // 保持角色在中央
```

## 响应式考虑

由于桌面端和移动端使用不同的图片源，可以为不同设备优化位置：

```typescript
// 如果需要不同设备使用不同位置，可以考虑在未来版本中支持：
// position: {
//   desktop: "center top",
//   mobile: "center center"
// }

// 当前版本统一使用一个位置值
position: "center top"
```

## 调试技巧

### 1. 使用浏览器开发者工具
- 打开开发者工具（F12）
- 选择壁纸图片元素
- 在样式面板中实时调整 `object-position` 值
- 找到最佳位置后复制到配置文件

### 2. 常用调试值
```typescript
// 调试时可以尝试这些值来理解效果
"0% 0%"     // 左上角
"50% 0%"    // 顶部居中  
"100% 0%"   // 右上角
"0% 50%"    // 左侧居中
"50% 50%"   // 正中央
"100% 50%"  // 右侧居中
"0% 100%"   // 左下角
"50% 100%"  // 底部居中
"100% 100%" // 右下角
```

## 最佳实践

1. **测试不同设备**：确保在桌面端和移动端都有良好效果
2. **考虑内容遮挡**：避免重要的壁纸内容被导航栏或文字遮挡
3. **保持一致性**：在整个网站中保持一致的视觉风格
4. **性能优化**：避免使用过大的偏移值导致图片加载区域超出视口

## 注意事项

- 百分比值基于容器尺寸计算
- 像素值为绝对定位，不随容器大小变化
- 负值可以实现图片裁剪效果
- 过大的偏移值可能导致图片主要内容不可见