# 登录 

 



<img src="./images/login.png" width="300" />

> [跳转到该页](http://www.happy6year.com/#/appIndex/login)

## 业务流程图

<img src="./images/登录业务流程图.png" width="450" />

## 核心代码

```javascript
// 登录
handleLogin () {
  if (this.validForm()) {
    this.$toast.loading({
      message: '登陆中...',
      duration: 10000,
      forbidClick: true
    })
    // 验证成功执行登录操作
    loginApi.login(this.loginForm).then(res => {
      if (res.data.code === ERR_OK) { // 登录成功
        // 保存token信息
        setItem(USER_TOKEN, res.data.token)
        this.setToken(res.data.token)
        this.setLoginUser(res.data.profile)

        if (this.$router.currentRoute.query.redirect) { // 跳回到原来页面
          // 使用replace是为了不保留登录页面历史记录
          this.$router.replace(this.$router.currentRoute.query.redirect)
          this.$router.go(-1)// 这里执行go是为了解决需要返回两次才能回退上一个页面的问题
        } else {
          this.$router.replace('/home')
        }
        this.resetForm()
        this.$toast.clear()
      } else {
        console.log(123)
        this.$toast(res.data.message)
      }
    }).catch(error => {
      this.$toast(error.data.message)
    })
  }
}
```
