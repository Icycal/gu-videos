# gu-videos

产品演示视频独立仓库，供 `Icycal.github.io` 个人主页的作品展示区通过 `raw.githubusercontent.com` 直链动态拉取播放。

## 文件

- `xiaoduwatch.mp4` —— 儿童手表小度助手（DuerOS OneApp）演示

## 用法

主页 `data.js` 中对应作品使用：

```js
media: { kind: "video", src: "https://raw.githubusercontent.com/Icycal/gu-videos/main/xiaoduwatch.mp4" }
```

> 视频文件较大，单独放在此仓库以保持主页主仓库轻量；经由 raw 直链播放，无需开启 GitHub Pages。
