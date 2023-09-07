# Deup

基础类, 所有插件需要继承这个类的抽象方法。

### execute()

执行插件, 必须调用的方法, 告知 `Deup` 执行那个类。

=== "定义"

    ```typescript
    public static execute(instance: Deup): void
    ```

=== "示例"

    ```typescript
    Deup.execute(new Plugin())
    ```

### config

[`Config`](./config.md) 整个插件的配置信息, 包括插件名称、颜色、图标等信息。

=== "定义"

    ```typescript
    config: Config
    ```

=== "示例"

    ```typescript
    config = {
      name: '插件名称',
      logo: 'https://example.com/logo.png',
      color: '#FFFFFF',
      background: ['#4995EC', '#4BA5E9'],
      headers: {
        'User-Agent': '...',
      },
    }
    ```

### inputs

[`Input`](./input.md) 插件的输入项, 会在添加服务的时候显示, 用户可以输入需要的信息。用户保存服务后会按 `key: value` 的方式保存的 `$storage.inputs` 里面, 通过 `await $storage.inputs` 可以获取到用户保存的输入项。

=== "定义"

    ```typescript
    inputs: Record<string, Input>
    ```

=== "示例"

    ```typescript
    inputs = {
      url: {
        label: '服务器',
        placeholder: 'https://example.com',
        required: true,
      },
    }

    // 获取用户输入的 url
    const url = (await $storage.inputs).url
    ```

### check()

用户新建服务保存的时候会调用 `check()` 方法, 用于检查用户输入的信息是否正确。

=== "定义"

    ```typescript
    abstract check(): Promise<boolean>
    ```

=== "示例"

    ```typescript
    async check() {
      const inputs = await $storage.inputs
      const response = await $axios.get(inputs.url, {
        headers: {
          Authorization: await $storage.get('token'),
        },
      })
      return response.status === 200
    }
    ```

### get()

获取对象信息, 用户访问具体对象时会调用这个方法, 返回值是具体对象信息 [`Object`](./object.md)。

=== "定义"

    ```typescript
    abstract get(object: Object): Promise<Object>
    ```

=== "示例"

    ```typescript
    async get(object) {
      return {
        id: object.id,
        name: '文件名称',
        type: 'image',
        isDirectory: false,
        url: 'https://example.com/image.png',
      }
    }
    ```

### list()

获取对象列表, 用户访问文件夹时会调用这个方法, 返回值是对象列表 [`Object[]`](./object.md)。

=== "定义"

    ```typescript
    abstract list(object: Object, offset: number, limit: number): Promise<Object[]>
    ```

=== "示例"

    ```typescript
    async list(object, offset, limit) {
      return [
        {
          id: '文件夹 ID',
          name: '文件夹名称',
          type: 'folder',
          isDirectory: true,
        },
        {
          id: '文件 ID',
          name: '文件名称',
          type: 'image',
          isDirectory: false,
          url: 'https://example.com/image.png',
        },
      ]
    }
    ```

### search()

搜索对象, 用户搜索时会调用这个方法, 返回值是对象列表 [`Object[]`](./object.md)。

=== "定义"

    ```typescript
    abstract search(object: Object, keyword: string, offset: number, limit: number): Promise<Object[]>
    ```

=== "示例"

    ```typescript
    async search(object, keyword, offset, limit) {
      return [
        {
          id: '文件夹 ID',
          name: '文件夹名称',
          type: 'folder',
          isDirectory: true,
        },
        {
          id: '文件 ID',
          name: '文件名称',
          type: 'image',
          isDirectory: false,
          url: 'https://example.com/image.png',
        },
      ]
    }
    ```
