---
up:
  - "[[Tools Map]]"
related:
created: 2026-01-13
tags:
  - tools/sop
---


`cd /Users/yangyu/Movies/00-录屏`

```
ffmpeg -i "input.mp4" -vn -acodec libmp3lame -q:a 0 "output.mp3"
```