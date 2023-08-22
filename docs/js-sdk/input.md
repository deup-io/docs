# Input

用户添加服务时, 需要输入的信息。

```typescript
interface Input {
  label: string;
  required: boolean;
  placeholder?: string;
}
```

### label

输入项的名称。

### required

是否必填。

### placeholder

输入项的提示信息。
