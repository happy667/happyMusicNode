# 注册 

 



<img src="./images/register.png" width="300" />

[跳转到该页](http://www.happy6year.com/#/appIndex/register)

## 业务流程图

<img src="./images/注册业务流程图.png" width="450" />

## 核心代码

```javascript
// 注册
handleRegister () {
  if (this.validForm()) { // 验证用户输入
    this.$toast.loading({
      message: '正在注册...',
      duration: 10000,
      forbidClick: true
    })
    this.registerForm.password = this.password1
    // 检查手机号是否已经注册
    registerApi.checkRegister(this.registerForm.phone).then(res => {
      if (res.data.code === ERR_OK) {
        if (res.data.exist !== 1) { // 不存在
          // 检查验证码是否输入正确
          registerApi.checkSms(this.registerForm.phone, this.registerForm.captcha).then(res => {
            if (res.data.code === ERR_OK) {
              // 注册
              registerApi.register(this.registerForm).then(res => {
                console.log(res)
                if (res.data.code === ERR_OK) {
                  this.$toast.clear()
                  this.$utils.alert({
                    message: '注册成功，快去登陆吧'
                  }).then(() => {
                    this.$router.push('/appIndex/login')
                  })
                  // 清空表单
                  this.resetForm()
                }
              })
            } else {
              this.$toast(res.data.message)
            }
          }).catch(res => {
            this.$toast('验证码错误,请发送验证码至您的手机')
          })
        } else {
          this.$toast.clear()
          this.$utils.alert({
            message: '该手机号已经注册'
          })
          // 清空表单
          this.resetForm()
        }
      }
    })
  }
},
  // 发送验证码
  handleSendSms () {
    if (checkIsNull(this.registerForm.phone)) { // 验证手机号是否输入
      this.$toast('手机号不能为空')
    } else if (!checkPhone(this.registerForm.phone)) { // 验证手机号格式
      this.$toast('手机号格式有误')
    } else { // 发送验证码
      registerApi.sendSms(this.registerForm.phone).then(res => {
        if (res.data.code === ERR_OK) {
          this.isDisabled = true
          this.$toast('验证码已发送至您的手机,请注意查收')
          // 恢复按钮状态
          setTimeout(() => {
            this.isDisabled = false
            this.sendText = '发送验证码'
          }, this.time)
        }
      }).catch(() => {
        this.$toast('验证码发送失败')
      })
    }
  }
```
