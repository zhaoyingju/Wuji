<template lang="jade">

    el-dialog(title="忘记密码", v-model="isShowDialog", :close-on-click-modal="false", :close-on-press-escape="false", @close="closeDialog")
        el-steps( :active="step", :center="true", :align-center="true")
            el-step(title="输入邮箱")
            el-step(title="设置新密码")
            el-step(title="设置成功")
        div.step-container
            div.step(v-show="step===1")
                div.tip 输入注册登录的邮箱地址，并点击下一步，你的邮箱将收到验证码。
                el-input.input(v-model="yEmail", placeholder="请输入邮箱", auto-complete="on", :autofocus="true")
                    el-button(slot="append", type="danger", @click="doNext") 下一步
            div.step(v-show="step===2")
                el-input.input(v-model="code", placeholder="请输入验证码")
                el-input.input(v-model="pwd", type="password", placeholder="输入新密码")
                el-input.input(v-model="repwd", type="password", placeholder="请输确认密码")
                el-button.save-btn(type="primary", @click="doSave") 保存
                el-button.prev-btn(:plain="true", @click="prev") 上一步
                div.tip *收不到验证码请检查邮箱的垃圾箱哦～
            div.step.svg-step(v-show="step===3", :class="{ active: isActive }")
                <svg t="1491578820882" class="icon-svg" style="" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="9059" xmlns:xlink="http://www.w3.org/1999/xlink" width="80" height="80"><path d="M512.006144 1019.902976c-0.043008 0-0.083968 0-0.126976 0-68.690944-0.016384-135.341056-13.4912-198.09792-40.052736-60.60032-25.648128-115.01568-62.352384-161.733632-109.09184S68.651008 769.586176 43.031552 708.972544C16.499712 646.204416 3.054592 579.54816 3.072 510.856192c0.016384-68.690944 13.492224-135.340032 40.05376-198.09792 25.649152-60.60032 62.353408-115.01568 109.092864-161.733632 46.74048-46.718976 101.173248-83.397632 161.784832-109.017088C376.730624 15.494144 443.350016 2.048 511.992832 2.048c0.04608 0 0.080896 0 0.126976 0 68.690944 0.016384 135.340032 13.492224 198.096896 40.05376 60.60032 25.649152 115.014656 62.353408 161.732608 109.093888s83.396608 101.172224 109.017088 161.785856c26.530816 62.769152 39.974912 129.425408 39.958528 198.116352-0.022528 95.492096-26.653696 188.572672-77.01504 269.180928l-52.10624-32.553984c44.25728-70.839296 67.6608-152.66816 67.68128-236.642304 0.01536-60.423168-11.798528-119.026688-35.111936-174.180352-22.523904-53.28896-54.781952-101.15584-95.879168-142.271488-41.096192-41.116672-88.947712-73.397248-142.225408-95.946752C631.126016 75.343872 572.52864 63.502336 512.105472 63.488c-0.036864 0-0.074752 0-0.111616 0-60.38528 0-118.949888 11.812864-174.06976 35.111936-53.287936 22.523904-101.154816 54.782976-142.271488 95.879168-41.116672 41.097216-73.397248 88.948736-95.946752 142.226432C76.366848 391.849984 64.526336 450.44736 64.512 510.871552c-0.014336 60.423168 11.798528 119.026688 35.111936 174.180352 22.523904 53.28896 54.782976 101.154816 95.879168 142.272512 41.096192 41.115648 88.948736 73.396224 142.226432 95.944704 55.143424 23.339008 113.7408 35.17952 174.164992 35.193856 0.034816 0 0.077824 0 0.111616 0 51.145728 0 101.280768-8.548352 149.03296-25.408512 46.186496-16.309248 89.196544-40.031232 127.837184-70.506496l38.047744 48.24064c-43.942912 34.659328-92.87168 61.641728-145.42848 80.19968C627.160064 1010.174976 570.134528 1019.902976 512.006144 1019.902976z" p-id="9060"></path><path d="M765.62432 106.51648" p-id="9061"></path><path d="M765.62432 106.51648" p-id="9062"></path><path d="M764.032 105.522176" p-id="9063"></path><path d="M765.62432 106.51648" p-id="9064"></path><path d="M764.032 105.522176" p-id="9065"></path><path d="M765.62432 106.51648" p-id="9066"></path><path d="M764.032 106.51648" p-id="9067"></path><path d="M224.538624 518.239232l65.235968-52.860928 130.543616 96.318464c0 0 180.251648-186.474496 354.28352-273.492992l24.858624 28.00128c0 0-217.521152 180.256768-329.399296 419.591168L224.538624 518.239232 224.538624 518.239232zM224.538624 518.239232" p-id="9068"></path></svg>
                div.success-tip
                    div 修改密码成功！ ~^o^~ 
                    div 马上登录，<a href="javascript:void(0);" @click="next">GO!</a>
</template>

<script>
import Vue from 'vue'
import { mapState, mapActions } from 'vuex'
import { Steps, Step, Dialog, Input, Button, Message} from 'element-ui'
import Validator from 'utils/validator'
// 引入组件
Vue.use(Dialog)
Vue.use(Steps)
Vue.use(Step)
Vue.use(Input)
Vue.use(Button)
export default {
    name: 'forgetpwd',
    props: {
    },
    data () {
        return {
            step: 1,
            yEmail: '', //需要从cookie或是storeage中获取过去邮箱
            code: '',
            pwd: '',
            repwd: '',
            isActive: false
        }
    },
    computed: {
        ...mapState({
            isShowDialog: state => state.account.isShowForgetPwdDialog
        })
    },
    watch: {
        step(val){
            if(val === 3){
                //由于transition对于display:none不起作用，因此需要做一下延时
                setTimeout(() => { this.isActive = true }, 20);
            }
        }
    },
    methods:{
        ...mapActions([
          'changeForgetPwdDialogStatus'
        ]),
        closeDialog(){
            this.reset();
            this.changeForgetPwdDialogStatus({status:false});
        },
        step1Valid(){
            let validator = new Validator();
            const errorMsg = validator.add(this.yEmail, [
                {strategy: 'isNotEmpty', errorMsg:'邮箱不能为空！'},
                {strategy: 'emailFormat', errorMsg:'邮箱格式错误了！'}
            ]).start();
            validator = null;
            return errorMsg;
        },
        doNext(){
            const errorMsg = this.step1Valid();
            if(errorMsg){
                return Message({ message: errorMsg, type: 'error', duration: 2000 });
            }
            //异步操作
            //...
            this.next();
        },
        step2Valid(){
            let validator = new Validator();
            const errorMsg = validator.add(this.code, [
                {strategy: 'isNotEmpty', errorMsg:'验证码不为空！'}
            ]).add(this.pwd, [
                {strategy: 'isNotEmpty', errorMsg:'新密码不为空！'}
            ]).add(this.repwd, [
                {strategy: 'isNotEmpty', errorMsg:'确认密码不为空！'},
                {strategy: 'confirmPwd:' + this.pwd, errorMsg:'前后密码要一致！'}
            ]).start();
            validator = null;
            return errorMsg;
        },
        doSave(){
            const errorMsg = this.step2Valid();
            if(errorMsg){
                return Message({ message: errorMsg, type: 'error', duration: 2000 });
            }
            //异步操作
            //...
            this.next();
        },
        next(){
            if (this.step++ > 2){
                this.reset();
                this.changeForgetPwdDialogStatus({status:false});
            }
        },
        reset(){
            this.step = 1;
            this.yEmail = ''; //可从cookie或是storeage中获取最新邮箱
            this.code = '';
            this.pwd = '';
            this.repwd = '';
            this.isActive = false;
        },
        prev(){
            this.step--;
        }
    },
    components: {
    }
}
</script>
<style lang="sass">
    @import "../../public/scss/_variables.scss";
    @import "../../public/scss/_mixins.scss";
    .svg-step{
        text-align: center;
        path{
            stroke: $main;
            stroke-width: 20px;
            fill: $white;
            stroke-dasharray: 8000px;
            stroke-dashoffset: 8000px;
            transition: stroke-dashoffset cubic-bezier(0.44, 0.01, 0.55, 0.96) 2s;
        }
        .success-tip, svg{
            display: inline-block;
        }
        .success-tip{
            vertical-align: top;
            text-align: left;
            margin-left: 30px;
            margin-top: 21px;
            opacity: 0;
            transition: opacity .2s cubic-bezier(0.44, 0.01, 0.55, 0.96) .6s;
        }

        &.active{
            path{
                stroke-dashoffset: 0px;
            }
            .success-tip{
                opacity: 1;
            }
        }
    }
    .el-dialog{
        min-width: 560px;
    }
    .step-container{
        .step{
            width: 70%;
            margin: auto;
            padding: 40px 0;
            .tip{
                margin: 10px 0 15px 0;
                line-height: 1.2;
                color: #333;
            }
            .save-btn,.prev-btn{
                width: 49.5%;
            }
            .prev-btn{
                margin-left: 1%;
            }
        }
        .input{
            margin-bottom: 20px;
            .el-input__inner{
                border: 1px solid #c0ccda;
                color: #666;
                &:focus{
                    border: 1px solid $main;
                }
            }
            .el-input-group__append{
                color: $white;
                background-color: $main;
                border-color: $main;
            }
        }
    }

</style>