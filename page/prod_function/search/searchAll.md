# 综合搜索

<img src="./images/searchAll.png" width="300"/>

[跳转到该页](http://www.happy6year.com/#/search/searchPage)

> 综合搜索展示了搜索歌曲、歌单、专辑、视频、歌手以及相关搜索

## 遇到的问题

1.如何根据后台得到的渲染顺序渲染组件？例如得到的顺序结果为:

`order:["song", "playList", "video", "sim_query", "mlog", "talk", "artist", "album", "djRadio", "user"]`

- 解决方式:使用动态组件渲染

- 实现思路：

  - 定义组件名称

  - 在data中定义需要渲染的组件名称

  ```javascript
   includeComponents: ['song', 'playList', 'album', 'artist', 'sim_query', 'video']
  ```

  - 过滤掉不需要渲染的组件

  - 获取排序的索引

  - 根据排序的索引进行重命名操作（由于定义的组件名称与后台数据不一致）

  - 讲重命名后的数组保存到data的order中用于渲染

    ```javascript
    // 处理排序结果
    handleOrder (order) {
      if (!order) return null
      // 过滤包含的组件
      let filterOrder = order.filter(item => this.includeComponents.includes(item))
      // 获取索引
      let songIndex = filterOrder.findIndex(item => item === 'song')
      let playListIndex = filterOrder.findIndex(item => item === 'playList')
      let albumIndex = filterOrder.findIndex(item => item === 'album')
      let artistIndex = filterOrder.findIndex(item => item === 'artist')
      let simQueryIndex = filterOrder.findIndex(item => item === 'sim_query')
      let videoIndex = filterOrder.findIndex(item => item === 'video')
      // 根据索引重命名（因为后台数据与组件定义名称不一致）
      if (songIndex !== -1) {
        filterOrder[songIndex] = 'SearchSong'
      }
      if (playListIndex !== -1) {
        filterOrder[playListIndex] = 'SearchSongSheet'
      }
      if (albumIndex !== -1) {
        filterOrder[albumIndex] = 'SearchAlbum'
      }
      if (artistIndex !== -1) {
        filterOrder[artistIndex] = 'SearchSinger'
      }
      if (simQueryIndex !== -1) {
        filterOrder[simQueryIndex] = 'SearchSimQuery'
      }
      if (videoIndex !== -1) {
        filterOrder[videoIndex] = 'SearchVideo'
      }
      return filterOrder
    }
    ```

  - 使用`<component>`动态渲染组件

        //这里result用于传递数据
        <component v-for="(item,index) in order"
        :is="item"
        :key="index"
        :song="result.song"
        :singer="result.singer"
        :album="result.album"
        :simQuery="result.simQuery"
        :songSheet="result.songSheet"
        :video="result.video"
        @setIndex="setCurrentIndex"
        @closeList="$emit('closeList')"/>
    ​

    ​


