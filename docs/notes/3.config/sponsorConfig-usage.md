---
title: 赞助配置
createTime: 2025/01/27 18:38:14
permalink: /config/sponsorConfig-usage/
---
# 赞助配置

## 概述

`sponsorConfig.ts` 文件用于配置网站赞助页面的支付方式、收款码、赞助者列表以及文章内赞助按钮等功能。支持多种支付方式（支付宝、微信、PayPal等），支持二维码展示和链接跳转，还可以在文章详情页底部显示赞助按钮。

## 文件位置

```
src/config/sponsorConfig.ts
```

## 页面开关

赞助页面的显示由 `siteConfig.ts` 中的页面开关控制：

```typescript
// src/config/siteConfig.ts
export const siteConfig: SiteConfig = {
  // ...
  pages: {
    sponsor: true, // 赞助页面开关
  },
};
```

当设置为 `false` 时，访问 `/sponsor/` 页面会自动跳转到 404 页面。

## 配置结构

```typescript
interface SponsorConfig {
  title?: string;              // 页面标题，默认使用 i18n
  description?: string;        // 页面描述文本
  usage?: string;              // 赞助用途说明
  methods: SponsorMethod[];    // 赞助方式列表
  sponsors?: SponsorItem[];    // 赞助者列表（可选）
  showSponsorsList?: boolean;  // 是否显示赞助者列表，默认 true
  showButtonInPost?: boolean;  // 是否在文章详情页底部显示赞助按钮，默认 false
}

interface SponsorMethod {
  name: string;                // 赞助方式名称
  icon?: string;               // 图标名称（Iconify 格式）
  qrCode?: string;             // 收款码图片路径（相对于 public 目录）
  link?: string;               // 赞助链接 URL
  description?: string;        // 描述文本
  enabled: boolean;            // 是否启用
}

interface SponsorItem {
  name: string;                // 赞助者名称
  amount?: string;             // 赞助金额（可选）
  date?: string;               // 赞助日期（可选，ISO 格式）
  message?: string;            // 留言（可选）
}
```

## 基础配置示例

```typescript
import type { SponsorConfig } from "../types/config";

export const sponsorConfig: SponsorConfig = {
  title: "赞助本站", // 页面标题，如果留空则使用 i18n 中的翻译
  description: "如果我的内容对你有帮助，欢迎通过以下方式赞助我，你的支持是我持续创作的动力！",
  usage: "您的赞助将用于服务器维护、内容创作和功能开发，帮助我持续提供优质内容。",
  
  // 是否显示赞助者列表
  showSponsorsList: true,
  // 是否在文章详情页底部显示赞助按钮
  showButtonInPost: true,

  // 赞助方式列表
  methods: [
    {
      name: "支付宝",
      icon: "fa6-brands:alipay",
      qrCode: "/assets/images/sponsor/alipay.png", // 收款码图片路径
      link: "", // 可选：支付宝链接
      description: "使用支付宝扫码赞助",
      enabled: true,
    },
    {
      name: "微信",
      icon: "fa6-brands:weixin",
      qrCode: "/assets/images/sponsor/wechat.png",
      link: "",
      description: "使用微信扫码赞助",
      enabled: true,
    },
    {
      name: "爱发电",
      icon: "simple-icons:afdian",
      qrCode: "", // 仅链接，不需要二维码
      link: "https://afdian.com/a/cuteleaf",
      description: "通过 爱发电 进行赞助",
      enabled: true,
    },
  ],

  // 赞助者列表（可选）
  sponsors: [
    {
      name: "夏叶",
      amount: "¥50",
      date: "2025-10-01",
      message: "感谢分享！",
    },
    {
      name: "匿名用户",
      amount: "¥20",
      date: "2025-10-01",
    },
  ],
};
```

## 配置选项详解

### 页面基础配置

| 选项 | 类型 | 必填 | 说明 | 默认值 |
|------|------|------|------|--------|
| `title` | `string` | 否 | 页面标题，留空则使用 i18n 翻译 | `i18n(sponsorTitle)` |
| `description` | `string` | 否 | 页面描述文本，留空则使用 i18n 翻译 | `i18n(sponsorDescription)` |
| `usage` | `string` | 否 | 赞助用途说明，会在页面上以提示框形式显示 | - |
| `showSponsorsList` | `boolean` | 否 | 是否显示赞助者列表 | `true` |
| `showButtonInPost` | `boolean` | 否 | 是否在文章详情页底部显示赞助按钮 | `false` |

### 赞助方式配置 (SponsorMethod)

| 选项 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | `string` | 是 | 赞助方式名称，如 "支付宝"、"微信"、"PayPal" |
| `icon` | `string` | 否 | 图标名称（Iconify 格式），如 "fa6-brands:alipay" |
| `qrCode` | `string` | 否 | 收款码图片路径（相对于 `public` 目录），如 "/assets/images/sponsor/alipay.png" |
| `link` | `string` | 否 | 赞助链接 URL，如果提供会显示跳转按钮 |
| `description` | `string` | 否 | 描述文本，显示在图标和名称下方 |
| `enabled` | `boolean` | 是 | 是否启用该赞助方式 |

**注意：** `qrCode` 和 `link` 至少需要提供一个，也可以同时提供。

### 赞助者配置 (SponsorItem)

| 选项 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | `string` | 是 | 赞助者名称，匿名可设置为 "匿名用户" |
| `amount` | `string` | 否 | 赞助金额，如 "¥50"、"$20" |
| `date` | `string` | 否 | 赞助日期，ISO 格式，如 "2025-10-01" |
| `message` | `string` | 否 | 赞助者留言 |

## 使用场景

### 1. 二维码支付方式（支付宝/微信）

```typescript
{
  name: "支付宝",
  icon: "fa6-brands:alipay",
  qrCode: "/assets/images/sponsor/alipay.png", // 需要将收款码图片放在 public 目录下
  description: "使用支付宝扫码赞助",
  enabled: true,
}
```

### 2. 链接跳转方式（PayPal/爱发电）

```typescript
{
  name: "爱发电",
  icon: "simple-icons:afdian",
  link: "https://afdian.com/a/cuteleaf",
  description: "通过 爱发电 进行赞助",
  enabled: true,
}
```

### 3. 同时支持二维码和链接

```typescript
{
  name: "支付宝",
  icon: "fa6-brands:alipay",
  qrCode: "/assets/images/sponsor/alipay.png",
  link: "https://qr.alipay.com/fkx13464ztczwm1jcvqax05", // 支付宝收款链接
  description: "使用支付宝扫码或点击链接赞助",
  enabled: true,
}
```

### 4. 完整配置示例

```typescript
export const sponsorConfig: SponsorConfig = {
  title: "赞助支持",
  description: "如果我的内容对你有帮助，欢迎通过以下方式赞助我！",
  usage: "您的赞助将用于服务器维护、内容创作和功能开发。",
  
  showSponsorsList: true,
  showButtonInPost: true,

  methods: [
    {
      name: "支付宝",
      icon: "fa6-brands:alipay",
      qrCode: "/assets/images/sponsor/alipay.png",
      description: "使用支付宝扫码赞助",
      enabled: true,
    },
    {
      name: "微信",
      icon: "fa6-brands:weixin",
      qrCode: "/assets/images/sponsor/wechat.png",
      description: "使用微信扫码赞助",
      enabled: true,
    },
    {
      name: "PayPal",
      icon: "fa6-brands:paypal",
      link: "https://paypal.me/cuteleaf",
      description: "通过 PayPal 进行赞助",
      enabled: true,
    },
    {
      name: "爱发电",
      icon: "simple-icons:afdian",
      link: "https://afdian.com/a/cuteleaf",
      description: "通过 爱发电 进行赞助",
      enabled: true,
    },
  ],

  sponsors: [
    {
      name: "张三",
      amount: "¥100",
      date: "2025-10-15",
      message: "感谢作者分享优质内容！",
    },
    {
      name: "李四",
      amount: "¥50",
      date: "2025-10-10",
    },
    {
      name: "匿名用户",
      amount: "¥20",
      date: "2025-10-05",
      message: "支持一下",
    },
  ],
};
```

## 图片准备

### 收款码图片路径

1. 将收款码图片保存在 `public/assets/images/sponsor/` 目录下
2. 在配置中使用相对于 `public` 的路径，如 `/assets/images/sponsor/alipay.png`

### 推荐的图片格式

- 格式：PNG、JPG、WEBP
- 尺寸：建议 200x200 像素以上，正方形最佳
- 文件大小：建议压缩后小于 200KB

## 国际化支持

赞助页面支持多语言，相关文本在以下语言文件中配置：

- `src/i18n/languages/zh_CN.ts` - 简体中文
- `src/i18n/languages/zh_TW.ts` - 繁体中文
- `src/i18n/languages/en.ts` - 英文
- `src/i18n/languages/ja.ts` - 日文
- `src/i18n/languages/ru.ts` - 俄文

如果 `title` 或 `description` 留空，会自动使用对应语言的翻译。

## 页面访问

配置完成后，赞助页面可以通过以下 URL 访问：

- 本地开发：`http://localhost:4321/sponsor/`
- 生产环境：`https://your-domain.com/sponsor/`

## 文章内赞助按钮

当 `showButtonInPost: true` 时，每篇博客文章的底部（在 License 组件之前）会显示一个赞助按钮，点击后会跳转到赞助页面。

按钮文本同样支持国际化，可通过语言文件自定义。

## 注意事项

1. **页面开关**：记得在 `siteConfig.ts` 中启用 `pages.sponsor`
2. **图片路径**：收款码图片必须放在 `public` 目录下
3. **至少一个方式**：每个赞助方式至少需要提供 `qrCode` 或 `link` 中的一个
4. **国际化**：建议配置多语言翻译，提升用户体验
5. **隐私保护**：赞助者信息需要手动维护，注意保护用户隐私

