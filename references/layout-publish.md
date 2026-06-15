# 排版与公众号草稿箱发布

## 自动排版目标

生成适合微信公众号复制或上传的内容：

- 短段落：每段 1-3 句。
- 强重点：核心句加粗或独立成引用块。
- 小标题：每 500-800 字一个。
- 图片位：头图、正文信息图、清单图、结尾系列图。
- 结尾：行动建议、系列预告、来源备注。
- 面向 30+ 高知用户时，排版要克制精致：留白充足、颜色少、字号层级清晰、卡片少而准，避免廉价渐变、夸张按钮和密集大字报。
- 转化型文章末尾使用“私信关键词”服务卡，但不要展示第三方工作备注、事实备注或内部校核痕迹。

默认交付：

1. `index.html` 本地预览页。
2. `article.html` 公众号正文 HTML 片段。
3. `assets/` 图片。
4. `draft_payload.json`，用于草稿箱接口。

## 公众号 HTML 注意事项

- 尽量使用内联样式或简单标签：`p`、`strong`、`section`、`img`。
- 不依赖外部 CSS、JS、字体或远程图片。
- 图片宽度使用 `width:100%;height:auto;display:block;`。
- 段落行高建议 1.75-1.9，字号 15-17px。
- 引用块和重点句用背景色/左边框实现，避免复杂布局。
- 正式推送前在公众号后台预览，因为微信会清洗部分 HTML/CSS。
- 精致版正文可使用：淡色导语卡、章节编号、细线分割、服务咨询卡、局部小表格。不要堆太多卡片。

## 草稿箱推送前置条件

只有满足以下条件才自动推送：

- 已提供或环境变量中存在公众号 `APPID` 和 `APPSECRET`。
- 账号具备对应接口权限，服务器 IP 白名单已配置。
- 封面图和正文图已经生成并可上传。
- 用户确认要“推送到草稿箱”，不是只要预览。

缺任一条件时，输出本地预览链接和待补字段，不声称已推送。

## 微信公众号接口流程

运行前必须核对官方文档的当前字段和限制。

常见流程：

1. 获取 access_token：
   `GET https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET`
2. 上传正文图片：
   `POST https://api.weixin.qq.com/cgi-bin/media/uploadimg?access_token=ACCESS_TOKEN`
   返回正文图片 URL，用于文章 `content` 内的 `img src`。
3. 上传封面永久素材：
   `POST https://api.weixin.qq.com/cgi-bin/material/add_material?access_token=ACCESS_TOKEN&type=thumb`
   返回 `thumb_media_id`。
4. 新增草稿：
   `POST https://api.weixin.qq.com/cgi-bin/draft/add?access_token=ACCESS_TOKEN`
   JSON 通常包含 `articles` 数组。

常用文章字段：

- `title`
- `author`
- `digest`
- `content`
- `content_source_url`
- `thumb_media_id`
- `need_open_comment`
- `only_fans_can_comment`

字段可能随平台变更；以运行时官方文档和接口返回为准。

## 发布失败处理

- token 错误：检查 AppID、AppSecret、IP 白名单、接口权限。
- 图片上传失败：检查格式、大小、文件路径、素材接口类型。
- 草稿创建失败：检查 `thumb_media_id`、标题长度、正文 HTML、图片 URL。
- HTML 样式丢失：生成更保守的 inline HTML。

失败时输出：接口、状态码、错误码、错误信息、下一步修复建议。

## 安全要求

- 不把 AppSecret 写入文章、HTML、日志或最终回复。
- 不把 access_token 暴露给用户可分享的预览页。
- 推送前确认公众号主体和草稿标题，避免发错账号。
