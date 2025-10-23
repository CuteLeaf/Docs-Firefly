---
title: Mermaid图表
createTime: 2025/08/21 13:26:53
permalink: /press/chart/
copyright:
  creation: reprint
  license: CC-BY-4.0
  source: https://docs.mizuki.mysqil.com
  author:
    name: 松坂有希
    url: https://github.com/matsuzaka-yuki
---

我们可以使用mermaid语法来在文章中绘制图表
```
    ```mermaid
    graph TD
        A[Start] --> B{Condition Check}
        B -->|Yes| C[Process Step 1]
        B -->|No| D[Process Step 2]
        C --> E[Subprocess]
        D --> E
        subgraph E [Subprocess Details]
            E1[Substep 1] --> E2[Substep 2]
            E2 --> E3[Substep 3]
        end
        E --> F{Another Decision}
        F -->|Option 1| G[Result 1]
        F -->|Option 2| H[Result 2]
        F -->|Option 3| I[Result 3]
        G --> J[End]
        H --> J
        I --> J
    ```
```