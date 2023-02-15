# Deup

基础类, 里面包含一些文章构建的基础方法, 比如 `render` 用于渲染文章.

### isDeupApp

`Deup.isDeupApp` 判断当前环境是否是 Deup 应用.

```typescript
public static isDeupApp: boolean
```

### render

最终的渲染方法, 调用这个方法就能看到文章的预览效果.

```typescript
public static render(block: Block): void
```
