# 建站简报 Schema（一句话需求 → 结构化简报）

> 用途：Step 1。把用户原话解析为下面的简报；`inferred: true` 表示推断值，方案确认时回显给用户核对。

## 字段定义

```json
{
  "brief_version": "1.0",
  "company": {
    "name": "string，企业全称，未知则标记 auto（落盘时自动匹配行业合理默认值，页面不出现 {{ }}）",
    "industry": "string，对照 taxonomy.md 行业表",
    "business_note": "string，一句话业务/产品说明，来自用户原话",
    "founded_or_scale": "string，可选，未知留空不编造"
  },
  "site": {
    "type": "brand | marketing | overseas | shop | micro",
    "market": "domestic | overseas | bilingual",
    "primary_goal": "lead | brand | sale | info",
    "audience": "string，目标访客：采购商/投资人/求职者/C 端消费者",
    "language": "zh-CN | en | zh+en",
    "nav_menu": ["5 个顶部菜单，不含首页；自动按业务选，各对应一个落地页"]
  },
  "design": {
    "style": "主风格，见 taxonomy.md 风格枚举",
    "style_accent": "点缀风格，可空",
    "brand_color": "string，用户给的 VI 色 HEX，无则空",
    "color_status": "chosen | pending；状态机：无 VI → pending（先出 A/B/C 候选，未展示候选禁止编码）→ 用户选 A/B/C 或给 HEX → chosen",
    "palette_candidates": [
      {"name":"A 稳健商务","primary":"","secondary":"","accent":"","background":"","mood":""}
    ],
    "palette": {"primary": "", "secondary": "", "accent": "", "background": ""},
    "mood": "string，用户口头气质描述，如'稳重、高级、有科技感'"
  },
  "quick_menu": {
    "enabled": true,
    "position": "right-middle | right-bottom | left-middle | left-bottom（待客户确认）",
    "backTop": true,
    "items": [{"id": "call|wechat|quote|email|qr", "show": true, "label": ""}]
  },
  "homepage_modules": [
    {"order": 1, "name": "Hero", "layout": "左文右图", "source": "行业调研/案例库"}
  ],
  "pages": [
    {"file": "products.html", "type": "list", "menu": "产品中心"},
    {"file": "product-detail.html", "type": "detail", "menu": "产品中心"}
  ],
  "content": {
    "products": ["string，已知产品/服务，未知留数组空，落盘时自动匹配行业默认条目"],
    "cases": ["真实案例，无则空，禁止虚构"],
    "qualifications": ["资质荣誉，无则空"],
    "news_or_articles": "boolean，是否需要新闻/资讯栏目",
    "downloads": "boolean，是否需要资料下载"
  },
  "conversion": {
    "cta": "string，主行动：询盘表单/电话/微信/WhatsApp/下载/预约",
    "contact": {"phone": "", "email": "", "address": "", "wechat": ""}（未知留空，落盘时自动匹配示例值并声明可替换）
  },
  "references": ["用户提供的参考网址，进入 gallery-guide.md 收录流程"],
  "deliverable": "static-html | web-app-builder | cms | plan-only",
  "gaps": ["需要用户补充的事实清单"]
}
```

## 默认值规则（不提问，直接采用并标注 inferred）

| 场景 | 默认 |
|---|---|
| 国内 B2B 制造/服务，未说卖货 | `type=marketing, primary_goal=lead, market=domestic, language=zh-CN` |
| 用户提到出口/外贸/海外客户 | `type=overseas, market=overseas, language=en（或双语）` |
| 零售/现货/要在线下单 | `type=shop, primary_goal=sale` |
| 只说"做个门面/介绍下公司"且业务简单 | `type=marketing` 轻量版，或 `micro` |
| 未指定颜色 | **不直接定色，且未展示 A/B/C 候选禁止开始编码**：color_status=pending，派生三套候选列入确认单；选定前中性临时色并标注"配色待选"，不锁定 |
| 未指定风格 | `企业简约扁平` |
| 未指定载体 | `static-html` 响应式单/多页 |

## 必须打断提问的条件（单次 ≤3 问）

1. 目标冲突：用户同时要"纯品牌形象"和"在线直接卖货"，需确认主线。
2. 行业/业务无法从原话判断（如只说"做个网站"）。
3. 给出的参考网站互相矛盾（一个极简高端、一个花哨促销）且用户无倾向。

## 解析输出格式

每次解析后先给用户一段 5-8 行的「我的理解」：公司是做什么的 → 判定类型与理由 → 风格配色 → 主 CTA → 待补充清单（未知信息将自动匹配行业合理默认值，交付时声明清单）；用户纠正后再落盘简报。
