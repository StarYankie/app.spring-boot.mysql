<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="register-form">
        <div class="logo-wrapper">
          <img class="logo" src="/static/images/logo.png" />
          <div class="tagline">Open source task management tool</div>
        </div>
        <form @submit.prevent="submitForm">
          <div v-show="errorMessage" class="alert alert-danger failed"> {{ errorMessage }} </div>
          <div class="form-group">
            <input type="text" class="form-control" id="username" v-model= "form.username">
          </div>
          <div class="form-group">
            <input type="email" class="form-control" id ="emailAddress" v-model= "form.emailAddress">
          </div>
          <div class="form-group">
            <input
              type="password"
              class="form-control"
              id="password"
              v-model= "form.password"
            >
          </div>
          <button type="submit" class="btn btn-primary btn-block">
            Create account
          </button>
          <p class="accept-terms text-muted">
            By clicking “Create account”, you agree to our
            <a href="#">terms of service</a> and <a href="#">privacy policy</a>.
          </p>
          <p class="text-center text-muted">
            Already have an account? <a href="/login">Sign in</a>
          </p>
        </form>
      </div>
    </div>
    <footer class="footer">
      <span class="copyright"
        >&copy; 2021 StarYankie ("스프링5와 Vue.js2로 시작하는 모던 웹
        애플리케이션 개발" 실습)</span
      >
      <ul class="footer-links list-inline float-right">
        <li class="list-inline-item"><a href="#">About</a></li>
        <li class="list-inline-item"><a href="#">Terms of Service</a></li>
        <li class="list-inline-item"><a href="#">Privacy Policy</a></li>
        <li class="list-inline-item">
          <a
            href="https://github.com/StarYankie/vuejs.spring-boot.mysql"
            target="_blank"
            >GitHub</a
          >
        </li>
      </ul>
    </footer>
  </div>
</template>

<script>
import registrationService from '@/services/registration'

export default {
  name: 'RegisterPage',
  data: function () {
    return {
      form: {
        username: '',
        emailAddress: '',
        password: ''
      },
      errorMessage: ''
    }
  },
  methods: {
    submitForm () {
      // TODO: 데이터 검증하기
      registrationService.register(this.form).then(() => {
        this.$router.push({ name: 'LoginPage' })
      })
        .catch((error) => {
          this.errorMessage =
          'Failed to register user. Reason: ' +
          (error.message ? error.message : 'Unknown') +
          '.'
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  max-width: 900px;
}
.register-form {
  margin-top: 50px;
  max-width: 320px;
}
.logo-wrapper {
  margin-bottom: 40px;
}
.footer {
  width: 100%;
  line-height: 40px;
  margin-top: 50px;
}
</style>
