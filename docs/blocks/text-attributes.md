# TextAttributes

文本的可设置属性.

```typescript
interface TextAttributes {
  content: string;
  level?: TextLevel;
}
```

### content

需要渲染的文本内容, 必填, 字符串类型.

### level

[`TextLevel`](text-level.md), 文本级别.
