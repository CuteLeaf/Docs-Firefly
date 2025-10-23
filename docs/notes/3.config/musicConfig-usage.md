---
title: 音乐播放器配置
createTime: 2025/01/27 18:38:13
permalink: /config/musicConfig-usage/
---
# 音乐播放器配置

## 概述

音乐播放器配置用于在网站中添加音乐播放功能，支持本地音乐和在线音乐两种模式。

## 文件位置

```
src/config/musicConfig.ts
```

## 基础配置

### 启用音乐播放器

```typescript
export const musicPlayerConfig: MusicPlayerConfig = {
  enable: true, // 启用音乐播放器功能
  mode: "local", // 播放器模式："local" 本地音乐，"meting" 在线音乐
};
```

## 播放器模式

### 本地音乐模式

```typescript
local: {
  playlist: [
    {
      id: 1,
      title: "歌曲名称",
      artist: "艺术家",
      cover: "/assets/music/cover/cover.jpg",
      url: "/assets/music/song.wav",
      duration: 240, // 时长（秒）
    },
  ],
}
```

**本地音乐文件要求：**
- 音乐文件放在 `public/assets/music/` 目录下
- 封面图片放在 `public/assets/music/cover/` 目录下
- 支持格式：MP3、WAV、OGG、M4A等

### 在线音乐模式（Meting API）

```typescript
meting: {
  // Meting API 地址
  api: "https://www.bilibili.uno/api?server=:server&type=:type&id=:id&auth=:auth&r=:r",
  
  // 歌单配置
  playlist: {
    id: "8814137515", // 歌单ID
    server: "netease", // 音乐平台
    type: "playlist", // 类型
  },
  
  // 备用 API 配置
  fallbackApis: [
    "https://api.injahow.cn/bete/?server=:server&type=:type&id=:id",
    "https://api.uomg.com/api/other/163music?format=json&id=:id",
  ],
}
```

**支持的音乐平台：**
- `netease`: 网易云音乐
- `tencent`: QQ音乐
- `kugou`: 酷狗音乐
- `xiami`: 虾米音乐
- `baidu`: 百度音乐

**类型选项：**
- `playlist`: 歌单
- `album`: 专辑
- `song`: 单曲

## 播放器行为配置

```typescript
behavior: {
  // 自动播放（注意：现代浏览器通常阻止自动播放）
  autoplay: false,
  
  // 默认音量 (0-1)
  defaultVolume: 0.7,
  
  // 默认播放模式
  defaultShuffle: false, // 随机播放
  defaultRepeat: 2, // 循环模式：0=不循环, 1=单曲循环, 2=列表循环
  
  // 播放器位置
  position: {
    bottom: 16, // 距离底部距离 (px)
    right: 16, // 距离右侧距离 (px)
    left: "auto", // 距离左侧距离 (px)，设为 "auto" 时使用 right 定位
  },
}
```

## 界面配置

### 动画配置

```typescript
ui: {
  animation: {
    // 封面旋转动画
    coverRotation: {
      enable: true, // 启用封面旋转
      speed: 3, // 旋转速度（秒/圈）
      pauseOnHover: true, // 鼠标悬停时暂停旋转
    },
  },
}
```

### 显示配置

```typescript
display: {
  showPlaylistButton: true, // 是否显示播放列表按钮
  showVolumeControl: true, // 是否显示音量控制
  showShuffleButton: true, // 是否显示随机播放按钮
  showRepeatButton: true, // 是否显示循环按钮
  showSkipButtons: true, // 是否显示上一首/下一首按钮
}
```

### 播放列表配置

```typescript
playlist: {
  maxHeight: 384, // 播放列表面板最大高度 (px)
  width: 320, // 播放列表面板宽度 (px)
  showTrackNumbers: true, // 是否显示歌曲序号
  showDuration: true, // 是否显示歌曲时长
}
```

## 响应式配置

### 移动端配置

```typescript
responsive: {
  mobile: {
    // 移动端播放器位置
    position: {
      bottom: 8,
      right: 8,
      left: 8,
    },
  },
  
  // 小屏幕配置 (≤480px)
  smallScreen: {
  },
}
```

## 错误处理配置

```typescript
errorHandling: {
  showErrorMessages: true, // 是否显示错误提示
  errorDisplayDuration: 3000, // 错误提示显示时长 (ms)
  autoSkipOnError: true, // 是否在播放失败时自动跳转到下一首
}
```

## 使用示例

### 完整配置示例

```typescript
export const musicPlayerConfig: MusicPlayerConfig = {
  enable: true,
  mode: "local",
  
  local: {
    playlist: [
      {
        id: 1,
        title: "使一颗心免于哀伤",
        artist: "知更鸟 / HOYO-MiX / Chevy",
        cover: "/assets/music/cover/109951169585655912.jpg",
        url: "/assets/music/使一颗心免于哀伤-哼唱.wav",
        duration: 240,
      },
    ],
  },
  
  behavior: {
    autoplay: false,
    defaultVolume: 0.7,
    defaultShuffle: false,
    defaultRepeat: 2,
    position: {
      bottom: 16,
      right: 16,
      left: "auto",
    },
  },
  
  ui: {
    animation: {
      coverRotation: {
        enable: true,
        speed: 3,
        pauseOnHover: true,
      },
    },
    display: {
      showPlaylistButton: true,
      showVolumeControl: true,
      showShuffleButton: true,
      showRepeatButton: true,
      showSkipButtons: true,
    },
    playlist: {
      maxHeight: 384,
      width: 320,
      showTrackNumbers: true,
      showDuration: true,
    },
  },
  
  responsive: {
    mobile: {
      position: {
        bottom: 8,
        right: 8,
        left: 8,
      },
    },
    smallScreen: {},
  },
  
  errorHandling: {
    showErrorMessages: true,
    errorDisplayDuration: 3000,
    autoSkipOnError: true,
  },
};
```

## 注意事项

1. **浏览器限制**：现代浏览器通常阻止自动播放，建议将 `autoplay` 设为 `false`
2. **文件格式**：确保音乐文件格式被浏览器支持
3. **文件大小**：注意音乐文件大小，过大的文件会影响加载速度
4. **版权问题**：使用在线音乐时请注意版权问题
5. **API稳定性**：在线音乐API可能不稳定，建议配置多个备用API
6. **尺寸配置**：播放器尺寸已固定，不再支持通过配置文件调整

## 常见问题

**Q: 音乐无法播放怎么办？**
A: 检查文件路径是否正确，确保音乐文件格式被浏览器支持

**Q: 如何添加更多歌曲？**
A: 在 `local.playlist` 数组中添加更多歌曲对象

**Q: 如何更换音乐平台？**
A: 修改 `meting.playlist.server` 的值

**Q: 播放器位置如何调整？**
A: 修改 `behavior.position` 中的数值

**Q: 如何禁用某些按钮？**
A: 在 `ui.display` 中将对应选项设为 `false`

**Q: 如何调整播放器尺寸？**
A: 播放器尺寸已固定，不再支持通过配置文件调整。如需自定义尺寸，需要修改源码中的CSS样式
