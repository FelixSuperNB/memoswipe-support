# 忆扫相册 / MemoSwipe 技术支持网页

用于 App Store Connect「技术支持网址 / Support URL」的静态网页。入口为本目录的 `index.html`，CSS、JavaScript、PNG Logo 和按钮 SVG 图标均已内嵌，无框架、构建工具、外部字体或 CDN。此目录是独立发布包，项目根目录原有的开发 README 保持原样。

页头 Logo 来自项目中的 `忆扫相册LOGO.png`，使用 144 × 144 像素的等比例缩小版本，并以 Base64 内嵌在 HTML 中。电脑显示为 48 × 48 像素，手机显示为 40 × 40 像素；原始图片保持不变，部署时无需额外上传图片文件。

## 本地预览

可以直接用浏览器打开 `index.html`。也可以在本目录运行：

```sh
python3 -m http.server 8080 --bind 127.0.0.1
```

打开 <http://127.0.0.1:8080>，结束预览时按 `Ctrl+C`。此命令只用于本地预览，部署不需要 Python。

## 发布到 GitHub Pages

建议创建独立的公开仓库，例如 `memoswipe-support`，只上传本目录的文件。

1. 在 GitHub 创建仓库 `memoswipe-support`。
2. 将本目录中的 `index.html`、`README.md`、`.nojekyll` 上传到该仓库根目录并提交到 `main`。不要将 `support-site/` 文件夹整体套在仓库根目录外层；发布仓库中应直接出现 `index.html`。
3. 进入仓库 **Settings → Pages**。
4. 在 **Build and deployment → Source** 选择 **Deploy from a branch**。
5. 在 **Branch** 选择 `main`，目录选择 **/ (root)**，点击 **Save**。
6. 等待 GitHub 的 Pages 部署成功，打开 Settings → Pages 显示的 HTTPS 网站地址。可以在仓库 **Actions** 中查看部署状态。

发布后的项目网站地址格式为：

```text
https://你的GitHub用户名.github.io/memoswipe-support/
```

这是地址格式示例，不是已部署链接。以 GitHub Pages 显示的实际地址为准；`main` 也应替换为实际发布分支。如果使用 `用户名.github.io` 同名仓库，网站位于 `https://用户名.github.io/`。

无需安装依赖或提供构建命令；`.nojekyll` 用于跳过 Jekyll 处理。GitHub Pages 的分支发布目录只支持仓库根目录 `/` 或 `/docs`，不能直接在设置里选择此 iOS 仓库的 `/support-site`。上述独立仓库方式不需要调整 iOS 项目。

官方说明：[GitHub Pages 发布来源配置](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

## 填写 App Store Connect

部署成功并检查公网访问后，将网站的 **HTTPS 页面地址**填入 App Store Connect 对应 App 版本本地化信息中的「技术支持网址 / Support URL」。请填写网页地址，不是 GitHub 仓库地址、源码文件地址、`mailto:` 地址或 localhost 预览地址。中英文使用同一地址即可。

提交审核前，用未登录账号的浏览器检查：

- 页面可以直接打开，无需登录；手机、电脑均可阅读。
- 浏览器首选语言为中文时显示简体中文；英文及其他语言回退英文；右上角可以随时切换。
- 两种语言下七个 FAQ 均能展开，关键规则一致。
- 发送邮件按钮打开邮件客户端，收件人为 `felixnb888@163.com`，主题和反馈模板与当前语言一致。只有在邮件客户端主动发送才会发出邮件。未配置邮件客户端时，可复制邮箱到自己的邮件服务使用。
- 复制邮箱按钮可用。优先使用 Clipboard API，失败时尝试传统复制；都不可用时选中邮箱并提示手动复制，辅助技术可读出操作结果。
- 两个飞书链接在未登录状态下均可打开。如果要求登录，请先在飞书中设置对外公开访问。本次工具无法读取这两个飞书页面，尚未确认其匿名访问权限，不能据此认定链接失效。

## 页面内容与维护

- 支持邮箱：`felixnb888@163.com`。
- 隐私政策：<https://my.feishu.cn/wiki/DArVwwzYCiVPxmktoGRcBCYinFc>。
- 使用条款：<https://my.feishu.cn/wiki/SXwDwqcQmiv0yXkeshvcJWlonSe>。
- 免费用户每天可浏览 60 项，照片与视频合并计算；会员无限浏览。
- 月度、年度会员自动续订；永久会员一次性购买，购买永久会员不会自动取消已有订阅。
- 左滑只加入 App 垃圾篓；系统删除前原片仍保留；系统删除后的恢复需前往系统照片 App 的「最近删除」。
- 浏览与整理记录保存在本地，不承诺卸载后恢复；恢复购买不等于恢复浏览记录。

英文正文直接写在 HTML 中；简体中文文案位于脚本的 `chinese` 对象，`data-i18n` 用于对应字段。改动文案时保持两种语言一致。邮件模板位于 `emailTemplates`；更新邮箱时，同时更新页面邮箱链接、显示文字及脚本的 `email` 常量。

首次语言根据浏览器首选语言判断；所有 `zh` 语言标签显示简体中文，其他语言使用英文。语言选择只保留在当前页面内存，不写 Cookie、localStorage 或 sessionStorage。禁用 JavaScript 时，完整英文内容、FAQ、邮件链接和政策链接仍可使用。

页面没有登录、反馈上传表单、统计、追踪、Cookie、网络数据提交或自动信息收集。仅在访问外部链接或主动使用邮件功能时离开本页面。GitHub Pages 与外链服务可能按各自政策处理正常访问日志；页面本身没有加入收集代码。

订阅管理与恢复购买说明参考 [Apple 取消订阅指南](https://support.apple.com/en-us/118428) 和 [Apple 恢复购买指南](https://support.apple.com/en-us/108096)。系统界面名称可能随 iOS 版本变化。

## 已完成的本地检查

- JavaScript 语法有效，49 处正文和 2 处无障碍标签的中英文对应完整。
- 检查中文、繁体中文浏览器标签、英文、法文、日文及缺省语言的初始选择；英文及其他非中文语言使用英文，中文语言标签显示简体中文。
- 浏览器中验证中英文切换、邮件链接及反馈模板、复制成功提示、七个 FAQ 展开。
- 模拟检查 Clipboard API 成功、传统复制回退、复制不可用时的手动复制提示。
- 浏览器中检查 320、390 和 1440 像素宽的页面视口，无内容横向溢出；可见按钮、联系邮箱和 FAQ 点击区域高度不小于 44 像素。
- 禁用 JavaScript 时，英文正文、邮件及政策链接、原生 FAQ 仍可用。
- 主要文字与按钮配色的对比度均超过 WCAG AA 普通文字的 4.5:1；未引用外部脚本、样式或字体，未加入自动信息收集代码。

以上是本地检查，不代表已验证 GitHub Pages 公网部署或飞书页面的匿名访问权限；真机邮件客户端及 VoiceOver 体验可在上线前进一步确认。

本次交付为本地静态文件，尚未创建 GitHub 仓库或执行公网部署。按上述步骤发布后，才能获得可用于 App Store Connect 的正式技术支持网址。
