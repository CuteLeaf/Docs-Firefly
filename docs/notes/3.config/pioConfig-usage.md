---
title: 看板娘配置
createTime: 2025/10/11 18:38:14
permalink: /config/pioConfig-usage/
---
# 看板娘配置

## 概述

`pioConfig.ts` 文件用于配置网站中的看板娘功能，支持 Spine 和 Live2D 两种类型的看板娘模型。

## 文件位置

```
src/config/pioConfig.ts
```

## 配置类型

### 1. Spine 看板娘配置

Spine 是一种2D骨骼动画技术，适合制作轻量级的看板娘动画。

#### 基本配置结构

```typescript
interface SpineModelConfig {
  enable: boolean;                    // 是否启用
  model: {
    path: string;                    // 模型文件路径
    scale: number;                   // 缩放比例
    x: number;                       // X轴偏移
    y: number;                       // Y轴偏移
  };
  position: {
    corner: string;                  // 显示位置
    offsetX: number;                 // X轴偏移
    offsetY: number;                 // Y轴偏移
  };
  size: {
    width: number;                   // 容器宽度
    height: number;                  // 容器高度
  };
  interactive: {
    enabled: boolean;                // 是否启用交互
    clickAnimations: string[];       // 点击动画列表
    clickMessages: string[];         // 点击消息列表
    messageDisplayTime: number;      // 消息显示时间
    idleAnimations: string[];        // 待机动画列表
    idleInterval: number;            // 待机动画间隔
  };
  responsive: {
    hideOnMobile: boolean;           // 移动端是否隐藏
    mobileBreakpoint: number;        // 移动端断点
  };
  zIndex: number;                    // 层级
  opacity: number;                   // 透明度
}
```

#### 配置示例

```typescript
export const spineModelConfig: SpineModelConfig = {
  enable: true,
  model: {
    path: "/pio/models/spine/firefly/1310.json",
    scale: 1.0,
    x: 0,
    y: 0,
  },
  position: {
    corner: "bottom-left",
    offsetX: 0,
    offsetY: 0,
  },
  size: {
    width: 250,
    height: 280,
  },
  interactive: {
    enabled: true,
    clickAnimations: [
      "emoji_0", "emoji_1", "emoji_2", 
      "emoji_3", "emoji_4", "emoji_5", "emoji_6"
    ],
    clickMessages: [
      "你好呀！我是流萤~",
      "今天也要加油哦！✨",
      "想要一起去看星空吗？🌟"
    ],
    messageDisplayTime: 3000,
    idleAnimations: ["idle", "emoji_0", "emoji_1"],
    idleInterval: 8000,
  },
  responsive: {
    hideOnMobile: true,
    mobileBreakpoint: 768,
  },
  zIndex: 1000,
  opacity: 1.0,
};
```

### 2. Live2D 看板娘配置

Live2D 是一种更高级的2D角色动画技术，提供更丰富的表情和动作。

#### 基本配置结构

```typescript
interface Live2DModelConfig {
  enable: boolean;                    // 是否启用
  model: {
    path: string;                    // 模型文件路径
  };
  position: {
    corner: string;                  // 显示位置
    offsetX: number;                 // X轴偏移
    offsetY: number;                 // Y轴偏移
  };
  size: {
    width: number;                   // 容器宽度
    height: number;                  // 容器高度
  };
  interactive: {
    enabled: boolean;                // 是否启用交互
    clickMessages: string[];         // 点击消息列表
    messageDisplayTime: number;      // 消息显示时间
  };
  responsive: {
    hideOnMobile: boolean;           // 移动端是否隐藏
    mobileBreakpoint: number;        // 移动端断点
  };
}
```

#### 配置示例

```typescript
export const live2dModelConfig: Live2DModelConfig = {
  enable: false,
  model: {
    path: "/pio/models/live2d/snow_miku/model.json",
  },
  position: {
    corner: "bottom-right",
    offsetX: 0,
    offsetY: 0,
  },
  size: {
    width: 230,
    height: 280,
  },
  interactive: {
    enabled: true,
    clickMessages: [
      "你好！我是Miku~",
      "有什么需要帮助的吗？",
      "今天天气真不错呢！"
    ],
    messageDisplayTime: 3000,
  },
  responsive: {
    hideOnMobile: true,
    mobileBreakpoint: 768,
  },
};
```

## 配置选项详解

### 位置配置 (position)

#### 显示位置 (corner)

| 值 | 说明 |
|----|------|
| `"bottom-left"` | 左下角 |
| `"bottom-right"` | 右下角 |
| `"top-left"` | 左上角 |
| `"top-right"` | 右上角 |

#### 偏移设置

```typescript
position: {
  corner: "bottom-right",
  offsetX: 20,  // 距离右边缘20px
  offsetY: 20,  // 距离底部20px
}
```

### 尺寸配置 (size)

```typescript
size: {
  width: 250,   // 容器宽度（像素）
  height: 280,  // 容器高度（像素）
}
```

**注意事项：**
- 尺寸过大会影响页面性能
- 建议根据模型实际大小调整
- 移动端会自动缩放

### 交互配置 (interactive)

#### 点击动画 (clickAnimations)

```typescript
clickAnimations: [
  "emoji_0",    // 动画名称1
  "emoji_1",    // 动画名称2
  "emoji_2"     // 动画名称3
]
```

**说明：**
- 动画名称必须与模型文件中的动画名称一致
- 点击时会随机播放其中一个动画
- 可以添加多个动画增加趣味性

#### 点击消息 (clickMessages)

```typescript
clickMessages: [
  "你好呀！我是流萤~",
  "今天也要加油哦！✨",
  "想要一起去看星空吗？🌟"
]
```

**说明：**
- 点击时会随机显示一条消息
- 支持emoji表情
- 消息会显示在模型旁边

#### 待机动画 (idleAnimations)

```typescript
idleAnimations: [
  "idle",      // 基础待机动画
  "emoji_0",   // 其他待机动画
  "emoji_1"
]
```

**说明：**
- 模型空闲时会循环播放这些动画
- 建议包含一个基础的idle动画
- 可以添加多个动画增加变化

### 响应式配置 (responsive)

```typescript
responsive: {
  hideOnMobile: true,        // 移动端隐藏
  mobileBreakpoint: 768,     // 移动端断点（像素）
}
```

**断点说明：**
- 屏幕宽度小于断点值时视为移动端
- 移动端可以隐藏看板娘以节省空间
- 建议断点设置为768px

## 模型文件管理

### 文件结构

```
public/pio/models/
├── spine/                    # Spine模型目录
│   └── firefly/             # 具体模型目录
│       ├── 1310.json        # 模型配置文件
│       ├── 1310.atlas       # 图集文件
│       └── 1310.png         # 纹理图片
└── live2d/                  # Live2D模型目录
    └── snow_miku/           # 具体模型目录
        ├── model.json       # 模型配置文件
        └── textures/        # 纹理目录
            └── *.png        # 纹理图片
```

### 模型文件获取

#### Spine 模型

1. 从官方商店购买或下载免费模型
2. 导出为JSON格式
3. 确保包含.atlas和.png文件

#### Live2D 模型

1. 从官方商店购买或下载免费模型
2. 确保包含model.json文件
3. 整理纹理文件到textures目录

## 性能优化建议

### 1. 模型选择

```typescript
// 选择轻量级模型
model: {
  path: "/pio/models/spine/simple-model.json", // 简单模型
  scale: 0.8,  // 适当缩小
}
```

### 2. 动画控制

```typescript
interactive: {
  idleInterval: 10000,  // 增加待机动画间隔
  clickAnimations: ["simple_click"], // 减少点击动画数量
}
```

### 3. 响应式设置

```typescript
responsive: {
  hideOnMobile: true,        // 移动端隐藏
  mobileBreakpoint: 1024,    // 提高断点
}
```

## 常见问题

### Q: 看板娘不显示怎么办？

A: 检查以下项目：
1. `enable` 是否设置为 `true`
2. 模型文件路径是否正确
3. 模型文件是否完整
4. 浏览器控制台是否有错误

### Q: 如何更换看板娘模型？

A: 修改 `model.path` 路径：

```typescript
model: {
  path: "/pio/models/spine/new-model/model.json",
}
```

### Q: 如何调整看板娘大小？

A: 修改 `size` 配置：

```typescript
size: {
  width: 200,   // 调整宽度
  height: 250,  // 调整高度
}
```

### Q: 如何添加更多点击消息？

A: 在 `clickMessages` 数组中添加：

```typescript
clickMessages: [
  "原有消息1",
  "原有消息2",
  "新消息1",  // 添加新消息
  "新消息2",  // 添加新消息
]
```

## 注意事项

1. **性能考虑**：看板娘会增加页面加载时间，建议在移动端隐藏
2. **文件大小**：模型文件较大，建议压缩纹理图片
3. **浏览器兼容**：某些旧浏览器可能不支持WebGL
4. **版权问题**：使用模型时注意版权许可
5. **用户体验**：避免过于频繁的动画影响阅读体验

## 高级配置

### 自定义动画序列

```typescript
interactive: {
  clickAnimations: [
    "wave",      // 挥手动画
    "jump",      // 跳跃动画
    "dance",     // 舞蹈动画
    "sleep"      // 睡觉动画
  ],
  idleAnimations: [
    "idle",      // 基础待机
    "blink",     // 眨眼
    "look_around" // 四处张望
  ],
}
```

### 动态消息系统

```typescript
clickMessages: [
  "现在是${new Date().getHours()}点哦~",
  "今天天气${weather}呢！",
  "欢迎第${visitCount}次访问！"
]
```

### 条件显示

```typescript
// 根据时间显示不同消息
const getTimeMessage = () => {
  const hour = new Date().getHours();
  if (hour < 12) return "早上好！";
  if (hour < 18) return "下午好！";
  return "晚上好！";
};
```
