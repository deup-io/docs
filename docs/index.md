# Deup Docs

Deup 是通过公开协议的方式来构建文章内容的应用, 您可以使用 `deup-js` 来实现文章的生成.

目前支持的内容类型有:

- 页面
- 文本
- 图片
- 视频

## 安装

```bash
npm install @deup-io/core
```

## 示例

```typescript
import Deup, { Page, Text, Image, Video } from '@deup-io/core'

Deup.render(
  new Page(
    {
      title: 'Hello World',
      description: 'Hello World',
    },
    [
      new Text({ content: 'Hello World' }),
      new Image({
        url: 'https://picsum.photos/200/300',
        headers: { 'X-Header': 'value' },
      }),
      new Video({
        url: 'https://flutter.github.io/assets-for-api-docs/assets/videos/butterfly.mp4',
        headers: { 'X-Header': 'value' },
      }),
    ],
  ),
);
```
