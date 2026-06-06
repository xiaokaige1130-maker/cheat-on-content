# Cheat on Content - 网红作弊器

把每一条内容变成可校准的实验：打分 -> 盲预测 -> 发布 -> 复盘 -> 进化评分公式。

## 功能特性

- **量化打分**：基于可进化的 rubric 对每篇内容多维度评分，让直觉可衡量
- **盲预测**：发布前写下预测并锁定（immutable），发布后用真实数据对账
- **T+3 天复盘**：数据回收后自动复盘，精确看到哪里判断准、哪里偏
- **rubric 自动进化**：连续偏差自动提示升级评分公式，升级需全量重打 + 跨模型审核
- **对标账号导入**：导入 5-10 条对标样本，工具立刻获得校准锚点
- **选题推荐与热点抓取**：候选池排序推荐 + 多源热点补充
- **受众画像**：从复盘评论数据自动派生受众画像
- **状态看板**：buffer 警戒、待复盘、候选池一目了然

## 技术栈

- **运行环境**：Bash / Shell 脚本
- **AI Agent**：Claude Code（默认）、Codex
- **数据源适配**：Python（抖音/小红书爬虫、Whisper 语音转文字）
- **存储**：Markdown 文件 + 可选 SQLite
- **Hook 机制**：Shell 脚本实现预测不可变性保护

## 快速开始

### 安装

```bash
git clone https://github.com/XBuilderLAB/cheat-on-content.git
cd cheat-on-content
bash install.sh
```

支持的 agent：
- Claude Code（默认）
- Codex：`bash install.sh --codex`
- 两个都装：`bash install.sh --all`
- 冻结版本（复制而非软链接）：`bash install.sh --copy`
- 卸载：`bash uninstall.sh`

### 首次使用

在你的内容项目目录中，打开支持 skill 的 agent，输入：

```
初始化 cheat-on-content
```

回答 5 个 yes/no 问题完成初始化。强烈建议导入对标账号（5-10 条样本）作为校准锚点。

### 日常使用

```
打分这篇 scripts/<...>.md         -> 评分
启动预测 scripts/<...>.md         -> 盲预测 + 决策日志
拍了 scripts/<...>.md            -> 建 video folder + buffer +1
已发布 https://...                -> buffer -1
复盘 videos/<...>/                -> T+3d 数据回收 + 复盘
状态 / 抓热点 / 找选题 / 升级 rubric / 找对标
```

## 项目结构

```
cheat-on-content/
├── SKILL.md                # 总协议 + 路由表
├── install.sh              # 安装脚本
├── uninstall.sh            # 卸载脚本
├── skills/                 # 15 个子 skill
│   ├── cheat-init/         # 初始化与 onboarding
│   ├── cheat-score/        # 单稿打分
│   ├── cheat-predict/      # 盲预测 + immutable 日志
│   ├── cheat-retro/        # 数据回收 + 复盘
│   ├── cheat-bump/         # rubric 升级
│   └── ...                 # 其他子 skill
├── shared-references/      # 跨 skill 共享协议（盲预测、升级验证、观察生命周期等）
├── templates/              # 用户项目的文件骨架模板
├── starter-rubrics/        # 各内容形态的先验评分规则
├── hooks/                  # harness 层强制钩子（预测不可变性保护等）
├── adapters/               # 数据源适配（抖音/小红书/热点/语音转文字）
├── migrations/             # schema 演进与版本迁移
├── tools/                  # 独立 CLI 工具
└── examples/               # 示例文件
```

## 许可证

MIT
