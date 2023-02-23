# ImageAttributes

图片的可设置属性.

```typescript
interface ImageAttributes {
  url: string;
  title?: string;
  width?: number;
  height?: number;
  headers?: Record<string, string>;
}
```

### url

图片地址, 必填, 字符串类型.

### title

图片标题.

### width

图片宽度.

### height

图片高度.

### headers

加载图片时使用的自定义头信息, map 类型.
