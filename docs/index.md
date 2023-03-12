# Deup Docs

Deup 是通过公开协议的方式来构建文章内容的应用, 您可以使用 `deup-js` 来实现文章的构建。

![](assets/images/app-store-badge.svg)

支持的内容类型有:

- 页面
- 文本
- 图片
- 视频

## 安装

```bash
npm install @deup-io/core
```

## 使用

Deup 目前支持两种方式来保存内容, 一种是使用剪贴板, 另一种是使用 Deup 插件功能编写一个网页来生成内容, 后续会新增其他的一些方式允许用户来保存内容, 比如通过自定义 api、微信等等。

### 剪切板

Deup 会监听剪贴板内容, 如果内容格式解析正确, 会自动渲染内容, 你可以通过下面的示例代码来生成需要渲染的内容:

> PS: 相同的内容只会解析渲染一次, 如果需要更新内容, 请修改内容后再次复制。

```typescript
import * as zlib from 'zlib';
import Deup, { Page, Text, TextHeading } from '@deup-io/core';

const message = Deup.render(
  new Page(
    {
      title: 'This is a page title.',
      description: 'This is a page description.',
    },
    [
      new Text({ content: 'clipboard', heading: TextHeading.H5 }),
      new Image({
        title: 'image',
        url: 'https://picsum.photos/200/300',
        headers: { 'X-Header': 'value' },
      }),
    ],
  ),
);

// 复制到剪切板的内容需要 base64 编码, gzip 压缩是可选的, 但是建议使用, 这样会减少复制的文本长度
const clipboard = zlib.gzipSync(message).toString('base64');
console.log(clipboard);
```

你可以尝试复制下面内容, 并打开 Deup 应用, 就可以看到文章内容。

```base64
H4sIAAAAAAAAE2WPSwrCMBCGr1JmXduiuOkJPIALQVykyWAG0iQkU1Gkd3dSUXxANvM/vp/cwasRoYeE3mCCGkbMWZ1FugPfYrFiOWvQlpyRGPTHt8V4ZbEUc6JhYsylpoNn9Cy2dhSHoJKRjEVlyJ9FtVuY5/rNoPHJ/4ZMyZUoc8x920bSeRqbaAOH3K67rt10nXSY2H0yygimBXBY7ZZD3ItyE8rmfPpdefX3lnIlT1Xls9UiN8IzmHWiyBT8f+rDbAr9ATNpq8pMAQAA
```

### 插件

你需要一台服务器, 或者建立本地的服务, 在你的服务里实现 `deup-js` 的功能, 并把你的网页地址添加到 Deup 的插件列表里。

```typescript
import Deup, { Page, Text, Image, Video, TextHeading, TextList } from '@deup-io/core';

// 调用 Deup.render 会通知 app 进行内容的解析
Deup.render(
  new Page(
    {
      title: 'This is a page title.',
      description: 'This is a page description.',
      tags: [
        { name: 'tag1', color: '#8bdb52' },
        { name: 'tag2', color: '#3c7ad1' },
      ],
    },
    [
      new Text({ content: 'headline1', heading: TextHeading.H1 }),
      new Text({ content: 'headline2', heading: TextHeading.H2 }),
      new Text({ content: 'headline3', heading: TextHeading.H3 }),
      new Text({ content: 'headline4', heading: TextHeading.H4 }),
      new Text({ content: 'headline5', heading: TextHeading.H5 }),
      new Text({ content: 'headline6', heading: TextHeading.H6, background: '#8bdb52' }),
      new Image({
        title: 'image',
        url: 'https://picsum.photos/200/300',
        headers: { 'X-Header': 'value' },
      }),
      new TextList([
        new Text({ content: 'This is a text.', color: '3c7ad1', underline: true, strikethrough: true }),
        new Text({ content: ' ' }),
        new Text({ content: 'This is a text.', background: '#8bdb52', heading: TextHeading.H5 }),
        new Text({ content: 'https://docs.deup.io', link: 'https://docs.deup.io', color: '#3c7ad1', underline: true }),
        new Text({ content: 'This is a text.', bold: true }),
        new Text({ content: 'This is a text.', italic: true }),
        new Text({ content: 'This is a text.', underline: true }),
        new Text({ content: 'This is a text.', strikethrough: true }),
      ]),
      new Video({
        title: 'video',
        url: 'https://sf1-hscdn-tos.pstatp.com/obj/media-fe/xgplayer_doc_video/flv/xgplayer-demo-720p.flv',
        headers: { 'X-Header': 'value' },
      }),
    ],
  ),
);
```
