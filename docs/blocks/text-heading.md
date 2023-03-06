# TextHeading

文本级别, 枚举类型.

```typescript
export enum TextHeading {
  H1 = 'h1',
  H2 = 'h2',
  H3 = 'h3',
  H4 = 'h4',
  H5 = 'h5',
  H6 = 'h6',
}
```

示例:

```typescript
new Text({ content: 'headline1', heading: TextHeading.H1 }),
```
