---
title: 樱花特效配置
createTime: 2025/01/27 18:38:13
permalink: /config/sakuraConfig-usage/
---
# 樱花特效配置

## 概述

樱花特效配置用于在网站中添加动态的樱花飘落效果，营造浪漫的视觉氛围。

## 文件位置

```
src/config/sakuraConfig.ts
```

## 基础配置

### 启用樱花特效

```typescript
export const sakuraConfig: SakuraConfig = {
  enable: true, // 启用樱花特效
  sakuraNum: 21, // 樱花数量
  limitTimes: -1, // 樱花越界限制次数，-1为无限循环
  size: {
    min: 0.5, // 樱花最小尺寸倍数
    max: 1.1, // 樱花最大尺寸倍数
  },
  opacity: {
    min: 0.3, // 樱花最小不透明度
    max: 0.9, // 樱花最大不透明度
  },
  speed: {
    horizontal: {
      min: -1.7, // 水平移动速度最小值
      max: -1.2, // 水平移动速度最大值
    },
    vertical: {
      min: 1.5, // 垂直移动速度最小值
      max: 2.2, // 垂直移动速度最大值
    },
    rotation: 0.03, // 旋转速度
    fadeSpeed: 0.03, // 消失速度，不应大于最小不透明度
  },
  zIndex: 100, // 层级
};
```

## 配置选项详解

### 基础设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `enable` | `boolean` | 是否启用樱花特效 | `true` |
| `sakuraNum` | `number` | 樱花数量 | `21` |
| `limitTimes` | `number` | 越界限制次数，-1为无限 | `-1` |

### 尺寸设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `size.min` | `number` | 樱花最小尺寸倍数 | `0.5` |
| `size.max` | `number` | 樱花最大尺寸倍数 | `1.1` |

### 透明度设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `opacity.min` | `number` | 樱花最小不透明度 | `0.3` |
| `opacity.max` | `number` | 樱花最大不透明度 | `0.9` |

### 速度设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `speed.horizontal.min` | `number` | 水平移动速度最小值 | `-1.7` |
| `speed.horizontal.max` | `number` | 水平移动速度最大值 | `-1.2` |
| `speed.vertical.min` | `number` | 垂直移动速度最小值 | `1.5` |
| `speed.vertical.max` | `number` | 垂直移动速度最大值 | `2.2` |
| `speed.rotation` | `number` | 旋转速度 | `0.03` |
| `speed.fadeSpeed` | `number` | 消失速度，不应大于最小不透明度 | `0.03` |

### 层级设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `zIndex` | `number` | 樱花层级 | `100` |

## 使用场景

### 1. 浪漫主题网站

```typescript
export const sakuraConfig: SakuraConfig = {
  enable: true,
  sakuraNum: 30, // 更多樱花
  limitTimes: -1,
  size: {
    min: 0.8,
    max: 1.5, // 更大的樱花
  },
  opacity: {
    min: 0.4,
    max: 0.95, // 更高的透明度
  },
  speed: {
    horizontal: {
      min: -2.0,
      max: -1.0, // 更慢的飘落
    },
    vertical: {
      min: 1.0,
      max: 1.8,
    },
    rotation: 0.02, // 更慢的旋转
    fadeSpeed: 0.02, // 更慢的消失
  },
  zIndex: 100,
};
```

### 2. 简约风格

```typescript
export const sakuraConfig: SakuraConfig = {
  enable: true,
  sakuraNum: 10, // 少量樱花
  limitTimes: -1,
  size: {
    min: 0.3,
    max: 0.8, // 较小的樱花
  },
  opacity: {
    min: 0.2,
    max: 0.7, // 较低的透明度
  },
  speed: {
    horizontal: {
      min: -1.0,
      max: -0.5,
    },
    vertical: {
      min: 2.0,
      max: 3.0, // 较快的飘落
    },
    rotation: 0.05,
    fadeSpeed: 0.05, // 较快的消失
  },
  zIndex: 100,
};
```

### 3. 节日主题

```typescript
export const sakuraConfig: SakuraConfig = {
  enable: true,
  sakuraNum: 50, // 大量樱花营造节日氛围
  limitTimes: -1,
  size: {
    min: 0.4,
    max: 1.2,
  },
  opacity: {
    min: 0.5,
    max: 1.0, // 完全不透明
  },
  speed: {
    horizontal: {
      min: -2.5,
      max: -1.5,
    },
    vertical: {
      min: 1.2,
      max: 2.5,
    },
    rotation: 0.04,
    fadeSpeed: 0.04,
  },
  zIndex: 100,
};
```

## 性能优化

### 根据设备调整

```typescript
// 根据设备性能调整樱花数量
const isMobile = typeof window !== 'undefined' && window.innerWidth < 768;

export const sakuraConfig: SakuraConfig = {
  enable: true,
  sakuraNum: isMobile ? 10 : 21, // 移动端减少樱花数量
  size: {
    min: 0.5,
    max: 1.1,
  },
  opacity: {
    min: 0.3,
    max: 0.9,
  },
  speed: {
    horizontal: { min: -1.7, max: -1.2 },
    vertical: { min: 1.5, max: 2.2 },
    rotation: 0.03,
    fadeSpeed: 0.03,
  },
  zIndex: 100,
};
```

### 条件启用

```typescript
// 只在特定页面启用
export const sakuraConfig: SakuraConfig = {
  enable: process.env.NODE_ENV === 'production', // 只在生产环境启用
  // ... 其他配置
};
```

## 自定义样式

### CSS 自定义

```css
/* 樱花容器 */
.sakura-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 100;
  overflow: hidden;
}

/* 单个樱花 */
.sakura {
  position: absolute;
  width: 10px;
  height: 10px;
  background: radial-gradient(circle, #ffb3ba 0%, #ff9a9e 100%);
  border-radius: 50% 0 50% 0;
  opacity: 0.8;
  animation: sakura-fall linear infinite;
}

/* 樱花飘落动画 */
@keyframes sakura-fall {
  0% {
    transform: translateY(-100vh) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(100vh) rotate(360deg);
    opacity: 0;
  }
}

/* 不同大小的樱花 */
.sakura.small {
  width: 6px;
  height: 6px;
}

.sakura.medium {
  width: 10px;
  height: 10px;
}

.sakura.large {
  width: 14px;
  height: 14px;
}
```

### 颜色自定义

```css
/* 粉色樱花 */
.sakura.pink {
  background: radial-gradient(circle, #ffb3ba 0%, #ff9a9e 100%);
}

/* 白色樱花 */
.sakura.white {
  background: radial-gradient(circle, #ffffff 0%, #f0f0f0 100%);
}

/* 渐变樱花 */
.sakura.gradient {
  background: linear-gradient(45deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
}
```

## 响应式设计

### 移动端优化

```typescript
export const sakuraConfig: SakuraConfig = {
  enable: true,
  sakuraNum: 15, // 移动端减少数量
  limitTimes: -1,
  size: {
    min: 0.4,
    max: 0.8, // 移动端使用较小尺寸
  },
  opacity: {
    min: 0.2,
    max: 0.8, // 移动端降低透明度
  },
  speed: {
    horizontal: {
      min: -1.2,
      max: -0.8,
    },
    vertical: {
      min: 1.8,
      max: 2.5, // 移动端加快速度
    },
    rotation: 0.04,
    fadeSpeed: 0.04, // 移动端加快消失速度
  },
  zIndex: 100,
};
```

## 注意事项

1. **性能影响**：樱花特效会消耗一定的 CPU 和内存资源
2. **用户体验**：过多的樱花可能影响用户阅读内容
3. **设备兼容**：在低性能设备上可能影响页面流畅度
4. **可访问性**：动画可能对某些用户造成不适
5. **透明度设置**：`opacity.min` 和 `opacity.max` 控制樱花的透明度范围
6. **消失速度**：`fadeSpeed` 不应大于 `opacity.min`，否则樱花可能不会完全消失

## 常见问题

**Q: 如何禁用樱花特效？**
A: 将 `enable` 设置为 `false`

**Q: 樱花数量多少合适？**
A: 建议在 10-30 个之间，根据网站性能调整

**Q: 如何调整樱花飘落速度？**
A: 修改 `speed` 配置中的数值，数值越大速度越快

**Q: 樱花会影响页面性能吗？**
A: 会有一定影响，建议在低性能设备上减少樱花数量

**Q: 如何自定义樱花颜色？**
A: 通过 CSS 覆盖 `.sakura` 类的背景样式

**Q: 樱花在哪些页面显示？**
A: 默认在所有页面显示，可以通过代码控制特定页面显示

**Q: 如何调整樱花层级？**
A: 修改 `zIndex` 值，确保樱花在合适的层级显示

**Q: 如何调整樱花透明度？**
A: 修改 `opacity.min` 和 `opacity.max` 值，控制樱花的透明度范围

**Q: 樱花消失太快怎么办？**
A: 减小 `fadeSpeed` 的值，让樱花消失得更慢

**Q: 樱花不消失怎么办？**
A: 确保 `fadeSpeed` 不大于 `opacity.min`，否则樱花可能不会完全消失
