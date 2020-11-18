<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_user-name">@{{ user.username }}</h1>
      <div class="user-profile_follower">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <button @click="followUser()">Click</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserProfile",
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
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
</style>