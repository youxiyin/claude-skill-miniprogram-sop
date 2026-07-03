---
name: miniprogram-sop
description: >
  从一段话到可上线的小程序标准化制作流水线（微信小程序）。5 阶段 + 5 道人闸：
  需求澄清→HTML 原型确认方向→脚手架→自动迭代循环长跑→真机部署上线；
  除"人必须判断"的 5 类闸门外，每一阶段由 agent 自动做到位。

  Use when the user wants to BUILD A NEW mini-program from a one-paragraph idea/description
  ("做个小程序""帮我做一个…小程序""写个小程序原型""从零做小程序")，or wants an HTML
  prototype of an app to confirm direction before coding. 不适用于给已存在项目改 bug（那走普通开发）。
metadata:
  full_spec: SOP-full.md（完整正文）；套件在本目录 phases/ templates/ redline-library/ prototype-shell/
---

# 小程序制作 SOP（可执行 skill）

**一句话**：用户给一段话 → 你先出 **HTML 原型**让他确认方向 → 确认后脚手架成真小程序 → 交给**自动迭代循环**长跑 → 只把不可替代的判断打包递给他，其余全自动。

**三条铁原则（贯穿全程）**
1. 把每类缺陷推到**最便宜的阶段**修：方向→P1(HTML)、逻辑数据→P3(循环)、真机部署→P4(上线)。
2. **领域知识 agent 起草、人只审批**（用 `templates/` 填，人在闸做判断题，不做填空题）。
3. **人闸=判断不是劳动**：每道闸把选项/建议默认/对比材料/点击清单备齐，人只点选/点头/拍照。

---

## 流程：5 阶段 + 5 人闸（按序推进）

> 每个阶段**先读对应 `phases/*.md` 再执行**（那里是完整指令）。本 SKILL.md 只是路由与总纲。

### P0 · 需求澄清 — 读 `phases/P0-需求澄清.md`
- 从用户那段话：判品类 → 套 `redline-library/<品类>.md`+`_generic.md` → 抽规格/页面/闭环。
- 用 `templates/` 起草三份领域资产到项目根：`spec-checklist.md` / `risk-register.md` / `user-journeys.md`。
- 只在关键信息缺失且无法安全默认时，打包问 2–3 个澄清题（品类必问项见 P0 文件）。
- **人闸①**：有澄清题就问，否则带"标注了假设的默认"直接进 P1。

### P1 · HTML 原型 — 读 `phases/P1-HTML原型.md`（★最关键的确认）
- 每页出静态 HTML，套 `prototype-shell/_mobile-frame.html`（手机边框+设计令牌，只用**可映射 wxml** 的结构）。
- 空/正常/满/异常各出一版；适老化类加大字号版；页面间可点跳转让用户能"走一遍"。
- 推给用户看（浏览器打开 / 经飞书·微信桥推文件或截图）。
- **人闸②（核心）**：反复改到用户说**"就是这个感觉"** → 冻结这套页面结构+视觉基调为基线（`prototype/` 留档 + 写 `prototype/BASELINE.md`）。

### P2 · 脚手架+骨架 — 读 `phases/P2-脚手架骨架.md`（全自动）
- 确认的 HTML → 真小程序（wxml/wxss/js）+ 数据层 + 云函数骨架（**从第一天带 config.json**：权限/触发器/env 占位，不留部署缺口）。
- 接入循环基建（从成熟 `automation/` 复制骨架，见下"P3 引擎来源"）+ 门禁审计脚本。
- **视觉保真锁**：实现页对比 `prototype/` 基线，关键差值降维成可断言差值，锁住"确认的样子"。
- `npm test` 全绿 + 先跑 1–2 轮 discovery 验资产真能抓 bug。
- **人闸③**：骨架验收，默认略过（不立住则自愈重来）。

### P3 · 自动迭代循环（= 通用循环全套，长期无人值守）
- 发现→对抗校验→修→锁测试→门禁全绿单条提交→judge 判分→分层收敛；discovery/polish/converging 模式机。
- 遵守**12 条铁律**（见下）。
- **人闸④**：遇产品取舍/主观 UI/文案 → 不自己拍板，追加 `human_decisions_needed`，打包+低风险预填默认递用户。

### P4 · 真机·部署·上线（agent 备清单，人执行）
- 自动生成：真机手测清单（改动页→点哪几下）、云函数部署清单、平台提审材料（隐私指引+内容安全）。
- **人闸⑤**：真机点一遍 / 部署云函数 / 微信后台提审——机器物理碰不到，只能清单化怼到人面前。

---

## 12 条铁律（P2/P3 绝对遵守）
1. 门禁全绿才算完成，红的不许提交。2. 测试不许骗绿，每修配一条**引出处**的锁测试（锁意图非碰巧行为）。3. 弱 finding 先对抗校验再改。4. 每轮从干净绿基线起、每修单独绿灯提交。5. 不替人做决策（产品/UI/文案/真机/密钥→human_decisions_needed）。6. 只改项目内文件；**禁改循环自身**；永不 push/部署。7. backlog 分层 P0>P1>P2>P3，P0 凌驾一切。8. **跨端复制的逻辑必配漂移测试**。9. **部署配置完整性**（openapi 权限/定时触发器/密钥占位进门禁审计）。10. **"代码有"≠"用户能用"**（端到端可达+符合意图才算完成）。11. **双向目标禁单向收紧**（堵漏侧必配反向断言+蜕变/属性不变量，防越修越坏）。12. **真实输入语料护栏**（OCR/识别类：合成占位=未验证不许收敛，硬锁≥1真实样本，缺真实格式当债催人补）。

## 只有人必须做的 5 类（其余全自动，别把能自动的甩给人）
① 方向对不对（P1）｜② 产品/业务取舍（P3）｜③ 真机验证（P4）｜④ 真实数据/语料（贯穿，铁律#12）｜⑤ 部署/平台提审（P4）。
> 完整"人做 vs 全自动"诚实清单见 `SOP-full.md` §5。**agent 不能替用户上线，但能把到上线之间每一步做到人闸前一步，且从不拿"我这边绿"糊弄人。**

---

## P3 引擎来源（脚手架时怎么装上循环）
本 skill 不含循环运行时代码；P2 装循环基建时，从**成熟项目**复制 `automation/` 骨架再改路径/云函数名：
参照一个成熟项目的 `automation/` 骨架（round-prompt.md 13步+12铁律 / loop-state.json / supervisor·watchdog·enable·disable / notify / decision-digest）与门禁审计脚本（deploy-config / behavior-lock-citation / realdevice-checklist / e2e-flow / fixture-authenticity）。领域知识（risk-register/spec-checklist/user-journeys）用 P0 产出的那三份。

## 复利
做完一个新品类项目，把新踩的红线**补回 `redline-library/<品类>.md`**——做的项目越多，P0 起草越准。同步改 companion kit 与飞书副本。
