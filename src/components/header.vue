<template>
<div class="">
<nav class="navbar navbar-expand-md bg-dark navbar-dark fixed-top">
   <a class="navbar-brand" href="#">导航</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#collapsibleNavbar">
      <span class="navbar-toggler-icon"></span>
    </button>
     <div class="collapse navbar-collapse justify-content-center" id="collapsibleNavbar">
    <ul class="navbar-nav">
      <li class="nav-item">
        <a class="nav-link" href="#">主页</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">文章目录</a>
      </li>sada
      <li class="nav-item ">
        <a class="nav-link" href="#">我的关联</a>
      </li> 
       <li class="nav-item ">
        <a class="nav-link" href="#">留言</a>
      </li>    
    </ul>
  </div>  
    <div class="collapse navbar-collapse justify-content-end" id="collapsibleNavbar">
    <ul class="navbar-nav">
      <li class="nav-item">
        <a class="nav-link" href="#"  @click="login" data-toggle="collapse" data-target="#collapsibleNavbar">登录</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#"   @click="reg" data-toggle="collapse" data-target="#collapsibleNavbar">注册</a>
      </li>
      <li class="nav-item ">
        <a class="nav-link" href="#">   </a>
      </li>    
    </ul>
  </div> 
</nav>

<transition name = "fade">
  <div class="container-fluid fadebox"  v-if='loginshow' id='loginbox'>
    <span class="row"><h2 class="loginwz">登录</h2> <h2 class="justify-content-end" @click="loginshow=!loginshow">&times;</h2></span>
    <form>
      <div class="form-group">
        <label for="email">账号</label>
        <input type="text" class="form-control" id="username" v-model="luser" placeholder="输入账户">
      </div>
      <div class="form-group">
        <label for="pwd">密码</label>
        <input type="password" class="form-control" id="pwd" v-model="lpass"  placeholder="输入密码">
      </div>
      <div class="form-check">
        <label class="form-check-label">
          <input class="form-check-input" type="checkbox"> 记住我
        </label>
      </div>
      <button type="submit" class="btn btn-primary" @click="loginaction">登录</button>
    </form>
  </div>
</transition>

<transition name = "fade">
  <div class="container-fluid fadebox"  v-if='regshow' id='regbox'>
    <span class="row"><h2 class="loginwz">注册</h2> <h2 class="justify-content-end" @click="regshow=!regshow">&times;</h2></span>
    <form>
      <div class="form-group">
        <label for="email">账号</label>
        <input type="text" class="form-control" id="username" v-model="name" placeholder="输入账户">
      </div>
      <div class="form-group">
        <label for="pwd">密码</label>
        <input type="password" class="form-control" id="lpwd" v-model="password" placeholder="输入密码">
      </div>
       <div class="form-group">
        <label for="pwd">重复密码</label>
        <input type="password" class="form-control" id="rpwd"  v-model="repassword" placeholder="输入密码">
      </div>
      <button type="submit" class="btn btn-primary" @click="regaction">注册</button>
    </form>
  </div>
</transition>

  </div>
</template>

<script>
import { constants } from 'fs';
export default {

  data(){
    return{
      loginshow:false,
      regshow:false,
      name:'',
      password:'',
      repassword:'',
      luser:'',
      lpass:'',

    }
  },
  methods:{
    login(){
      this.loginshow=true;
      this.regshow=false;
    },
    reg(){
      this.regshow=true;
       this.loginshow=false;
    },
    loginaction(){
         
        if(this.luser===''||this.lpass==='')
      {
        alert('请填入用户名和密码！')
        this.password=this.repassword='';
        return
      }
      this.axios.post('http://localhost:8888/api/login',{
        name:this.luser,
        password:this.lpass,
        }).then((res)=>{
          console.log(res.data)
      })


    },


    

    regaction(){
      if(this.password===''||this.repassword===''||this.name==='')
      {
        alert('请填入用户名和密码！')
        this.password=this.repassword='';
        return
      }
      if(this.password!==this.repassword)
      {
        alert('两次密码不一致！')
        this.password=this.repassword='';
        return
      }
      
     let a=this.axios.post('http://localhost:8888/api/reg',{
         name:this.name,
         password:this.password,
       }).then((response) => {

         if(response.data=="200"){
           alert('注册成功！')
           return
         }
         if(response.data=="400"){
           alert('注册失败！')
           return
         }
           if(response.data=="300"){
           alert('用户已经存在！')
           return
         }
      }).catch(()=>{

      })
      console.log(this.name)
    }

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.loginwz{
  margin-left: 1.5rem;
}

.fadebox{
  position: fixed;
  top:30%;
  background-color: rgb(151, 151, 151);
  border-radius: 25px;
  padding: 20px;
  z-index: 99;
}
.fade-enter-active, .fade-leave-active {
    transition:  0.5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active, 2.1.8 版本以下 */ {
    opacity: 0
}

</style>