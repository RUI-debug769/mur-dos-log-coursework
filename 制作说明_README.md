# MUR DOS LOG — 制作说明

> 《解密DeekSeek：从基础到创意实践》课程大作业 · 源文件与制作说明

## 一、项目信息

| 项目 | 内容 |
|---|---|
| 作品名称 | MUR DOS LOG |
| 作品形式 | 个人博客网站（静态站点） |
| 线上地址 | **https://murdok.me**（主站）／ **https://rui-debug769.github.io**（GitHub Pages 镜像） |
| 源码仓库 | https://github.com/RUI-debug769/backup-blog （public） |
| 技术栈 | Astro 7 · Svelte 5 · Tailwind CSS 4 · Stylus · TypeScript |
| 构建工具 | pnpm 9（Node.js ≥ 22.12） |
| 部署方式 | GitHub Actions 构建 → rsync → 云服务器（Nginx） |
| 基础主题 | 开源主题 [Shirone](https://github.com/LyraVoid/Shirone)（MIT），在其之上二次开发 |

## 二、项目介绍

MUR DOS LOG 是一个面向本人的长期个人站点，用于集中记录项目进展、技术笔记、阅读与日常生活。它同时也是本课程的最终作品——一个从需求、视觉、交互到部署链路都完整走通的真实项目。

项目分两个阶段：

- **v1（2026-10-17 — 10-25）**：从零手写 Astro 7 站点，建立内容集合、RSS、sitemap 与自动部署；随后进行水墨／朱砂／数学层的视觉改造，并接入 Live2D 看板娘。
- **v2（2026-10-25 — 10-28）**：以开源主题 Shirone 为基底重构，重建站点标识与配色体系，迁移全部文章，补齐追番／书单／相册／碎碎念／友链栏目，重写开场动画，并完成上线收尾。

> **说明（学术诚信）**：v2 的骨架与主题层基于 MIT 协议的开源主题 Shirone；本人在其之上完成的原创与改造部分已在下方「原创与改造清单」中逐项列出，未在本清单中的基础能力应视为上游主题提供。

## 三、功能说明

| 栏目 / 功能 | 说明 |
|---|---|
| 首页 | 站点标题、打字机引文、Hero 图轮换（16 张）、分类胶囊、文章卡、统计与日历 |
| 开场动画 | 三段式「终端 quine → glitch 崩解 → 漫画格少女」，17 秒，可跳过、可重播 |
| 文章 | Markdown/MDX 渲染、公式与代码高亮、浮动目录、字数与阅读时长、前后篇导航 |
| 归档 / 分类 / 标签 / 系列 | 按时间、分类、标签、系列聚合 |
| 追番 | 接入 Kazumi 的 WebDAV 数据，按「在看 / 看完 / 想看」分组 |
| 书单 | 结构化书目，八国语言文案键值补全 |
| 相册 / 碎碎念 / 友链 | 图像网格、短文本流、外部站点清单 |
| 数学彩蛋 | Gray-Scott 图灵斑图、正二十面体、交换图、Konami 键序列、Gödel 404 |
| 看板娘 | Live2D 双角色（洛天依、桃濑日和），可拖动、位置按相对坐标持久化 |
| 主题系统 | 明暗双主题 + 多套配色风格（Tonal Spot / Vibrant / Content / Expressive / Rainbow / Fruit Salad / Monochrome / Neutral / Fidelity）+ 五种背景纹理；切换时圆形扩散过渡 |
| 检索与订阅 | pagefind 全文搜索、RSS / Atom、sitemap、robots、llms.txt |
| 音乐播放器 | 接入网易云歌单 |
| 无障碍 | 键盘可达、焦点环、开场遮罩 aria-hidden、Playwright a11y 断言 |

### 原创与改造清单（本人完成）

1. `src/components/Intro.astro`（652 行）：自指开场动画全部代码——真实 quine 与哥德尔数、17 秒质数分镜（3/5/2/5/2）、行号高亮 2/3/5/7/11/13/17、三段式转场、主题跟随、重播机制。
2. Live2D 看板娘组件：双角色、自由拖动、相对坐标持久化、图层修复。
3. 数学彩蛋移植：Gray-Scott 图灵斑图、正二十面体、交换图、Konami。
4. 站点标识、配色与版式调校、Hero 素材池、文章封面、favicon。
5. 8 篇文章撰写与迁移、旧链接重定向。
6. 追番数据接入（Kazumi WebDAV）、书单页与多语言键值。
7. CI/CD 迁移（npm → pnpm）、部署管道、测试修正。

## 四、目录结构（主要部分）

```
blog-v2/
├── src/
│   ├── components/          # 组件（含 Intro.astro、Live2DWidget.astro、easter/）
│   ├── content/             # 文章内容集合
│   ├── pages/               # 路由页面（首页/归档/追番/书单/相册/友链/404…）
│   ├── layouts/             # 布局
│   ├── styles/              # 全局样式与排版
│   ├── config/              # 站点配置
│   ├── data/                # 追番、书单等数据
│   └── i18n/                # 多语言文案
├── public/                  # 静态资源（Live2D 模型、插画、图标）
├── .github/workflows/       # CI：ci.yml / deploy.yml / content-validate.yml
├── astro.config.mjs
├── package.json
└── DESIGN.md                # 设计 token（颜色、字体、间距）
```

## 五、运行方法

### 环境要求

- Node.js ≥ 22.12
- pnpm 9（`npm i -g pnpm@9`）

### 本地开发

```bash
pnpm install
pnpm dev          # 默认 http://localhost:4321
```

### 构建与预览

```bash
pnpm build        # 产物输出到 dist/
pnpm preview      # 本地预览构建结果
```

### 测试与检查

```bash
pnpm test         # Playwright 端到端与无障碍断言（需先 npx playwright install）
pnpm lint         # Biome 静态检查
```

### 发布文章

在 `src/content/` 下按既有 frontmatter 规范新建 Markdown 文件 → 提交 → 推送到 main，GitHub Actions 自动构建并同步到服务器。

```bash
git add -A && git commit -m "post: <标题>" && git push
```

### 部署

`.github/workflows/deploy.yml`：`pnpm install --frozen-lockfile` → `pnpm build` → `rsync` 到服务器 `/var/www/blog/`，由 Nginx 托管。所需 Secrets：`ECS_HOST` / `ECS_USER` / `ECS_SSH_KEY`。

## 六、素材与版权说明

| 素材 | 来源 | 说明 |
|---|---|---|
| 主题骨架 Shirone | https://github.com/LyraVoid/Shirone | MIT 协议，已保留 LICENSE |
| Live2D 洛天依模型 | https://github.com/SheepLiu712/Agent-LuoTianyi | 遵循原仓库声明 |
| Live2D 桃濑日和模型 | Live2D 官方示例模型 | 仅作个人展示 |
| 插画 / 立绘 | AI 生成（Seedream 等）+ 本人筛选 | 以「角色圣经」约束一致性 |
| 追番数据 | Kazumi（WebDAV 同步） | 个人观看记录 |

## 七、AI 工具使用声明

本项目主要开发工具为 **Claude Code 客户端 + DeepSeek 模型接口**：Claude Code 负责工程外壳（读写文件、执行命令、组织多轮协作），实际推理由 DeepSeek 系列模型提供，会话中可按任务切换不同档位。图像素材使用图像生成模型（Seedream 等）产出，并由本人筛选与修正。

课程中学到的技术路线（MoE 稀疏激活、MLA、推理链）并非纸面知识，而是判断依据：用于预估长上下文重构的成本、判断何时切换档位、何时把需求压缩成文档重新喂入。完整的协作过程见同目录 `AI交互记录.md`。
