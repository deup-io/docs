# Page

页面类型, 可以包含任意子块, 继承自 [`Block`](../block.md).

### new Page()

[`PageAttributes`](page-attributes.md), 构造函数.

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

### add()

添加子块.

```typescript
add(block: Block): void
```
