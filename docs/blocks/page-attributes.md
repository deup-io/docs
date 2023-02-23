# PageAttributes

页面的可设置属性.

```typescript
interface PageAttributes {
  title: string;
  description?: string;
  tags?: Tag[];
}
```

### title

页面的标题, 必填, 字符串类型.

### description

页面的内容描述, 可选, 字符串类型.

### tags

[`Tag`](../tag.md), 页面标签.
