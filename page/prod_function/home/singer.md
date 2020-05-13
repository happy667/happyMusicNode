# 歌手

 



<img src="./images/singer.png" width="300"/>

[跳转到该页 ](http://www.happy6year.com/#/)

> 根据歌手类型、地区对歌手进行分类,点击不同类型获取歌手列表,点击歌手跳转到歌手详情,也可以收藏歌手（需要登录）

## 实现思路

- 根据接口文档定义歌手类型数据，并渲染到分类列表中

  ```javascript
  // 歌手类型
  export const SINGER_TYPE = {
    all: -1,
    maleSinger: 1,
    femaleSinger: 2,
    band: 3
  }
  // 歌手类型列表（带名称）
  export const SINGER_TYPE_LIST = [
    {
      typeId: SINGER_TYPE.all,
      name: '全部'
    },
    {
      typeId: SINGER_TYPE.maleSinger,
      name: '男歌手'
    },
    {
      typeId: SINGER_TYPE.femaleSinger,
      name: '女歌手'
    },
    {
      typeId: SINGER_TYPE.band,
      name: '乐队'
    }
  ]
  // 地区类型
  export const AREA_TYPE = {
    all: -1,
    chinese: 7,
    western: 96,
    japan: 8,
    han: 16,
    other: 0
  }
  // 地区类型列表（带名称）
  export const AREA_TYPE_LIST = [
    {
      typeId: AREA_TYPE.all,
      name: '全部'
    },
    {
      typeId: AREA_TYPE.chinese,
      name: '华语'
    },
    {
      typeId: AREA_TYPE.western,
      name: '欧美'
    },
    {
      typeId: AREA_TYPE.japan,
      name: '日本'
    },
    {
      typeId: AREA_TYPE.han,
      name: '韩国'
    },
    {
      typeId: AREA_TYPE.other,
      name: '其他'
    }
  ]
  ```


- 默认歌手类型为全部、地区类型为全部

  ```javascript
    data () {
      return {
        singerList: [], // 歌手列表
        singerTypeList: SINGER_TYPE_LIST, // 歌手类型列表
        areaTypeList: AREA_TYPE_LIST, // 地区类型列表
        area: AREA_TYPE.all, // 地区类型
        singerType: SINGER_TYPE.all, // 歌手类型
        loadMore: false,
        more: false
      }
    }
  ```

- 点击不同歌手类型或者地区类型传入相应的typeId向后台发起请求

- 传入pullUp属性到betterScroll中实现上拉加载更多歌手

- 每当获取完数据就刷新下betterScroll()

  ```javascript
   watch: {
      loadMore () {
        this.$nextTick(() => {
          this.refresh()
        })
      }
    }
  ```

  ​

