<template>
  <div>
    <div class="left-padding">
      <img src="../assets/logo.png" alt class="logo" />
      <div class="flex icon-field" @click="$router.push('/home')">
        <img src="../assets/home.png" alt class="icon" />
        <p>ホーム</p>
      </div>
      <div class="flex icon-field" @click="$router.push('/profile')">
        <img src="../assets/profile.png" alt class="icon" />
        <p>プロフィール</p>
      </div>
      <div class="flex icon-field" @click="$router.dispatch('logout')">
        <img src="../assets/logout.png" alt class="icon" />
        <p>ログアウト</p>
      </div>
    </div>
    <hr />
    <ShareMessage />
  </div>
</template>

<script>
import ShareMessage from "../components/ShareMessage";
export default {
  components: {
    ShareMessage
  }
};
</script>

<style scoped>
.left-padding {
  margin: 20px;
}
.logo {
  width: 100px;
}
.icon-field {
  margin-top: 15px;
  cursor: pointer;
}
.icon-field p {
  font-size: 16px;
  padding-left: 15px;
}
.icon {
  width: 25px;
  height: 25px;
}
.flex {
  display: flex;
}
@media screen and (max-width: 480px) {
  .logo {
    width: 150px;
  }
  .icon {
    width: 30px;
    height: 30px;
  }
}
</style>