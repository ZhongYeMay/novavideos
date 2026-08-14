# NOVA Videos

这个仓库作为 `ZhongYeMay/test_web` 的公开视频源。

## 推荐目录

```text
novavideos/
├─ videos.json
├─ videos/
│  ├─ example.mp4
│  └─ ...
└─ thumbnails/
   ├─ example.webp
   └─ ...
```

## 添加视频

1. 将 MP4 / WebM 视频放入 `videos/`。
2. 可选：将封面放入 `thumbnails/`。
3. 在 `videos.json` 的 `videos` 数组中添加一项。

示例：

```json
{
  "id": "example",
  "title": "示例视频",
  "channel": "NOVA Studio",
  "category": "生活",
  "tags": ["生活", "摄影"],
  "src": "videos/example.mp4",
  "thumbnail": "thumbnails/example.webp",
  "duration": "03:20",
  "views": "1,024",
  "published": "刚刚"
}
```

`src` 和 `thumbnail` 可以使用仓库内相对路径；NOVA VIDEO 会自动拼接到本仓库的 Raw GitHub 地址。也可以填写完整的 `https://` URL。

> 这个方案适合个人测试站和小规模演示。GitHub 仓库 / Raw 文件并不是专业视频 CDN，大文件和高并发场景建议以后迁移到对象存储或视频 CDN。
