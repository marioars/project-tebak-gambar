<template>
  <div id="homepage">
    <div class="home">
      <img src="https://media.giphy.com/media/27bK4xfPEEOvAheEgX/giphy.gif" width="200px">
      <h1>whAtS oN yoUr scReeN</h1>
      <div id="userJoin">
        <form @submit.prevent="addUser">
          <label for="name">enter your name</label>
          <br />
          <input v-model="user" type="text" name="name" id="name" placeholder="your name" />
          <br />
          <br />
          <button class="btn btn-dark" type="submit">Submit</button>
        </form>
        <router-link to="/guide"> How to play </router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      user: ""
    };
  },
  methods: {
    addUser() {
      const sound =  require(("../assets/videoplayback_online-audio-converter.com.mp3"));
      if (sound) {
        const audio = new Audio(sound);
        audio.play();
      }
      this.$store.commit("ADD_USER", this.user)
      localStorage.setItem("user", this.user)

      this.$store.dispatch('addPlayer', this.user)
        .then(response => {
          this.$router.push('/game')
        })
        .catch(err => {
          console.log(err)
        })
    }
  }
}
</script>