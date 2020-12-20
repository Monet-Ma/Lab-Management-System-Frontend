<template>
    <a-layout class="login">
        <div class="login-bg-container">
            <img :class="['login-bg', bgBlur ? 'login-bg-focus' : '']" src="../assets/njust.jpg"/>
        </div>
        <a-layout-content>
            <a-card title="统一身份认证" class="login-card">
                <a-form :form="form" @submit="handleSubmit">
                    <a-form-item>
                        <a-input
                            @focus="focusInput"
                            @blur="unfocusInput"
                            v-decorator="['number', { rules: [{ required: true, message: '请输入学号' }] }]"
                            placeholder="学号"
                        >
                            <a-icon slot="prefix" type="user" style="color: rgba(0,0,0,.25)" />
                        </a-input>
                    </a-form-item>
                    <a-form-item>
                        <a-input
                            @focus="focusInput"
                            @blur="unfocusInput"
                            v-decorator="['password', { rules: [{ required: true, message: '请输入密码' }] }]"
                            placeholder="密码"
                        >
                            <a-icon slot="prefix" type="lock" style="color: rgba(0,0,0,.25)" />
                        </a-input>
                    </a-form-item>
                    <a-form-item>
                        <a-checkbox style="float: left"
                            v-decorator="[
                            'remember',
                            {
                                valuePropName: 'checked',
                                initialValue: true,
                            },
                            ]"
                        >
                            记住我
                        </a-checkbox>
                        <a-radio-group style="float: right" default-value="student" @change="handleRoleChange">
                            <a-radio-button value="student">
                            学生
                            </a-radio-button>
                            <a-radio-button value="teacher">
                            教师
                            </a-radio-button>
                            <a-radio-button value="admin">
                            管理员
                            </a-radio-button>
                        </a-radio-group>
                        <a-button type="primary" html-type="submit" style="width: 100%">
                            登录
                        </a-button>
                    </a-form-item>
                </a-form>
            </a-card>
        </a-layout-content>
    </a-layout>
</template>

<script>

export default {
  name: 'Login',
  components: {},
  data() {
      return {
        bgBlur: false,
        form: this.$form.createForm(this, { name: 'coordinated' }),
      }
  },
  methods: {
      handleSubmit(e) {
      e.preventDefault();
      this.form.validateFields((err, values) => {

      });
    },

    focusInput(e) {
        this.bgBlur = true;
    },
    
    unfocusInput(e) {
        this.bgBlur = false;
    }
  }
}
</script>
<style scoped>
.login {
    height: 90vh;
    align-items: center;
}

.login-card {
    border-radius: 10px;
}

.login-bg-container {
    height: 90vh;
    width: 100%;
    position: absolute;
}

.login-bg {
    width: 100%;
    height: 100%;
    object-fit: cover;

    transition: 1s cubic-bezier(.19,.64,.08,.99);
}

.login-bg-focus {
    filter: blur(10px);
    object-position: 0% 0%;
}

.login-card {
    width: 400px;
    top: 50%;
    transform: translateY(-50%);
    opacity: 0.8;
    backdrop-filter: blur(10px);
}
</style>
