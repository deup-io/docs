# Storage

持久化存储, 用于存储一些需要持久化的数据, 例如用户的登录状态, 一些配置等等, 每个服务的存储空间是隔离的。

### inputs

用户新建服务时填写的 `inputs` 信息, 例如 `url`, `username`, `password` 等等。

=== "定义"


    ```typescript
    public get inputs(): Promise<Record<string, string>>
    ```

=== "调用"

    ```typescript
    const inputs = await $storage.inputs
    ```

### get(key)

获取存储的数据。

=== "定义"

    ```typescript
    public async get(key: string): Promise<any>
    ```

=== "调用"

    ```typescript
    const token = await $storage.get('token')
    ```

### set(key, value)

设置存储的数据。

=== "定义"

    ```typescript
    public async set(key: string, value: any): Promise<void>
    ```

=== "调用"

    ```typescript
    await $storage.set('token', '...')
    ```

### remove(key)

删除存储的数据。

=== "定义"

    ```typescript
    public async remove(key: string): Promise<boolean>
    ```

=== "调用"

    ```typescript
    $storage.remove('token')
    ```

### clear()

清空存储的数据。

=== "定义"

    ```typescript
    public async clear(): Promise<boolean>
    ```

=== "调用"

    ```typescript
    $storage.clear()
    ```
