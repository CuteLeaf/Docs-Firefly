---
title: 用户资料配置
createTime: 2025/01/27 18:38:13
permalink: /config/profileConfig-usage/
---
# 用户资料配置

## 概述

用户资料配置用于设置网站的个人信息，包括头像、姓名、简介和社交链接等。

## 文件位置

```
src/config/profileConfig.ts
```

## 基础配置

### 设置个人信息

```typescript
export const profileConfig: ProfileConfig = {
  avatar: "/assets/images/avatar.webp", // 头像路径
  name: "Firefly", // 用户名
  bio: "Hello, I'm Firefly.", // 个人简介
  links: [ // 社交链接
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

## 配置选项详解

### 基础信息

| 选项 | 类型 | 说明 | 必填 |
|------|------|------|------|
| `avatar` | `string` | 头像图片路径 | 否 |
| `name` | `string` | 用户名 | 是 |
| `bio` | `string` | 个人简介 | 否 |

### 社交链接

| 选项 | 类型 | 说明 | 必填 |
|------|------|------|------|
| `name` | `string` | 链接名称 | 是 |
| `icon` | `string` | 图标名称 | 是 |
| `url` | `string` | 链接地址 | 是 |

## 头像配置

### 支持的图片格式

- **WebP**：推荐，文件小，质量高
- **PNG**：支持透明背景
- **JPG**：通用格式
- **SVG**：矢量图，可缩放

### 头像尺寸建议

- **推荐尺寸**：200x200 像素
- **最小尺寸**：100x100 像素
- **最大尺寸**：500x500 像素
- **宽高比**：1:1（正方形）

### 头像路径示例

```typescript
export const profileConfig: ProfileConfig = {
  // 本地图片
  avatar: "/assets/images/avatar.webp",
  
  // 或者使用网络图片
  avatar: "https://example.com/avatar.jpg",
  
  // 或者不设置头像
  // avatar: undefined,
};
```

## 社交链接配置

### 常用社交平台

```typescript
export const profileConfig: ProfileConfig = {
  // ... 其他配置
  links: [
    // GitHub
    {
      name: "GitHub",
      icon: "fa6-brands:github",
      url: "https://github.com/username",
    },
    
    // Twitter
    {
      name: "Twitter",
      icon: "fa6-brands:twitter",
      url: "https://twitter.com/username",
    },
    
    // LinkedIn
    {
      name: "LinkedIn",
      icon: "fa6-brands:linkedin",
      url: "https://linkedin.com/in/username",
    },
    
    // 邮箱
    {
      name: "Email",
      icon: "fa6-solid:envelope",
      url: "mailto:your-email@example.com",
    },
    
    // 个人网站
    {
      name: "Website",
      icon: "fa6-solid:globe",
      url: "https://your-website.com",
    },
  ],
};
```

### 图标库支持

Firefly 支持多种图标库：

#### Font Awesome 6
```typescript
{
  name: "GitHub",
  icon: "fa6-brands:github", // Font Awesome 6 品牌图标
  url: "https://github.com/username",
}
```

#### Material Design Icons
```typescript
{
  name: "Email",
  icon: "mdi:email", // Material Design Icons
  url: "mailto:your-email@example.com",
}
```

#### Simple Icons
```typescript
{
  name: "Discord",
  icon: "simple-icons:discord", // Simple Icons
  url: "https://discord.gg/server",
}
```

### 自定义图标

```typescript
{
  name: "自定义链接",
  icon: "custom-icon", // 使用自定义图标
  url: "https://example.com",
}
```

## 完整配置示例

### 开发者个人资料

```typescript
export const profileConfig: ProfileConfig = {
  avatar: "/assets/images/avatar.webp",
  name: "张三",
  bio: "全栈开发者，热爱开源，专注于 Web 技术和用户体验。",
  links: [
    {
      name: "GitHub",
      icon: "fa6-brands:github",
      url: "https://github.com/zhangsan",
    },
    {
      name: "Twitter",
      icon: "fa6-brands:twitter",
      url: "https://twitter.com/zhangsan",
    },
    {
      name: "LinkedIn",
      icon: "fa6-brands:linkedin",
      url: "https://linkedin.com/in/zhangsan",
    },
    {
      name: "Email",
      icon: "fa6-solid:envelope",
      url: "mailto:zhangsan@example.com",
    },
  ],
};
```

### 设计师个人资料

```typescript
export const profileConfig: ProfileConfig = {
  avatar: "/assets/images/avatar.png",
  name: "李四",
  bio: "UI/UX 设计师，专注于创造美观且实用的数字产品。",
  links: [
    {
      name: "Dribbble",
      icon: "fa6-brands:dribbble",
      url: "https://dribbble.com/lisi",
    },
    {
      name: "Behance",
      icon: "fa6-brands:behance",
      url: "https://behance.net/lisi",
    },
    {
      name: "Instagram",
      icon: "fa6-brands:instagram",
      url: "https://instagram.com/lisi",
    },
    {
      name: "Portfolio",
      icon: "fa6-solid:briefcase",
      url: "https://lisi.design",
    },
  ],
};
```

### 博主个人资料

```typescript
export const profileConfig: ProfileConfig = {
  avatar: "/assets/images/avatar.jpg",
  name: "王五",
  bio: "技术博主，分享编程心得和生活感悟。",
  links: [
    {
      name: "GitHub",
      icon: "fa6-brands:github",
      url: "https://github.com/wangwu",
    },
    {
      name: "微博",
      icon: "fa6-brands:weibo",
      url: "https://weibo.com/wangwu",
    },
    {
      name: "知乎",
      icon: "fa6-brands:zhihu",
      url: "https://zhihu.com/people/wangwu",
    },
    {
      name: "RSS",
      icon: "fa6-solid:rss",
      url: "/rss.xml",
    },
  ],
};
```

## 样式自定义

### CSS 自定义

```css
/* 个人资料容器 */
.profile-container {
  text-align: center;
  padding: 2rem;
  background: var(--card-bg);
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* 头像样式 */
.profile-avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid var(--primary);
  margin-bottom: 1rem;
}

/* 用户名样式 */
.profile-name {
  font-size: 1.5rem;
  font-weight: bold;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
}

/* 个人简介样式 */
.profile-bio {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

/* 社交链接容器 */
.profile-links {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
}

/* 社交链接样式 */
.profile-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background: var(--button-bg);
  color: var(--text-primary);
  text-decoration: none;
  border-radius: 6px;
  transition: all 0.2s ease;
}

.profile-link:hover {
  background: var(--primary);
  color: white;
  transform: translateY(-2px);
}
```

## 响应式设计

### 移动端优化

```css
/* 移动端样式 */
@media (max-width: 768px) {
  .profile-container {
    padding: 1.5rem;
  }
  
  .profile-avatar {
    width: 100px;
    height: 100px;
  }
  
  .profile-name {
    font-size: 1.25rem;
  }
  
  .profile-links {
    gap: 0.5rem;
  }
  
  .profile-link {
    padding: 0.4rem 0.8rem;
    font-size: 0.9rem;
  }
}
```

## 注意事项

1. **图片优化**：建议使用 WebP 格式的头像，文件更小
2. **链接有效性**：定期检查社交链接是否有效
3. **隐私保护**：不要在简介中暴露过多个人信息
4. **图标一致性**：建议使用同一图标库的图标保持风格一致

## 常见问题

**Q: 如何更换头像？**
A: 将新头像文件放在 `public/assets/images/` 目录下，然后修改 `avatar` 路径

**Q: 支持哪些图标库？**
A: 支持 Font Awesome 6、Material Design Icons、Simple Icons 等

**Q: 如何添加新的社交链接？**
A: 在 `links` 数组中添加新的链接对象

**Q: 头像不显示怎么办？**
A: 检查图片路径是否正确，确保图片文件存在

**Q: 如何自定义社交链接样式？**
A: 通过 CSS 覆盖 `.profile-link` 类的样式

**Q: 可以设置多个邮箱吗？**
A: 可以，添加多个邮箱链接即可

**Q: 如何让链接在新窗口打开？**
A: 链接默认会在新窗口打开，无需额外配置
