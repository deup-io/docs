# 快速开始

本教程将带你快速创建一个简单的 Deup 插件脚本。

> 感谢您阅读本教程, 期待您提供更多的插件脚本, 请在 [GitHub](https://github.com/deup-io/deup){target=_blank} 上提交您 PR。

目前支持的插件:

- [Alist](./alist.md)
- [Movies & TV](./movies-tv.md)
- [Unsplash](./unsplash.md)
- [IPTV](./iptv.md)

## 创建一个类

首先, 我们需要创建一个类, 这个类需要继承 `Deup` 类。

```typescript
class MyPlugin extends Deup {
  // ...
}
```

## 插件的配置信息

接下来, 我们需要定义插件的配置信息, 包括插件名称、颜色、图标等信息。

```typescript
class MyPlugin extends Deup {
  config = {
    name: '插件名称',
    logo: 'https://s2.loli.net/2023/08/17/dZeUNcuftSLaG41.png',
  };
}
```

## 定义服务输入信息

配置服务的输入, 这些信息会在新建服务时转为输入框, 用于填写服务需要用的的信息。

```typescript
class MyPlugin extends Deup {
  config = {
    // ...
  };

  inputs = {
    url: {
      label: '服务器',
      required: false,
      placeholder: 'https://example.com',
    },
    image: { label: '图片地址', required: true, placeholder: '填写图片地址' },
  };
}
```

## 实现 check() 方法

`check()` 方法会在服务保存的时候调用, 可以用来检测用户填写的信息是否正确。

```typescript
class MyPlugin extends Deup {
  // ...

  async check() {
    // 可以在 check 方法中获取用户输入的信息
    const url = (await $storage.inputs).url
    return url != '123'; // url
  }
}
```

## 实现 get() 方法

`get()` 方法是用来获取具体对象信息的, 参数是 `list()` 返回的对象信息。

```typescript
class MyPlugin extends Deup {
  // ...

  async get(object) {
    const image = (await $storage.inputs).image;

    return {
      id: '-',
      name: '测试图片',
      type: 'image',
      url: image,
    };
  }
}
```

## 实现 list() 方法

`list()` 方法是用来获取对象列表的, 首页默认 `object = null`。

```typescript
class MyPlugin extends Deup {
  // ...

  async list(object, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        id: '-', // id 为必填项
        name: '测试图片',
        type: 'image',
        thumbnail: image,
      },
    ];
  }
}
```

## 实现 search() 方法

`search()` 方法是用来搜索对象的, 参数是搜索关键词。

```typescript
class MyPlugin extends Deup {
  // ...

  async search(object, keyword, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        id: '-', // id 为必填项
        name: '测试图片-搜索结果',
        type: 'image',
        thumbnail: image,
      },
    ];
  }
}
```

## 调用 execute() 方法

`execute()` 方法是用来告知 Deup 使用那个类作为插件的入口。

```typescript
Deup.execute(new MyPlugin());
```

## 完整代码

```typescript
class MyPlugin extends Deup {
  config = {
    name: '我的插件',
    logo: 'https://s2.loli.net/2023/08/17/dZeUNcuftSLaG41.png',
  };

  inputs = {
    url: {
      label: '服务器',
      required: false,
      placeholder: 'https://example.com',
    },
    image: { label: '图片地址', required: true, placeholder: '填写图片地址' },
  };

  async check() {
    const url = (await $storage.inputs).url
    return url != '123'; // url
  }

  async get(object) {
    const image = (await $storage.inputs).image;

    return {
      id: '-',
      name: '测试图片',
      type: 'image',
      url: image,
    };
  }

  async list(object, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        id: '-',
        name: '测试图片',
        type: 'image',
        thumbnail: image,
      },
    ];
  }

  async search(object, keyword, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        id: '-',
        name: '测试图片-搜索结果',
        type: 'image',
        thumbnail: image,
      },
    ];
  }
}

Deup.execute(new MyPlugin());
```
