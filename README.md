# gu-videos

个人主页（`icycal.github.io`）**作品集的图片 / 视频图床**。主页仓库只存代码与配置，所有媒体素材集中在这里，**经 GitHub Pages 提供**（不走第三方 CDN）。

## 启用

本仓库开了 **GitHub Pages**：仓库 Settings → Pages → Source 选 `Deploy from a branch` → Branch `main` / `(root)` → Save。
生效后资源通过下面这个域名直出：

```
https://icycal.github.io/gu-videos/
```

> 国内直接访问 `github.io` 比 jsDelivr 稳得多。早期曾用 jsDelivr，但它在国内网络下
> 经常 `ERR_TIMED_OUT`，浏览器里图片 / 视频全部加载不出来，已弃用。

## 目录结构

所有作品素材统一放在 `portfolio/` 下，按作品分子目录（子目录名 = 主页 `data.js` 里的作品 slug）：

```
portfolio/
├── xiaodu/            儿童手表小度助手
│   ├── xiaodu-crop.webp        封面（透明）
│   └── xiaoduwatch.mp4         演示视频 (7.3MB, H.264)
├── stethoscope/       智能多模听诊器
│   ├── stethoscope-main.webp   主图 / 封面（透明）
│   ├── stethoscope-photo.webp  实拍图
│   └── stethoscope.mp4         演示视频 (2.0MB, H.264)
├── zhuge/             诸葛智能体
│   ├── overview.webp           列表封面
│   ├── conversation.webp       详情主图
│   └── slide_03 ~ slide_16.webp  演示幻灯片
└── wifimodule/        AIDK 物联网平台 · WiFi 模组
    ├── alx830x.webp            ALX830X 模组实物
    ├── alx830x-spec.webp       ALX830X 参数表
    ├── alx850x.webp            ALX850X 模组实物
    └── alx850x-spec.webp       ALX850X 参数表
```

> ⚠️ **目录与文件名必须全 ASCII，不要用中文。** 顶层目录叫 `portfolio`（= 作品集）而不是中文。
> 中文路径在 GitHub Pages 下会被反复 URL-encode / 解码，部分浏览器拿不到资源。

## 用法

主页 `data.js` 里这样引用（GitHub Pages 直接 serve main 分支文件，无需版本号）：

```js
// 图片
cover: { kind: "image", src: "https://icycal.github.io/gu-videos/portfolio/stethoscope/stethoscope-main.webp" }

// 视频
{ kind: "video", src: "https://icycal.github.io/gu-videos/portfolio/stethoscope/stethoscope.mp4" }
```

改完 `data.js` 记得 bump HTML 里的 `data.js?v=` 缓存版本号，否则访客浏览器仍会拉旧路径。

## 约定

- **图片统一 WebP**：透明图 `quality 90` 保留 alpha，照片类缩放到最大宽 1000~1600 后 `quality 82~88`。
- **视频必须 H.264 (avc1) + yuv420p + faststart**。HEVC (hvc1) 在多数浏览器里播不了（需装解码扩展）。
  转码命令：
  ```
  ffmpeg -i input.mp4 -c:v libx264 -crf 23 -preset slow -pix_fmt yuv420p \
         -c:a aac -b:a 96k -movflags +faststart output.mp4
  ```
- 新增作品素材时，在 `portfolio/` 下建与 slug 同名的子目录，不要往仓库根目录堆文件。
