<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__user-name">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__follower">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "femianjorin11",
        firstName: "Oluwafemi",
        lastName: "Anjorin",
        emial: "femianjorin@rocketmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twotter is Amazing!" },
          { id: 2, content: "Don't forget to Subscribe to Our Channel" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourited Tweet #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

h1 {
  margin: 0;
}

.user-profile__admin-badge {
  background-color: purple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile__twoots-wrapper {
  display: grid;
  grid-gap: 10px;
  width: 80%;
}
</style>