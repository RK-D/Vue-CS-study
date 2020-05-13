/* eslint-disable max-len */
<template>
  <div class="register">
    <b-row class="mt-5">
      <b-col
        md="8"
        offset-md="2"
        lg="6"
        offset-lg="3"
      >
        <b-card title="注册">
          <b-form>
            <b-form-group label="姓名">
              <b-form-input
                v-model="$v.user.name.$model"
                type="text"
                placeholder="请输入昵称"
              ></b-form-input>
            </b-form-group>

            <b-form-group label="手机号">
              <b-form-input
                v-model="$v.user.telephone.$model"
                type="number"
                placeholder="请输入手机号"
                :state="validateState('telephone')"
              ></b-form-input>
              <b-form-invalid-feedback :state="validateState('telephone')">
                手机号不符合要求
              </b-form-invalid-feedback>
              <!-- <b-form-valid-feedback :state="validation">
                手机号正确.
              </b-form-valid-feedback> -->
            </b-form-group>

            <b-form-group label="密码">
              <b-form-input
                v-model="$v.user.password.$model"
                type="password"
                placeholder="请输入密码"
                :state="validateState('password')"
              ></b-form-input>
              <b-form-invalid-feedback :state="validateState('password')">
                密码必须为6~16位
              </b-form-invalid-feedback>
            </b-form-group>

            <b-form-group>
              <b-button
                @click="register "
                variant="outline-primary"
                block=""
              >注册
              </b-button>
            </b-form-group>

          </b-form>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { required, minLength, maxLength } from 'vuelidate/lib/validators';

const telephoneValidator = (value) => /^1[3|4|5|7]\d{9}$/.test(value);

export default {
  data() {
    return {
      user: {
        name: '',
        telephone: '',
        password: '',
      },
      // 此处拼写错误导致 验证不成功
      validations: null,
    };
  },
  validations: {
    user: {
      name: {
        required,
      },
      telephone: {
        required,
        telephone: telephoneValidator,
      },
      password: {
        required,
        minLength: minLength(6),
        maxLength: maxLength(16),
      },
    },
  },
  methods: {
    validateState(name) {
      const { $dirty, $error } = this.$v.user[name];
      return $dirty ? !$error : null;
    },
    register() {
      console.log('register');
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
