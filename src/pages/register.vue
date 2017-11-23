<template>
 	<section id="sign">
		<h1 class="sign-title">注册</h1>
		<div class='sign-form register'>
			<div>
				<img src="../assets/phone.png" id='tel' alt=""><input type="text" name="tel" placeholder="请输入手机号" v-model='phone' @blur='phoneTest(phone)' @focus='hidePhoneWaring()'><span class="warning">{{phoneWarning}}</span>
			</div>
			<div>
				<img src="../assets/pwd.png" alt=""><input id='pwd' type="password" name="pwd" placeholder="请输入密码" v-model='password' @blur='pwdTest(password)' @focus='hidePwdWaring()'><span class="warning">{{pwdWring}}</span>
			</div>
			<div>
				<img src="../assets/pwdRepeate.png" alt="">
				<input id='pwdRepeate' type="password" name="pwdRepeate" placeholder="请再次输入密码" v-model='pwdRepeate' @blur='pwdTest(pwdRepeate)'>
				<span class="warning pwdEqual" v-show='pwdRepeate!=password'>两次密码不一致！</span>
			</div>
			<div>
				<button id="register-submit" @click='signUp'>注册</button><span class="warning prompt">{{loginWrong}}</span>
			</div>
			<div><router-link to='../login' >已有帐号，立即登录</router-link></div>
		</div>
	</section>
</template>

<script>
import { appKey, appId, dev } from "../config/config";

export default {
    name: "register",
    data() {
        return {
            phone: "",
            password: "",
            pwdRepeate: "",
            phoneWarning: "",
            loginWrong: "",
            pwdWring: "",
            phoneChecked: false,
            pwdChecked: false,
            opacity: 1,
            telReg: /^[1][3,4,5,7,8][0-9]{9}$/,
            pwdReg: /^[a-zA-Z]\w{5,17}$/
        };
    },
    methods: {
        // 手机号验证
        phoneTest: function(phone) {
            if (phone == "") {
                this.phoneWarning = "请填写完整";
                this.phoneChecked = false;
            } else {
                if (!this.telReg.test(phone)) {
                    this.phoneWarning = "手机号格式错误";
                    this.phoneChecked = false;
                } else {
                    this.phoneChecked = true;
                }
            }
        },

        // 密码验证
        pwdTest: function(password) {
            if (password == "") {
                this.pwdWring = "请填写完整";
                this.pwdChecked = false;
            } else {
                if (!this.pwdReg.test(password)) {
                    this.pwdWring = "密码格式错误";
                    this.pwdChecked = false;
                } else {
                    this.pwdChecked = true;
                }
            }
        },
        // 聚焦时清除警告
        hidePhoneWaring: function() {
            this.phoneWarning = "";
            this.loginWrong = "";
        },
        hidePwdWaring: function() {
            this.pwdWring = "";
            this.loginWrong = "";
        },
        // 注册
        signUp: function() {
            if (
                this.password == "" ||
                this.phone == "" ||
                this.pwdRepeate == ""
            ) {
                this.loginWrong = "* 请填写完整！";
                this.flashingWarning();
            } else if (
                this.phoneChecked &&
                this.pwdChecked &&
                this.password.trim() == this.pwdRepeate.trim()
            ) {
                this.$http
                    .post(
                        "https://baas.qingful.com/2.0/class/public/table/user/add",
                        {
                            phone: this.phone.trim(),
                            password: this.password.trim()
                        },
                        {
                            headers: {
                                "Content-Type": "application/json",
                                "x-qingful-appid": appId,
                                "x-qingful-dev": dev,
                                "x-qingful-appkey": appKey
                            }
                        }
                    )
                    .then(
                        function(res) {
                            // 跳转登录
                            this.$router.push({ path: "/login" });
                        },
                        function(err) {
                            console.log("获取数据失败");
                        }
                    );
            } else {
                this.flashingWarning();
            }
        },
        // 闪烁警告
        flashingWarning: function() {
            const spans = document.querySelectorAll("span");
            let i = 0,
                timer;

            clearInterval(timer);
            timer = setInterval(function() {
                var toggle = i++ % 2 ? "0" : "1";
                spans.forEach(function(span) {
                    span.style.opacity = toggle;
                });
                i > 4 && clearInterval(timer);
            }, 80);
        }
    }
};
</script>


<style scoped>
a {
    text-decoration: none;
    color: rgba(175, 47, 47, 0.3);
}

#sign {
    width: 460px;
    margin: 0 auto;
}

.sign-title {
    text-align: center;
    color: rgba(175, 47, 47, 0.15);
    font-size: 50px;
    margin: 75px 0 80px 0;
    font-weight: 100;
}

.sign-form {
    background: #fff;
    width: 100%;
    padding-bottom: 20px;
    border: 1px solid #f5f5f5;
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6,
        0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6,
        0 17px 2px -6px rgba(0, 0, 0, 0.2);
}

.sign-form div {
    width: 380px;
    height: 45px;
    margin: 0 auto;
    border: 1px solid #ededed;
    position: relative;
}

.sign-form div input {
    display: block;
    height: 100%;
    width: 100%;
    border: 0;
    outline: medium;
    color: #4d4d4d;
    font-size: 16px;
    text-indent: 35px;
    -webkit-text-rendering: optimizeLegibility;
    -moz-text-rendering: optimizeLegibility;
    text-rendering: optimizeLegibility;
}

.sign-form div input::-webkit-input-placeholder {
    font-weight: 300;
    color: #e6e6e6;
}

.sign-form div input::-moz-placeholder {
    font-weight: 300;
    color: #e6e6e6;
}

.sign-form div input::input-placeholder {
    font-weight: 300;
    color: #e6e6e6;
}

.sign-form div a:hover {
    color: rgba(175, 47, 47, 0.6);
}

.sign-form div img {
    position: absolute;
    top: 0;
    left: 8px;
    bottom: 0;
    margin: auto;
    width: 15px;
    height: 20px;
}

.sign-form div button {
    width: 100%;
    height: 100%;
    border: 0;
    outline: medium;
    cursor: pointer;
    background: rgba(175, 47, 47, 0.3);
    color: #fff;
    text-align: center;
    line-height: 50px;
    font-size: 18px;
    border-radius: 5px;
}

.sign-form div button:hover {
    background: rgba(175, 47, 47, 0.6);
}

.sign-form div:nth-child(1) {
    margin-top: 36px;
}

.sign-form div:last-child {
    text-align: right;
    font-size: 12px;
    line-height: 40px;
    border: none;
}

.warning {
    position: absolute;
    display: block;
    height: 100%;
    right: 5px;
    top: 0;
    color: rgba(175, 47, 47, 0.3);
    line-height: 50px;
    font-size: 14px;
}

.prompt {
    top: -45px;
    font-size: 12px;
    left: 0;
    right: 0;
}

/* 注册私有 */

.register div:nth-child(2) {
    margin: 30px auto;
}

.register div:nth-child(4) {
    margin-top: 40px;
    border: none;
}

/* 登录私有 */

.login div:nth-child(2) {
    margin-top: 30px;
}

.login div:nth-child(3) {
    margin-top: 40px;
    border: none;
}
</style>
