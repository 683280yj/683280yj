# 开发规范 / Development Standards

适用于本人全部仓库。目标：**内行不笑、外行觉得酷** —— 低冗余、可复现、易接手。

---

## 一、代码规范 / Code Standards

### 语言与栈
- 前端默认 **TypeScript + React + Tailwind + Vite**；静态站优先 **Astro / 静态生成**。
- 脚本/CLI 用 **Shell (zsh/bash)** 或 **Python**；避免无意义的纯 HTML 单文件 Demo 冒充项目。
- 每个仓库必须有明确的 `package.json` / `pyproject.toml` / `Makefile` 等可复现入口。

### 命名
- 变量/函数：`camelCase`；组件 / 类 / 常量：`PascalCase` / `UPPER_SNAKE`。
- 文件：组件用 `PascalCase.tsx`，工具用 `kebab-case.ts`，测试 `*.test.ts`。
- 分支：`feat/`、`fix/`、`chore/`、`docs/`、`refactor/` 前缀。

### 提交
- 遵循 **Conventional Commits**：`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`。
- 一条提交只做一件事；不堆 `update` / `wip` 这类无意义信息。
- 禁止把密钥、`.env`、大二进制（>5MB）提交进仓库（用 `.gitignore` + Git LFS）。

### 结构
- `src/` 放源码，`public/` 放静态资源，`scripts/` 放一次性脚本，`docs/` 放文档。
- README 必须含：一句话定位、安装/运行命令、目录说明、截图或示例。

---

## 二、Fork 二次开发规范 / Fork & Secondary Dev

> 当前 70+ fork 仓库，按下列流程管理，避免「fork 了就忘」。

### Fork 前
- 先 Star + Watch，明确目的：**学源码** / **二次开发** / **提上游 PR**。
- 目的为「仅阅读」的仓库，不要长期保留 fork，看完即删。

### Fork 后初始化
```bash
git clone https://github.com/683280yj/<repo>.git
cd <repo>
git remote add upstream https://github.com/<ORIGINAL_OWNER>/<repo>.git
git fetch upstream
```
- 本地默认分支保持与 `upstream` 同步，自有改动一律走 **feature 分支**，不污染 `main`。

### 二次开发
- 所有改动从 `upstream/main` 最新处切 `feat/xxx` 分支。
- 定期 `git fetch upstream && git rebase upstream/main` 保持不脱节。
- 自有增强若具备通用性 → 向上游提 PR；纯私有需求 → 保留在 fork，README 注明「基于 <upstream> 的二次开发」。

### 同步与清理
- 每月巡检一次 fork 列表：已合入上游 / 已弃用的 fork 直接 **archive 或 delete**。
- fork 仓库命名若与上游冲突，加 `-patch` / `-dev` 后缀区分。

---

## 三、Pull Request 规范 / PR Standards

### 提交 PR 前
- 自检：`lint` + `build` + `test` 全绿；`git diff --stat` 控制在最小必要范围。
- 标题用 Conventional Commits；描述写清 **动机 / 改动 / 验证方式**。

### PR 描述模板
```markdown
## 动机
为什么改（解决什么问题 / 来源 issue）

## 改动
- 要点 1
- 要点 2

## 验证
- [ ] lint 通过
- [ ] 本地 build 通过
- [ ] 手动验证步骤
```

### Review 清单
- [ ] 单一职责，不夹带无关改动
- [ ] 无硬编码密钥 / 敏感信息
- [ ] 破坏性变更在描述中显式标注
- [ ] 自测通过，必要时附截图 / 录屏

### 合并
- 个人仓库自测通过的 fix/feat 直接 squash merge，保持线性历史。
- 他人贡献 PR 必须 review 通过 + CI 绿后才能合；不合入未声明来源的复制代码。

---

> 规范不是约束，是让「下次接手自己」成本归零。
