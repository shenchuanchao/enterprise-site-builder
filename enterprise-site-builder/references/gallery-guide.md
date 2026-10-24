# 参考网站收录与自动分类流程

> 用途：用户投喂优秀网址时（Step 3b），把网站按统一字段收录进案例库，供后续对标。默认用浏览器打开采集，不写爬虫。

## 收录流程

1. **逐个打开**：用浏览器访问用户给的 URL；打不开/需登录/已下线则记录原因并跳过，不编造内容。
2. **截图首屏**：保存首屏截图到案例库同目录 `screenshots/`，文件名用条目 id。
3. **抽取字段**（对照 `assets/gallery.template.json`）：
   - `id`：序号自动递增，如 `ref-001`
   - `url`、`name`（站点/公司名）
   - `industry`：对照 taxonomy.md 行业表归并
   - `site_type`：brand / marketing / overseas / shop / micro
   - `palette`：取首屏主色、辅助色、强调色 HEX（取色器或肉眼估读，标注 `estimated: true`）
   - `style`：对照风格枚举选 1 主 + 1 点缀
   - `layout`：hero / bento / grid / story-scroll / carousel 等
   - `motion`：动效类型与强度（none / micro / heavy）
   - `strengths`：2-3 条可借鉴点（具体到模块，如"首屏三栏能力卡片+右侧固定询价栏"）
   - `avoid`：1-2 条不适配点（如"重动画拖慢加载，B2B 不照搬"）
   - `source_note`：收录日期、来源（用户投喂/公开榜单）
4. **去重**：同 URL 不重复收录；同站多页面只收首页为代表。
5. **追加入库**：把条目追加到案例库 JSON 数组；维护一份按 `industry → site_type → style` 的索引小节，便于 3a 检索。

## 检索匹配（3a）

按简报四维（类型、行业、风格、气质）在库中筛 2-3 条：
- 同行业同类型优先；库内无同行业时放宽到同类型+近风格。
- 每条输出：网址、为什么像、借鉴哪 1-2 个具体模块、哪里不学。
- 禁止整站复制文案与视觉，只借结构与手法。

## 采集注意

- 只采集公开可见内容；不绕过登录、不抓取私有数据。
- 色值为肉眼/工具估读时标 `estimated: true`，不作为客户 VI 依据。
- 案例库文件位置：`assets/gallery.json`（由 `gallery.template.json` 复制填充；模板保留不动）。
