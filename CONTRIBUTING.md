# 向 NOVA Videos 投稿

NOVA Videos 接受公开投稿，但不会把仓库写权限直接开放给陌生贡献者。这样可以避免现有视频、Release 和 `videos.json` 被误删或恶意修改。

## 最简单：使用「视频投稿」表单

1. 登录 GitHub。
2. 先把视频放到你自己控制的公开 HTTPS 地址。推荐做法是：在你自己的 GitHub 仓库中创建 Release，并把 MP4 / WebM 作为 Release asset 上传。
3. 打开本仓库的 Issues，选择 **视频投稿**。
4. 填写标题、视频直链、真实 tags、封面、时长和简介。
5. 提交后等待自动审核。
6. 小时级扫描任务审核通过后会直接把视频加入本仓库的 `videos.json`，NOVA VIDEO 随后按 `tags` 将它加入对应分区。

> GitHub 只有对仓库有写权限的人才能在这个仓库里直接创建 Release。因此普通投稿者应使用自己的 Release/公开 HTTPS 视频地址，而不是要求获得本仓库写权限。

## 自动审核与入库

投稿不再要求维护者手动回复 `/approve`。小时级扫描任务会直接审核所有仍处于打开状态、标题以 `[视频投稿]` 开头的投稿 Issue。

自动入库前会检查：

- 投稿 Issue 使用 `[视频投稿]` 标题前缀。
- 三项投稿确认均已勾选。
- 视频标题、视频直链和 Tags 均非空。
- 视频地址是可验证的公开 `https://` URL；GitHub Release asset 会优先通过 GitHub 元数据确认存在。
- `tags` 只采用投稿者明确填写的值，不猜测额外分区。
- 封面若填写，也必须是公开的 `https://` URL。
- 时长只采用投稿者明确填写的数据，并将中文/全角冒号规范化；未填写则允许网站播放时读取媒体元数据。
- `videos.json` 中不存在相同 `src` 或相同稳定投稿 ID，防止重复入库。
- 不会从 Release `download_count`、文件名或标题推断播放量、点赞、评论等互动数据。

审核成功后，自动任务会使用稳定 ID `submission-<Issue编号>` 写入 `videos.json`，记录投稿者和原始 Issue 地址，并在 Issue 中回复入库 commit 后关闭该 Issue。

如果投稿缺字段、地址无法验证、确认项未勾选、重复或存在明确风险，扫描任务不会入库；在有可修复问题时会留言说明并保持 Issue 打开。

## 进阶：Fork + Pull Request

你也可以 Fork 本仓库，在自己的 Fork 中维护视频资源，然后向本仓库提交 Pull Request 修改 `videos.json`。

请确保：

- `src` 是可公开访问的 HTTPS 视频地址。
- `thumbnail`（如果有）是可公开访问的 HTTPS 图片地址。
- `tags` 必须是真实投稿标签；网站分区直接来自这里。
- 不要伪造播放量、点赞、评论或其他互动数据。
- `id` 应保持唯一且稳定。
- 你拥有视频/封面的版权或获得了公开展示授权。

## 推荐 manifest 项

```json
{
  "id": "your-video-id",
  "title": "视频标题",
  "channel": "频道名",
  "category": "可选兼容字段",
  "tags": ["vlog", "旅行"],
  "src": "https://github.com/you/repo/releases/download/tag/video.mp4",
  "thumbnail": "https://example.com/cover.webp",
  "duration": "12:34",
  "description": "视频简介",
  "published": "2026-08-14"
}
```

## 审核原则

系统只会自动接收资料完整、链接可验证并完成权利确认的投稿。明显侵权、恶意文件、故意泄露他人隐私、无法公开访问或与填写信息明显不符的投稿不会进入正式清单。
