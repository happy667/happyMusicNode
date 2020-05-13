# 推荐

 



<img src="images/recommend.png" width="300"/>

> [跳转到该页](http://www.happy6year.com/#/)

> 展示页由轮播图、新歌推送、推荐歌单、新碟上线四个组件组成

> 该页面使用了三个swiper组件，分别是首页轮播、新歌推送、以及新碟上线

## 遇到的问题

##### 1、同一个页面使用多个swiper,如何解决冲突问题？

- 解决方式：为每个swiper添加不同的class，在初始化时通过这个类名来初始化就不会存在冲突了。

##### 2、滑动swiper时会导致导航栏跟着滑动，与vant发生冲突

- 原因：由于事件冒泡的原因，在滑动swiper过程中也触发了vant的tab组件的相应事件。


- 解决方式：再初始化swiper时添加函数`sliderMove()`,使用`e.stopPropagation()`阻止事件传播。


## 核心代码

```javascript
// 初始化轮播图组件
initSwiper () {
  // 通过settimeout 解决数据还没有完全加载的时候就已经渲染swiper，导致loop失效。
  setTimeout(() => {
    // eslint-disable-next-line no-unused-vars
    var mySwiper = new Swiper('.sw-banner', {
      pagination: {
        el: '.swiper-pagination',
        clickable: true
      },
      observer: true, // 修改swiper自己或子元素时，自动初始化swiper
      observeParents: true, // 修改swiper的父元素时，自动初始化swiper
      autoplay: {
        disableOnInteraction: false,
        delay: 5000
      },
      loop: true,
      // 使用图片懒加载
      lazy: {
        loadPrevNext: true,
        loadOnTransitionStart: true,
        loadPrevNextAmount: 1
      },
      on: {
        sliderMove (e) {
          e.stopPropagation()
        }

      }
    })
    }, 0)
}
```



