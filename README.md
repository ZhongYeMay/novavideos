# NOVA Videos

这个仓库是 `ZhongYeMay/test_web` 的公开视频源。`videos.json` 是 NOVA VIDEO 的正式视频清单，网站会根据每个视频的真实 `tags` 自动生成分区。

## 🎬 公开投稿

**任何 GitHub 用户都可以投稿视频，不需要获得本仓库写权限。**

最简单的方式：

1. 先把视频上传到你自己控制的公开 HTTPS 地址；推荐使用你自己的 GitHub Release asset。
2. 打开本仓库 **Issues → 视频投稿**。
3. 填写视频标题、直链、真实 tags、封面、时长和简介。
4. 提交后等待审核。
5. 审核通过后，维护者会把它加入 `videos.json`，网站会自动显示并按 tags 分区。

投稿表单：

`https://github.com/ZhongYeMay/novavideos/issues/new?template=video_submission.yml`

完整规则见 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

> 为什么不直接让所有人创建本仓库 Release？GitHub 的 Release 管理需要仓库写权限。把写权限公开给陌生人会允许其修改/删除仓库内容，因此 NOVA Videos 使用“公开投稿 + 审核”的方式。

## 维护者添加视频

大视频推荐使用 GitHub Release；小型测试资源也可以直接放在仓库中。

```text
novavideos/
├─ videos.json
├─ videos/
│  └─ ...
└─ thumbnails/
   └─ ...
```

示例：

```json
{
  "id": "example",
  "title": "示例视频",
  "channel": "NOVA Studio",
  "category": "生活",
  "tags": ["生活", "摄影"],
  "src": "https://github.com/example/repo/releases/download/v1/example.mp4",
  "thumbnail": "https://example.com/example.webp",
  "duration": "03:20",
  "description": "视频简介",
  "published": "2026-08-14"
}
```

`src` 和 `thumbnail` 可以使用仓库内相对路径，NOVA VIDEO 会自动拼接到本仓库 Raw GitHub 地址；也可以填写完整 `https://` URL。

### 关于互动数据

播放量、点赞、收藏、评论和观看进度目前属于 NOVA VIDEO 浏览器本地数据，不应在投稿时伪造或写入静态清单冒充全站数据。

> 这个方案适合个人测试站和小规模公开视频项目。GitHub 仓库 / Releases 并不是专业视频 CDN，大规模流量场景应迁移到专用对象存储或视频分发服务。
