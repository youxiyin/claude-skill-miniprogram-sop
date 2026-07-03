# HTML 原型外壳用法

`_mobile-frame.html` = P1 原型的统一底座（手机边框 375×812 + 设计令牌 + 常用可映射组件）。

## 出一个页面
1. 复制 `_mobile-frame.html` → `prototype/<页面名>.html`。
2. 改：`<title>`、`.navbar` 标题、`.screen` 里的内容、`.tabbar` 的 `active` 高亮。
3. 关键状态各出一版：正常 / 空态（用 `.empty` 块）/ 异常 / 满载。
4. 适老化类：给 `<html>` 加 `class="a11y-large"` 出一版大字号。
5. 页面间跳转：`<a href="其它页.html">` 让用户能走一遍。

## 改主题
只动 `:root` 里的设计令牌（主色/底色/字号/圆角/触控盒）。**全站一致靠这里，别在各页硬写颜色。**

## 保真铁律（决定 P2 转 wxml 会不会走样）
- ✅ 只用能映射 wxml 的结构：`view`(div) / `text`(span) / `image`(img) / `scroll-view`(.screen) / `button`(.btn) / `input`。
- ❌ 别用：canvas 特效、复杂 keyframe 动画、grid 高级布局、position 绝对定位堆叠——wxml 做不出或很别扭。
- 触控盒 ≥ `--tap-min`（适老化下限 44/52px），别出比这更小的可点区域。

## 冻结基线
人闸②确认后，`prototype/` 整套 HTML **保留不删**——P2 要拿它做"实现 vs 原型"的视觉保真回归比对基准。
