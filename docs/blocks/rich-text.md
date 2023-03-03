# RichText

文本类型, 继承自 [`Block`](../block.md).

### new RichText()

`children` 只允许为 [`Text`](text.md) 类型, 构造函数.

```typescript
new RichText(children: Text[])
```

示例:

```typescript
new RichText([
  new Text({ content: 'This is a text.', background: '#8bdb52', level: TextLevel.H5 }),
  new Text({ content: 'https://docs.deup.io', link: 'https://docs.deup.io', color: '#3c7ad1', underline: true }),
])
```