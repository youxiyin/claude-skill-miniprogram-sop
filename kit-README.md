# 小程序制作 SOP · 可执行套件

把 [`../小程序制作标准化SOP-v1.md`](../小程序制作标准化SOP-v1.md) 的 P0–P2 落成"能照着跑"的脚手架。
你给一段话，照下面三步，从**需求 → HTML 原型 → 骨架小程序**跑通，再交给自动迭代循环长跑。

## 怎么用（喂 agent 的顺序）

| 步 | 喂这份 | 你做什么 | 产出 |
|---|---|---|---|
| **P0** | `phases/P0-需求澄清.md` + 你那段话 | 答澄清题（若有） | `spec-checklist.md` / `risk-register.md` / `user-journeys.md`（用 `templates/` 起草）|
| **P1** | `phases/P1-HTML原型.md` | **看效果，反复到"就是这个感觉"** | `prototype/*.html`（套 `prototype-shell/`）|
| **P2** | `phases/P2-脚手架骨架.md` | （可选）扫一眼骨架 | 真小程序骨架 + 循环基建 + 视觉保真锁，门禁全绿 |

之后：`automation/enable.sh` 起循环 → 先跑 1–2 轮 discovery 验资产真能抓 bug → 放手长跑。

## 目录

```
小程序制作SOP/
├── README.md                 ← 本文（runbook）
├── phases/                   ← 三个阶段的"喂给 agent 的指令"
│   ├── P0-需求澄清.md
│   ├── P1-HTML原型.md
│   └── P2-脚手架骨架.md
├── templates/                ← agent 起草领域知识的空模板
│   ├── spec-checklist.template.md
│   ├── risk-register.template.md
│   └── user-journeys.template.md
├── redline-library/          ← 品类红线库（P0 按品类套用，做一个沉淀一个）
│   ├── _generic.md           ← 任何小程序都适用的通用红线
│   ├── 医疗健康.md  ├── 电商批发.md
│   ├── 社交内容.md  ├── 工具效率.md  └── 预约服务.md
└── prototype-shell/          ← HTML 原型外壳（手机边框+设计令牌，保证一致+可映射 wxml）
    ├── _mobile-frame.html
    └── README.md
```

## 三条铁原则（贯穿全程）
1. **把每类缺陷推到最便宜的阶段修**：方向→P1(HTML)、逻辑数据→P3(循环)、真机部署→P4(上线)。
2. **领域知识 agent 起草、人只审批**：`templates/` 由 agent 填，你在人闸做判断题。
3. **人闸=判断不是劳动**：每道闸 agent 已备好选项/默认/清单，你只点选/点头/拍照。

## 五道人闸（只有这五类必须你来，其余全自动）
① 方向对不对（P1）｜② 产品/业务取舍（P3）｜③ 真机验证（P4）｜④ 真实数据·语料（贯穿，铁律#12）｜⑤ 部署·平台提审（P4）。

> 详见 SOP 正文 §5"诚实清单"。**agent 不能替你上线，但能把到上线之间每一步做到人闸前一步，且从不拿"我这边绿"糊弄你。**
