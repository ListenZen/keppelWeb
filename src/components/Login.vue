<template>
  <el-dialog title="登录" :visible.sync="dialogFormVisible" width="20%" center>
    <el-form :model="form" class="login" :label-position="formLabelPosition">
      <el-form-item label="用户名:" :label-width="formLabelWidth">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="密码:" :label-width="formLabelWidth">
        <el-input v-model="form.password"></el-input>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button type="primary" @click="login">登 录</el-button>
    </div>
  </el-dialog>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      dialogFormVisible: true,
      formLabelWidth: '80px',
      formLabelPosition: 'left',
      form: {
        name: '',
        password: ''
      }
    }
  },
  methods: {
    login () {
      this.$axios.post('http://127.0.0.1:8080/account/login', {
        name: this.form.name,
        password: this.form.password
      }).then(result => {
        if (result.data !== 'success') {
          this.$message.error('用户名或密码错误')
        } else {
          this.$router.push({ path: 'home' })
        }
      })
    }
  }
}
</script>

<style scoped>
.login {

}
</style>
