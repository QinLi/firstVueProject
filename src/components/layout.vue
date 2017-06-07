<template>
  <div>
    <div class="app-head">
      <div class="app-head-inner">
        <router-link :to="{path: '/'}">
          <img src="../assets/logo.png" alt="">
        </router-link>
        <div class="head-nav">
          <ul class="nav-list">
            <li>{{username}}</li>
            <li v-if="this.username !== ''" class="nav-pile">|</li>

            <li v-if="this.username !== ''">退出</li>
            <li v-if="this.username !== ''" class="nav-pile">|</li>

            <li v-if="this.username === ''" @click="logClick">登陆</li>
            <li v-if="this.username === ''" class="nav-pile">|</li>

            <li v-if="this.username === ''" @click="regClick">注册</li>
            <li v-if="this.username === ''" class="nav-pile">|</li>

            <li @click="aboutClick">关于</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="app-content">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>

    <div class="app-foot">
      <p>© 2016 fishenal MIT</p>
    </div>

    <my-dialog :is-show="isShowAboutDialog" @on-close="closeDialog('isShowAboutDialog')">
    <p>about</p>
    </my-dialog>


    <my-dialog :is-show="isShowLogDialog" @on-close="closeDialog('isShowLogDialog')">
    <log-form @has-log="onSuccessLog"></log-form>
    </my-dialog>

    <my-dialog :is-show="isShowRegDialog" @on-close="closeDialog('isShowRegDialog')">
    <reg-form></reg-form>
    </my-dialog>

  </div>
</template>

<script>
import Dialog from './dialog'
import LogForm from './logForm'
import RegForm from './regForm'
export default {
  name: 'hello',
  components: {
    MyDialog: Dialog,
    LogForm: LogForm,
    RegForm: RegForm
  },
  data () {
    return {
      isShowAboutDialog: false,
      isShowLogDialog: false,
      isShowRegDialog: false,
      username: ''
    }
  },
  methods: {
    aboutClick: function () {
      this.isShowAboutDialog = true
    },
    logClick: function () {
      this.isShowLogDialog = true
    },
    regClick: function () {
      this.isShowRegDialog = true
    },
    closeDialog: function (attr) {
      this[attr] = false
    },
    onSuccessLog: function (data) {
      this.username = data.username
      this.closeDialog('isShowLogDialog')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background: #f0f2f5;
  font-family: "Helvetica Neue",Helvetica,Arial,"Hiragino Sans GB","Hiragino Sans GB W3","Microsoft YaHei UI","Microsoft YaHei","WenQuanYi Micro Hei",sans-serif;
  font-size: 14px;
  color: #444;
}
.app-head {
  background: #363636;
  color: #b2b2b2;
  height: 90px;
  line-height: 90px;
  width: 100%;
}
.app-head-inner {
  width: 1200px;
  margin: 0 auto;
}
.head-logo {
  float: left;
}
.app-head-inner img {
  width: 50px;
  margin-top: 20px;
}
.head-nav {
  float: right;
}
.head-nav ul {
  overflow: hidden;
}
.head-nav li {
  cursor: pointer;
  float: left;
}
.nav-pile {
  padding: 0 10px;
}
.app-foot {
  text-align: center;
  height: 80px;
  width: 100%;
  line-height: 80px;
  background: #e3e4e8;
  clear: both;
  margin-top: 30px;
}
.button {
  background: #4fc08d;
  color: #fff;
  display: inline-block;
  padding: 10px 20px;
  cursor: pointer;
}
.button:hover {
  background: #4fc08d;
}
.g-form {
font-family:"Microsoft YaHei";
}
.g-form-line {
  padding: 15px 0;
}
.g-form-label {
  width: 100px;
  font-size: 16px;
  display: inline-block;
}
.g-form-input {
  display: inline-block;
}
.g-form-input input {
  height: 30px;
  width: 200px;
  line-height: 30px;
  vertical-align: middle;
  padding: 0 10px;
  border: 1px solid #ccc;
}
.g-form-btn {
  padding-left: 100px;
}
.g-form-error {
  color: red;
  padding-left: 15px;
}
</style>
