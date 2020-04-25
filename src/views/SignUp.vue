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
      text: "新規登録"
    };
  },
  components: {
    HeaderAuth,
    Card
  }
};
</script>