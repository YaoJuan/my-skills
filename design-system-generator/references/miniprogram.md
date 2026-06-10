# WeChat Mini Program — DESIGN.md Reference

## Platform Constraints

| Constraint | Rule |
|-----------|------|
| Units | Use `rpx` for all sizing. Base: 750rpx = screen width on iPhone 6. Common: `32rpx` padding, `28rpx` body text, `32rpx` subheading, `40rpx` heading |
| Fonts | System fonts only — no custom web fonts. Use `-apple-system` / `PingFang SC` / `Helvetica Neue` stack |
| Components | Prefer WeUI components (mp-cells, mp-btn, mp-dialog) over custom — they handle safe areas automatically |
| Safe Area | Always account for iPhone notch/dynamic island top and home indicator bottom. Use `env(safe-area-inset-*)` or WeUI's built-in handling |
| Images | All images via CDN or local assets — no external URLs at runtime |
| Navigation | WeChat provides the top nav bar (title + back button). Custom nav bar only when `navigationStyle: custom` |
| Dark Mode | Support via `@media (prefers-color-scheme: dark)` or `wx.getSystemInfoSync().theme` |
| Touch Targets | Minimum 44×44px (approximately 88×88rpx) for all tappable elements |

---

## DESIGN.md Structure for Mini Program

Use this exact section structure when generating:

```markdown
# DESIGN.md — [Project Name] (微信小程序)

## 1. 项目概览
[一句话描述产品定位和目标用户]

## 2. 视觉风格
- 整体基调: [轻量/商务/活泼/严肃]
- 明暗主题: [仅亮色 / 仅暗色 / 跟随系统]
- 信息密度: [宽松 / 适中 / 紧凑]
- 设计参考: [类似微信、支付宝、京东等产品的哪个方向]

## 3. 色彩系统

| 名称 | rpx变量 / CSS变量 | Hex | 用途 |
|------|-----------------|-----|------|
| 主色 | --color-primary | #XXXXXX | 按钮、链接、激活态 |
| 辅助色 | --color-secondary | #XXXXXX | 标签、角标 |
| 背景色 | --color-bg | #F7F8FA | 页面背景 |
| 卡片背景 | --color-surface | #FFFFFF | 卡片、弹窗 |
| 分割线 | --color-border | #EEEEEE | 列表分割线 |
| 主文字 | --color-text-primary | #333333 | 标题、正文 |
| 次文字 | --color-text-secondary | #999999 | 辅助信息、时间戳 |
| 成功 | --color-success | #07C160 | 成功状态（微信绿） |
| 警告 | --color-warning | #FF9900 | 警告状态 |
| 错误 | --color-error | #FA5151 | 错误、删除 |

暗色模式覆盖:
| 名称 | Hex (暗色) |
|------|-----------|
| 背景色 | #1A1A1A |
| 卡片背景 | #2C2C2C |
| 主文字 | #EFEFEF |

## 4. 字体排版

字体栈: `-apple-system, 'PingFang SC', 'Helvetica Neue', sans-serif`

| 层级 | rpx大小 | 字重 | 行高 | 用途 |
|------|---------|------|------|------|
| 页面标题 | 36rpx | 600 | 1.4 | 导航栏标题 |
| 卡片标题 | 32rpx | 500 | 1.4 | 列表项主标题 |
| 正文 | 28rpx | 400 | 1.6 | 描述文字 |
| 辅助文字 | 24rpx | 400 | 1.5 | 时间、标签、提示 |
| 极小文字 | 20rpx | 400 | 1.4 | 角标、版权 |

## 5. 间距系统

基础单位: 8rpx

| Token | rpx | 用途 |
|-------|-----|------|
| space-xs | 8rpx | 图标与文字间距 |
| space-sm | 16rpx | 行内元素间距 |
| space-md | 24rpx | 卡片内间距 |
| space-lg | 32rpx | 页面水平边距（标准） |
| space-xl | 48rpx | 模块间距 |

页面水平边距: 32rpx（两侧）
列表项高度: 96rpx（单行）/ 120rpx（双行）
底部安全区: 使用 `padding-bottom: env(safe-area-inset-bottom)` 或 WeUI 处理

## 6. 组件规范

### 按钮
- 主按钮: 背景 `--color-primary`，白色文字，圆角 `8rpx`，高度 `88rpx`，全宽或固定宽度
- 次按钮: 边框 `--color-primary`，主色文字，背景透明
- 危险按钮: 背景 `--color-error`，白色文字
- 禁用态: opacity 0.4，不可点击
- 加载态: 显示 loading icon，文字改为"处理中..."

### 卡片
- 背景: `--color-surface`
- 圆角: `16rpx`
- 阴影: `0 2rpx 12rpx rgba(0,0,0,0.06)`
- 内边距: `32rpx`
- 卡片间距: `16rpx`

### 列表 (cells)
- 优先使用 WeUI mp-cells 组件
- 分割线颜色: `--color-border`
- 箭头图标: 使用 WeUI 标准箭头
- 激活态背景: `rgba(0,0,0,0.04)`

### 输入框
- 边框: `1rpx solid --color-border`
- 圆角: `8rpx`
- 高度: `88rpx`（单行）
- 聚焦边框: `--color-primary`
- placeholder颜色: `--color-text-secondary`

### 底部导航 (tabbar)
- 使用微信原生 tabBar 配置（不用自定义组件）
- 图标尺寸: 40×40px（非rpx，在 app.json 中配置）
- 选中色: `--color-primary`
- 未选中色: `#999999`

### 弹窗/Modal
- 优先使用 WeUI mp-dialog
- 遮罩: `rgba(0,0,0,0.5)`
- 圆角: `24rpx`（仅上圆角的底部弹出式）

## 7. 页面布局原则

- 页面容器左右 padding: `32rpx`
- 顶部留出微信导航栏高度（约 88rpx + 状态栏）
- 使用 flex 布局，避免 float
- 长列表使用 `<scroll-view>` 或虚拟列表，不用普通 view 堆叠
- 底部操作栏固定时，需加 `padding-bottom: env(safe-area-inset-bottom) + 自定义间距`

## 8. 注意事项

**Do:**
- 所有尺寸用 rpx，保证多机型适配
- 图片都加 `lazy-load` 属性
- 点击反馈用 `hover-class`
- 空状态页面提供友好提示和操作入口

**Don't:**
- 不用 `px` 单位（除非是边框 `1px` 场景）
- 不使用外部字体文件
- 不在组件内直接操作 DOM（用数据驱动）
- 不写超过 3 层的嵌套选择器

## 9. Agent Prompt Guide

**快速色彩参考:**
- 主色: [PRIMARY_HEX]
- 背景: [BG_HEX]  
- 文字: [TEXT_HEX]

**可直接使用的 Prompt 模板:**

构建新页面:
> "参照 DESIGN.md，用 WXML/WXSS 构建一个[页面名称]页面，使用色彩系统中的 CSS 变量，卡片遵循卡片规范，间距使用 space-* token。"

提取组件:
> "参照 DESIGN.md 的组件规范，封装一个可复用的[组件名]组件，支持 props: [xxx]。"

修复样式一致性:
> "检查这段 WXML/WXSS，找出不符合 DESIGN.md 的地方并修正：使用正确的 rpx 单位、CSS 变量、圆角和间距。"
```

---

## Extraction Tips (for screenshot mode)

When analyzing a Mini Program screenshot:
- Background color dominance → determine light/dark
- Tap the most prominent CTA button color → primary color
- List item height estimation: standard WeUI cell is ~96rpx (48px on 2x screen)
- If you see the standard WeChat nav bar (gray/white with title), it's default nav
- Green buttons → likely `#07C160` WeChat brand green unless clearly different
