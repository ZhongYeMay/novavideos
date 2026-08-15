# NOVA Videos 投稿审核流程

普通投稿者通过 `.github/ISSUE_TEMPLATE/video_submission.yml` 提交视频，不拥有本仓库写权限。

## 批准一个投稿

确认视频、封面、tags、简介和版权声明没有明显问题后，由仓库维护者 `ZhongYeMay` 在该 `[视频投稿]` Issue 中单独回复：

```text
/approve
```

小时级自动扫描只信任 **作者为 `ZhongYeMay` 的 `/approve` 评论**。投稿者或其他用户自己发送 `/approve` 不会触发入库。

## 自动入库规则

批准后，扫描任务会：

1. 重新读取 Issue 正文和全部评论。
2. 验证三项投稿确认均已勾选。
3. 验证视频地址使用 `https://`；能确认是 GitHub Release asset 时优先读取对应 GitHub 元数据。
4. 只使用投稿表单明确填写的 tags，不从标题、文件名、URL 或 Release tag 猜测。
5. 可选封面必须使用 `https://`。
6. 规范化明确填写的时长（例如 `36：27` → `36:27`）；未填写时不伪造。
7. 检查 `videos.json` 中是否已有相同 `src`。
8. 使用 `submission-<Issue编号>` 作为稳定 ID。
9. 将投稿写入 `videos.json`，保留 `submissionIssue` 和 `submitter` 元数据。
10. 在 Issue 中回复入库 commit，并关闭 Issue。

## 不会自动做的事情

- 不会自动批准任何投稿。
- 不会接受非维护者的 `/approve`。
- 不会把 GitHub Release 的 `download_count` 当作播放量。
- 不会猜测 tags、播放量、点赞量或评论数。
- 无法验证的地址会保持待审核状态，不会勉强入库。

如需拒绝投稿，直接关闭 Issue 即可，不要发送 `/approve`。
