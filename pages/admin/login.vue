<template>
  <el-card
    class="login-card"
    shadow="always"
  >
    <el-form
      :model="controls"
      :rules="rules"
      ref="form"
      @submit.native.prevent="onSubmit"
    >
      <h3 class="mb">Войти в админпанель</h3>

      <el-form-item label="Логин" prop="login">
        <el-input v-model.trim="controls.login"/>
      </el-form-item>

      <div class="mb2">
        <el-form-item label="Пароль" prop="password">
          <el-input
            type="password"
            v-model="controls.password"
          />
        </el-form-item>
      </div>

      <el-form-item class="login-card__button">
        <el-button 
          type="primary" 
          round
          native-type="submit"
          :loading="loading"
        >
          Войти
        </el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
export default {
  layout: 'empty',
  data() {
    return {
      loading: false,
      controls: {
        login: '',
        password: ''
      },
      rules: {
        login: [
          { required: true, message: 'Введите логин', trigger: 'blur' }
        ],
        password: [
          { required: true, message: 'Введите пароль', trigger: 'blur' },
          { min: 6, message: 'Пароль должен быть не менее 6 символов', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate(async valid => {
        if(valid) {
          this.loading = true

          // post querry

          try {
            const formData = {
              login: this.controls.login,
              password: this.controls.password
            }
            // next we do dispatch
            await this.$store.dispatch('auth/login', formData)
            this.$router.push('/admin')
          } catch (e) {
            this.loading = false
          }
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  .login-card {
    width: 350px;

    .login-card__button {
      display: flex;
      justify-content: flex-end;
      align-items: center;
      margin-bottom: 0;
    }
  }
</style>

