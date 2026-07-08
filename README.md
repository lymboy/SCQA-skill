# scqa-writer

一个Claude Code skill，做中文技术内容的诊断、重写、润色和从零写作。

和市面上的humanizer类工具不一样的地方：它不只在语言层删删改改，而是先修结构，再修论证，最后才磨语言。AI技术文章真正的病根不在词句，在更深的两层——骨架是提纲扩写（节与节没有论证关系），血肉是无本之木（判断后面没有亲手做过才写得出的证据）。只磨皮肤，改完还是AI文。

## 为什么不只是另一个humanizer

现有去AI味方案（humanizer、Humanizer-zh、De-AI等）都停在语言层：删路标词、拆排比、换AI高频词。但有一类文章语言层已经很干净了——有行号、有机制解释——读起来依然是文档不是博客。病在结构（十四节穷尽覆盖、没有取舍）和人称（全文找不到一个"我"）。这种文章humanizer根本治不了，必须动骨架。

## 三层修复

| 层           | 治什么病                         | 用什么药                                             |
| ------------ | -------------------------------- | ---------------------------------------------------- |
| 骨架（结构） | 提纲扩写、无中心判断、抽屉式罗列 | 逆向大纲、一句话判断、SCQA开头、疑问链重排、选题取舍 |
| 血肉（论证） | 判断悬空、因果跳步、类比装饰     | 挣来的具体性、机制解释、算账、代码克制、个人在场     |
| 皮肤（语言） | 路标词、排比、设问自答、翻译腔   | 四源合并痕迹库 + 量化限额                            |

判断任何一段文字该不该改，靠的不是黑名单，是两个问题：这句话是不是只有真做过的人才写得出？这一节在回答读者的哪个问题？答不上来，才是真问题。

## 四种模式

- **诊断**：只出报告，列出Top 5-8个问题，给位置和修法，不动稿
- **重写**：两段式，先给诊断+一句话判断+新骨架，确认后再成稿
- **润色**：只走语言层，直接给成稿
- **从零写**：给素材，先对齐判断、出骨架，再成稿

## 目录结构

```
SCQA-skill/
├── README.md
└── scqa-writer/
    ├── SKILL.md                    # 主流程、灵魂三问、硬门槛、输出约定
    └── references/
        ├── structure.md            # 骨架手术：逆向大纲 / SCQA / 疑问链
        ├── argumentation.md        # 血肉审计：挣来的具体性 / 机制解释 / 个人在场
        ├── ai-traces.md            # 皮肤：四源合并痕迹库 + 作者个人残留模式
        └── exemplars.md            # 正样本拆解 + 病例对照 + 改写示范
```

## 安装

```bash
cp -r scqa-writer ~/.claude/skills/scqa-writer
```

装完之后，在Claude Code里说"优化这篇文章""去AI味""诊断一下这篇"就能触发。

## 输出保证

- 成稿是标准Markdown，不含Obsidian专属语法（callout、wikilink、嵌入、标签），任何平台都能渲染
- 交稿前做乱码检查，`�`和编码损坏字符能修就修，修不了就标注出来问作者，不原样保留
- 中英文之间不加盘古空格（写"Agent引擎"不写"Agent 引擎"），这种空格是一眼可辨的AI排版痕迹
- 重写不磨平锋利判断，黑名单让位于"删掉这个形式，信息还在吗"

## 校准来源

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)，经blader/humanizer、op7418/Humanizer-zh汉化
- [OUBIGFA/De-AI-Prompt-Enhancer](https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL)的中文原生痕迹与量化门槛思路
- [ai-zixun/humanizer-zh](https://github.com/ai-zixun/humanizer-zh)的翻译腔清单
