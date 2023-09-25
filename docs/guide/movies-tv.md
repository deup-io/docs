# Movies & TV

![](../assets/images/movies-tv/1.png){ width="200" } ![](../assets/images/movies-tv/2.png){ width="200" } ![](../assets/images/movies-tv/3.png){ width="200" }

[https://cdn.jsdelivr.net/gh/deup-io/deup/movies-tv.js](https://cdn.jsdelivr.net/gh/deup-io/deup/movies-tv.js){target=_blank}

国内播放源: [https://cdn.jsdelivr.net/gh/deup-io/deup/movies-tv-cn.js](https://cdn.jsdelivr.net/gh/deup-io/deup/movies-tv-cn.js){target=_blank}

> PS: 优势是国内的 CDN 地址, 但是没有实现分类筛选功能, 如果您有兴趣感谢您实现并提交 PR。

```javascript
/**
 * MoviesTv plugin for Deup
 *
 * @class MoviesTv
 * @extends {Deup}
 * @author ZiHang Gao
 */
class MoviesTv extends Deup {
  /**
   * Define the basic configuration
   *
   * @type {{layout: string, name: string, pageSize: number, timeout: number}}
   */
  config = {
    name: 'Movies & TV - CN',
    layout: 'poster',
    timeout: 10000,
    pageSize: 20,
  };

  /**
   * Base url
   *
   * @type {string}
   * @private
   */
  _baseUrl = 'https://api.guangsuapi.com/api.php/provide/vod/from/gsm3u8';

  /**
   * Check inputs
   *
   * @returns {Promise<boolean>}
   */
  async check() {
    try {
      return (await this.list()).length > 0;
    } catch (e) {
      $alert(e.message);
    }

    return false;
  }

  /**
   * Get the object information
   *
   * @param object
   * @returns {Promise<any>}
   */
  async get(object) {
    return object.extra ? { ...object, name: object.extra.name } : object;
  }

  /**
   * Get the video list
   *
   * @param object
   * @param offset
   * @param limit
   * @returns {Promise<*>}
   */
  async list(object = null, offset = 0, limit = 20) {
    try {
      const page = Math.floor(offset / limit) + 1;
      const response = await $axios.get(
        `${this._baseUrl}?ac=detail&pg=${page}&pagesize=${limit}`,
      );
      return this.formatVideoList(response.data);
    } catch (e) {
      $alert(e.message);
    }

    return [];
  }

  /**
   * Get the video list by keyword
   *
   * @param object
   * @param keyword
   * @param offset
   * @param limit
   * @returns {Promise<*>}
   */
  async search(object, keyword, offset, limit) {
    try {
      const page = Math.floor(offset / limit) + 1;
      const response = await $axios.get(
        `${this._baseUrl}?ac=detail&wd=${keyword}&pg=${page}&pagesize=${limit}`,
      );

      return this.formatVideoList(response.data);
    } catch (e) {
      $alert(e.message);
    }

    return [];
  }

  /**
   * Format object list
   *
   * @param data
   * @returns {*}
   */
  formatVideoList(data) {
    return data.list.map((video) => {
      const playUrls =
        video.vod_play_note === ''
          ? video.vod_play_url.split('#')
          : video.vod_play_url.split(video.vod_play_note)[1].split('#');

      return {
        id: `${video.vod_id}#1`,
        name: video.vod_name,
        type: 'video',
        remark: video.vod_name,
        thumbnail: video.vod_pic,
        poster: video.vod_pic,
        modified: new Date(
          Date.parse(video.vod_time.replace(' ', 'T')),
        ).toISOString(),
        url: playUrls[0].split('$')[1],
        extra: {
          name:
            playUrls.length > 1 ? playUrls[0].split('$')[0] : video.vod_name,
        },
        related: playUrls.map((value, key) => {
          const [name, url] = value.split('$');
          return {
            id: `${video.vod_id}#${key + 1}`,
            name: playUrls.length > 1 ? name : video.vod_name,
            url,
            type: 'video',
            thumbnail: video.vod_pic,
          };
        }),
      };
    });
  }
}

Deup.execute(new MoviesTv());
```
