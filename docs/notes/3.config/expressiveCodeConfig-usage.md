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

### 设置代码高亮主题

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  theme: "github-dark", // 代码高亮主题
};
```

## 支持的主题

### 深色主题（推荐）

由于 Firefly 主题主要使用深色背景，建议使用深色主题：

| 主题名称 | 说明 | 特点 |
|----------|------|------|
| `github-dark` | GitHub 深色主题 | 经典，易读性好 |
| `monokai` | Monokai 主题 | 色彩丰富，对比度高 |
| `dracula` | Dracula 主题 | 紫色调，现代感强 |
| `one-dark` | One Dark 主题 | 简洁，护眼 |
| `nord` | Nord 主题 | 冷色调，专业感 |
| `tokyo-night` | Tokyo Night 主题 | 日系风格，优雅 |

### 浅色主题

| 主题名称 | 说明 | 特点 |
|----------|------|------|
| `github-light` | GitHub 浅色主题 | 经典，适合浅色背景 |
| `solarized-light` | Solarized 浅色主题 | 护眼，对比度适中 |
| `min-light` | Min 浅色主题 | 极简风格 |

## 主题配置示例

### 使用 GitHub 深色主题

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  theme: "github-dark",
};
```

### 使用 Monokai 主题

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  theme: "monokai",
};
```

### 使用 Dracula 主题

```typescript
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  theme: "dracula",
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

## 自定义样式

### 覆盖主题样式

如需自定义代码块样式，可以在 `astro.config.mjs` 中配置：

```javascript
// astro.config.mjs
export default defineConfig({
  // ... 其他配置
  markdown: {
    shikiConfig: {
      theme: 'github-dark',
      wrap: true,
      transformers: [
        // 自定义转换器
      ]
    }
  }
});
```

### CSS 自定义

通过 CSS 自定义代码块样式：

```css
/* 代码块容器 */
.shiki {
  border-radius: 8px;
  padding: 1rem;
  margin: 1rem 0;
  overflow-x: auto;
}

/* 行号样式 */
.shiki .line-number {
  color: #6e7681;
  margin-right: 1rem;
  user-select: none;
}

/* 代码文本样式 */
.shiki code {
  font-family: 'Fira Code', 'JetBrains Mono', monospace;
  font-size: 0.9rem;
  line-height: 1.6;
}

/* 复制按钮样式 */
.copy-button {
  position: absolute;
  top: 0.5rem;
  right: 0.5rem;
  background: rgba(255, 255, 255, 0.1);
  border: none;
  border-radius: 4px;
  color: white;
  cursor: pointer;
  padding: 0.25rem 0.5rem;
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

## 性能优化

### 按需加载

代码高亮主题会按需加载，只加载实际使用的语言：

```typescript
// 只加载常用语言
export const expressiveCodeConfig: ExpressiveCodeConfig = {
  theme: "github-dark",
  // 可以添加语言过滤配置
};
```

### 缓存优化

代码高亮结果会被缓存，提高构建速度。

## 注意事项

1. **主题选择**：建议选择与网站整体风格一致的主题
2. **性能考虑**：主题文件大小会影响构建速度
3. **可读性**：确保代码在所选主题下有良好的可读性
4. **一致性**：在整个网站中保持代码高亮风格一致

## 常见问题

**Q: 如何更换代码高亮主题？**
A: 修改 `theme` 字段的值即可

**Q: 支持自定义主题吗？**
A: 支持，可以通过 CSS 覆盖样式或使用自定义主题文件

**Q: 代码高亮影响构建速度吗？**
A: 会有一定影响，但通常可以接受

**Q: 如何禁用代码高亮？**
A: 不建议禁用，但可以通过 CSS 隐藏高亮效果

**Q: 支持哪些编程语言？**
A: 支持大多数主流编程语言，具体列表请参考 Shiki 文档

**Q: 如何添加新的编程语言支持？**
A: 通常不需要手动添加，Shiki 会自动检测语言类型
