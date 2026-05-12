> Make AI Writing Better for Everyone

## 📖 为什么做这个项目

当你第三次调试同一个润色 prompt 时，隔壁组的同学可能已经用现成的模板改完了三篇论文。

在学术圈，prompt 工程正在成为一种"隐性资源"——顶尖研究组有完善的模板库，而大多数人还在从零摸索。更进一步，agent skills 作为新兴技术能更强大地助力论文写作，但由于存在一定使用门槛，大部分人还不知道如何上手。我们不想看到这种不平等继续。

## 🎯 我们做了什么

我们调研了 [**MSRA**](https://www.microsoft.com/en-us/research/lab/microsoft-research-asia-zh-cn/)、[**Seed**](https://seed.bytedance.com/zh/)、[**SH AI Lab**](https://www.shlab.org.cn/) 等顶尖研究机构的研究员，以及**北大**、**中科大**、**上交**的硕博同学，将他们日常使用的写作技巧开源出来：

- **📝 Prompt 模板库**（Part I）：13 个覆盖翻译、润色、分析等场景的实战 prompt，每个附有输入/输出示例
- **🤖 Agent Skills**（Part II）：论文写作相关 skills 的配置教程与使用场景速查
- **⚡ 统一 Agent Skill**（Part III，推荐）：将全部 prompt 内嵌进单一 [`skill/SKILL.md`](skill/SKILL.md)，Claude Code / Cursor 自动识别意图路由执行，无需手动复制 prompt
- **🎉 News**：新上线 [**arxiv-translator-skill**](https://github.com/Leey21/arxiv-translator)，从 LaTeX 源码翻译并编译 ArXiv 论文

**不要在 prompt 调试上浪费时间，把精力留给真正的科研。**

---

## 📑 目录 (Table of Contents)

- [Part I: 写作 Prompt 速查](#part-i-写作-prompt-速查)
- [Part II: Agent Skills 配置与速查](#part-ii-agent-skills-配置与速查)
- [Part III: 统一 Agent Skill（推荐）⚡](#part-iii-统一-agent-skill推荐)

---

# Part I: 写作 Prompt 速查

> 💡 **使用方式**：每个任务下方给出了输入/输出示例，帮助你判断是否适用。完整 prompt 见 [`skill/SKILL.md`](skill/SKILL.md) 对应 Template，复制后粘贴到任意大模型对话框即可使用。
>
> 或直接使用 [Part III 的统一 Skill](#part-iii-统一-agent-skill推荐)，无需手动复制。

---

## Template A · 中转英

将中文草稿翻译并润色为英文 LaTeX 学术段落。自动去除 AI 味、避免破折号、输出 Part 1 [LaTeX] + Part 2 [Translation]。

**示例输入**
```
我们提出了一种新的注意力机制，能够在保持计算效率的同时显著提升长序列建模能力。
```

**示例输出（Part 1）**
```latex
We propose a novel attention mechanism that substantially improves long-sequence modeling
while preserving computational efficiency.
```

→ 完整 prompt 见 [`skill/SKILL.md` Template A](skill/SKILL.md)

---

## Template B · 英转中

将英文 LaTeX 片段直译为中文，自动清洗 `\cite{}`、`\ref{}`、数学公式等 LaTeX 命令，保留原文句序便于对照。

**示例输入**
```latex
We propose \textsc{FocusNet}, which leverages a hierarchical attention module \cite{vaswani2017} to capture multi-scale dependencies.
```

**示例输出**
```
我们提出 FocusNet，其利用层级注意力模块来捕获多尺度依赖关系。
```

→ 完整 prompt 见 [`skill/SKILL.md` Template B](skill/SKILL.md)

---

## Template C · 中转中（Word 场景）

将口语化中文草稿重构为正式学术段落，适配 Word 纯文本输出（无 Markdown 符号）。

**示例输入**
```
我们的方法主要有三个优点，第一个是速度快，第二个是效果好，第三是容易扩展到别的任务上去。
```

**示例输出（Part 1）**
```
所提方法在三个维度上表现出显著优势：推理效率较基线方法明显提升，性能指标达到当前最优水平，
且具备良好的跨任务迁移能力，可无缝适配多种下游场景。
```

→ 完整 prompt 见 [`skill/SKILL.md` Template C](skill/SKILL.md)

---

## Template D · 缩写

微幅压缩英文 LaTeX 段落（减少约 5–15 词），保留全部技术细节，输出 LaTeX + 修改日志。

**示例**
```
# Before
In order to reduce the computational overhead associated with the attention mechanism,
we adopt a sparse attention strategy that selectively attends to a subset of tokens.

# After
To reduce attention overhead, we adopt a sparse strategy that selectively attends
to a token subset.
```

→ 完整 prompt 见 [`skill/SKILL.md` Template D](skill/SKILL.md)

---

## Template E · 扩写

微幅扩充英文 LaTeX 段落（增加约 5–15 词），显式化隐含逻辑，不注水，输出 LaTeX + 修改日志。

**示例**
```
# Before
This design reduces memory usage.

# After
This design reduces memory usage by avoiding redundant key-value storage,
which is particularly beneficial for long-context inference.
```

→ 完整 prompt 见 [`skill/SKILL.md` Template E](skill/SKILL.md)

---

## Template F · 表达润色（英文 LaTeX）

深度润色英文 LaTeX，修正 Chinglish、冠词错误、句式生硬等问题，达到顶会投稿水准。输出 LaTeX + 中文直译 + 修改日志。

**示例**
```
# Before
The performance of our method is better than the baselines in all the experiments.

# After
The proposed method consistently outperforms all baselines across experiments.
```

→ 完整 prompt 见 [`skill/SKILL.md` Template F](skill/SKILL.md)

---

## Template G · 去 AI 味（英文 LaTeX）

识别并替换 AI 高频词（leverage, delve into, pivotal, underscore…），去除机械连接词与列表结构，还原自然学术语感。

**高频替换词参考**

> leverage → use · delve into → investigate · pivotal → key · underscore → emphasize · unveil → show · bolster → strengthen · endeavor → try · elucidate → explain

**示例**
```
# Before
We leverage a novel framework to delve into the pivotal factors that underscore model robustness.

# After
We use a novel framework to investigate the key factors that affect model robustness.
```

→ 完整 prompt 见 [`skill/SKILL.md` Template G](skill/SKILL.md)

---

## Template H · 去 AI 味（中文 Word）

去除"毋庸置疑""范式转移""颠覆性"等空洞渲染词，消除英式长定语与"被"字句，输出可直接粘贴入 Word 的纯文本。

**示例**
```
# Before
毋庸置疑，本文提出的方法在多个维度上展现了令人惊叹的颠覆性能力。

# After
实验结果表明，所提方法在多个评测维度上取得了显著性能提升。
```

→ 完整 prompt 见 [`skill/SKILL.md` Template H](skill/SKILL.md)

---

## Template I · 逻辑检查

高容忍度终稿审查，仅报告逻辑矛盾、术语不一致、严重 Chinglish，风格偏好一律忽略。

**输出示例**
```
[检测通过，无实质性问题]
```
或
```
第 2 段将 "feature extractor" 与 "encoder" 混用且无说明，建议统一术语。
```

→ 完整 prompt 见 [`skill/SKILL.md` Template I](skill/SKILL.md)

---

## Template J · 生成图的 Caption

将中文描述转化为符合顶会规范的英文图标题（自动判断 Title Case / Sentence case，去掉冗余开头）。

**示例**
```
输入：展示我们方法在三个数据集上的性能对比
输出：Performance Comparison of the Proposed Method on Three Benchmarks
```

→ 完整 prompt 见 [`skill/SKILL.md` Template J](skill/SKILL.md)

---

## Template K · 生成表的 Caption

同上，针对表格优化，优先使用 Comparison with / Ablation study on / Results on 等标准句式。

**示例**
```
输入：消融实验，验证各模块的贡献
输出：Ablation Study on the Contribution of Each Component
```

→ 完整 prompt 见 [`skill/SKILL.md` Template K](skill/SKILL.md)

---

## Template L · 实验分析

输入实验数据表格（CSV/Excel），输出 `\paragraph{核心结论} + 分析文本` 格式的 LaTeX 段落，禁止编造数据。

**示例输出**
```latex
\paragraph{Superiority over Baselines.}
Our method achieves 84.3\% on benchmark X, outperforming the strongest baseline by 2.1\%,
while reducing inference time by 18\%.
```

→ 完整 prompt 见 [`skill/SKILL.md` Template L](skill/SKILL.md)

---

## Template M · Reviewer 视角审稿

上传 PDF，指定目标会议，输出 Summary / Strengths / Weaknesses / Rating + 针对作者的改稿建议。

**示例输出片段**
```
Rating: 6/10
主要问题：缺少在 COCO 数据集上的对比实验，无法验证方法的泛化性声明。
可救性：可在修订期补充；若补充后指标持平基线，需调整贡献表述。
```

→ 完整 prompt 见 [`skill/SKILL.md` Template M](skill/SKILL.md)

---

# Part II: Agent Skills 配置与速查

> 🎯 **适用对象**：Cursor、Claude Code 等 AI coding 工具用户
>
> 如果只想用统一 skill 而不关心底层配置，直接跳到 [Part III](#part-iii-统一-agent-skill推荐)。

## 配置方式（OpenSkills）

```bash
# 安装 OpenSkills
npm i -g openskills

# 安装 research 相关 skills
npx openskills install zechenzhangAGI/AI-research-SKILLs

# 安装 Anthropic 官方 skills
npx openskills install anthropics/skills

# 安装本 repo 的统一 skill
npx openskills install MengMengLi18/awesome-ai-research-writing
```

参考：[Cursor Agent Skills 文档](https://cursor.com/docs/context/skills) · [OpenSkills](https://github.com/numman-ali/openskills)

## Skills 速查表

| Skill | 来源 | 核心用途 |
| --- | --- | --- |
| **20-ml-paper-writing** | [zechenzhangAGI/AI-research-SKILLs](https://github.com/zechenzhangAGI/AI-research-SKILLs) | 从 repo 起稿 → 会议模板 → 引用核实 → checklist → 格式迁移；含 booktabs 表格 / 图规范 |
| **humanizer** | [blader/humanizer](https://github.com/blader/humanizer) | 去 AI 写作痕迹，注入自然语感（节奏变化、承认不确定性、减少堆砌） |
| **docx** | [anthropics/skills](https://github.com/anthropics/skills) | 创建/编辑 .docx，支持 Word 模板填充、带修订痕迹的 redlining |
| **doc-coauthoring** | [anthropics/skills](https://github.com/anthropics/skills) | 分阶段协作写作：收集上下文 → 按节起草 → 读者测试 |
| **canvas-design** | [anthropics/skills](https://github.com/anthropics/skills) | 生成论文架构图 / 示意图，输出 .pdf / .png |
| **ai-research-writing** | 本 repo | 统一路由全部 13 个写作 prompt，自动检测意图/格式/语言 |

![Skills 配置与触发示意](images/example.png)

---

# Part III: 统一 Agent Skill（推荐）⚡

> 将 Part I 全部 13 个 prompt 内嵌进单一 `skill/SKILL.md`，agent 自动识别意图路由执行——无需手动复制 prompt，无需区分 LaTeX/Word 版本，支持多步骤 pipeline。

## 安装

```bash
git clone https://github.com/MengMengLi18/awesome-ai-research-writing
cd awesome-ai-research-writing
mkdir -p .claude/skills/ai-research-writing
cp skill/SKILL.md .claude/skills/ai-research-writing/SKILL.md
```

或一键安装：

```bash
npx openskills install MengMengLi18/awesome-ai-research-writing
```

## 使用：直接说需求即可

| 说这句话 | 自动触发 |
| --- | --- |
| 「帮我把这段中文翻成英文 LaTeX」 | Template A · CN→EN |
| 「把这段 LaTeX 翻译成中文」 | Template B · EN→CN |
| 「这段中文帮我改成论文格式」 | Template C · CN→CN |
| 「这段太长了缩短一点」 | Template D · Shorten |
| 「字数不够帮我扩写」 | Template E · Expand |
| 「润色这段英文 LaTeX」 | Template F · Polish EN |
| 「去一下 AI 味」（LaTeX） | Template G · De-AI EN |
| 「去一下 AI 味」（中文） | Template H · De-AI CN |
| 「逻辑检查一下」 | Template I · Logic Check |
| 「帮我生成图的 caption」 | Template J · Figure Caption |
| 「帮我生成表的 caption」 | Template K · Table Caption |
| 「帮我分析这组实验数据」 | Template L · Experiment Analysis |
| 「以 Reviewer 视角审一下这篇论文」 | Template M · Reviewer Critique |
| 「翻译完再去一下 AI 味」 | 自动 Chain A → G |

完整 prompt 内容与设计说明见 [`skill/SKILL.md`](skill/SKILL.md)。

---

[![Star History Chart](https://api.star-history.com/svg?repos=MengMengLi18/awesome-ai-research-writing&type=Date)](https://star-history.com/#MengMengLi18/awesome-ai-research-writing&Date)
