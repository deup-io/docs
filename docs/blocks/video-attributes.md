# VideoAttributes

图片的可设置属性.

```typescript
interface VideoAttributes {
  url: string;
  headers?: Record<string, string>;
}
```

### url

视频地址, 必填, 字符串类型.

### headers

加载视频时使用的自定义头信息, map 类型.
