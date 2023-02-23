# VideoAttributes

图片的可设置属性.

```typescript
interface VideoAttributes {
  url: string;
  title?: string;
  thumbnail?: string;
  width?: number;
  height?: number;
  headers?: Record<string, string>;
}
```

### url

视频地址, 必填, 字符串类型.

### title

视频标题.

### thumbnail

视频封面

### width

图片宽度.

### height

图片高度.

### headers

加载视频时使用的自定义头信息, map 类型.
