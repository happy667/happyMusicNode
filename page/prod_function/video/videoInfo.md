# 视频详情

<img src="./images/videoInfo.png" width="300" />

## 功能介绍

1. 播放视频
2. 全屏播放
3. 视频点赞
4. 视频评论
5. 视频收藏
6. 视频分享
7. 相似视频推荐

## 通用组件video封装

```javascript
<template>
  <div class="video-container"
       ref="container">
    <!-- 播放器区域 -->
    <div class="player"
         ref="player"
         :class="isFullScreen?'full':''"
         @click.stop="handleClickScreen">
      <!-- loading -->
      <loading :loading="videoLoad"
               height="5rem"
               size="1.5rem"
               noValue />
      <div class="cover-image"
           v-if="showCoverImage">
        <img v-lazy="videoParams.coverUrl"
             class="animated fadeIn">
      </div>
      <div class="videoBox"
           ref="videoBox">
        <video :src="videoParams.url"
               class="animated fadeIn"
               preload='metadata'
               ref="video"
               muted
               :id="videoParams.id"
               playsinline=""
               webkit-playsinline=""
               x5-playsinline=""
               x-webkit-airplay
               x5-video-ignore-metadata
               @canplay="handleCanplay"></video>

        <div class="cover-controller"
             ref="coverController">
          <!-- 头部导航 -->
          <transition enter-active-class="animated fadeInDown faster"
                      leave-active-class="animated fadeOutUp faster">

            <div class="top-container"
                 v-if="isClickScreen||isFirstPlay">
              <div class="back"
                   @click.stop="routerBack">
                <van-icon name="arrow-left" />
              </div>
              <div class="title">
                {{videoParams.name}}
              </div>
            </div>
          </transition>
          <!-- 播放按钮 -->
          <template v-if="isFirstPlay">
            <div class="big-btn"
                 v-show="isFirstPlay">
              <van-icon name="play-circle-o" />
            </div>
          </template>
          <template v-else>
            <transition enter-active-class="animated fadeIn faster"
                        leave-active-class="animated fadeOut faster">
              <div class="big-btn"
                   v-show="isClickScreen">
                <van-icon @click.stop="handleTogglePlay"
                          :name="playIcon" />
              </div>
            </transition>
          </template>

          <div class="bottom-controller">
            <template v-if="isFirstPlay">
              <div class="controller-box">
                <div class="play-controller">
                  <div class="play-left">
                    <!-- 播放次数 -->
                    <div class="play-count"
                         v-show="isFirstPlay">
                      <i class="iconfont icon-bofang"></i>
                      {{videoParams.playCount|convertCount}}
                    </div>
                  </div>

                  <div class="play-right">
                    <!-- 播放时长-->
                    <div class="play-time"
                         v-show="isFirstPlay">
                      <i class="iconfont icon-shichang"></i>
                      {{duration|convertTime}}
                    </div>
                  </div>
                </div>
              </div>
            </template>
            <template v-else>
              <transition enter-active-class="animated fadeInUp faster"
                          leave-active-class="animated fadeOutDown faster">
                <div class="controller-box"
                     v-if="isClickScreen">
                  <div class="play-controller">
                    <div class="play-left">
                      <!-- 播放进度-->
                      <div class="play-progress"
                           v-show="isClickScreen">
                        {{currenTime|convertTime}}/{{duration|convertTime}}
                      </div>

                    </div>
                    <div class="play-right">
                      <!-- 全屏-->
                      <div class="full"
                           v-show="isClickScreen"
                           @click.stop="handleFullScreen">
                        <i class="iconfont"
                           :class="fullIcon"></i>
                      </div>
                    </div>
                  </div>
                </div>
              </transition>

            </template>

          </div>
        </div>
      </div>
      <!-- 进度条-->
      <div class="progress"
           :style="progressStyle">
        <van-slider active-color="#FD4979"
                    @input="handleSlideChange"
                    v-model="slideVal">
          <div slot="button"
               v-show="isClickScreen"
               :class="isClickScreen?'button':''">
          </div>
        </van-slider>
      </div>
    </div>
    <slot></slot>
  </div>
</template>
<script>
import 'common/js/convert.js'
import screenfull from 'screenfull'
import { mapMutations, mapState } from 'vuex'
export default {
  props: {
    videoParams: {
      type: Object,
      default: () => { }
    }
  },
  data () {
    return {
      slideVal: 0,
      isFirstPlay: true, // 是否是第一次播放
      isPlay: false, // 是否播放
      isClickScreen: false, // 是否点击了播放器
      currenTime: 0, // 当前播放时长
      videoLoad: true, // video是否加载
      showCoverImage: true, // 是否显示封面
      isFullScreen: false// 是否全屏
    }
  },
  mounted () {
    // 获取播放时长时间
    this.$nextTick(() => {
      this.video = this.$refs.video
      // 关闭静音
      // 静音 告诉谷歌浏览器, 这个视频是安全的, 可以默默播放.
      this.video.muted = false
    })
  },

  computed: {
    ...mapState(['oldVideo', 'playing', 'audio']),
    playIcon () {
      return this.isPlay ? 'pause-circle-o' : 'play-circle-o'
    },
    duration () {
      return this.videoParams.duration / 1000
    },
    fullIcon () {
      return this.isFullScreen ? 'icon-suoxiao' : 'icon-fangda'
    },
    progressStyle () {
      let transform = ''
      // 全屏并且点击屏幕
      if (this.isFullScreen && this.isClickScreen) {
        transform = `translate3d(0,-0.2rem,0)`
      }
      return {
        transform
      }
    }
  },
  watch: {
    currenTime () {
      // 当视频播放完了就初始化
      if (this.currenTime >= this.duration) {
        this.initVideo(this.video)
      }
    },
    isPlay () {
      // 如果有歌曲播放就暂停
      if (this.playing && this.isPlay) {
        this.setPlaying(false)
        this.$nextTick(() => {
          this.audio.pause()
        })
      }
    },
    isFullScreen () {
      if (this.isFullScreen) {
        this.setOpenFullScreenStyle()
        this.$emit('openFullScreen')
      } else {
        this.setCloseFullScreenStyle()
        this.$emit('closeFullScreen')
      }
    }
  },
  methods: {
    ...mapMutations(['setOldVideo', 'setPlaying']),
    // 可以播放
    handleCanplay () {
      setTimeout(() => {
        this.$nextTick(() => {
          this.videoLoad = false
          // 更新时间
          this.updateTime()
          // 如果网络为wifi则自动播放
          let netWork = this.$utils.getNetworkType()
          if (netWork === 'wifi') {
            this.handleClickScreen()// 自动播放
          }
        })

        this.$forceUpdate()// 由于获取推荐视频中触发了多个异步请求,导致页面无法随时更新，需要刷新才可以重新渲染，使用forceUpdate解决这个问题，使他可以重新渲染
      }, 20)
    },
    // 更新时间
    updateTime () {
      this.video.ontimeupdate = () => {
        // 更新滚动条
        let width = (this.video.currentTime / this.duration) * 100
        this.currenTime = this.video.currentTime
        this.slideVal = width
      }
    },
    // 重置视频
    initVideo (video) {
      // 重置播放
      this.currentTime = 0
      this.slideVal = 0
      this.isPlay = false
      this.isClickScreen = false
      this.isFirstPlay = true
      this.showCoverImage = true
      // video.load()
    },
    // 暂停上一个视频
    // pauseOldVideo (obj) {
    //   if (this.oldVideo && this.oldVideo.video) {
    //     if (this !== this.oldVideo) {
    //       this.pauseVideo(obj)
    //     }
    //   }
    // },
    // 暂停视频
    pauseVideo (obj) {
      if (obj.isPlay) {
        obj.isPlay = false
        obj.video.pause()
      }
      obj.isFirstPlay = true
      obj.isClickScreen = false
    },
    // 暂停当前视频
    pauseCurrentVideo () {
      if (this.video) {
        this.pauseVideo(this)
      }
    },
    // 滑动进度条
    handleSlideChange () {
      this.video.currentTime = this.slideVal * this.duration / 100
    },
    // 点击屏幕
    handleToggleScreen () {
      this.isClickScreen = !this.isClickScreen
      this.hideBtn()
    },
    // 隐藏按钮
    hideBtn (waiting = true) {
      if (waiting) {
        if (this.timer) clearTimeout(this.timer)
        this.timer = setTimeout(() => { // 超过三秒如果没有操作就关掉控件
          if (this.isClickScreen) {
            // 判断是否为播放状态,如果是就隐藏
            if (this.isPlay) this.isClickScreen = false
          }
        }, 5000)
      } else {
        if (this.isClickScreen) {
          // 判断是否为播放状态,如果是就隐藏
          if (this.isPlay) this.isClickScreen = false
        }
      }
    },
    // 点击播放暂停
    handleTogglePlay () {
      this.isPlay = !this.isPlay
      if (this.isPlay) {
        this.video.play()
      } else {
        this.video.pause()
      }
      this.hideBtn()
    },
    // 处理点击屏幕
    handleClickScreen () {
      if (this.videoLoad) return
      if (this.isFirstPlay) {
        // 暂停上一次正在播放的video
        // this.pauseOldVideo(this.oldVideo)
        if (this !== this.oldVideo) {
          this.setOldVideo(this)
        }
        // 隐藏封面
        this.showCoverImage = false
        // 将video宽由1px变为100%(因为poster兼容性不好)
        // 设置video样式
        this.setVideoStyle()
        this.isFirstPlay = false
        this.handleTogglePlay()
      } else {
        this.handleToggleScreen()
      }
    },
    // 切换全屏播放
    handleFullScreen () {
      if (!screenfull.isEnabled) { // 如果不允许进入全屏，发出不允许提示
        this.$toast({
          message: '不支持全屏',
          type: 'fail'
        })
      } else {
        if (!this.isFullScreen) {
          this.isFullScreen = true
          this.hideBtn(false)
        } else {
          this.isFullScreen = false
        }
      }
    },
    setVideoStyle () {
      this.$nextTick(() => {
        let video = this.$refs.video
        video.style.width = '100%'
      })
    },
    // 设置打开全屏样式
    setOpenFullScreenStyle () {
      let player = this.$refs.player
      let w = document.documentElement.clientWidth || document.body.clientWidth
      let h = document.documentElement.clientHeight || document.body.clientHeigth
      let cha = Math.abs(h - w) / 2
      player.style.width = h + 'px'
      player.style.height = w + 'px'
      player.style.top = window.scrollY + 'px'
      player.style.transform = 'translate(-' + cha + 'px,' + cha + 'px) rotate(90deg)'
      document.body.style.overflow = 'hidden'
    },
    // 设置关闭全屏样式
    setCloseFullScreenStyle () {
      let player = this.$refs.player
      player.style.width = '100%'
      player.style.height = '5rem'
      player.style.top = 0
      player.style.transform = ''
      document.body.style.overflow = ''
    },
    routerBack () {
      if (this.isFullScreen) {
        this.isFullScreen = false
      } else {
        this.$utils.routerBack()
      }
    }
  }
}
</script>
<style lang="stylus" scoped>
@import '~common/stylus/variable';

.video-container>>>.van-loading {
  position: absolute;
  width: 100%;
  z-index: 90;
  background: $color-common-b;
}

.video-container {
  width: 100%;
  box-shadow: 0 0.05rem 1rem rgba(0, 0, 0, 0.1);
  background: $color-common-background;

  .player {
    position: relative;
    width: 100%;
    height: 5rem;

    &.full {
      position: absolute;
      left: 0;
      top: 0;
      z-index: 999;
    }

    .cover-image {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 10;

      img {
        display: block;
        width: 100%;
        height: 100%;
      }
    }

    .videoBox {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;

      video {
        display: block;
        width: 1px;
        height: 100%;
        object-fit: fill;
        object-position: center center;
      }

      .cover-controller {
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        z-index: 10;

        .big-btn {
          position: absolute;
          top: 50%;
          left: 50%;
          margin-left: -1rem;
          margin-top: -1rem;
          width: 2rem;
          height: 2rem;
          background: rgba(255, 255, 255, 0);
          display: flex;
          align-items: center;
          justify-content: center;

          .van-icon {
            display: block;
            color: #fff;
            font-size: 2rem;
            opacity: 0.7;
          }
        }

        .top-container {
          position: absolute;
          width: 100%;
          top: 0;
          left: 0;
          display: flex;
          height: 1.2rem;
          line-height: 1.2rem;
          color: #fff;
          box-sizing: border-box;

          .back {
            width: 1rem;
            height: 100%;
            margin-right: 0.2rem;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: $font-size-small;
          }

          .title {
            no-wrap();
            font-size: $font-size-smaller;
          }
        }

        .bottom-controller {
          position: absolute;
          width: 100%;
          bottom: 0;
          left: 0;
          padding: 0 0.3rem;
          box-sizing: border-box;

          .controller-box {
            width: 100%;
            height: 1.2rem;
            line-height: 1.2rem;
            box-sizing: border-box;
            transition: all 0.5s;

            .play-controller {
              display: flex;
              justify-content: space-between;
              color: #fff;

              .play-right {
                text-align: center;

                .full {
                  width: 1rem;
                  font-size: $font-size-small;
                }
              }
            }
          }
        }
      }
    }

    .progress {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      z-index: 10;
      transition: all 0.5s;

      .button {
        width: 0.25rem;
        height: 0.25rem;
        border-radius: 50%;
        background: $color-common;
      }
    }
  }
}
</style>
```

## 视频详情页数据获取流程

1. 获取视频url
2. 获取点赞数评论数
3. 获取歌手信息

## 核心代码

```javascript
// 获取视频详情
async getVideoDetail (id) {
  try {
    const { data: res } = await videoApi.getVideoDetail(id)
    if (res.code === ERR_OK) {
      // 获取视频url
      const { data: res2 } = await videoApi.getVideoUrl(id)
      if (res2.code === ERR_OK) {
        // 获取点赞数评论数
        const { data: res3 } = await videoApi.getVideoDetailInfo(id)
        if (res2.code === ERR_OK) {
          // 获取歌手信息
          const { data: res4 } = await singerApi.getSinger(res.data.artistId)
          if (res4.code === ERR_OK) {
            const data = res.data
            let creatorList = []
            let video = new VideoDetail({
              id: data.id,
              coverUrl: data.cover,
              name: data.name,
              playCount: data.playCount,
              subCount: data.subCount,
              commentCount: data.commentCount,
              shareCount: data.shareCount,
              publishTime: data.publishTime,
              desc: data.desc,
              duration: data.duration,
              creatorName: data.artists.map(item => item.name).join('/'),
              creatorList,
              followed: res.subed,
              url: res2.data.url,
              liked: res3.liked,
              likeCount: res3.likedCount,
              artist: { id: res4.artist.id, name: res4.artist.name, avatarUrl: res4.artist.picUrl }
            })
            data.artists.forEach(item => {
              let creator = new Singer({
                id: item.id,
                name: item.name
              })
              creatorList.push(creator)
            })
            this.commentCount = data.commentCount
            this.video = video
            if (!this.video.url) {
              this.$toast.fail('暂无视频资源')
            }
          }
        }
      }
    }
  } catch (e) {
    this.$toast(e.data.message)
    this.$router.replace('/')
  }
}
```

