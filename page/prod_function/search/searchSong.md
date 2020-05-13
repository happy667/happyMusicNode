# 歌曲搜索

<img src="./images/searchSong.png" width="300"/>

[跳转到该页](http://www.happy6year.com/#/search/searchPage)

> 搜索歌曲，支持上拉加载更多歌曲

## 遇到的问题

1.在歌曲上拉加载时其他页面的上拉加载也跟着触发

- 原因：vant中的列表组件加载更多是通过监听页面滚动距离而触发，所以在加载更多歌曲的同时其他页面也会触发上拉加载事件

- 解决方式：如果当前tab组件索引为当前页面则执行上拉加载事件

  ```javascript
  // 上拉加载更多单曲
  handlePullingUp () {
    // 加载时判断当前滚动的页面是否为该页面，因为其他页面在上拉加载时会干扰该页面
    if (this.searchCurrentIndex === 1) {
      if (this.song.isNull) { // 没有结果了
        this.finished = true
        return
      }
      setTimeout(async () => {
        if (this.song.songList.length >= this.song.songCount) {
          this.finished = true
        } else {
          await this.getSearchSong()
        }
        this.loading = false
      }, 500)
    } else {
      this.loading = false
    }
  }
  ```

  ​
