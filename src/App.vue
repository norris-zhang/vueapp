<template>
  <div id="app">
    <nav>
      <div class="navigation__logo">
        Twotter
      </div>
      <div class="navigation__user" v-if="user">
        {{ user.username }}
      </div>
    </nav>
    <router-view />
  </div>
  <Loader />
</template>

<script>
import { useStore } from 'vuex';
import { computed } from 'vue';
import Loader from "@/components/Loader";

export default {
  name: "App",
  components: {
    Loader
  },
  setup() {
    const store = useStore();
    const user = computed(() => store.state.User.user);

    return {
      user
    };
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin: 0;
  padding: 0;
  background-color: #f3f5fa;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: deeppink;
    color: white;

    .navigation__loop {
      font-weight: bold;
      font-size: 24px;
    }

    .navigation__user {
      font-weight: bold;
    }
  }
}
</style>
