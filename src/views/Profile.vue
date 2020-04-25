<template>
  <div class="flex" v-if="hoge">
    <div class="left">
      <SideNavi />
    </div>
    <div class="right">
      <div class="title">
        <p>プロフィール</p>
      </div>
      <div class="profile">
        <div class="flex-profile">
          <p class="profile-name">{{ name }}</p>
          <div @click="edit">
            <button>変更する</button>
          </div>
        </div>
        <p class="text" v-if="active">{{ profile }}</p>
        <input type="text" v-model="profile" v-else />
      </div>
      <Message />
    </div>
  </div>

  <div v-else>
    <Header />
    <div class="profile">
      <div class="flex-profile">
        <p class="profile-name">{{ name }}</p>
        <div @click="edit">
          <button>変更する</button>
        </div>
      </div>
      <p class="text" v-if="active">{{ profile }}</p>
      <input type="text" v-model="profile" v-else />
    </div>
    <Message />
    <Footer />
  </div>
</template>

<script>
import axios from "axios";
import Header from "../components/Header";
import Footer from "../components/Footer";
import SideNavi from "../components/SideNavi";
import Message from "../components/Message";
export default {
  data() {
    return {
      active: true,
      name: "太郎",
      profile: "私は太郎です",
      hoge: ""
    };
  },
  methods: {
    edit() {
      if (!this.active) {
        axios
          .put("https://blooming-citadel-39489.herokuapp.com/user", {
            email: this.$store.state.user.email,
            profile: this.profile
          })
          .then(response => {
            this.$store.dispatch("changeUserData", {
              profile: this.profile
            });
            console.log(response);
          });
      }
      this.active = !this.active;
    }
  },
  created() {
    if (screen.width >= 480) {
      this.hoge = true;
    } else {
      this.hoge = false;
    }
  },
  components: {
    SideNavi,
    Header,
    Footer,
    Message
  }
};
</script>

<style scoped>
.left {
  width: 22%;
  height: 100vh;
  border-right: 1px solid white;
}
.right {
  width: 78%;
  height: 100vh;
}
.flex {
  display: flex;
}
.profile {
  padding: 20px;
  border-bottom: solid 1px white;
}
.profile-name {
  font-size: 24px;
}
.title {
  border-bottom: 1px solid white;
}
.title p {
  font-size: 20px;
  font-weight: bold;
  margin: 15px;
}
.flex-profile {
  display: flex;
  justify-content: space-between;
}
button {
  width: 100px;
  text-align: center;
  padding: 8px 0 10px;
  color: #fff;
  background-color: #5419da;
  border-radius: 25px;
  display: block;
  margin: 0 0 0 auto;
}
input {
  color: black;
}
@media screen and (max-width: 480px) {
  button {
    font-size: 10px;
    width: 70px;
    border-radius: 25px;
  }
  .text {
    font-size: 10px;
  }
}
</style>
