---
title: 评论配置
createTime: 2025/01/27 18:38:13
permalink: /config/commentConfig-usage/
---
# 评论配置

## 概述

Firefly 支持多种主流评论系统，无需改动业务代码，仅通过 `src/config/commentConfig.ts` 配置即可灵活切换、控制注册、开启访问量统计等功能。

支持的评论系统：
- Twikoo
- Waline
- Giscus
- Disqus
- 支持关闭评论（type: none）

## 文件位置

```
src/config/commentConfig.ts
```

## 多评论系统通用配置

```ts
export const commentConfig: CommentConfig = {
  type: 'waline',            // 当前启用的评论系统（twikoo/waline/giscus/disqus/none）
  twikoo: {
    envId: 'https://twikoo.vercel.app',
    lang: 'zh-CN',
    visitorCount: true,       // 文章访问量统计开关（true/false）
  },
  waline: {
    serverURL: 'https://waline.vercel.app',
    lang: 'zh-CN',
    login: 'enable',          // 评论登录模式（enable/force/disable）
    visitorCount: true,       // 支持访问量统计（true/false）
  },
  giscus: {
    repo: 'xxx',
    repoId: 'xxx',
    category: 'xxx',
    categoryId: 'xxx',
    mapping: 'title',
    strict: '0',
    reactionsEnabled: '1',
    emitMetadata: '1',
    inputPosition: 'top',
    theme: 'light',
    lang: 'zh-CN',
    loading: 'lazy',
  },
  disqus: {
    shortname: 'firefly',
  },
};
```

### 主要字段说明
- `type`：全局唯一，指定启用哪个评论系统（none 代表禁用评论与统计）
- `visitorCount`（twikoo/waline专用）：每系统可分别开关访问量统计
- `login`（waline专用）：控制是否需要登录后评论（force=强制登录，disable=只允许匿名，enable=两种均可）

更多类型细节见 `src/types/config.ts`。

## Twikoo、Waline 访问量统计统一配置

只需在对应子对象下设置 `visitorCount: true`，在文章（PostMeta）区、评论区即可自动显示 PV。

- true：同时激活评论区和访问量统计，不想显示只需改为 false。
- 两系统相互独立，互不影响。

## Giscus、Disqus 配置

目前 Giscus、Disqus 配置无需 visitorCount 字段——如未来官方支持，可无缝加入。

## 登录模式说明（以 Waline 为例）
- `login: 'enable'`   —— 推荐，访客/账号/OAuth 都可评论
- `login: 'force'`    —— 仅允许登录后评论，适合私密或社区站点
- `login: 'disable'`  —— 纯匿名评论/无需第三方登录

可根据实际使用需求调整。

## 如何切换评论系统/访问量统计
1. 只需改动 `type` 字段即可一键切换主评论系统，无需重启项目
2. 独立控制每个系统的 `visitorCount`, 分别管理是否显示统计区块

## 配置注意事项
- 需保证评论系统开关、统计开关与自身 config 匹配
- commentsConfig 变更后建议刷新页面、重启服务以确保 UI/逻辑同步
- 配置项注释中含有详细每字段功能说明，可直接查阅 config 源文件

---

如需更完整示例与联动场景说明，请查阅 Firefly 根目录 `README.md` 或类型定义 `src/types/config.ts`。
