# 首页 

 



<img src="./images/index.png" width="300" />

[跳转到该页](http://www.happy6year.com/#/index)

## 核心代码

```markdown
<!-- 操作 -->
<div class="option">
  <router-link to="/appIndex/login"
                tag="div">
  <btn text="登录" />
  </router-link>
  <p>OR</p>
  <!-- 注册 -->
  <router-link to="/appIndex/register"
                tag="div">
  <btn text="注册" />
  </router-link>
  </div>
  <!-- 游客登录 -->
  <div class="visitor-login"
    @click="handleVisitorLogin">
  <a href="JavaScript:;">游客登录</a>
</div>
```



> 通过`<router-link>`进行登录、注册及游客登录的路由跳转