# 个人中心

**功能介绍**

1. 我的关注
2. 我的最爱
3. 每日推荐
4. 听歌排行
5. 收藏的专辑
6. 收藏的歌单
7. 收藏的视频
8. 修改密码
9. 修改用户信息
10. 注销登录

## 效果图

<img src="./images/userInfo.png" width="300" />

## 我的关注

> 查看用户关注的歌手

<img src="./images/myFollow.png" width="300" />

## 我的最爱

> 查看用户收藏的歌曲

<img src="./images/myLike.png" width="300" />

## 每日推荐

> 查看每日的歌曲、歌单推荐列表

<img src="./images/userRecommend.png" width="300" />

## 听歌排行

> 

> 获取用户听歌记录排行

<img src="./images/playRanking.png" width="300" />

## 用户编辑

> 更改用户信息

<img src="./images/edit.png" width="300" />

## 修改密码

> 修改账户密码

<img src="./images/editPassword.png" width="300" />

## 退出登录

> 退出登录

**业务流程**

- 清空vuex中用户所有信息
- 移除localStroage中的token
- 跳转到个人首页

**退出后效果图**

<img src="./images/logout.png" width="300" />

**核心代码**

```javascript
// 退出登录
logout () {
  this.$utils.alertConfirm({ message: '确定要退出登录吗', confirmButtonText: '退出' }).then(() => {
    loginApi.logout().then(res => {
      if (res.data.code === ERR_OK) {
        // 清空用户所有信息
        clearItem(USER_TOKEN)
        this.setLoginUser(null)
        this.setUserLikeList(null)
        this.setToken(null)
        // 添加不缓存路由
        this.$store.commit('setAddNoCacheComponents', 'user')
        this.$router.replace('/user')// 跳转到个人首页
      }
    })
  }).catch(() => { })
}
```

