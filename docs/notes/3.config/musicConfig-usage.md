---
title: 音乐播放器配置
createTime: 2025/01/27 18:38:13
permalink: /config/musicConfig-usage/
---
# 音乐播放器配置

## 概述

音乐播放器配置用于在网站中添加音乐播放功能，基于 APlayer 和 MetingJS，支持本地音乐和在线音乐两种模式。

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
      name: "歌曲名称",
      artist: "艺术家",
      url: "/assets/music/song.wav", // 音乐文件路径
      cover: "/assets/music/cover/cover.jpg", // 封面图片路径（可选）
      lrc: "", // 歌词内容，支持 LRC 格式（可选）
    },
  ],
}
```

**本地音乐文件要求：**
- 音乐文件放在 `public/assets/music/` 目录下
- 封面图片放在 `public/assets/music/cover/` 目录下
- 支持格式：MP3、WAV、OGG、M4A等
- 路径使用相对于 `public` 目录的路径（以 `/` 开头）

### 在线音乐模式（Meting API）

```typescript
meting: {
  // Meting API 地址
  api: "https://api.i-meto.com/meting/api?server=:server&type=:type&id=:id&r=:r",
  
  // 音乐平台：netease=网易云音乐, tencent=QQ音乐, kugou=酷狗音乐, xiami=虾米音乐, baidu=百度音乐
  server: "netease",
  
  // 类型：song=单曲, playlist=歌单, album=专辑, search=搜索, artist=艺术家
  type: "playlist",
  
  // 歌单/专辑/单曲 ID 或搜索关键词
  id: "8814137515", // 网易云音乐歌单ID示例
  
  // 认证 token（可选）
  auth: "",
  
  // 备用 API 配置（当主 API 失败时使用）
  fallbackApis: [
    "https://api.i-meto.com/meting/api?server=:server&type=:type&id=:id&r=:r",
  ],
  
  // MetingJS 脚本路径
  // 默认使用 CDN：https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js
  // 备用CDN：https://unpkg.com/meting@2/dist/Meting.min.js
  // 也可配置为本地路径（支持非根目录部署）
  jsPath: "https://unpkg.com/meting@2/dist/Meting.min.js",
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
- `search`: 搜索
- `artist`: 艺术家

**MetingJS 脚本路径说明：**
- 支持 CDN 路径（http:// 或 https:// 开头）
- 支持本地路径（以 `/` 开头，会自动处理非根目录部署问题）
- 如果不配置，默认使用 `https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js`

## APlayer 配置选项

```typescript
player: {
  // 是否自动播放（浏览器可能会阻止，需用户交互一次网页后才自动播放）
  autoplay: true,
  
  // 主题色
  theme: "var(--btn-regular-bg)", // 可以使用 CSS 变量或颜色值
  
  // 循环模式：'all'=列表循环, 'one'=单曲循环, 'none'=不循环
  loop: "all",
  
  // 播放顺序：'list'=列表顺序, 'random'=随机播放
  order: "list",
  
  // 预加载：'none'=不预加载, 'metadata'=预加载元数据, 'auto'=自动
  preload: "auto",
  
  // 默认音量 (0-1)
  volume: 0.7,
  
  // 是否互斥播放（同时只能播放一个播放器）
  mutex: true,
  
  // 歌词类型：0=不显示, 1=显示（需要提供 lrc 字段）, 2=显示（从 HTML 内容读取）, 3=异步加载（从 API 获取）
  lrcType: 3,
  
  // 歌词是否默认隐藏（当 lrcType 不为 0 时，可以通过此选项控制初始显示状态）
  // true=默认隐藏（用户可以通过歌词按钮手动显示）, false=默认显示
  lrcHidden: true,
  
  // 播放列表是否默认折叠
  listFolded: false,
  
  // 播放列表最大高度
  listMaxHeight: "340px",
  
  // localStorage 存储键名
  storageName: "aplayer-setting",
}
```

**播放器固定位置和迷你模式说明：**
- `fixed` 和 `mini` 默认为 `true`，无需在配置中设置
- 播放器固定在页面右下角（fixed 模式）
- 默认以迷你模式显示（mini 模式）
- 如果需要修改这些行为，需要修改组件源码

**自动播放说明：**
- 现代浏览器通常会阻止自动播放音频
- 配置 `autoplay: true` 后，播放器会在用户第一次交互（点击、滚动、按键等）后自动开始播放
- 这是浏览器安全策略的要求，无法绕过

**歌词配置说明：**
- `lrcType: 0` - 不显示歌词
- `lrcType: 1` - 显示歌词（需要在本地音乐的 `lrc` 字段中提供歌词内容）
- `lrcType: 2` - 从 HTML 内容读取歌词（用于单个本地音乐）
- `lrcType: 3` - 异步加载歌词（用于 Meting API，从 API 获取歌词）
- `lrcHidden` - 当歌词功能启用时，控制初始显示状态

## 响应式配置

```typescript
responsive: {
  mobile: {
    // 在移动端是否隐藏
    hide: false,
    
    // 移动端断点（小于此宽度时应用移动端配置）
    breakpoint: 768, // 单位：px
  },
}
```

## 使用示例

### 完整配置示例（本地音乐）

```typescript
export const musicPlayerConfig: MusicPlayerConfig = {
  enable: true,
  mode: "local",
  
  local: {
    playlist: [
      {
        name: "使一颗心免于哀伤",
        artist: "知更鸟 / HOYO-MiX / Chevy",
        url: "/assets/music/使一颗心免于哀伤-哼唱.wav",
        cover: "/assets/music/cover/109951169585655912.jpg",
        lrc: "", // 歌词内容，支持 LRC 格式
      },
    ],
  },
  
  player: {
    autoplay: true,
    theme: "var(--btn-regular-bg)",
    loop: "all",
    order: "list",
    preload: "auto",
    volume: 0.7,
    mutex: true,
    lrcType: 3,
    lrcHidden: true,
    listFolded: false,
    listMaxHeight: "340px",
    storageName: "aplayer-setting",
  },
  
  responsive: {
    mobile: {
      hide: false,
      breakpoint: 768,
    },
  },
};
```

### 完整配置示例（Meting API）

```typescript
export const musicPlayerConfig: MusicPlayerConfig = {
  enable: true,
  mode: "meting",
  
  meting: {
    api: "https://api.i-meto.com/meting/api?server=:server&type=:type&id=:id&r=:r",
    server: "netease",
    type: "playlist",
    id: "8814137515",
    auth: "",
    fallbackApis: [
      "https://api.i-meto.com/meting/api?server=:server&type=:type&id=:id&r=:r",
    ],
    jsPath: "https://unpkg.com/meting@2/dist/Meting.min.js",
  },
  
  player: {
    autoplay: true,
    theme: "var(--btn-regular-bg)",
    loop: "all",
    order: "list",
    preload: "auto",
    volume: 0.7,
    mutex: true,
    lrcType: 3, // Meting API 模式下使用 3 从 API 获取歌词
    lrcHidden: false, // 默认显示歌词
    listFolded: false,
    listMaxHeight: "340px",
    storageName: "aplayer-setting",
  },
  
  responsive: {
    mobile: {
      hide: false,
      breakpoint: 768,
    },
  },
};
```

### 单个本地音乐配置示例（使用 MetingJS）

当本地音乐列表只有一首歌曲时，会自动使用 MetingJS 渲染：

```typescript
local: {
  playlist: [
    {
      name: "歌曲名称",
      artist: "艺术家",
      url: "/assets/music/song.wav",
      cover: "/assets/music/cover/cover.jpg",
      lrc: "[00:00.00] 歌词内容...", // 歌词内容，lrcType 会使用 2
    },
  ],
}
```

### 多个本地音乐配置示例（使用 APlayer 直接初始化）

当本地音乐列表有多首歌曲时，会使用 APlayer 直接初始化：

```typescript
local: {
  playlist: [
    {
      name: "歌曲1",
      artist: "艺术家1",
      url: "/assets/music/song1.wav",
      cover: "/assets/music/cover/cover1.jpg",
      lrc: "", // 多个音乐时，lrcType 使用配置的值
    },
    {
      name: "歌曲2",
      artist: "艺术家2",
      url: "/assets/music/song2.wav",
      cover: "/assets/music/cover/cover2.jpg",
      lrc: "",
    },
  ],
}
```

## 路径处理说明

音乐播放器组件会自动处理非根目录部署的路径问题：

- 本地音乐文件的 `url` 和 `cover` 路径会自动使用 `url()` 工具函数处理
- MetingJS 脚本路径如果配置为本地路径（以 `/` 开头），也会自动处理
- CDN 路径（http:// 或 https:// 开头）不会进行任何处理，直接使用

## 注意事项

1. **浏览器限制**：现代浏览器通常阻止自动播放，即使设置了 `autoplay: true`，也需要用户交互一次后才会自动播放
2. **文件格式**：确保音乐文件格式被浏览器支持（MP3、WAV、OGG、M4A等）
3. **文件大小**：注意音乐文件大小，过大的文件会影响加载速度
4. **版权问题**：使用在线音乐时请注意版权问题
5. **API稳定性**：在线音乐API可能不稳定，建议配置多个备用API
6. **固定位置**：播放器默认固定在右下角，`fixed` 和 `mini` 默认均为 `true`，无法通过配置文件修改
7. **歌词显示**：Meting API 模式下，歌词需要 API 返回歌词数据才能显示；本地音乐模式下，需要提供 `lrc` 字段内容
8. **路径配置**：本地音乐文件的路径必须相对于 `public` 目录，以 `/` 开头

## 常见问题

**Q: 音乐无法播放怎么办？**
A: 检查文件路径是否正确，确保音乐文件格式被浏览器支持，文件路径以 `/` 开头

**Q: 如何添加更多歌曲？**
A: 在 `local.playlist` 数组中添加更多歌曲对象

**Q: 如何更换音乐平台？**
A: 修改 `meting.server` 的值（netease、tencent、kugou等）

**Q: 自动播放不生效怎么办？**
A: 这是正常的浏览器安全策略，需要用户交互一次后才会自动播放。如果页面加载后立即需要播放，需要用户先点击页面任意位置

**Q: 如何隐藏歌词？**
A: 设置 `player.lrcHidden: true`，或设置 `player.lrcType: 0` 完全禁用歌词功能

**Q: 如何获取网易云音乐歌单ID？**
A: 在网易云音乐网页版打开歌单，URL 中的数字就是歌单ID，例如：`https://music.163.com/#/playlist?id=8814137515` 中的 `8814137515`

**Q: 如何在非根目录部署时使用本地 MetingJS 脚本？**
A: 将 MetingJS 脚本文件放在 `public/assets/js/` 目录下，然后在配置中设置 `meting.jsPath: "/assets/js/Meting.min.js"`，组件会自动处理路径问题

**Q: 歌词不显示怎么办？**
A: 
- Meting API 模式：检查 `lrcType` 是否为 `3`，并确认 API 返回了歌词数据
- 本地音乐模式：检查是否提供了 `lrc` 字段内容，并设置正确的 `lrcType`（单个音乐使用 `2`，多个音乐使用 `1`）

**Q: 播放器位置可以调整吗？**
A: 播放器固定在右下角，位置无法通过配置文件调整。如需调整，需要修改组件源码中的 CSS 样式