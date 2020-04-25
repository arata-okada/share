<template>
  <div class="flex" v-if="hoge">
    <div class="left">
      <SideNavi />
    </div>
    <div class="right">
      <div class="title">
        <p>ホーム</p>
      </div>
      <Message :id="id" />
      <div class="comment">
        <div class="comment-title">
          <p>コメント</p>
        </div>
        <div class="message" v-for="(comment, index) in data" :key="index">
          <div class="flex">
            <p class="name">{{ comment.comments_user[0].name }}</p>
          </div>
          <div>
            <p class="text">{{ comment.comment.content }}</p>
          </div>
        </div>
        <input type="text" v-model="content" />
        <div @click="send">
          <button>コメント</button>
        </div>
      </div>
    </div>
  </div>

  <div v-else>
    <Header />
    <Message :id="id" />
    <div class="comment">
      <div class="comment-title">
        <p>コメント</p>
      </div>
      <div class="message" v-for="(comment, index) in data" :key="index">
        <div class="flex">
          <p class="name">{{ comment.comments_user[0].name }}</p>
        </div>
        <div>
          <p class="text">{{ comment.comment.content }}</p>
        </div>
      </div>
      <input v-model="content" type="text" />
      <div @click="send">
        <button>コメント</button>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import SideNavi from "../components/SideNavi";
import Header from "../components/Header";
import Footer from "../components/Footer";
import Message from "../components/Message";
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      hoge: "",
      content: "",
      data: "",
    };
  },
  methods: {
    send() {
      axios
        .post("https://evening-journey-63012.herokuapp.com//comments", {
          shares_id: this.id,
          user_id: this.$store.state.user.id,
          content: this.content,
        })
        .then((response) => {
          console.log(response);
          this.content = "";
        });
    },
    comment() {
      axios
        .get("https://evening-journey-63012.herokuapp.com//shares/" + this.id)
        .then((response) => {
          this.data = response.data.comments;
        });
    },
  },
  created() {
    if (screen.width >= 480) {
      this.hoge = true;
    } else {
      this.hoge = false;
    }
    this.comment();
  },
  components: {
    SideNavi,
    Header,
    Footer,
    Message,
  },
};
</script>

<style scoped>
.left {
  width: 22%;
  height: 100vh;
}
.right {
  width: 78%;
  height: 100vh;
}
.flex {
  display: flex;
}
.title {
  border-bottom: 1px solid white;
  border-left: 1px solid white;
  padding: 15px;
}
.title p {
  font-size: 20px;
  font-weight: bold;
}
.share-message {
  border-bottom: 1px solid white;
}
.comment-title {
  text-align: center;
  padding-top: 10px;
  padding-bottom: 10px;
  border-bottom: 1px solid white;
  border-left: 1px solid white;
}
.comment input {
  width: 95%;
  height: 30px;
  margin-top: 20px;
  margin-bottom: 15px;
  margin-left: 10px;
  border-radius: 10px;
  border: 1px solid white;
  background-color: #15202b;
  color: white;
}
.message {
  padding-top: 10px;
  padding-left: 10px;
  padding-bottom: 10px;
  border-bottom: 1px solid white;
  border-left: 1px solid white;
}
.text {
  margin-top: 10px;
  font-size: 10px;
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
@media screen and (max-width: 480px) {
  .comment-title {
    border-left: none;
  }
  .message {
    border-left: none;
  }
  button {
    font-size: 10px;
    width: 70px;
    border-radius: 25px;
  }
}
</style>
