# 项目结构

```json
├─babel.config.js

├─package-lock.json

├─package.json

├─postcss.config.js

├─README.md

├─vue.config.js

├─src

|  ├─App.vue

|  ├─main-dev.js         		   -----开发环境入口文件

|  ├─main-prod.js                   -----生产环境入口文件

|  ├─views				          -----视图

|  |   ├─AppIndex.vue              -----app登录首页

|  |   ├─Home.vue                  -----首页

|  |   ├─User.vue        		  -----个人首页

|  |   ├─appIndex      

|  |   |    ├─FindPassword.vue      -----找回密码

|  |   |    ├─Index.vue             -----登录首页

|  |   |    ├─Login.vue             -----登录

|  |   |    └Register.vue           -----注册

|  ├─store                          -----存放全局数据

|  |   ├─actions.js               

|  |   ├─getters.js

|  |   ├─index.js

|  |   ├─mutations.js

|  |   ├─state.js

|  |   ├─moduls

|  |   |   ├─user                   -----用户数据

|  |   |   |  ├─actions.js

|  |   |   |  ├─mutations.js

|  |   |   |  └state.js

|  |   |   ├─singer                 -----歌手数据

|  |   |   |   ├─mutations.js

|  |   |   |   └state.js

|  |   |   ├─search                 -----搜索数据

|  |   |   |   ├─mutations.js

|  |   |   |   └state.js

|  |   |   ├─player                 -----播放器数据

|  |   |   |   ├─actions.js

|  |   |   |   ├─getters.js

|  |   |   |   ├─mutations.js

|  |   |   |   └state.js

|  ├─router                         -----配置路由跳转

|  |   └index.js

|  ├─plugins                        -----配置插件

|  |    ├─vant.js

|  |    └vueLazyLoad.js

|  ├─components                     -----存放组件

|  |     ├─user                     -----用户组件

|  |     |  ├─Edit.vue			   -----用户编辑

|  |     |  ├─MyFollow.vue          -----我的关注

|  |     |  ├─MyLike.vue		   -----我的最爱

|  |     |  ├─PlayRanking.vue       -----听歌排行

|  |     |  ├─Recommend.vue         -----每日推荐

|  |     |  ├─edit                  -----用户编辑

|  |     |  |  ├─EditNickname.vue   -----修改昵称

|  |     |  |  └EditPassword.vue    -----修改密码

|  |     ├─home                     -----首页

|  |     |  ├─Header.vue            -----页面头部（头部搜索）

|  |     |  ├─Section.vue           -----导航栏nav

|  |     |  ├─video                 -----存放视频相关组件

|  |     |  |   ├─Video.vue         -----视频播放器

|  |     |  |   ├─VideoInfo.vue     -----视频详情

|  |     |  |   ├─VideoItem.vue     -----视频列表项

|  |     |  |   └VideoList.vue      -----视频列表

|  |     |  ├─songSheet             -----存放歌单相关组件

|  |     |  |     ├─SongSheetDisc.vue    -----歌单详情

|  |     |  |     ├─SongSheetItem.vue    -----歌单列表项

|  |     |  |     ├─SongSheetList.vue    -----歌单列表
-
|  |     |  |     ├─SongSheetSquare.vue  ----歌单广场

|  |     |  |     ├─SongSheetSquare      -----存放歌单广场相关组件

|  |     |  |     |        └SongSheetSquareSwiper.vue   -----歌单广场轮播组件

|  |     |  |     ├─songSheetMini         -----歌单列表（列表样式小）

|  |     |  |     |       ├─SongSheetMiniItem.vue   -----歌单列表项

|  |     |  |     |       └SongSheetMiniList.vue    -----歌单列表

|  |     |  ├─song                        -----存放歌曲相关组件

|  |     |  |  ├─SongComment.vue          -----歌曲评论

|  |     |  |  ├─SongItem.vue             -----歌曲列表项

|  |     |  |  ├─SongList.vue             -----歌曲列表

|  |     |  |  └SongSwiper.vue            -----歌曲轮播

|  |     |  ├─singer                      -----存放歌手相关组件

|  |     |  |   ├─Singer.vue              -----歌手父组件

|  |     |  |   ├─SingerInfo.vue          -----歌手详情

|  |     |  |   ├─SingerItem.vue          -----歌手列表项

|  |     |  |   ├─singerIntroduce.vue     -----歌手简介

|  |     |  |   ├─singerInfo              -----存放歌手详情相关组件

|  |     |  |   |     ├─SingerAlbum.vue   -----歌手专辑

|  |     |  |   |     ├─SingerDetail.vue  -----歌手简介

|  |     |  |   |     ├─SingerMV.vue      -----歌手mv

|  |     |  |   |     ├─SingerSong.vue    -----歌手单曲

|  |     |  |   |     ├─SingerSynopsis.vue  -----歌手展示

|  |     |  |   |     ├─singerMV          -----存放歌手mv相关组件

|  |     |  |   |     |    ├─MvItem.vue   -----mv列表项

|  |     |  |   |     |    └MvList.vue    -----mv列表

|  |     |  |   ├─album                   -----存放专辑相关组件

|  |     |  |   |   ├─AlbumInfo.vue       -----专辑详情

|  |     |  |   |   ├─AlbumComment.vue    -----专辑评论

|  |     |  ├─section                     

|  |     |  |    ├─NavBar.vue             -----首页导航栏

|  |     |  ├─search                      -----存放搜索相关组件

|  |     |  |   ├─Search.vue              -----搜索一级路由（父组件）

|  |     |  |   ├─SearchBox.vue           -----搜索一级路由信息

|  |     |  |   ├─SearchList.vue          -----搜索列表

|  |     |  |   ├─SearchResult.vue        -----搜索结果（二级路由）

|  |     |  |   ├─searchResult            -----存放搜索结果相关组件

|  |     |  |   |      ├─Album.vue        -----搜索专辑

|  |     |  |   |      ├─Comprehensive.vue  -----综合搜索

|  |     |  |   |      ├─Singer.vue       -----搜索歌手

|  |     |  |   |      ├─Song.vue         -----搜索歌曲

|  |     |  |   |      ├─SongSheet.vue    -----搜索歌单

|  |     |  |   |      ├─Video.vue        -----搜索视频

|  |     |  |   |      ├─comprehensive    -----存放综合搜索相关内容

|  |     |  |   |      |       ├─SearchAlbum.vue          -----专辑

|  |     |  |   |      |       ├─SearchSimQuery.vue       -----相关查询

|  |     |  |   |      |       ├─SearchSinger.vue         -----歌手

|  |     |  |   |      |       ├─SearchSong.vue			 -----歌曲

|  |     |  |   |      |       ├─SearchSongSheet.vue      -----歌单

|  |     |  |   |      |       └SearchVideo.vue           -----视频

|  |     |  ├─recommend								   -----存放导航栏推荐页相关组件

|  |     |  |     ├─Recommend.vue					    -----推荐（父组件）			

|  |     |  |     └RecommendSwiper.vue 					-----推荐轮播组件

|  |     |  ├─ranking								   -----存放导航栏排行页相关组件

|  |     |  |    ├─List.vue							    -----排行列表

|  |     |  |    ├─OfficialList.vue						-----官方排行列表

|  |     |  |    └Ranking.vue						   -----排行（父组件）

|  |     |  ├─playList								  -----存放播放列表相关组件

|  |     |  |    ├─PlayList.vue						   -----播放列表

|  |     |  |    ├─section							   -----播放列表主体

|  |     |  |    |    └Section.vue						

|  |     |  |    ├─header							  -----播放列表头部

|  |     |  |    |   └Header.vue

|  |     |  ├─header								-----存放首页头部搜索组件

|  |     |  |   └HeaderSearch.vue

|  |     |  ├─comment								-----存放评论组件

|  |     |  |    ├─CommentItem.vue					 -----评论列表项

|  |     |  |    └CommentList.vue					 -----评论列表

|  |     ├─common									-----存放通用组件

|  |     |   ├─Button.vue							-----按钮

|  |     |   ├─Follow.vue							-----收藏

|  |     |   ├─Loading.vue							-----加载

|  |     |   ├─NoResult.vue							-----空结果

|  |     |   ├─OverlayImage.vue						-----遮罩层图片

|  |     |   ├─PlayAll.vue							-----播放全部

|  |     |   ├─Player.vue							-----播放器

|  |     |   ├─Position.vue							-----定位

|  |     |   ├─Scroll.vue							-----封装better-scroll

|  |     |   ├─SingerPopup.vue						-----歌手弹出层

|  |     |   ├─Title.vue							-----标题

|  |     |   ├─video								-----存放视频列表相关组件（用于搜索视频，相关视频）

|  |     |   |   ├─VideoItem.vue					 -----视频列表项

|  |     |   |   └VideoList.vue						-----视频列表

|  |     |   ├─singer_desc							-----存放歌手列表相关组件（用于搜索结果处）

|  |     |   |      ├─SingerItem.vue				 -----歌手列表项

|  |     |   |      └SingerList.vue					-----歌手列表

|  |     |   ├─play									存放播放器相关组件

|  |     |   |  ├─FullScreenPlay.vue				-----全屏播放器

|  |     |   |  ├─MiniPlay.vue						-----迷你播放器

|  |     |   |  ├─section							-----播放器主体

|  |     |   |  |    └Section.vue

|  |     |   |  ├─header							-----播放器头部

|  |     |   |  |   └Header.vue

|  |     |   |  ├─footer							-----播放器底部

|  |     |   |  |   ├─Footer.vue

|  |     |   |  |   ├─play							

|  |     |   |  |   |  ├─PlayController.vue			-----控件

|  |     |   |  |   |  ├─PlayFunction.vue			-----功能

|  |     |   |  |   |  └PlayProgress.vue			-----进度条

|  |     |   ├─miniSwiper						   -----存放迷你轮播组件

|  |     |   |     ├─MiniSwiper.vue

|  |     |   |     └MiniSwiperItem.vue

|  |     |   ├─img								 -----图片

|  |     |   |  └Image.vue

|  |     |   ├─album						     -----存放专辑列表相关组件

|  |     |   |   ├─AlbumItem.vue				  -----专辑列表项

|  |     |   |   └AlbumList.vue					 -----专辑列表

|  ├─axios									   -----请求处理

|  |   |api.config.js

|  |   └request.js	

|  ├─assets

|  |   ├─images								  -----存放所需要的图片

|  |   |   ├─cover-bg.svg

|  |   |   ├─digital-album.svg

|  |   |   ├─loading.svg

|  |   |   ├─logo.png

|  |   |   └logoIndex.png

|  |   ├─common							-----存放通用文件

|  |   |   ├─stylus						-----存放stylus样式

|  |   |   |   ├─global.styl			-----通用样式

|  |   |   |   ├─index.styl				-----整合所有stylus文件

|  |   |   |   ├─reset.styl				-----默认样式重置 

|  |   |   |   └variable.styl			-----项目中需要用到的变量、函数

|  |   |   ├─js		

|  |   |   | ├─album.js					-----专辑类

|  |   |   | ├─albumDetail.js			-----专辑详情类

|  |   |   | ├─area.js					-----邮政编码

|  |   |   | ├─config.js				-----配置文件

|  |   |   | ├─convert.js				-----vue filter

|  |   |   | ├─dom.js					-----封装dom相关函数

|  |   |   | ├─globalComponents.js		-----全局组件

|  |   |   | ├─localStorage.js			-----封装本地存储

|  |   |   | ├─mixin.js					-----mixin

|  |   |   | ├─singer.js				-----歌手类

|  |   |   | ├─song.js					-----歌曲类

|  |   |   | ├─songSheetDetail.js		-----歌单详情类

|  |   |   | ├─user.js					-----用户类

|  |   |   | ├─utils.js					-----工具

|  |   |   | ├─valid.js					-----表单验证

|  |   |   | ├─video.js					-----视频类

|  |   |   | └videoDetail.js			-----视频详情类

|  |   |   ├─font						-----存放阿里图标

|  |   |   |  ├─iconfont.css

|  |   |   |  ├─iconfont.eot

|  |   |   |  ├─iconfont.js

|  |   |   |  ├─iconfont.json

|  |   |   |  ├─iconfont.svg

|  |   |   |  ├─iconfont.ttf

|  |   |   |  ├─iconfont.woff

|  |   |   |  └iconfont.woff2

|  ├─api								-----存放api接口

|  |  ├─config.js						-----请求相关配置

|  |  ├─login.js						-----登录相关api

|  |  ├─ranking.js						-----排行相关api

|  |  ├─recommend.js					-----推荐相关api

|  |  ├─register.js						-----注册相关api

|  |  ├─search.js						-----搜索相关api

|  |  ├─singer.js						-----歌手相关api

|  |  ├─song.js							-----歌曲相关api

|  |  ├─user.js							-----用户相关api

|  |  └video.js							-----视频相关api

├─public

|   ├─index.html

|   └logo.ico
```