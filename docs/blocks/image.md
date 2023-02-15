# Image

图片类型, 继承自 `Block`.

### new Image()

Constructs a new image.

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