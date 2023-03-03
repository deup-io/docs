# TextAttributes

文本的可设置属性.

```typescript
interface TextAttributes {
  content: string;
  color?: string;
  background?: string;
  link?: string;
  level?: TextLevel;
  bold?: boolean;
  italic?: boolean;
  underline?: boolean;
  strikethrough?: boolean;
}
```

### content

需要渲染的文本内容, 必填, 字符串类型.

### color

文本颜色, 示例: `#8bdb52`.

### background

文本背景颜色, 示例: `#8bdb52`.

### link

跳转链接, 示例: `https://docs.deup.io`.

### level

[`TextLevel`](text-level.md), 文本级别.

### bold

文本是否加粗, 布尔类型.

### italic

文本是否为斜体, 布尔类型.

### underline

是否显示下划线, 布尔类型.

### strikethrough

是否显示删除线, 布尔类型.
