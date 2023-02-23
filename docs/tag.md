# Tag

块标签, 目前只有 [`Page`](blocks/page.md) 类型支持设置标签.

```typescript
interface Tag {
  name: string;
  color: string;
}
```

### name

标签名称.

### color

标签背景颜色, hex 格式, 示例 `#ffff00`
