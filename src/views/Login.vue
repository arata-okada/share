<template>
  <div>
    <HeaderAuth />
    <Card :value="text" />
  </div>
</template>

<script>
import HeaderAuth from "../components/HeaderAuth";
import Card from "../components/Card";
export default {
  data() {
    return {
      text: "ログイン"
    };
  },
  components: {
    HeaderAuth,
    Card
  }
};
</script>