<template>
  <div class="login-register">
    <div class="wapper-all">
      <transition name="fade">
        <div class="box-empty" v-if="showLoginRegister">
          <div class="go-in-empty">
            <!--关闭按钮-->
            <!--<div class="close" @click="hideLogin()">-->
            <!--<span>-->
            <!--<svg-icon iconClass="icon-guanbi4"></svg-icon>-->
            <!--</span>-->
            <!--</div>-->
            <!--3种登录共用头部logo-->
            <div class="platform-name">
              <img class="LOGO" src="../../../static/images/logo/logo-1.png" alt="">
              <!--<svg-icon iconClass="icon-logo"></svg-icon>-->
            </div>
            <h1 class="platform-desc">
              <span href="#">{{subText(modeData.subTy)}}</span>知声，发出属于你的声音</h1>
            <!--3种登陆方式-->
            <!--第一种-使用密码登陆方式（手机或邮箱）-->
            <div class="use-password">
              <div class="input-box">

                <div class="com-input">
                  <!--第一种账号密码(手机号或邮箱)-->
                  <input class="input-login" type="text"
                         placeholder="请输入手机号或者邮箱"
                         v-if="modeData.usePassword.activePassword"
                         v-model="formData.usePassword.phoneOrEmail"
                  >
                  <!--第二种手机号验证码-->
                  <input class="input-login" type="text"
                         placeholder="输入手机号"
                         v-if="modeData.usePhoneCode.activePhoneCode"
                         v-model="formData.usePhoneSecurityCode.phone"
                  >
                  <!--第三种注册-->
                  <input class="input-login" type="text"
                         placeholder="输入手机号"
                         v-if="modeData.useRegister.activeRegister"
                         v-model="formData.usePhoneCode.phone"

                  >
                </div>
                <!--第二种-->
                <!--验证码图片-->
                <div class="security-code"
                     v-if="formData.usePhoneCode.phone"

                >
                  <div class="code-guide">
                    <span class="guide-left">请点击图中倒立的文字</span>
                    <span class="guide-right">
              <svg-icon iconClass="icon-zhongxin1"></svg-icon>
            </span>
                  </div>
                  <img src="../../../static/images/验证码图/下载.jpg" alt="">
                </div>
                <!--手机号登陆2次及以上出现验证码保证账号安全-->
                <div class="com-input hideCode"
                     v-if="modeData.usePhoneCode.activePhoneCode"
                     :class="{'showCode':modeData.usePhoneCode.showSecurityCode}"
                >
                  <!--第一种-->
                  <input class="input-login" type="password"
                         placeholder="验证码"
                         v-if="modeData.usePhoneCode.activePhoneCode"
                  >

                  <!--第一种-->
                  <span class="input-svg"
                        v-if="modeData.usePhoneCode.activePhoneCode"
                  >
                <img class="vali-code" src="../../../static/images/验证码图/code.jpg" alt="">
              </span>
                </div>
                <div class="com-input">
                  <!--第一种-->
                  <input class="input-login" type="password"
                         placeholder="输入密码"
                         v-if="modeData.usePassword.activePassword"
                         v-model="formData.usePassword.password"
                  >
                  <!--第二种-->
                  <input class="input-login" type="text"
                         placeholder="输入6位短信验证码"
                         v-if="modeData.usePhoneCode.activePhoneCode"
                         v-model="formData.usePhoneSecurityCode.securityCode"
                  >
                  <!--第三种注册-->
                  <input class="input-login" type="text"
                         placeholder="输入6位短信验证码"
                         v-if="modeData.useRegister.activeRegister"
                         v-model="formData.usePhoneCode.securityCode"
                  >
                  <!--第一种-->
                  <span class="input-svg"
                        v-if="modeData.usePassword.activePassword"

                  >
                <svg-icon iconClass="icon-mimabukejian"></svg-icon>
              </span>
                  <!--第二种-->
                  <div class="getPhoneCodeBtn"
                       v-if="modeData.usePhoneCode.activePhoneCode"
                  >
                <span
                  @click="repeatClick()"
                >获取短信验证码</span>
                  </div>
                  <!--第三种注册-->
                  <div class="getPhoneCodeBtn"
                       v-if="modeData.useRegister.activeRegister"
                  >
                <span
                  @click="repeatClick()"
                >获取短信验证码</span>
                  </div>
                </div>
                <!--密码登陆2次及以上出现验证码保证账号安全-->
                <div class="com-input" v-if="modeData.usePassword.activePassword">
                  <!--第一种-->
                  <input class="input-login" type="text"
                         placeholder="验证码"
                         v-if="modeData.usePassword.activePassword"
                         v-model="formData.usePassword.securityCode"
                  >

                  <!--第一种-->
                  <span class="input-svg"
                        v-if="modeData.usePassword.activePassword"
                  >
                <img class="vali-code" src="../../../static/images/验证码图/code.jpg" alt="">
              </span>
                </div>

              </div>

              <!--手机号登陆-忘记密码 按钮-->
              <div class="btn-group">
                <!--第一种-->
                <span class="btn-left"
                      v-if="modeData.usePassword.activePassword"
                      @click="changeShow('pc')"
                >手机验证码登录</span>
                <!--第二种-->
                <span class="btn-left"
                      v-if="modeData.usePhoneCode.activePhoneCode"
                      @click="changeShow('pw')"
                >密码登录(手机号或邮箱)</span>
                <!--第一种-->
                <span class="btn-right"
                      v-if="modeData.usePassword.activePassword"
                >忘记密码?</span>
                <!--第二种-->
                <span class="btn-right"
                      v-if="modeData.usePhoneCode.activePhoneCode"
                >接收语音验证码</span>
              </div>
            </div>
            <!--第3种-使用注册登陆方式-->
            <div class="use-register">

            </div>

            <!--提交登陆按钮-->
            <div class="submit-btn" @click="subBtn(modeData.subTy)">{{subText(modeData.subTy)}}</div>
            <!--注册的footer-tip-->
            <div class="footer-tip">

              <!--登录结构-->
              <div class="login-status" v-if="!modeData.useRegister.activeRegister">
                <!--没有账号？注册-->
                <div class="account-status">

                  <!--第一二种-->
                  <span
                    v-if="!modeData.useRegister.activeRegister"
                  >没有账号？
                  <a href="javascript:;"
                     @click="changeShow('rg')"
                  >注册</a></span>
                  <!--第三种-->
                  <span
                    v-if="modeData.useRegister.activeRegister"
                  >已有账号？<a href="javascript:;">登录</a></span>
                </div>
                <!--第三方登陆-->
                <div class="third-party-empty">
              <span class="third-party-btn"
                    @click="changeShow('sp')"
                    v-if="!modeData.useSocialPlatform.activeSocialPlatform"
              >第三方社交账号登陆</span>
                  <!--点击展开第三方平台-->
                  <div class="show-third-party"
                       v-if="modeData.useSocialPlatform.activeSocialPlatform"
                  >
                    <div class="item-list">
                  <span class="item">
                    <svg-icon iconClass="icon-weixin2"></svg-icon>
                  </span>
                      <span class="item">
                    <svg-icon iconClass="icon-github5"></svg-icon>
                  </span>
                      <span class="item">
                    <svg-icon iconClass="icon-weiboheibai"></svg-icon>
                  </span>
                      <span class="item">
                    <svg-icon iconClass="icon-icon28"></svg-icon>
                  </span>
                    </div>
                  </div>
                </div>
              </div>
              <!--注册结构-->
              <div class="register-status" v-if="modeData.useRegister.activeRegister">
              <span class="register-tip">
                注册即代表同意
                <a href="#">《知声协议》</a>
                <a href="#">《隐私保护指引》</a>
              </span>
                <!--已有账号？登录-->
                <div class="hasAccount">
                  已有账号?
                  <a href="#"
                     @click="changeShow('pw')"
                  >登录</a>
                </div>
              </div>
            </div>


          </div>
        </div>
      </transition>
      <!--选择技术领域标签-->
      <transition name="fade">
        <technology-label v-if="showTeLa"></technology-label>
      </transition>
    </div>
  </div>
</template>

<script>
  // import '@/common/ship.css'
  import selectBox from '../../components/Select-Box/Select-Box.vue'
  import technologyLabel from './technologyLabel'
  import _mm from '@/util/mm.js'

  export default {
    name: "login-register",
    data() {
      return {
        showLoginRegister: true,  //控制登录注册隐藏
        showTeLa: false,    //控制标签隐藏
        formData: {
          //手机号或者邮箱登录(密码)
          usePassword: {
            phoneOrEmail: '',
            password: '',
            securityCode: ''
          },
          //手机号验证码登录
          usePhoneSecurityCode: {
            phone: '',
            securityCode: ''
          },
          //注册
          usePhoneCode: {
            phone: '',
            securityCode: '',
          }
        },
        modeData: {
          //判断提交是<<手机号或者邮箱登录(lg)>><<手机验证码登录lgCode>>还是注册(rg)方式
          subTy: 'lg',
          subText: {
            login: '登录',
            register: '注册'
          },
          usePassword: {
            activePassword: true,
          },
          usePhoneCode: {
            activePhoneCode: false,
            clickCount: 0,
            //多点出现验证码框
            showSecurityCode: false
          },
          useRegister: {
            activeRegister: false
          },
          //使用第三方社交平台登录
          useSocialPlatform: {
            activeSocialPlatform: false
          }
        }
      }
    },
    props: {
      toGo: {
        type: String
      }
    },
    computed: {
      subText() {
        return function (val) {
          if (val === 'lg' || val === 'lgCode') {
            return this.modeData.subText.login;
          }
          return this.modeData.subText.register;
        }
      }
    },
    mounted() {
      if (this.toGo === 'lg') {
        this.$set(this.modeData, 'subTy', 'lg');
        this.changeShow('pw');
      } else {
        this.$set(this.modeData, 'subTy', 're');
        this.changeShow('rg')
      }
    },
    components: {
      selectBox,
      technologyLabel
    },

    methods: {
      //  登录/注册提交事件
      subBtn(typ) {
        if (typ === 'lg') {
          // 手机号邮箱登陆(密码)
          if (!_mm.validate(this.formData.usePassword.phoneOrEmail, 'phone') && !_mm.validate(this.formData.usePassword.phoneOrEmail, 'email')) {
            this.$error('请输入正确的手机号或者邮箱');
            return;
          }
          if (!_mm.validate(this.formData.usePassword.password, 'password')) {
            this.$error('请输入大于等于6位的密码');
            return;
          }
          if (!_mm.validate(this.formData.usePassword.securityCode, 'require')) {
            this.$error('验证码错误');
            return;
          }
          this.$error('辛苦了,老铁', '#0084ff')
        } else if (typ === 'lgCode') {
          //手机号验证码登录
          if (!_mm.validate(this.formData.usePhoneSecurityCode.phone, 'phone')) {
            this.$error('请输入正确的手机号');
            return;
          }
          if (!this.formData.usePhoneSecurityCode.securityCode || !(this.formData.usePhoneSecurityCode.securityCode.length === 6)) {
            this.$error('请输入正确验证码')
            return;
          }
          this.$error('都没问题了', '#0084ff')
        } else if (typ === 'rg') {
          //注册
          if (!_mm.validate(this.formData.usePhoneCode.phone, 'phone')) {
            this.$error('请输入正确的手机号');
            return;
          }
          if (!this.formData.usePhoneCode.securityCode || !(this.formData.usePhoneCode.securityCode.length === 6)) {
            this.$error('请输入正确验证码')
            return;
          }
          this.$error('没错误,可以走了', '#0084ff');
          setTimeout(() => {
            this.showTeLa = true;
          }, 2000)

        }

      },
      hideLogin() {
        this.$emit('toGoMe')
      },
      changeShow(who) {
        if (who === 'pc') {
          //手机验证码登录
          this.$set(this.modeData, 'subTy', 'lgCode');
          this.$set(this.modeData.usePassword, 'activePassword', false);
          this.$set(this.modeData.usePhoneCode, 'activePhoneCode', true);
          this.$set(this.modeData.useRegister, 'activeRegister', false)
        } else if (who === 'pw') {
          //手机号或邮箱登录
          this.$set(this.modeData, 'subTy', 'lg');
          this.$set(this.modeData.useRegister, 'activeRegister', false);
          this.$set(this.modeData.usePassword, 'activePassword', true);
          this.$set(this.modeData.usePhoneCode, 'activePhoneCode', false)
        } else if (who === 'sp') {
          //社交账号登录
          this.$set(this.modeData.useSocialPlatform, 'activeSocialPlatform', true)
        } else if (who === 'rg') {
          //注册
          this.$set(this.modeData, 'subTy', 'rg');
          this.$set(this.modeData.usePassword, 'activePassword', false);
          this.$set(this.modeData.usePhoneCode, 'activePhoneCode', false);
          this.$set(this.modeData.useRegister, 'activeRegister', true)
        }
      },
      //第二种(重复点击获取验证码出现的验证码框)
      repeatClick() {
        if (this.modeData.usePhoneCode.clickCount >= 1) {
          this.$set(this.modeData.usePhoneCode, 'showSecurityCode', true);
          return;
        }
        this.modeData.usePhoneCode.clickCount++;
      }
    }
  }
</script>

<style lang="stylus" scoped>
  @import '~@/common/stylus/mixins.styl'
  .fade-enter-active, .fade-leave-active {
    transition: opacity .4s;
  }

  /* 定义进入动画的初始状态*/
  .fade-enter {
    opacity: 0
  }

  /* 定义进入动画的结束状态*/
  .fade-enter-to {
    opacity: 1
  }

  /* 定义离开动画的初始状态*/
  .fade-leave {
    opacity: 1
  }

  /* 定义离开动画的结束状态*/
  .fade-leave-to {
    opacity: 0
  }

  .login-register
    width: 100%
    height: 100%
    background-image url("../../../static/images/register-login/bg3.jpg")

    .wapper-all
      background: #000

      .bg
        img
          width: 100%
          height: 100%
          position: absolute
          top: 0
          left: 0

      .box-empty
        clearFix()
        position: relative

        .go-in-empty
          border-radius .2rem
          /*padding:0 1rem*/
          position: fixed
          top: 50%
          left: 50%
          margin: -244px -215px
          z-index: 101
          width: 430px
          /*height:500px*/
          background: #fff
          /*padding-bottom 2rem*/
          padding: 2.2rem 2rem 1.8rem
          font-size: 14px;
          box-sizing border-box

          .close
            position: absolute
            top 1rem
            right -3.4rem
            z-index 101
            cursor: pointer;

            .svg-icon
              font-size 1.4rem
              fill #ffffff

          .platform-name
            text-align center
            /*background: #ccc*/

            .LOGO
              width: 8rem

            .svg-icon
              font-size 4rem
              fill #0084ff

          .platform-desc
            font-weight normal
            text-align center
            color: #0084ff
            font-size 22px
            margin .8rem 0 0

          /*background: wheat*/
          //第一种-使用密码登陆方式(手机或邮箱)

          .use-password
            .input-box
              margin: 1rem 0 1rem

              .com-input
                padding: 1rem 0
                border-bottom 1px solid #ebebeb
                transition .2s
                /*background: #ccc*/
                clearFix()

                &.hideCode
                  display: none
                  height: 0

                  &.showCode
                    height: auto
                    display: block

                &:not(:first-child)
                  padding-top 1.6rem

                .input-login
                  width: 11rem
                  /*letter-spacing .2rem*/
                  display: inline-block
                  font-size 16px

                .input-svg
                  float: right
                  position: relative
                  cursor: pointer;

                  .svg-icon
                    font-size 1.6rem
                    fill #8590a6

                  .vali-code
                    position: absolute
                    top -.2rem
                    right: 0
                    width: 4.6rem

                .getPhoneCodeBtn
                  float: right
                  cursor: pointer;
                  font-size 16px

                  span
                    color: #175199

                    &:hover
                      color: #77839c

            .security-code
              margin: 0 0 .2rem
              background: #f9f9f9

              img
                display: block
                margin: .4rem auto
                width: 60%
                padding-bottom .6rem

              .code-guide
                padding-top .2rem
                clearFix()

                .guide-left
                  float: left
                  color: #8590a6

                .guide-right
                  cursor: pointer;
                  float: right

            .btn-group
              margin .2rem 0 1.6rem

              /*background: #ccc*/
              clearFix()

              .btn-left
                cursor: pointer;
                float: left
                color: #343d83

              .btn-right
                cursor: pointer;
                float: right
                color: #8590a6

          .submit-btn
            font-size 16px
            cursor: pointer
            width: 100%
            padding: .6rem 0
            background: #0084ff
            text-align center
            color: #ffffff
            border-radius .2rem
            transition .2s

            &:hover
              background: #0060bf

          .footer-tip
            margin-top 1rem
            /*margin-bottom 1rem*/
            color: #8590a6
            width: 100%

            .login-status
              .third-party-empty
                float: right
                position: relative
                /*margin:0 auto*/

                .third-party-btn
                  display: inline-block
                  cursor: pointer;

                  &:hover
                    color: #a68b9a

                .show-third-party
                  position: absolute
                  right: 0
                  top: 0
                  width: 148px
                  /*background: #ccc*/

                  .item-list
                    float: right

                    .item
                      cursor: pointer;
                      display: inline-block
                      /*&:not(:last-child)*/
                      /*margin-left .6rem*/

                      .svg-icon
                        font-size 1.6rem

                        &:hover
                          fill #a68b9a

              .account-status
                float: left

            /*font-size 16px*/

            .register-status
              .register-tip
                font-size 14px

                a
                  color #8590a6

                  &:hover
                    color #6f7990

            .hasAccount
              text-align center
              display: block
              margin-top 1.5rem
              font-size 16px


          /*第二种-使用手机号验证码登陆方式*/

          .use-phone-code
            .input-box
              margin: .4rem 0 1rem

              .com-input
                padding: .6rem 0
                border-bottom 1px solid #ebebeb
                clearFix()

                .input-login
                  width: 15rem
                  /*letter-spacing .2rem*/
                  display: inline-block

                .input-svg
                  float: right

                  .svg-icon
                    fill #8590a6
</style>
