<!--  -->
<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">{{ isLogin ? "Sign in" : "Sign up"}}</h1>
          <p class="text-xs-center">
            <nuxt-link v-if="isLogin" to="/register">Need an account?</nuxt-link>
            <nuxt-link v-else to="/login">Have an account?</nuxt-link>
          </p>

          <ul class="error-messages">
            <li>That email is already taken</li>
          </ul>

          <form @submit.prevent="onSubmit">
            <fieldset v-if="isLogin" class="form-group">
              <input class="form-control form-control-lg" type="text" placeholder="Your Name" />
            </fieldset>
            <fieldset class="form-group">
              <input
                v-model="user.email"
                class="form-control form-control-lg"
                type="text"
                placeholder="Email"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                v-model="user.password"
                class="form-control form-control-lg"
                type="password"
                placeholder="Password"
              />
            </fieldset>
            <button
              class="btn btn-lg btn-primary pull-xs-right"
            >{{ isLogin ? "Sign in" : "Sign up"}}</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import request from "@/utils/request";
export default {
  name: "Login",
  components: {},
  data() {
    return {
      user: {
        email: "",
        password: "",
      },
    };
  },
  computed: {
    isLogin() {
      return this.$route.name === "login";
    },
  },
  methods: {
    async onSubmit() {
      const { data } = await request({
        method: "post",
        url: "/api/users/login",
        data: {
          user: this.user,
        },
      });

      console.log(data);
    },
  },
};
</script>
<style>
</style>