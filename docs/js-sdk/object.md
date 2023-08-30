# 对象信息

```typescript
interface Object {
  name: string;
  type: ObjectType;
  isDirectory: boolean;
  path?: string;
  thumbnail?: string;
  poster?: string;
  created?: string;
  modified?: string;
  size?: number;
  url?: string;
  isLive?: boolean;
  related?: Object[];
  headers?: Record<string, string>;
}
```

### name

对象名称。

### type

[`ObjectType`](./object-type.md) 对象类型, 可选值: `folder`、`image` 等。

### isDirectory

是否是文件夹。

### path

对象的路径, 如果 `path` 的值不为 `null`, 获取对象内容时会使用 `path+name` 的值作为参数。

### thumbnail

对象的缩略图。

### poster

对象的海报图。

### created

对象的创建时间, 示例: `2020-01-01T00:00:00.000Z`。

### modified

对象的修改时间, 示例: `2020-01-01T00:00:00.000Z`。

### size

对象的大小, 单位: 字节, 示例: `1024`。

### url

对象的调用链接。

### isLive

是否是直播视频流。

### related

相关对象, 例如: 视频的字幕文件。

PS: 目前仅视频的字幕文件会从 `related` 里面获取, 匹配后缀名为 `.srt`/`.ass`/`.vtt` 的文件。

### headers

调用播放地址时的请求头, 示例: `{ 'User-Agent': '...' }`。如果这个字段存在, 会覆盖 [`Config`](./config.md) 里面的 `headers` 字段。
