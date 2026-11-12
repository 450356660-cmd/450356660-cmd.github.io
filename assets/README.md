# 素材放置说明 / Asset Drop Zone

把文件按下面的**文件名和尺寸**放进来即可，页面会自动读取；文件名不要改。
Put files in with the exact names below — the page reads them automatically.

## 目录结构

```
site/
├── index.html                  ← 页面本体（文案/颜色/品牌名都在里面改）
├── CNAME                       ← 部署时自动生成，绑自定义域名用
└── assets/
    ├── favicon.svg             ← 浏览器标签小图标（可替换）
    ├── logo.svg                ← 完整 logo（备用）
    ├── video/
    │   ├── hero.mp4            ← 首屏背景视频
    │   ├── hero-poster.jpg     ← 首屏视频封面（视频加载前显示）
    │   └── showreel.mp4        ← 点击 "Showreel" 播放的年度混剪
    ├── work/
    │   ├── case-01.jpg  … case-06.jpg    ← 6 个案例封面
    └── clients/
        └── client-01.svg … client-08.svg ← 客户 logo（可选）
```

## 规格要求

| 文件 | 尺寸 | 格式 | 体积上限 | 说明 |
|---|---|---|---|---|
| `video/hero.mp4` | 1920×1080 或 2560×1440 | H.264 MP4，**无声** | 8 MB | 8–15 秒循环，镜头运动缓慢、画面不要太乱（上面要压白色大字） |
| `video/hero-poster.jpg` | 1920×1080 | JPG，sRGB | 300 KB | 视频第一帧即可 |
| `video/showreel.mp4` | 1920×1080 | H.264 MP4 | 60 MB | 60–120 秒，可带声音 |
| `work/case-01.jpg`、`case-06.jpg` | 2400×1030（约 21:9） | JPG，sRGB | 500 KB | 大图位（第 1、6 个案例） |
| `work/case-02~05.jpg` | 1600×1000（约 16:10） | JPG，sRGB | 400 KB | 常规卡片位 |
| `clients/client-0X.svg` | 高度一致即可（建议 40px 高） | SVG 优先，PNG 需透明底 | 100 KB | 深色底上可读（建议白色/浅色版 logo） |
| `favicon.svg` | 64×64 | SVG | 10 KB | 深色底 + 单色标志 |

## 两条硬提醒

1. **竖屏素材不要直接放**：卡片是横向裁切（`background-size: cover`），竖屏视频截图会被裁掉上下；请提供横版画面。
2. **视频一定要压缩**：GitHub Pages 单文件上限 100 MB、仓库建议 < 1 GB。`hero.mp4` 超过 8 MB 手机端首屏会明显卡顿。压缩命令：
   ```bash
   ffmpeg -i 原片.mp4 -vf "scale=1920:-2" -c:v libx264 -crf 26 -preset slow -an -movflags +faststart video/hero.mp4
   ffmpeg -i 原片.mp4 -vf "scale=1920:-2" -c:v libx264 -crf 23 -preset slow -c:a aac -b:a 128k -movflags +faststart video/showreel.mp4
   ```

## 想改成更多案例 / 换顺序

`index.html` 里搜 `<!-- 案例 1` 那段，卡片是块状结构，复制一个 `<article class="card">…</article>` 改 `case-0X.jpg` 和文案即可。文案同时要改两处：HTML 里的默认中文 + 底部 `I18N` 词典里的 `zh` / `en`。
