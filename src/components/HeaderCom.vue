<template>
  <div>
    <el-row>
      <el-col :span="24">
        <ul>
          <li v-if="store.state.NickName == undefined" @click="OpenLogin">
            <el-link :underline="false">ログイン</el-link>
          </li>
          <li v-if="store.state.NickName == undefined" @click="OpenRegister">
            <el-link :underline="false">サインアップ</el-link>
          </li>
          <li v-if="store.state.NickName != undefined"> 
            <el-link :underline="false">{{store.state.NickName}}</el-link>
          </li>
          <li v-if="store.state.NickName != undefined">
            <el-link :underline="false" href="/personcenter">マイページ</el-link>
          </li>
          <li v-if="store.state.NickName != undefined" @click="LogOut">
            <el-link :underline="false">ログアウト</el-link>
          </li>
        </ul>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="8">
        <el-link :underline="false" href="/">
          <el-image
            style="width: 200px; height: 100px"
            src="/images/zhaoxi_logo.png"
            fit="contain"
          />
        </el-link>
      </el-col>
      <el-col :span="8">
        <el-input
          class="w-50 m-2"
          style="margin-top: 30px"
          size="large"
          placeholder="商品搜索"
          :suffix-icon="Search"
        />
      </el-col>
      <el-col :span="8">
        <div class="service-item">
          <a id="header-chat" href="javascript:void(0);">
            <span class="icon icon-headset"></span>
            <span class="service-item-info">在线客服</span>
          </a>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="18">
        <el-menu :default-active="activeIndex" class="el-menu-header" mode="horizontal" router>
          <el-menu-item index="/">首页</el-menu-item>
          <el-menu-item index="/loveflower">爱情鲜花</el-menu-item>
          <el-menu-item index="/birthdayflower">生日鲜花</el-menu-item>
          <el-menu-item index="/friendflower">友情鲜花</el-menu-item>
          <el-menu-item index="/weddingflower">婚庆鲜花</el-menu-item>
        </el-menu>
      </el-col>
    </el-row>
  </div>
  <LoginCom />
  <RegisterCom />
</template>
<script setup>
import LoginCom from "./LoginCom.vue";
import RegisterCom from "./RegisterCom.vue";
import { useStore } from 'vuex'
const store = useStore()
const OpenLogin = () => {
  store.commit('OpenLogin')
}
const OpenRegister = () => {
  store.commit('OpenRegister')
}
const LogOut=()=>{
  //清理vuex状态 //清理localStorage
  localStorage.removeItem('NickName');
  localStorage.removeItem('token');
  store.commit('SettingNickName', undefined)
}
</script>
<style lang="scss">
ul {
  list-style: none;
  padding-left: 80%;
  li {
    float: left;
    margin-left: 20px;
  }
}
.service-item {
  display: inline-block;
  font-size: 14px;
  color: #71797f;
  vertical-align: top;
  line-height: 47px;
  margin-top: 25px;
  margin-left: -200px;
  a {
    text-decoration: none;
    color: inherit;
  }
  .icon-headset {
    background-position: -34px -102px;
    width: 24px;
    height: 24px;
    margin-top: 12px;
    margin-right: 8px;
    display: inline-block;
    background-image: url(//localhost:8080/images/common_sprite.png);
    background-repeat: no-repeat;
    vertical-align: top;
  }
}
.el-menu-header {
  margin-left: 30% !important;
  border-bottom: 0px !important;
  .el-menu-item {
    width: 170px !important;
  }
}
</style>