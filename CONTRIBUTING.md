# 向 NOVA Videos 投稿

NOVA Videos 接受公开投稿，但不会把仓库写权限直接开放给陌生贡献者。这样可以避免现有视频、Release 和 `videos.json` 被误删或恶意修改。

## 最简单：使用「视频投稿」表单

1. 登录 GitHub。
2. 先把视频放到你自己控制的公开 HTTPS 地址。推荐做法是：在你自己的 GitHub 仓库中创建 Release，并把 MP4 / WebM 作为 Release asset 上传。
3. 打开本仓库的 Issues，选择 **视频投稿**。
4. 填写标题、视频直链、真实 tags、封面、时长和简介。
5. 提交后等待维护者审核。
6. 审核通过后，小时级扫描任务会自动把视频加入本仓库的 `videos.json`，NOVA VIDEO 随后按 `tags` 将它加入对应分区。

> GitHub 只有对仓库有写权限的人才能在这个仓库里直接创建 Release。因此普通投稿者应使用自己的 Release/公开 HTTPS 视频地址，而不是要求获得本仓库写权限。

## 审核与自动入库

只有仓库维护者 **ZhongYeMay** 可以批准普通 Issue 投稿。

维护者确认投稿信息无误后，在对应的 `[视频投稿]` Issue 中单独回复：

```text
/approve
```

每小时扫描任务会检查这个指令。只有当 `/approve` 评论的作者是 `ZhongYeMay` 时，才会继续自动入库；其他用户发送同样的文字会被忽略。

自动入库前会再次检查：

- 投稿 Issue 使用 `[视频投稿]` 标题前缀。
- 三项投稿确认均已勾选。
- 视频地址是公开的 `https://` URL。
- `tags` 非空，并按投稿者实际填写值写入，不猜测额外分区。
- 封面若填写，也必须是 `https://` URL。
- 时长只采用投稿者明确填写的数据，并将中文/全角冒号规范化；未填写则允许网站播放时读取媒体元数据。
- `videos.json` 中不存在相同 `src` 的视频，防止重复入库。
- 不会从 Release `download_count`、文件名或标题推断播放量、点赞等互动数据。

审核成功后，自动任务会使用稳定 ID `submission-<Issue编号>` 写入 `videos.json`，记录投稿者和原始 Issue 地址，并在 Issue 中回写入库结果后关闭该 Issue。

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

投稿需要人工审核。明显侵权、恶意文件、故意泄露他人隐私、无法公开访问或与填写信息明显不符的投稿不会进入正式清单。
