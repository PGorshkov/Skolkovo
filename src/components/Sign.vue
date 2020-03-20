<template>
  <section class="sign">
    <el-card shadow="always">
      <div slot="header">
        <h2 class="sign__title">Представьтесь</h2>
      </div>
      <el-form ref="form" :model="user" :rules="rules" @submit.native.prevent="submitForm">
        <el-form-item prop="name">
          <el-input v-model="user.name" placeholder="Укажите Ваше имя"/>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm">Войти</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </section>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'sign',
  data: () => ({
    user: {
      id: `u${(+new Date).toString(16)}`,
      name: null
    },
    rules: {
      name: [
        { required: true, message: 'Укажите имя', trigger: 'blur'},
        { min: 3, max: 10, message: 'Символов должно быть от 3 до 10', trigger: 'blur'}
      ]
    }
  }),
  methods: {
    ...mapActions(['sendAuth']),
    submitForm() {
      this.$refs['form'].validate((valid) => {
        if (valid) {
          this.sendAuth(this.user)
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .sign{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 100vh;
    &__title{
      margin: 0;
      font-size: 20px;
      font-weight: bold;
    }
  }
</style>
