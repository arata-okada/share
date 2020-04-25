<template>
  <div>
    <div v-for="(value, key, index) in shares" :key="index">
      <div class="message">
        <div class="flex">
          <p class="name">{{ value.name }}</p>
          <img class="icon" src="../assets/heart.png" @click="fav(key)" alt />
          <p class="number">{{ value.like.length }}</p>
          <img
            class="icon"
            src="../assets/cross.png"
            @click="del(key)"
            alt
            v-if="path && profile"
          />
          <img
            class="icon detail"
            src="../assets/detail.png"
            @click="
              $router.push({
                path: '/detail/' + value.item.id,
                params: { id: value.item.id },
              })
            "
            alt
            v-if="profile"
          />
        </div>
        <p class="text">{{ value.item.share }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      shares: [],
      path: true,
      profile: true,
    };
  },
  methods: {
    fav(index) {
      let result = this.shares[index].like.some((value) => {
        return value.user_id == this.$store.state.user.id;
      });
      if (result) {
        this.shares[index].like.forEach((element) => {
          if (element.user_id == this.$store.state.user.id) {
            axios
              .delete("https://evening-journey-63012.herokuapp.com//like", {
                data: {
                  shares_id: this.shares[index].item.id,
                  user_id: this.$store.state.user.id,
                },
              })
              .then((response) => {
                console.log(response);
              });
          }
        });
      } else {
        axios
          .post("https://evening-journey-63012.herokuapp.com//like", {
            shares_id: this.shares[index].item.id,
            user_id: this.$store.state.user.id,
          })
          .then((response) => {
            console.log(response);
          });
      }
    },
    del(index) {
      axios
        .delete(
          "https://evening-journey-63012.herokuapp.com//shares/" +
            this.shares[index].item.id
        )
        .then((response) => {
          console.log(response);
        });
    },
    async getShares() {
      let data = [];
      let shares = await axios.get(
        "https://evening-journey-63012.herokuapp.com//shares"
      );
      for (let i = 0; i < shares.data.length; i++) {
        console.log(shares);
        await axios
          .get("HerokuのURL/shares/" + shares.data[i].id)
          .then((response) => {
            if (this.$route.name == "profile") {
              if (response.data.item.user_id == this.$store.state.user.id) {
                data.push(response.data);
              }
            } else if (this.$route.name == "detail") {
              if (response.data.item.id == this.id) {
                data.push(response.data);
              }
            } else {
              data.push(response.data);
            }
          });
      }
      this.shares = data;
    },
  },
  created() {
    if (this.$route.name === "home") {
      this.path = false;
    }
    if (this.$route.name === "detail") {
      this.profile = false;
    }
    this.getShares();
  },
};
</script>

<style scoped>
.flex {
  display: flex;
}
.icon {
  width: 25px;
  height: 25px;
}
.detail {
  margin-left: 50px;
}
.message {
  padding: 20px;
  border-bottom: solid 1px white;
  border-left: solid 1px white;
}
.name {
  font-size: 18px;
  font-weight: bold;
  margin-right: 10px;
}
.text {
  margin-top: 10px;
}
.number {
  margin-left: 10px;
  margin-right: 10px;
}
@media screen and (max-width: 480px) {
  .icon {
    width: 30px;
    height: 30px;
  }
  .text {
    font-size: 10px;
  }
  .message {
    border-left: none;
  }
}
</style>
