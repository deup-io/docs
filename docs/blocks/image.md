# Image

图片类型, 继承自 [`Block`](../block.md).

### new Image()

[`ImageAttributes`](image-attributes.md), 构造函数.

```typescript
new Image(attr: ImageAttributes)
```

示例:

```typescript
new Image({
  url: 'https://picsum.photos/200/300',
  headers: { 'X-Header': 'value' },
})
```