# GitHub Pages 与腾讯云 COS

每次推送 `main` 分支，GitHub Actions 会自动构建并发布网站到 GitHub Pages。首次使用时，请在仓库 **Settings → Pages → Build and deployment** 中将 Source 设为 **GitHub Actions**。

网站地址为：`https://zyasdfghjkl123456789.github.io/zhouyaodexiaomimi/`

## 上传视频

1. 打开网站右下角的齿轮图标。
2. 输入腾讯云 COS 的 `SecretId` 和 `SecretKey`，点击保存授权。
3. 上传首页背景视频，或在“添加项目”中上传项目封面；上传完成后内容清单会同步到 COS。
4. 访客刷新网站后可以看到新增内容；项目视频会以播放器形式打开并可点击播放。

密钥仅保存在当前浏览器的 localStorage 中，不会提交到 GitHub。请使用只允许该存储桶写入的腾讯云子账号密钥。

## COS CORS

在 COS 控制台为桶 `zhouyaoxiaomimi-1508436871`（广州，`ap-guangzhou`）添加 CORS 规则：

- Origin：`https://zyasdfghjkl123456789.github.io`
- Methods：`GET, PUT, HEAD, POST`
- Allowed Headers：`*`
- Expose Headers：`ETag`、`Content-Length`、`x-cos-request-id`
- Max-Age：`600`

网站后台只能使用权限限制到该存储桶的子账号密钥，不能使用腾讯云主账号永久密钥。更安全的正式方案是由服务端签发 STS 临时密钥。
