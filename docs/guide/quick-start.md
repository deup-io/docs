# 快速开始

本教程将带你快速创建一个最简单的 Deup 插件脚本。

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
    color: '#FFFFFF',
    background: ['#4995EC', '#4BA5E9'],
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

## 实现 getObject() 方法

`getObject()` 方法是用来获取具体对象信息的, 参数是对象的完整路径。

```typescript
class MyPlugin extends Deup {
  // ...

  async getObject(path) {
    const image = (await $storage.inputs).image;

    return {
      name: '测试图片',
      type: 'image',
      isDirectory: false,
      url: image,
    };
  }
}
```

## 实现 getList() 方法

`getList()` 方法是用来获取对象列表的, 首页默认是空字符串 `""`。

```typescript
class MyPlugin extends Deup {
  // ...

  async getList(path, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        name: '测试图片',
        type: 'image',
        isDirectory: false,
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

  async search(path, keyword, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        name: '测试图片-搜索结果',
        type: 'image',
        isDirectory: false,
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
    color: '#FFFFFF',
    background: ['#4995EC', '#4BA5E9'],
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

  async getObject(path) {
    const image = (await $storage.inputs).image;

    return {
      name: '测试图片',
      type: 'image',
      isDirectory: false,
      url: image,
    };
  }

  async getList(path, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        name: '测试图片',
        type: 'image',
        isDirectory: false,
        thumbnail: image,
      },
    ];
  }

  async search(path, keyword, offset, limit) {
    const image = (await $storage.inputs).image;

    return [
      {
        name: '测试图片-搜索结果',
        type: 'image',
        isDirectory: false,
        thumbnail: image,
      },
    ];
  }
}

Deup.execute(new MyPlugin());
```