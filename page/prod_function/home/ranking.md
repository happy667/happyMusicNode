# 排行榜

 



<img src="./images/ranking.png" width="300"/>

[跳转到该页](http://www.happy6year.com/#/)

## 遇到的问题

##### 1、数据未加载完成，betterscroll已经完成初始化,等数据加载完成时页面会无法滑动

​	解决方式：监听排行列表，调用`betterScroll`的`refresh()`方法进行刷新

```javascript
watch: {
  rankingList () {
    this.refresh()
  }
}
```

```javascript
// 刷新
refresh () {
  this.$refs.ranking_scroll.refresh()
}
```