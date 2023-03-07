# TextList

文本列表类型, 继承自 [`Block`](../block.md).

### new TextList()

`children` 只允许为 [`Text`](text.md) 类型, 构造函数.

```typescript
new TextList(children?: Text[])
```

示例:

```typescript
new TextList([
  new Text({ content: 'This is a text.', background: '#8bdb52', heading: TextHeading.H5 }),
  new Text({ content: 'https://docs.deup.io', link: 'https://docs.deup.io', color: '#3c7ad1', underline: true }),
])
```

### add()

添加子块.

```typescript
add(child: Text): void
```
