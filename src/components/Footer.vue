<template>
  <div class="footer">
    <img class="icon" src="../assets/home.png" @click="$router.push('/home')" />
    <img
      class="icon"
      src="../assets/profile.png"
      @click="$router.push('/profile')"
    />
    <img
      class="icon"
      src="../assets/logout.png"
      @click="$router.push('/logout')"
    />
  </div>
</template>

<style scoped>
.icon {
  width: 25px;
}
.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  padding-bottom: 15px;
  padding-top: 15px;
  display: flex;
  justify-content: space-around;
  border-top: 1px solid white;
  background-color: #15202b;
}
@media screen and (max-width: 480px) {
  .icon {
    width: 30px;
    height: 30px;
  }
}
</style>
