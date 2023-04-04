---
description: 学习使用 Mermaid
---

# Mermaid

### 概述

Mermaid lets you create diagrams and visualizations using text and code.

It is a JavaScript based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically.

The main purpose of Mermaid is to help documentation catch up with development.

{% embed url="https://mermaid.js.org/" %}
Mermaid 官网
{% endembed %}

### 流程图 Flowchart

#### 示例一

```mermaid
graph TD
  A --> B
  A --> C
  B --> D
  C --> D
```

```mermaid
graph TD
  A --> B
  A --> C
  B --> D
  C --> D
```

### 时序图 Sequence diagram

#### 示例一

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
```

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/> prevail
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Joly good!
    
```

### 甘特图 Gantt diagram

#### 示例一

### 类图 Class diagram

#### 示例一
