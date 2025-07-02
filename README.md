# bump-version

一个智能的语义化版本管理命令行工具，专为现代 JavaScript/TypeScript 项目设计。

## 简介

`bump-version` 是一个交互式的版本管理工具，它遵循[语义化版本规范](https://semver.org/)，支持正式版本和预发布版本的管理。该工具通过友好的命令行界面，自动化处理版本号更新、Git 提交和标签创建等繁琐的发布流程。

## 职责

本工具负责以下核心任务：

- **版本号管理**：自动计算和更新符合语义化版本规范的版本号
- **Git 集成**：自动创建规范的提交信息和标签
- **发布流程自动化**：一键完成版本更新、提交、标签创建和推送
- **预发布版本支持**：管理 alpha、beta、RC 等预发布版本的迭代
- **安全检查**：确保在干净的工作区和正确的分支上进行发布

## 特性

### 🎯 核心特性

- **交互式界面**：通过友好的命令行交互界面选择版本类型和更新方式
- **智能版本计算**：自动根据当前版本和选择的类型计算下一个版本号
- **预发布版本管理**：
  - 支持 alpha、beta、RC 三种预发布类型
  - 自动处理预发布版本间的升级路径
  - 支持预发布版本转正式版本
- **Git 工作流集成**：
  - 自动提交 package.json 和 package-lock.json（如果存在）
  - 创建带注释的 Git 标签
  - 一键推送到远程仓库
- **安全保护**：
  - 检查工作区是否有未提交的更改
  - 警告非主分支发布（可选择继续）
  - 执行前显示详细的执行计划

### 📦 版本类型支持

1. **正式版本**
   - Patch (修订号): 错误修复 (1.0.0 → 1.0.1)
   - Minor (次版本号): 新功能，向后兼容 (1.0.0 → 1.1.0)
   - Major (主版本号): 重大更新，可能不兼容 (1.0.0 → 2.0.0)

2. **预发布版本**
   - Alpha: 内部测试版本 (1.0.0 → 1.0.1-alpha.0)
   - Beta: 公开测试版本 (1.0.0-alpha.1 → 1.0.0-beta.0)
   - RC: 候选发布版本 (1.0.0-beta.1 → 1.0.0-rc.0)

## 安装

### 全局安装

```bash
npm install -g bump-version
```

### 项目内安装

```bash
npm install --save-dev bump-version
```

## 使用

### 基本使用

在项目根目录（包含 package.json 的目录）运行：

```bash
bump-version
```

### 使用流程

1. **启动工具**
   ```bash
   bump-version
   ```

2. **选择发布类型**
   - 正式版本 (Production)
   - Alpha 版本
   - Beta 版本
   - RC 版本

3. **选择版本递增类型**（仅在需要时）
   - Patch: 修复 bug
   - Minor: 新增功能（向后兼容）
   - Major: 重大更改（可能不兼容）

4. **确认执行计划**
   - 查看版本变更详情
   - 确认执行步骤
   - 输入 y 确认或 n 取消

### 示例场景

#### 发布修复版本
```
当前版本: 1.0.0 → 新版本: 1.0.1
```

#### 发布新功能
```
当前版本: 1.0.1 → 新版本: 1.1.0
```

#### 发布 Alpha 测试版
```
当前版本: 1.1.0 → 新版本: 1.2.0-alpha.0
```

#### Alpha 版本迭代
```
当前版本: 1.2.0-alpha.0 → 新版本: 1.2.0-alpha.1
```

#### 升级到 Beta 版本
```
当前版本: 1.2.0-alpha.2 → 新版本: 1.2.0-beta.0
```

#### 发布正式版本
```
当前版本: 1.2.0-rc.1 → 新版本: 1.2.0
```

## 开发

### 环境要求

- Node.js >= 14.0.0
- Git
- npm 或 yarn

### 克隆项目

```bash
git clone https://github.com/ai-app-base/bump-version-js.git
cd bump-version-js
```

### 安装依赖

```bash
npm install
```

### 开发命令

```bash
# 开发模式运行
npm run dev

# 构建项目
npm run build

# 运行测试
npm test

# 运行测试（带 UI）
npm run test:ui

# 生成测试覆盖率报告
npm run coverage
```

### 项目结构

```
bump-version-js/
├── src/
│   └── bump-version.ts      # 主程序源码
├── tests/
│   ├── bump-version.integration.test.ts  # 集成测试
│   └── setup.ts             # 测试设置
├── dist/                    # 构建输出目录
├── package.json            # 项目配置
├── tsconfig.json           # TypeScript 配置
└── vitest.config.ts        # 测试框架配置
```

### 技术栈

- **语言**: TypeScript
- **测试框架**: Vitest
- **依赖库**:
  - prompts: 命令行交互
  - chalk: 终端颜色输出
  - execa: 子进程执行（测试用）

### 测试

项目包含完整的集成测试，覆盖以下场景：

- 版本号升级逻辑（patch/minor/major）
- 预发布版本管理（alpha/beta/rc）
- 错误处理（未提交更改、分支检查、用户取消）
- Git 操作验证（提交信息、标签创建）

运行测试：
```bash
npm test
```

### 贡献指南

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'feat: add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建 Pull Request

### 提交规范

项目遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

- `feat:` 新功能
- `fix:` 修复 bug
- `docs:` 文档更新
- `style:` 代码格式调整
- `refactor:` 代码重构
- `test:` 测试相关
- `chore:` 构建过程或辅助工具的变动

## 许可证

[ISC](LICENSE)

## 相关链接

- [语义化版本规范](https://semver.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Repository](https://github.com/ai-app-base/bump-version-js)