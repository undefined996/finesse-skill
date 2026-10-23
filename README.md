[中文](README.md) | [English](README.en.md)

![finesse-skill cover](assets/cover.jpg)

<div align="center">

# finesse-skill

**绝不廉价的高级界面 —— 品牌惊艳 · 产品精密 · 手机原生**

给 AI 编码助手用的设计技能。它不生成"还行"的页面，它生成有灵魂、有工艺、经得起看的页面。

[![version](https://img.shields.io/badge/version-0.22.0-111?style=flat-square)](https://github.com/mouse-lin/finesse-skill/releases)
[![license](https://img.shields.io/badge/license-MIT-111?style=flat-square)](LICENSE)
[![rules](https://img.shields.io/badge/设计规则-31_篇-c9863f?style=flat-square)](skills/finesse-ui/references)
[![examples](https://img.shields.io/badge/示例页面-30_个-5ee9c8?style=flat-square)](skills/finesse-ui/examples)

[快速开始](#快速开始) · [四条路线](#四条路线register) · [核心能力](#核心能力) · [示例作品](#示例作品) · [安装](#安装--工具支持) · [使用清单](USAGE.md)

</div>

---

## 快速开始

```bash
npx skills add https://github.com/mouse-lin/finesse-skill
```

然后在对话里直接说话就行：

> "用 finesse 做一个精品咖啡的落地页"
> "做个团队数据仪表台"
> "设计一个记账 app 的界面"

它会**先回你一句它打算做什么**（用你看得懂的话），等你点头才开始写代码。

> [!TIP]
> 第一次用、又没有设计背景？先看 **[使用清单 USAGE.md](USAGE.md)** —— 教你怎么提需求、怎么否决、怎么迭代。

---

## 四条路线（register）

同一个 brief，不同的路线走出来是**完全不同的设计语言**。finesse 先判定路线，再决定一切。

| 路线 | 什么页面 | 优化什么 | 核心手法 |
|:---|:---|:---|:---|
| **brand**<br><sub>设计即产品</sub> | 落地页 · 品牌站 · 发布页<br>作品集 · 行业 hero 页 | 惊艳 + 灵魂<br>第一印象 | 选一个灵魂 + 造**一个**真视觉引擎<br><sub>Three.js / GLSL / Canvas / WebGL / GSAP</sub> |
| **product**<br><sub>设计服务产品</sub> | 仪表盘 · 后台 · analytics<br>数据表 · app shell · 设置 | 清晰 + 密度<br>可用性 | 组件系统 + 数据可视化<br><sub>先定配色，否则每个仪表盘都是蓝的</sub> |
| **commerce**<br><sub>混合</sub> | 商详 · 列表 · 购物车 · 结算 | 转化<br>不玩阴的 | 按这页在做什么，归到上面两路<br><sub>卖单品像 brand，筛列表像 product</sub> |
| **h5**<br><sub>容器路线</sub> | H5 · 移动端页面 · 活动页<br>小程序页 · app 原型 · 移动商详 | 手上的手感 | **先钉死手机框架**，再套上面三路之一<br><sub>移动商详 = h5 + commerce</sub> |

四条路共享同一底色：**高级感物理层 + 反廉价审查**。仪表盘不许长得廉价，H5 也一样。

<details>
<summary><b>它具体怎么跑（五步）</b></summary>

<br>

1. **先读 brief** —— 先问"这页有没有桌面形态"，没有就是 h5；再分 brand / product / commerce。输出一句 Design Read 定方向，**停下来等你确认**。
2. **拧三个旋钮** —— SOUL（风格辨识度）· SPECTACLE（视觉炫技，招牌旋钮）· DENSITY（信息密度）。product 模式 SPECTACLE 压低、DENSITY 拉高。
3. **铺物理层** —— grain 噪点 · vignette 暗角 · 字重张力 · 半透明边框 · OKLCH 色彩锁定。h5 则**先立框架**，再铺所套 register 的物理层。
4. **分流**
   - **brand** → 选灵魂（行业→风格人格）+ 造一个 hero 引擎，五类选一，**100% 做透**（不做五个半成品）
   - **product** → 组件系统 + 数据可视化（信息架构 · 表格 · 图表 · 表单 · 交互状态全集）
   - **h5** → 选六种手机形态之一（app 壳 / 翻页 deck / snap 叙事 / 移动商详 / 手机官网 / 沉浸单屏）+ 照抄原生家具
5. **反廉价黑名单 + 起飞前自检**，再交付。

</details>

---

## 核心能力

<table>
<tr>
<td width="50%" valign="top">

**视觉工艺**

- **高级感物理层** — grain / vignette / 字重张力 / 配色家族<br><sub>提炼自 53 页行业展示页语料</sub>
- **五类 hero 视觉引擎** — Three.js · Canvas · WebGL-FBO · GSAP · CSS-only，各含 reduced-motion 降级骨架
- **3D 效果谱系** — CSS 伪 3D（倾斜 / 翻转 / coverflow / 景深）+ Three.js 真 3D
- **Apple 设计语言** — 官网展示 · 应用界面 · 空间材质，按页面用途选择<br><sub>系统字体 · 黑白层级 · 内容驱动的 Bento · 跟手反馈，适用于现有四条路线</sub>
- **OKLCH 配色阶梯** — restrained / committed / full / drenched 四档承诺

</td>
<td width="50%" valign="top">

**决策与防错**

- **反同质化引擎** — 五轴组合造灵魂，而不是从清单里挑<br><sub>带跨次构建记忆，"别重复"这条规则才真的会触发</sub>
- **反廉价黑名单** — 经生产验证的 AI tells + 绝对禁区 + reflex-reject 字体/配色清单
- **起飞前自检** — 承诺兑现 · 廉价扫描 · a11y · 移动地板
- **本地检测器** — `detect.mjs` 机械扫 slop 与"宣称了没做到"

</td>
</tr>
<tr>
<td width="50%" valign="top">

**product 路线**

- 仪表盘信息架构 · 六种 shell 形态
- 25 种图表选型 × a11y 分级 × 库推荐
- 手搓图表实现层（零依赖 SVG 配方）
- 数据表 · 表单 · 交互状态全集
- **product 专属配色库** — 5 套中性色阶 + 16 个强调色 + 12 套可直接粘贴的组合
- **AI 工作台**（你委派、然后盯着的页面）—— 三时态同屏 · 运行流取代图表 · 九种运行态 · 常驻停止 · 人在回路审批卡 · 成本回执<br><sub>它不像仪表盘那样死于看不懂，也不像流程页那样死于走不完 —— 它死于不可信</sub>

</td>
<td width="50%" valign="top">

**h5 路线**

- 视口契约 · `body` 锁死 / 容器滚动的**架构反转**
- 560px 桌面手机画框 · 安全区数学
- **拇指区反转** —— 主操作一律放底部
- 触摸法则（`passive` / `pointercancel` / tap-highlight / 44px）
- 六种手机形态 + 原生家具配方<br><sub>状态栏 · TabBar · 底部 sheet · FAB · push 与手写 FLIP 转场</sub>

</td>
</tr>
</table>

---

## 示例作品

出自同一设计基因，却刻意长得毫不相干 —— 这正是反同质化引擎在做的事。

<details open>
<summary><b>brand 路线</b> —— 视觉引擎 · 灵魂驱动 · 多行业覆盖</summary>

<br>

| | |
|:---:|:---:|
| ![Nexus — Three.js 粒子轨道环，分布式智能平台](assets/examples/nexus.png) | ![Drift — Canvas 2D 流场粒子，品牌落地页](assets/examples/drift.png) |
| **Nexus** · Three.js 粒子轨道环 | **Drift** · Canvas 2D 流场粒子 |
| ![Forge — Three.js 粒子火焰，游戏工作室](assets/examples/forge.png) | ![Volt — 纯电汽车，粗体排版](assets/examples/volt.png) |
| **Forge** · Three.js 粒子火焰 | **Volt** · 粗体排版 · 纯电汽车 |
| ![Morning Ritual — 精品咖啡，editorial 浅色主题](assets/examples/coffee.png) | ![Eclipse — 数据引力平台，粗体排版](assets/examples/eclipse.png) |
| **Morning Ritual** · editorial 浅色 | **Eclipse** · 数据引力平台 |

</details>

<details>
<summary><b>product 路线</b> —— 组件系统 · 数据可视化 · 六种 shell 形态</summary>

<br>

| | |
|:---:|:---:|
| ![Buildly — AI 增长分析，经典侧边栏 shell + 面积图描线 + 甜甜圈](assets/examples/buildly.jpg) | ![Pulsegrid — 基础设施监控，发光 sparkline + 高级自定义滑块](assets/examples/stakent.jpg) |
| **Buildly** · 经典侧边栏 + 面积图描线 | **Pulsegrid** · 发光 sparkline + 自定义滑块 |
| ![ACRU — 团队效率，侧边栏经典 shell + 悬停 tooltip 柱状图](assets/examples/acru.jpg) | ![PawCare+ — 宠物健康看护，真实照片热点标注 + 主题色切换](assets/examples/pawcare.jpg) |
| **ACRU** · 浅色侧边栏 + tooltip 柱状图 | **PawCare+** · 照片热点标注 + 主题色切换 |
| ![Nodeflux — API 控制台，浮层面板 + 真 bento + 同心用量环](assets/examples/nodeflux.jpg) | ![Inkline — 内容发布 CMS，三栏 triptych + 浏览器预览热点标注](assets/examples/inkline.jpg) |
| **Nodeflux** · 浮层面板 + 真 bento | **Inkline** · 三栏 triptych + 浏览器预览 |
| ![Huddle — 团队协作，顶部导航 bento + 撞色任务卡 + 多弧甜甜圈 + 语音波形](assets/examples/huddle.jpg) | ![Threadline — 客服运营，浮层面板 + 不对称 bento + 环形仪表盘](assets/examples/ledgerio.jpg) |
| **Huddle** · 顶导 bento + 多弧甜甜圈 | **Threadline** · 不对称 bento + 环形仪表 |

</details>

<details open>
<summary><b>工作台</b> —— 围着他自己反复做的一件事转，一个物种、两副身体</summary>

<br>

> **先分清「工作台」和「后台」，这是这个 Skill 里最容易做错、也最贵的一步。**
>
> | | **后台** | **工作台** |
> |---|---|---|
> | 围着什么转 | 一批业务对象 —— N 个客户 · 订单 · 设备 · 工单 | **他自己反复在做的一件事** —— 记账 · 值守 · 带娃 · 写作 · 处理异常单 |
> | 为什么打开 | 有活要处理：来单了、告警了、该出报表了 | 到点了，回来看一眼 · 记一笔 · 收个尾 |
> | 数据谁写 | 系统、对接、别人 | **他自己**，几秒钟，成本必须接近零 |
> | 性格 | **中性是义务** —— 它活在别人的品牌里，旁边还有十一个工具 | **必须有** —— 这是他的台子，中性的没有第二次打开的理由 |
>
> **人数和屏幕都不是判据。** 一家人共用的记账台、一个小组共用的值守台都是工作台；一个人独用的进销存仍是后台。屏幕只决定它用哪副身体 ——

**身体一 · 电脑上开**

![RELAY 订单异常处理台 — 三栏工作台，暗色左轨 + 运行流 + 右侧凭据栏，审批卡在流里](assets/examples/relay.jpg)

**RELAY · 订单异常处理台** —— 这台子还带了一层能力：**有 agent 在替他跑活**。这一层跟身体正交（手机上的工作台也能带），它加的不是版式，是"凭什么信得过"。dashboard 靠"读得懂"活，向导靠"填得完"活，**带 agent 的靠"信得过"活**：

| 屏上的东西 | 它在回答什么 |
|---|---|
| 左轨三段：正在跑 · 排队 · 今天跑完的 | 三个时态同屏，不用切页就知道全局 |
| 中间**运行流**取代图表，9 步逐条带耗时 | 「它现在在干什么」—— 而不是一个转圈 |
| 审批卡**长在流里**，写明 要做什么 / 影响什么 / **凭什么（带链接回到第 2 步）** | 「它凭什么这么建议」 |
| 右栏：它看得到什么 · 它能动什么（只读/读写/需你批准） | 权限不是设置页里的一行字，是当场可见的 |
| 底部回执 `42.6s · 18.2k token · ¥0.41` + 本月预算条 | 「这要花我多少钱」—— 账单不该月底才出现 |
| 常驻**停止**（顶部一个、输入框一个） | 「我怎么让它停」—— 关标签页停不掉任何东西 |

配色是 `product-palettes.md` 第 7 套，接上了带 agent 时专属的语义色对：**brick =「在等你」，olive =「它自己干完的」，而且 brick 更响是故意的** —— 眼睛该落在被卡住的那一条，不是自己解决了的两百行。全页只有一个持续动画：当前步骤上的心跳环。

**身体二 · 手机上开**

<table>
<tr>
<td width="50%" align="center" valign="top">
<img src="assets/examples/h5-fern.jpg" width="270" alt="蕨 — 每日饮食记录工作台，亮色手机框 + 11 段弧形仪表 + 黑色药丸 TabBar 与凸起 FAB"><br><br>
<b>形态 A.1 · 手机身体</b> &nbsp;<sub>（暖沙 + 赭石）</sub><br>
<sub>11 段弧形仪表（23×37 胶囊，奇偶双色）<br>亮色手机框 · 黑色药丸 TabBar + 凸起 FAB<br><b>一天记几次，一次几秒</b></sub>
</td>
<td width="50%" align="center" valign="top">
<img src="assets/examples/h5-peach.jpg" width="270" alt="桃 — 每日习惯工作台，粉彩渐变 + 三习惯同心多弧圆环 + 心情/饮水/体重 tiles"><br><br>
<b>形态 A.1 · 手机身体</b> &nbsp;<sub>（粉彩渐变）</sub><br>
<sub>三个习惯共用一个同心多弧圆环<br>渐变卡面不靠描边也立得住 · 零图片<br><b>「高级」和「柔软」不是反义词</b></sub>
</td>
</tr>
</table>

> **同一个形态、同一套家具，两个样子完全不同** —— 这正是重点。工作台是**他的**，所以性格是必需品；而后台必须中性。
>
> **上面三张图是同一个物种。** RELAY 在电脑上、蕨和桃在手机上，共享的是「围着他反复做的一件事转 · 到点回来 · 他自己写数据 · 必须有性格」。不同的只有身体：桌面用 `product-ui.md` 的 shell（但带这份克制的密度），手机用 `h5-mobile.md` 的 **形态 A.1**。RELAY 多的那层 agent 机械是**能力**，手机身体一样能带（`ai-console.md` §9 就是它的手机形态）。

</details>

<details open>
<summary><b>h5 路线</b> —— 竖屏 390×844，桌面上自动套一层手机画框</summary>

<br>

<table>
<tr>
<td width="50%" align="center" valign="top">
<img src="assets/examples/h5-pawpal.jpg" width="270" alt="PAWPAL 毛毛档案 — 宠物养护 App，悬浮胶囊 TabBar + 中间凸起 FAB + 三段粗圆环 + 白色底部 sheet"><br><br>
<b>形态 A · app 壳</b> &nbsp;<sub>（包 product）</sub><br>
<sub>悬浮胶囊 TabBar + 凸起 FAB · 三段粗圆环<br>胶囊柱状图 · 白色底部 sheet<br><b>切换宠物整页重绘，而家具一动不动</b></sub>
</td>
<td width="50%" align="center" valign="top">
<img src="assets/examples/h5-brew.jpg" width="270" alt="烘豆日记 — 挂耳咖啡商品详情，scroll-snap 图集 + SKU 面板 + 吸底四段购买栏"><br><br>
<b>形态 D · 移动商详</b> &nbsp;<sub>（包 commerce）</sub><br>
<sub>scroll-snap 图集 + 页码 · SKU 面板联动改价<br>加购小球抛物线飞入 + 角标弹跳<br><b>吸底购买栏，安全区算进 padding</b></sub>
</td>
</tr>
</table>

> 这两页也在 `skills/finesse-ui/examples/` 里，**打开就能跑**。图片是代码生成的 SVG 占位符（`PH()`），换成真实图片 URL 即可 —— 周围的 CSS 一行都不用改。

</details>

<details open>
<summary><b>Apple 设计语言</b> —— 卡片比例 · 黑白层级 · 留白与交互</summary>

<br>

| | |
|:---:|:---:|
| ![Apple Bento — 主视觉跨行，辅助卡片围绕内容组织](assets/examples/apple-bento.jpg) | ![Apple Contrast — 黑白背景与产品明暗共同建立层级](assets/examples/apple-contrast.jpg) |
| **[Bento Grid](skills/finesse-ui/examples/apple-bento.html)** · 主卡层级 + 网格重排 | **[黑白对比](skills/finesse-ui/examples/apple-contrast.html)** · 明度层级 + 产品留白 |

[卡片总览](skills/finesse-ui/examples/apple-overview.html) · [标准圆角](skills/finesse-ui/examples/apple-corners.html) · [横竖间距](skills/finesse-ui/examples/apple-layout.html) · [多图排版](skills/finesse-ui/examples/apple-gallery.html) · [配色关系](skills/finesse-ui/examples/apple-palette.html)

> **七个可交互的设计练习** —— 调整间距、切换主卡位置、拖动图库、展开产品细节，把比例与节奏放到手上比较。字体、材质和跟手反馈也纳入同一套规范。
>
> <sub>产品图片用于设计学习，权利归原权利人；[素材说明](skills/finesse-ui/examples/apple/ASSETS.md)。</sub>

</details>

---

## 安装 & 工具支持

> [!NOTE]
> 推荐用 `npx skills`，一条命令通用于所有 agent。其他工具的手动装法在下面的折叠区里。

```bash
# 安装全部 skill（运行时会让你选装到哪个 agent）
npx skills add https://github.com/mouse-lin/finesse-skill

# 只装 finesse-ui
npx skills add https://github.com/mouse-lin/finesse-skill --skill "finesse-ui"
```

安装后在对话里说"用 finesse 做一个 …"或 `/finesse` 即可触发。

| 工具 | 深度 | 装法 |
|:---|:---|:---|
| **Claude Code** | 完整 | `npx skills` 或原生插件 `.claude-plugin/plugin.json` |
| **Trae / Trae 国内版** | 完整镜像 | 复制整个 `.trae/skills/finesse-ui/` 目录 |
| **CodeBuddy** | 完整镜像 | 复制整个 `.codebuddy/skills/finesse-ui/` 目录 |
| **豆包 Doubao** | 完整镜像 | 复制 `.doubao/skills/finesse-ui/` 到豆包技能目录（[见下](#豆包doubao)） |
| **Cursor** | 单文件规则 | 复制 `.cursor/rules/finesse-ui.mdc` |
| **OpenAI Codex** | 单文件指令 | 复制 `AGENTS.md` 到项目根目录 |
| **GitHub Copilot** | 单文件指令 | 复制 `.github/copilot-instructions.md` |
| **其他（ChatGPT / API）** | 手动 | 把 `SKILL.md` 粘进 system prompt |

<details>
<summary><b>各工具的具体命令</b></summary>

<br>

### Cursor

```bash
cp .cursor/rules/finesse-ui.mdc your-project/.cursor/rules/
```

编辑 HTML / CSS / JS / TS / Vue / Svelte 文件时会自动加载。

### OpenAI Codex

```bash
cp AGENTS.md your-project/AGENTS.md
```

或直接把 `skills/finesse-ui/SKILL.md` 的内容粘进 Codex 对话。

### GitHub Copilot

```bash
cp .github/copilot-instructions.md your-project/.github/
```

Copilot 会自动读取并以 finesse 标准生成代码。

### Trae

```bash
cp -r .trae/skills/finesse-ui your-project/.trae/skills/
# 国内版：
cp -r .trae-cn/skills/finesse-ui your-project/.trae-cn/skills/
```

### CodeBuddy

```bash
cp -r .codebuddy/skills/finesse-ui your-project/.codebuddy/skills/
```

### 豆包（Doubao）

豆包桌面版的技能目录与 Claude Code 同构（`SKILL.md` + `references/` + `scripts/` 按需加载），但它是**全局安装**，不放进项目：

```bash
# macOS 豆包桌面版
DOUBAO=~/"Library/Application Support/Doubao/Default/.doubao/agent_mode/workspace/.user_skills"
mkdir -p "$DOUBAO" && cp -r .doubao/skills/finesse-ui "$DOUBAO"/
```

`.user_skills/` 与豆包内置的 `.skills/` 同级，是用户技能的加载根。装完重启豆包，问一句"你现在能用哪些技能"确认它在列表里。部分版本还会读 `~/Doubao/skills/`，如果没被识别，两处各放一份。

用之前先知道三件事：

- **豆包没有 `/finesse` 斜杠命令**。它不认 `user-invocable`，只能自然语言触发——说需求就行，或直接点名"用 finesse 做一个…"。
- **触发词和豆包内置技能重叠**。内置的 `doubao-app-builder` 覆盖「H5 / 网页应用 / 管理后台 / 工作台 / 数据看板」，`doubao-creative-design` 覆盖「落地页 / 详情页 / Banner」，都会来抢同一句话。所以豆包镜像换了一份**中文优先、长度对齐豆包内置技能**的 frontmatter（正文与 reference 和源逐字一致，不是精简版）。万一还是被内置技能接走，在提示里点名 `finesse-ui`。
- **`scripts/detect.mjs` 需要 node**。豆包环境没有 node 时只是跳过机器自检，其余规则照常。

> **为什么这几个是"完整镜像"**：Trae / CodeBuddy / 豆包的 Skills 目录结构与 Claude Code 原生一致，能按需加载全部 reference 文件，所以直接复制整个目录就拿到完整深度，不是精简版。
>
> **改动请只提 `skills/finesse-ui/`**：那里是唯一真源，其余四份镜像和 Cursor 规则都是从它派生的静态拷贝，由维护者统一同步。直接改镜像的 PR 会在下次同步时被覆盖。豆包镜像唯一手工维护的是它自己的 frontmatter，正文同样来自源。

</details>

---

## 仓库结构

<details>
<summary><b>展开完整目录树</b></summary>

<br>

```
finesse-skill/
├── skills/finesse-ui/
│   ├── SKILL.md                  # 主入口：方法论 + 流程 + 路由
│   ├── references/               # 31 篇详细规则，AI 用到哪篇读哪篇
│   └── examples/                 # 30 个打开就能跑的示例页 + 索引
├── .claude-plugin/plugin.json    # Claude Code 原生插件
├── .cursor/rules/finesse-ui.mdc  # Cursor 规则（单文件，自动加载）
├── AGENTS.md                     # OpenAI Codex 指令
├── .github/copilot-instructions.md
├── .trae/ · .trae-cn/ · .codebuddy/   # 完整镜像（脚本同步）
├── .doubao/skills/finesse-ui/     # 豆包镜像（正文同源，frontmatter 为豆包定制）
├── USAGE.md · USAGE.en.md        # 给非设计背景用户的使用清单
└── README.md · LICENSE
```

### 那 31 篇规则都写了什么

| 分类 | 文件 |
|:---|:---|
| **方法论** | `divergence.md` 反同质化五轴 · `style-personas.md` 行业→灵魂 · `inspiration-catalog.md` 48 页技法索引 |
| **brand** | `design-dna.md` 物理层 · `hero-engines.md` 五类引擎 · `page-crafting.md` 实现层 · `3d-effects.md` |
| **product** | `product-ui.md` · `product-palettes.md` 配色库 · `workflow-ui.md` 流程页 · **`ai-console.md`** AI 工作台 · `dataviz.md` 图表选型 · `chart-crafting.md` 手搓图表 |
| **commerce / h5** | `commerce-ui.md` · **`h5-mobile.md`** 手机专属全套 |
| **Apple 设计语言** | [`apple-design.md`](skills/finesse-ui/references/apple-design.md) 字体与材质 · [`apple-patterns.md`](skills/finesse-ui/references/apple-patterns.md) 卡片与布局 |
| **动效与交互** | `motion.md` 动效选型 · `interaction-motion.md` 跟手、中断与速度衔接 |
| **移动端** | `mobile-floor.md` 桌面页在手机上不坏掉的六条 |
| **质量闸门** | `anti-cheap.md` 反廉价 · `preflight.md` 起飞前自检 · `audit.md` 只读诊断 · `redesign-mode.md` 改造模式（审计优先） · `component-scope.md` 单组件八态 |
| **项目记忆** | `init.md` 写 PRODUCT.md · `document.md` 提取现有设计系统 · `design-model.md` 多页一致性 · `theming.md` 主题切换 |
| **表达** | `plain-words.md` 把内部黑话翻成人话 · `asset-sourcing.md` 取图决策 |

</details>

---

## 范围之外

finesse 覆盖 brand、product、commerce 和 h5，范围很宽。只有这两种情况不适合：

- **纯后端 / API / 无界面的数据任务**
- 明确要求"无个性、零打磨"的页面 —— finesse 总会带上工艺，真要平庸是另一种工具

h5 这条线还有一个边界：它管手机页面的**设计**，不管外围的**平台管道**。微信 JS-SDK 接入、分享卡片配置、支付对接、原生 bridge、小程序脚手架都是工程活儿 —— 页面做完，这些交出去。

---

<div align="center">
<sub>

**MIT License** · 作者 西瓜同学

觉得有用的话，点个 ⭐ 让更多人看到

</sub>
</div>
