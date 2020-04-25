<template>
  <div class="flex" v-if="hoge">
    <div class="left">
      <SideNavi />
    </div>
    <div class="right">
      <div class="title">
        <p>ホーム</p>
      </div>
      <Message />
    </div>
  </div>

  <div v-else>
    <Header />
    <div class="share-message">
      <ShareMessage />
    </div>
    <Message />
    <Footer />
  </div>
</template>

<script>
import SideNavi from "../components/SideNavi";
import Message from "../components/Message";
import Header from "../components/Header";
import Footer from "../components/Footer";
import ShareMessage from "../components/ShareMessage";

export default {
  data() {
    return {
      hoge: ""
    };
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
    Message,
    ShareMessage
  }
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
</style>
