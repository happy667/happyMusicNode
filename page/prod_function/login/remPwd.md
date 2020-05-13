# 忘记密码 

 



<img src="./images/remPwd.png" width="300" />

[跳转到该页](http://www.happy6year.com/#/appIndex/findPassword)

## 业务流程图

<img src="./images/修改密码业务流程图.png" width="450" />

## 核心代码

```javascript
// 修改
handleUpdate () {
  if (this.validForm()) { // 验证用户输入
    this.$toast.loading({
      message: '修改中...',
      duration: 10000,
      forbidClick: true
    })
    // 检查手机号是否已经注册
    registerApi.checkRegister(this.updateForm.phone).then(res => {
      console.log(res.data)
      if (res.data.code === ERR_OK) {
        if (res.data.exist === 1) { // 存在
          // 检查验证码是否输入正确
          registerApi.checkSms(this.updateForm.phone, this.updateForm.captcha).then(res => {
            console.log(res)
            if (res.data.code === ERR_OK) {
              // 修改
              registerApi.register(this.updateForm).then(res => {
                console.log(res)
                if (res.data.code === ERR_OK) {
                  this.$toast.clear()
                  this.$utils.alert({
                    message: '密码修改成功，快去登陆吧'
                  }).then(() => {
                    this.resetForm()
                    this.$router.push('/appIndex/login')
                  })
                }
              })
            }
          }).catch(error => {
            this.$toast(error.data.message)
          })
        } else {
          this.$toast.clear()
          this.$utils.alert({
            message: '该手机号尚未注册'
          }).then(() => {
            this.$router.push('/appIndex/login')
          })
          // 清空表单
          this.resetForm()
        }
      } else {
        this.$toast(res.data.message)
      }
    }).catch(err => {
      this.$toast(err.data.message)
    })
  }
},
  // 发送验证码
  handleSendSms () {
    if (checkIsNull(this.updateForm.phone)) { // 验证手机号是否输入
      this.$toast('手机号不能为空')
    } else if (!checkPhone(this.updateForm.phone)) { // 验证手机号格式
      this.$toast('手机号格式有误')
    } else { // 发送验证码
      registerApi.sendSms(this.updateForm.phone).then(res => {
        if (res.data.code === ERR_OK) {
          this.isDisabled = true
          this.$toast('验证码已发送至您的手机,请注意查收')
          // 恢复按钮状态
          setTimeout(() => {
            this.isDisabled = false
            this.sendText = '发送验证码'
          }, this.time)
        }
      }).catch(error => {
        this.$toast(error.data.message)
      })
    }
  }
```
