# gu-videos

个人主页（`Icycal.github.io`）**作品集的图片 / 视频图床**。主页仓库只存代码与配置，所有媒体素材集中在这里，经 jsDelivr CDN 引用。

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

> ⚠️ **目录与文件名必须全 ASCII，不要用中文。**
> jsDelivr 对含非 ASCII 字符的路径不缓存，而是返回 301 跳到
> `raw.githubusercontent.com`。小图片跟随重定向还能加载，但视频会直接失败：
> `<video>` 的 Range 请求打到 raw 上会得到 `MEDIA_ELEMENT_ERROR: Format error`（code 4）。
> 实测：`作品集/stethoscope/stethoscope.mp4` 播放失败，改成 `portfolio/stethoscope/stethoscope.mp4` 后正常。
> 所以顶层目录叫 `portfolio`（= 作品集）而不是中文。

## 用法

主页 `data.js` 里这样引用（`@main` 固定指向 main 分支）：

```js
// 图片
cover: { kind: "image", src: "https://cdn.jsdelivr.net/gh/Icycal/gu-videos@main/portfolio/stethoscope/stethoscope-main.webp" }

// 视频
{ kind: "video", src: "https://cdn.jsdelivr.net/gh/Icycal/gu-videos@main/portfolio/stethoscope/stethoscope.mp4" }
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
