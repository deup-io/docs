# Block

抽象类, 所有的块类型都继承自 `Block`.

### type

[`BlockType`](block-type.md), 块类型.

```typescript
protected type: BlockType
```

### attributes

块属性.

```typescript
protected attributes:
    | PageAttributes
    | TextAttributes
    | ImageAttributes
    | VideoAttributes
```

### children

子块, 目前只有 `page` 类型, 才允许有子快.

```typescript
protected children?: Block[]
```
