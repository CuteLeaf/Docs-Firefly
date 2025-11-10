---
title: 代码高亮配置
createTime: 2025/01/27 18:38:13
permalink: /config/expressiveCodeConfig-usage/
---
# 代码高亮配置

## 概述

代码高亮配置用于设置 Markdown 代码块的语法高亮主题和样式。

## 文件位置

```
src/config/expressiveCodeConfig.ts
```

## 基础配置

### 多主题支持（推荐）

Firefly 支持为暗色和亮色模式分别配置不同的代码高亮主题，代码块会根据当前主题模式自动切换：

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  // 暗色主题（用于暗色模式）
  darkTheme: "one-dark-pro",
  // 亮色主题（用于亮色模式）
  lightTheme: "one-light",
  
  // 更多样式请看expressive-code的官方文档
  // https://expressive-code.com/guides/themes/
};
```

### 单主题配置（已弃用）

> ⚠️ **注意**：`theme` 字段已被弃用，推荐使用 `darkTheme` 和 `lightTheme` 来分别配置暗色和亮色主题。

## 支持的主题

### 暗色主题

| 主题名称 | 说明 | 特点 |
|----------|------|------|
| `github-dark` | GitHub 暗色主题 | 经典，易读性好 |
| `one-dark-pro` | One Dark Pro 主题 | 简洁，护眼，VS Code 流行主题 |
| `monokai` | Monokai 主题 | 色彩丰富，对比度高 |
| `dracula` | Dracula 主题 | 紫色调，现代感强 |
| `one-dark` | One Dark 主题 | 简洁，护眼 |
| `nord` | Nord 主题 | 冷色调，专业感 |
| `tokyo-night` | Tokyo Night 主题 | 日系风格，优雅 |
| `catppuccin-macchiato` | Catppuccin Macchiato | 柔和色调，现代设计 |

### 亮色主题

| 主题名称 | 说明 | 特点 |
|----------|------|------|
| `github-light` | GitHub 亮色主题 | 经典，适合亮色背景 |
| `one-light` | One Light 主题 | 简洁，与 One Dark Pro 配对 |
| `solarized-light` | Solarized 亮色主题 | 护眼，对比度适中 |
| `min-light` | Min 亮色主题 | 极简风格 |
| `catppuccin-latte` | Catppuccin Latte | 柔和色调，现代设计 |

## 主题配置示例

### 使用 One Dark Pro 和 One Light（推荐）

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  darkTheme: "one-dark-pro",
  lightTheme: "one-light",
};
```

### 使用 GitHub 主题

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  darkTheme: "github-dark",
  lightTheme: "github-light",
};
```

### 使用 Catppuccin 主题

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  darkTheme: "catppuccin-macchiato",
  lightTheme: "catppuccin-latte",
};
```

### 使用 Monokai 和 Solarized Light

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  darkTheme: "monokai",
  lightTheme: "solarized-light",
};
```

## 代码块功能特性

### 语法高亮

支持多种编程语言的语法高亮：

- **前端**：HTML, CSS, JavaScript, TypeScript, Vue, React
- **后端**：Python, Java, C++, C#, Go, Rust, PHP
- **数据库**：SQL, MongoDB, Redis
- **配置**：JSON, YAML, TOML, XML
- **其他**：Markdown, Bash, Docker, Git

### 行号显示

代码块默认显示行号：

````markdown
```javascript
function hello() {
  console.log("Hello, World!");
}
```
````

### 代码复制

每个代码块都有复制按钮，方便用户复制代码。

### 语言标识

代码块会显示编程语言标识：

````markdown
```typescript
interface User {
  name: string;
  age: number;
}
```
````

## 主题切换机制

### 自动切换

代码块主题会根据用户选择的网站主题模式（暗色/亮色）自动切换：

- **暗色模式**：使用 `darkTheme` 配置的主题
- **亮色模式**：使用 `lightTheme` 配置的主题

### 技术实现

Firefly 通过以下方式实现主题切换：

1. **禁用自动媒体查询**：在 `astro.config.mjs` 中设置 `useDarkModeMediaQuery: false`
2. **使用 data-theme 属性**：通过 `data-theme` 属性手动控制主题切换
3. **主题选择器**：使用 `themeCssSelector` 配置主题选择逻辑

```javascript
// astro.config.mjs
expressiveCode({
  themes: [expressiveCodeConfig.darkTheme, expressiveCodeConfig.lightTheme],
  useDarkModeMediaQuery: false,
  themeCssSelector: (theme) => `[data-theme='${theme.name}']`,
  // ... 其他配置
})
```

## 自定义样式

### 在 astro.config.mjs 中配置

如需自定义代码块样式，可以在 `astro.config.mjs` 中配置：

```javascript
// astro.config.mjs
import { expressiveCodeConfig } from "./src/config";

export default defineConfig({
  integrations: [
    expressiveCode({
      themes: [expressiveCodeConfig.darkTheme, expressiveCodeConfig.lightTheme],
      useDarkModeMediaQuery: false,
      themeCssSelector: (theme) => `[data-theme='${theme.name}']`,
      styleOverrides: {
        borderRadius: "0.75rem",
        codeFontSize: "0.875rem",
        codeFontFamily: "'JetBrains Mono Variable', ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace",
        codeLineHeight: "1.5rem",
        // ... 其他样式配置
      },
    }),
  ],
});
```

### 背景颜色说明

> **重要**：代码块的背景颜色现在使用主题自带的颜色，不再被 CSS 变量覆盖。这样代码块会根据当前主题模式（暗色/亮色）自动显示对应的背景颜色。

### CSS 自定义

如果需要进一步自定义代码块样式，可以通过 CSS 覆盖：

```css
/* 代码块容器 */
.expressive-code {
  border-radius: 0.75rem;
  margin: 1rem 0;
}

/* 代码文本样式 */
.expressive-code code {
  font-family: 'JetBrains Mono Variable', ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace;
  font-size: 0.875rem;
  line-height: 1.5rem;
}

/* 行号样式 */
.expressive-code .line-number {
  color: var(--code-line-number-color);
  margin-right: 1rem;
  user-select: none;
}
```

## 代码块使用示例

### JavaScript 代码

````markdown
```javascript
// 箭头函数示例
const greet = (name) => {
  return `Hello, ${name}!`;
};

// 使用示例
console.log(greet("World"));
```
````

### TypeScript 代码

````markdown
```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

class UserService {
  private users: User[] = [];
  
  addUser(user: User): void {
    this.users.push(user);
  }
  
  getUser(id: number): User | undefined {
    return this.users.find(user => user.id === id);
  }
}
```
````

### Python 代码

````markdown
```python
def fibonacci(n):
    """计算斐波那契数列的第n项"""
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# 使用示例
for i in range(10):
    print(f"F({i}) = {fibonacci(i)}")
```
````

### CSS 代码

````markdown
```css
.button {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: none;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  font-size: 1rem;
  padding: 0.75rem 1.5rem;
  transition: transform 0.2s ease;
}

.button:hover {
  transform: translateY(-2px);
}
```
````

## 功能特性

### 语法高亮

支持多种编程语言的语法高亮：

- **前端**：HTML, CSS, JavaScript, TypeScript, Vue, React
- **后端**：Python, Java, C++, C#, Go, Rust, PHP
- **数据库**：SQL, MongoDB, Redis
- **配置**：JSON, YAML, TOML, XML
- **其他**：Markdown, Bash, Docker, Git

### 行号显示

代码块默认显示行号：

````markdown
```javascript
function hello() {
  console.log("Hello, World!");
}
```
````

### 代码复制

每个代码块都有复制按钮，方便用户复制代码。

### 语言标识

代码块会显示编程语言标识：

````markdown
```typescript
interface User {
  name: string;
  age: number;
}
```
````

### 可折叠代码块

支持可折叠的代码块，适合展示长代码：

````markdown
```javascript:src/app.js
// 点击标题可以折叠/展开代码块
function example() {
  // 代码内容
}
```
````

## 性能优化

### 主题优化

Expressive Code 会自动移除未使用的主题，减少构建体积。只加载配置中指定的主题。

### 缓存优化

代码高亮结果会被缓存，提高构建速度。

## 注意事项

1. **主题配对**：建议为暗色和亮色模式选择配对的主题（如 `one-dark-pro` 和 `one-light`）
2. **性能考虑**：主题文件大小会影响构建速度，但通常影响不大
3. **可读性**：确保代码在所选主题下有良好的可读性
4. **一致性**：在整个网站中保持代码高亮风格一致
5. **背景颜色**：代码块背景颜色使用主题自带的颜色，无需手动设置

## 常见问题

**Q: 如何更换代码高亮主题？**
A: 修改 `darkTheme` 和 `lightTheme` 字段的值即可

**Q: 代码块在切换主题时没有变化？**
A: 确保 `astro.config.mjs` 中已正确配置 `useDarkModeMediaQuery: false` 和 `themeCssSelector`

**Q: 支持自定义主题吗？**
A: 支持，可以参考 [Expressive Code 官方文档](https://expressive-code.com/guides/themes/) 使用自定义主题

**Q: 代码高亮影响构建速度吗？**
A: 会有一定影响，但通常可以接受。Expressive Code 已经做了很多优化

**Q: 如何禁用代码高亮？**
A: 不建议禁用，但可以通过 CSS 隐藏高亮效果

**Q: 支持哪些编程语言？**
A: 支持大多数主流编程语言，具体列表请参考 [Shiki 文档](https://shiki.matsu.io/languages)

**Q: 如何添加新的编程语言支持？**
A: 通常不需要手动添加，Shiki 会自动检测语言类型

**Q: 为什么代码块背景颜色不变化？**
A: 确保 `astro.config.mjs` 中没有覆盖背景颜色的配置，让 Expressive Code 使用主题自带的背景颜色

**Q: 可以在代码块中使用自定义样式吗？**
A: 可以，通过 `styleOverrides` 配置或 CSS 自定义样式
