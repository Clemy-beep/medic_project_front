<template>
  <div class="hello">
    <h3>Login</h3>
    <form method="post" @submit.prevent="handleSubmit">
      <label for="username">Username</label>
      <input
        type="text"
        name="username"
        id="username"
        v-model="user.username"
        required
      />
      <label for="password">Password</label>
      <input
        type="password"
        name="password"
        id=""
        v-model="user.password"
        required
      />
      <input type="submit" value="Login" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  methods: {
    async handleSubmit() {
      await axios({
        method: "post",
        url: "https://apidoctor.quidam.re/api/login_check",
        data: {
          username: this.user.username,
          password: this.user.password,
        },
      })
        .then((res) => {
          if (res.data.token) {
            sessionStorage.setItem("token", res.data.token);
            this.$router.push("/consultations");
          }
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },

  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

label {
  display: block;
  color: #42b983;
  margin: 0.5em;
}

form {
  margin: 2em;
}

input[type="text"],
input[type="password"] {
  height: 44px;
  border: 1px solid #42b983;
  border-radius: 8px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

input[type="submit"] {
  padding: 0.3em;
  margin-top: 2em;
  height: 44px;
  border: none;
  background-color: #42b983;
  border-radius: 8px;
  width: 84px;
}
</style>
