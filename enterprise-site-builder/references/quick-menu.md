# 悬浮快捷菜单（热门组合与配置规范）

> 用途：Step 5/6 给页面加常驻快捷入口时查阅。国内 B2B 默认竖排图标条，出海站换 WhatsApp/邮件组合。

## 热门组合（按优先级）

| 项 | 类型 | 说明 | 默认 |
|---|---|---|---|
| 电话咨询 | tel 一键拨打 | 桌面/手机都最直接，手机端唤起拨号 | 开 |
| 微信/企业微信 | 弹二维码面板 | 不点直达，点开弹二维码卡片 | 开 |
| 获取报价/在线留言 | 锚点跳到询盘区 | 与主 CTA 一致，不另起表单 | 开 |
| 返回顶部 | 滚动 >400px 出现 | 独立小按钮，平滑回顶 | 开 |
| 邮件联系 | mailto | 商务/出海常用 | 按需 |
| 在线客服 | 接入客服系统 | 有客服系统再开，不做空壳 | 按需 |
| QQ / 抖音 / 视频号 | 二维码面板 | 国内私域导流 | 按需 |
| WhatsApp / Messenger | 直链 | 仅出海站 | 出海开 |

单条菜单总数建议 ≤5 个，过多反而降低点击。

## 位置惯例

- **桌面右中竖排**（right-middle）：国内 B2B 最常见，视线自然落点，不占正文。
- **右下**（right-bottom）：FAB/返回顶部/单主行动按钮惯例，离右手拇指近。
- **左中/左下**：右侧已被在线客服插件占用、或设计对称需要时使用。
- **手机端**：默认右下拇指区；若配置为"中"，自动下沉到底部附近，避免遮挡首屏主按钮；按钮 ≥44px，留 `env(safe-area-inset-bottom)` 安全区。
- 与滚动条、cookie 条、底部导航保持 16-24px 间隙，不遮挡主 CTA。

## 配置项（页面内 QM_CONFIG）

```js
const QM_CONFIG = {
  enabled: true,                 // 总开关：false 整条隐藏
  position: 'right-middle',       // right-middle | right-bottom | left-middle | left-bottom
  backTop: true,                 // 返回顶部
  items: [
    {show:true, kind:'tel',    icon:'📞', label:'电话咨询', value:'tel:电话'},
    {show:true, kind:'wechat', icon:'💬', label:'微信咨询', qr:'二维码图'},
    {show:true, kind:'anchor', icon:'📝', label:'获取报价', target:'#contact'},
    {show:false,kind:'mailto', icon:'✉️', label:'邮件', value:'mailto:邮箱'},
  ]
};
```

## 禁忌

- 不自动弹出客服窗轰炸；二维码点开才展开。
- 不遮挡主 CTA、表单提交按钮和底部导航。
- 不用高饱和大面积色块，与站点 60-30-10 配色一致，强调色只用于 hover。
- 电话/微信/二维码未拿到真实素材时自动匹配示例值（电话 0755-XXXX XXXX、微信号文本），交付说明声明可替换；不编造可拨通的他人号码。
