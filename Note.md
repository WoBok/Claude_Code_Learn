# Claude Code 学习笔记

## 一、记忆系统概述

Claude Code 有两套记忆系统：

| 类型 | 说明 |
|------|------|
| **CLAUDE.md 文件** | 由用户编写的持久化指令 |
| **Auto memory** | Claude 自动生成的学习笔记，存储在 `~/.claude/projects/<project>/memory/` 目录下 |

---

## 二、CLAUDE.md 文件的四种作用域

| 作用域 | 位置 | 用途 |
|--------|------|------|
| 管理策略 | Windows: `C:\Program Files\ClaudeCode\CLAUDE.md` | 组织级统一指令 |
| 项目指令 | `./CLAUDE.md` 或 `./.claude/CLAUDE.md` | 团队共享的项目指令 |
| 用户指令 | `~/.claude/CLAUDE.md` | 个人偏好设置 |
| 本地指令 | `./CLAUDE.local.md` | 项目特定的个人偏好，不提交到 git |

---

## 三、导入外部文件

CLAUDE.md 文件可以使用 `@path/to/import` 语法导入其他文件。

**特点：**
- 导入的文件在启动时与 CLAUDE.md 一起展开并加载到上下文中
- 这是一种**引用机制**，不会真正修改 CLAUDE.md 文件本身
- 原始的 CLAUDE.md 文件内容保持不变

**示例：**
```markdown
See @README for project overview and @package.json for available npm commands.

# Additional Instructions
- git workflow @docs/git-instructions.md
```

---

## 四、规则目录 `.claude/rules/`

对于大型项目，可以将指令拆分到 `.claude/rules/` 目录下：
- 每个 `.md` 文件覆盖一个主题
- 支持子目录组织
- 可使用 YAML frontmatter 的 `paths` 字段限定规则适用的文件范围

**示例：**
```markdown
---
paths:
  - "src/api/**/*.ts"
---

# API Development Rules
- All API endpoints must include input validation
```

---

## 五、自动记忆 (Auto Memory)

### 开启/关闭自动记忆

在 `settings.json` 或项目的 `.claude/settings.local.json` 中添加：

```json
{
  "autoMemoryEnabled": false
}
```

或通过环境变量：`CLAUDE_CODE_DISABLE_AUTO_MEMORY=1`

### 存储结构

```
~/.claude/projects/<project>/memory/
├── MEMORY.md          # 索引文件，每次会话加载前200行
├── debugging.md       # 详细调试笔记
├── api-conventions.md # API 设计决策
└── ...                # 其他主题文件
```

---

## 六、VSCode 集成注意事项

**问题：** 在 VSCode 中直接使用 Terminal 打开 Claude Code 无法使用 `/ide` 命令连接 VSCode。

**解决方法：**
- 使用 `Ctrl + Shift + P` → `Claude Code: Open in Terminal`
- 注意：此方式无法使用 `#` 号自动记录到 CLAUDE.md 中

---

## 七、常见问题排查

### Claude 不遵循 CLAUDE.md 指令

1. 运行 `/memory` 确认 CLAUDE.md 文件是否被加载
2. 检查指令是否具体明确（如用 "使用2空格缩进" 而非 "格式化代码"）
3. 检查是否有冲突的指令

### CLAUDE.md 文件过大

- 目标控制在 200 行以内
- 使用 `@path` 导入拆分内容
- 使用 `.claude/rules/` 目录组织规则

---

## 八、官方 Memory 文档总结

### 核心概念

Claude Code 的记忆系统帮助 Claude 跨会话保留上下文。每个会话开始时都是全新的上下文窗口，两套机制承载知识：

| 对比项 | CLAUDE.md | Auto Memory |
|--------|-----------|-------------|
| 编写者 | 用户 | Claude |
| 内容 | 指令和规则 | 学习和模式 |
| 作用域 | 项目/用户/组织 | 每个工作树 |
| 加载 | 每次会话完整加载 | 每次会话加载前200行 |
| 用途 | 编码标准、工作流、架构 | 构建命令、调试洞察、偏好 |

### CLAUDE.md 文件位置优先级

更具体的位置优先于更广泛的位置：

1. **管理策略** - 组织级强制指令，无法被排除
2. **项目指令** - `./CLAUDE.md` 或 `./.claude/CLAUDE.md`
3. **用户指令** - `~/.claude/CLAUDE.md`
4. **本地指令** - `./CLAUDE.local.md`（不提交 git）

### 加载机制

- Claude Code 从当前工作目录向上遍历目录树加载 CLAUDE.md
- 子目录中的 CLAUDE.md 在访问该目录时按需加载
- 使用 `/init` 命令可自动生成初始 CLAUDE.md

### 编写有效指令的要点

| 要点 | 建议 |
|------|------|
| 大小 | 目标每文件 < 200 行 |
| 结构 | 使用标题和列表组织 |
| 具体 | "用2空格缩进" 而非 "格式化代码" |
| 一致 | 避免矛盾的规则 |

### 路径特定规则

使用 YAML frontmatter 限定规则适用的文件：

```markdown
---
paths:
  - "src/api/**/*.ts"
  - "lib/**/*.ts"
---
```

### Auto Memory 工作方式

- Claude 自动决定什么值得记住
- 存储在 `~/.claude/projects/<project>/memory/`
- `MEMORY.md` 作为索引，主题文件存储详情
- 使用 `/memory` 命令查看和管理

### 常用命令

| 命令 | 说明 |
|------|------|
| `/memory` | 查看已加载的 CLAUDE.md 和规则文件 |
| `/init` | 自动生成 CLAUDE.md |
| `/compact` | 压缩上下文（CLAUDE.md 会完整保留） |