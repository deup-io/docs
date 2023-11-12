# 对象信息

```typescript
interface Object {
  id: string;
  name?: string;
  type?: ObjectType;
  remark?: string;
  thumbnail?: string;
  poster?: string;
  cover?: string;
  created?: string;
  modified?: string;
  size?: number;
  url?: string;
  isLive?: boolean;
  related?: Object[];
  options?: ObjectOptions;
  extra?: Record<string, any>;
  headers?: Record<string, string>;
}
```

### id

对象唯一 ID。

### name

对象显示名称。

### type

[`ObjectType`](./object-type.md) 对象类型, 可选值: `folder`、`image` 等。

### remark

对象的备注信息。

### thumbnail

对象的缩略图。

### poster

对象的海报图。

### cover

对象的封面图。

### created

对象的创建时间, 示例: `2020-01-01T00:00:00.000Z`。

### modified

对象的修改时间, 示例: `2020-01-01T00:00:00.000Z`。

### size

对象的大小, 单位: 字节, 示例: `1024`。

### url

对象的调用链接。

`ObjectType.IMAGE` 和 `ObjectType.WEBVIEW` 类型的对象, `url` 为链接地址, 目前支持 `blob` scheme。

支持 `text` 和 `base64` 两种数据解析方式。

示例:

```json
{
  id: '-',
  name: 'webview',
  type: 'webview',
  url: 'blob://text/<html><meta name="viewport" content="width=device-width,initial-scale=1"><body>Deup</body></html>',
}
```

```json
{
  id: '-',
  name: 'image',
  type: 'image',
  url: 'blob://base64/<base64>',
}
```


### isLive

是否是直播视频流。

### related

相关对象, 例如: 视频的字幕文件。

PS: 目前仅视频的字幕文件会从 `related` 里面获取, 匹配后缀名为 `.srt`/`.ass`/`.vtt` 的文件。

### options

[`ObjectOptions`](./object-options.md) 对象可配置项, 目前仅支持设置 `folder` 类型设置下级打开的视图等信息。

### extra

额外信息, 你可以在这里存放一些自定义的信息, 例如: 文件的路径。

### headers

调用播放地址时的请求头, 示例: `{ 'User-Agent': '...' }`。如果这个字段存在, 会覆盖 [`Config`](./config.md) 里面的 `headers` 字段。
