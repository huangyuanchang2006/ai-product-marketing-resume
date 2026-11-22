# AGENTS.md

网页版求职简历（AI 产品市场活动实习 · 日本市场）。单文件静态 HTML，无 JS、无构建、无依赖。

## 改哪里

| 路径 | 角色 | 可动 |
| --- | --- | --- |
| `notes/resume-review/黄元畅 AI产品活动Resume.html` | **唯一工作对象**。163 行，内联 CSS | ✅ |
| `notes/resume-review/copy-review.md` | 58 条文案台账，是文案的单一事实来源 | ✅ 必须同步 |
| `notes/resume-review/README.md` | 版式规格与口径依据 | ✅ 查规格 |
| `notes/resume-review/1280.png` / `390.png` | 对照截图 | ✅ 改完刷新 |
| `output/pdf/黄元畅-AI产品市场活动简历.pdf` | 网页同源导出的 A4 PDF | ✅ 网页定稿后刷新 |
| `index.html`（根目录） | 旧的 20 分钟快版 | ❌ 已废弃 |
| `PRODUCT.md` | 长期个人站愿景（双语、策展、Obsidian） | ❌ 与本次求职简历无关 |
| `design.md` / `arc/` / `reference/` | 旧设计记录 / 架构备忘 / 只读素材 | ❌ 只读 |

`reference/` 由自身的 `.gitignore` 排除，不入库，共 21 MB。

## 硬边界（已定过，不要重新讨论）

1. **网页是主交付，PDF 是同一 HTML 的导出版。** 不用纸质简历的字号/一页/禁动效规则反向限制网页；PDF 用独立打印样式保证图片和超链接有效。
2. **三块内容已砍掉，不回归**：拟拓展日本社群、CSSA 外联（熊猫外卖洽谈 / 日興総業提案）、日语授课（给大阪日本高中生上课）。
3. **不编造外部证明。** 没有来源的数字、头衔、用户量一律不写。

## 文案规范

1. STAR 结构，写结果不写形容词。
2. **加粗只给名词短语**，普通动词不加粗。
3. 数字优先于定性描述（`18 期` `6 条` `+435.6%` 是视觉锚点）。
4. 去掉无据的强度词（「活跃」「经常」「大量」）——面试一追问就露底。
5. 中英混排：品牌名与专有名词保留原文；标点用中文全角，除非整段是英文。

完整版见 `~/.workbuddy-ai/skills/resume-master/SKILL.md`（**只读文案章节**，它的 PDF 脚本与本项目无关，别执行）。

## 强制：改文案必须同步台账

改 HTML 里的任何一句话，同一轮内更新 `copy-review.md` 对应行。
这个项目已经因此偏过两轮（#10、#26 用户批过但没落进 HTML，台账和成品对不上）。**不要重复这个错误。**

## 强制：改版式必须真实截图验收

```bash
cd "notes/resume-review"
node ~/.claude/skills/oil-ui-pro/scripts/shoot.mjs "黄元畅 AI产品活动Resume.html" --size 1280x1400 --full --out /tmp/shots-desk
node ~/.claude/skills/oil-ui-pro/scripts/shoot.mjs "黄元畅 AI产品活动Resume.html" --size 390x1600 --full --out /tmp/shots-mob
```

查单块细节：加 `--selector ".entry" --zoom 2`。

**不要靠读 CSS 判断版式对错。** 这个项目已出现两次「CSS 看起来没问题、实际把中文词切断」：一次桌面折行留孤字「备」，一次 390px 把「发布」拆成「包装与发」/「布准备」。

## 已知坑

1. **HTML 里没有 JS，也没有 side-nav。** 早前「side-nav 结构还在、只是 `display:none`」的说法指的是根目录废弃的 `index.html`，不是这个文件。加侧导航要从零写。
2. **Instagram 的 `+150.2% vs. Oct 21` 是环比**（近 30 天对比上一个 30 天），不是「从接手起涨了 150%」。页面写的是「30 天对比上一周期」，刻意没写「接手后」。若确认接手日期早于 2026-09-21 才可改成更强因果。
3. **`.roles li + li { border-left }` 在 flex-wrap 下有 bug**：桌面折行后第二行开头会多一条孤立竖线。CSS 第 20 行仍是这个写法。
4. **图片全是相对路径**（7 张，都在 `notes/resume-review/`）。任何「复制到临时目录再渲染」的工具链都会裂图。
5. `notes/resume-review/README.md` 第 3 行链到 `preview.html`，该文件已不存在（被改名为 `黄元畅 AI产品活动Resume.html`），待修。
6. `.codex/hooks.json` 与 `.claude/settings.local.json` 指向 `~/.agents/skills/impeccable/scripts/hook.mjs`，**该文件不存在**，所以这两个 hook 目前是空转，不会产生输出也不会阻断。

## 当前状态

文案已收尾并全部落地。**下一步是 layout / 交互**，剩 4 个待定项（小红书数据、RateMyCourse 用户数、「拍摄」措辞、手机端交付量是否恢复并列）。

细节见 `notes/handoff-2026-11-22-to-codex.md`。那份是某一次交接的快照，本文档才是长期约定；两者冲突时以本文档为准。
