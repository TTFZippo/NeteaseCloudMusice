<!-- 登录方式选择页 -->
<template>
  <div class="content-wrapper">
    <main class="top-container">
      <div class="left">
        <img src="../../../assets/images/phone.png" alt="">
        <button class="login-phone"  @click="gotoDialogPage($event, 'login_phone')">手机号登录</button>
        <button class="signup"  @click="gotoDialogPage($event, 'signup')">注&nbsp;册</button>
      </div>
      <ul class="other-options">
        <li>
          <img src="../../../assets/images/wechat.png" alt="">
          <a href="https://music.163.com/api/sns/authorize?snsType=10&clientType=web2&callbackType=Login&forcelogin=true" @click="verifyChecked">微信登录</a>
        </li>
        <li>
          <img src="../../../assets/images/qq.png" alt="">
          <a href="https://music.163.com/api/sns/authorize?snsType=5&clientType=web2&callbackType=Login&forcelogin=true" @click="verifyChecked">QQ登录</a>
        </li>
        <li>
          <img src="../../../assets/images/sina.png" alt="">
          <a href="https://music.163.com/api/sns/authorize?snsType=2&clientType=web2&callbackType=Login&forcelogin=true" @click="verifyChecked">微博登录</a>
        </li>
        <li>
          <img src="../../../assets/images/netease.png" alt="">
          <a href="javascript:;" @click="gotoDialogPage($event, 'login_email')">网易邮箱账号登录</a>
        </li>
      </ul>
    </main>
    <footer class="footer">
      <div class="protocols">
        <input v-model="isChecked" type="checkbox">
        <span>同意</span>
        <a href="http://st.music.163.com/official-terms/service">《服务条款》</a>
        <a href="http://st.music.163.com/official-terms/service">《隐私政策》</a>
        <a href="http://st.music.163.com/official-terms/service">《儿童隐私政策》</a>
      </div>

      <!-- 底部二维码 -->
      <div class="qrcode" @click="gotoDialogPage($event, 'login_qrcode')">
        <img src="../../../assets/images/qrcode_bottom.png" alt="">
      </div>
    </footer>
    <!-- 提示同意协议拟态框 -->
    <my-modal :isShow="isModalShow" @finished="resetModalShow"></my-modal>
  </div>
</template>

<script>
import modal from '../../../components/modal'
import {mapMutations} from 'vuex'
export default {
  components: {
    'my-modal': modal
  },
  data () {
    return {
      isChecked: false,
      isModalShow: false
    }
  },
  methods: {
    ...mapMutations(['changeDialogState']),
    // 重新将isModalShow置false
    resetModalShow() {
      this.isModalShow = false;
    },
    // 验证是否同意协议
    verifyChecked(event) {
      if(!this.isChecked) {
        event.preventDefault();
        this.isModalShow = true;
        return false;
      }
      return true;
    },
    // 验证是否同意协议并跳转dailog页面
    gotoDialogPage(event, next) {
      if(!this.verifyChecked(event)) return;
      this.changeDialogState(next);
    }
  }
}

</script>

<style scoped>
.content-wrapper a{
  text-decoration: none;
  font-size: 12px;
}
.top-container {
  padding: 30px 8% 0 8%; 
  display: flex;
}
.top-container .left {
  display: flex;
  flex-direction: column;
  justify-content: space-between; 
  border-right: 1px solid rgba(0, 0, 0, .1);
  height: 220px;
}
.top-container .left img,
.top-container .left button{
  outline: none;
  width: 80%;
}
.top-container .left button {
  border-radius: 3px;
  border: 2px solid rgba(0, 0, 0, .1);
  height: 32px;
  font-size: 12px;
}
.top-container .left .login-phone {
  background-image: linear-gradient(180deg, rgb(94, 163, 227), rgb(30, 111, 191));
  border: 1px solid rgba(0, 0, 0, .1);
  outline: none;
  color: white;
  cursor: pointer;
  letter-spacing: 2px;
}
.top-container .left .login-phone:hover {
  background-image: linear-gradient(180deg, rgb(94, 163, 227), rgb(52, 131, 206));
}
.top-container .left .signup {
  cursor: pointer;
  background-image: linear-gradient(180deg, rgb(254, 254, 254), rgb(241, 241, 241));
  text-align: center;
}
.top-container .left .signup:hover {
  background-image: linear-gradient(180deg, rgb(255, 255, 255), rgb(249, 249, 249));
}

/* 其他登录选项部分 */
.other-options {
  padding-left: 5%;
  width: 35%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  list-style: none;
  height: 220px;
  
}
.other-options img{
  width: 40px;
  margin-right: 10px;
  vertical-align: middle;
}
.other-options a {
  color: black;
}
.footer {
  padding-left: 8%;
}

/* 政策条款 */
.protocols {
  font-size: 12px;
}
.protocols input {
  vertical-align: middle;
}
.protocols a {
  color: #507DAF;
}
.protocols a:hover {
  text-decoration: underline;
}

.qrcode {
  float: right;
  cursor: pointer;
}
.qrcode img{
  width: 50px;
}
</style>
