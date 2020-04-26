<template>
  <div class="card">
    <p>{{ value }}</p>
    <div class="form">
      <input
        placeholder="ユーザーネーム"
        type="text"
        v-model="name"
        v-if="value === '新規登録'"
      />
      <input
        placeholder="プロフィール"
        type="text"
        v-model="profile"
        v-if="value === '新規登録'"
      />
      <input type="email" v-model="email" placeholder="メールアドレス" />
      <input type="password" v-model="password" placeholder="パスワード" />
      <button @click="auth">{{ value }}</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["value"],
  data() {
    return {
      name: "",
      profile: "",
      email: "",
      password: "",
    };
  },
  methods: {
    auth() {
      if (this.value == "新規登録") {
        axios
          .post("https://secret-earth-28647.herokuapp.com/register", {
            name: this.name,
            profile: this.profile,
            email: this.email,
            password: this.password,
          })
          .then((response) => {
            console.log(response);
            this.$router.replace("/");
          })
          .catch((error) => {
            alert(error);
          });
      } else {
        this.$store.dispatch("login", {
          email: this.email,
          password: this.password,
        });
      }
    },
  },
};
</script>

<style scoped>
button {
  width: 100px;
  text-align: center;
  padding: 8px 0 10px;
  color: #fff;
  background-color: #5419da;
  border-radius: 25px;
  cursor: pointer;
}
.card {
  margin: 100px auto;
  width: 350px;
  background: #fff;
  border-radius: 5px;
  padding: 20px;
}
.card p {
  color: #000;
  font-weight: bold;
  text-align: center;
}
input {
  margin-top: 15px;
  width: 80%;
  border-radius: 10px;
  padding: 10px;
  border: 1px solid #000;
  color: #000;
  outline: none;
}
.form {
  text-align: center;
}
.form button {
  margin-top: 15px;
}

@media screen and (max-width: 480px) {
  .card {
    margin: 100px auto;
    width: 80%;
  }
}
</style>
