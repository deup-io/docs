# Page

页面类型, 可以包含任意子块, 继承自 `Block`.

### new Page()

Constructs a new page.

```typescript
new Page(attr: PageAttributes, children?: Block[])
```

示例:

```typescript
new Page(
  {
    title: 'Hello World',
    description: 'Hello World',
  },
  [new Text({ content: 'Hello World' })],
);
```
