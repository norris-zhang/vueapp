<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ fullname }}</h1>
      <div class="user-profile__admin-badge" v-if="state.followers > 5">Admin</div>
      <div class="user-profile__admin-no-badge" v-else>&nbsp;</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>
      <button @click="followUser">Follow</button>
      <CreateTwootPanel @add-twoot="addTwoot"/>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel";
import { reactive, computed, watch } from 'vue'

export default {
  name: "UserProfile",
  components: { TwootItem, CreateTwootPanel },
  setup() {
    const state = reactive({
      followers: 0,
      user: {
        id: 1,
        username: "nzhang",
        firstName: "Norris",
        lastName: "Zhang",
        email: "nzhang@bravurasolutions.com",
        isAdmin: true,
        twoots: [
          {
            id: 1,
            content:
              "Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime, ea enim, a eligendi saepe consequuntur nihil sapiente nemo eaque necessitatibus unde cumque distinctio atque soluta porro corporis officia. Odio, error!",
          },
          { id: 2, content: "I am not a long text." },
        ],
      }
    });

    const fullname = computed(() => `${state.user.firstName} ${state.user.lastName}`);

    watch(
      () => state.followers,
      (newFollowers, oldFollowers) => {
        if (newFollowers > oldFollowers) {
          console.log(`${fullname.value} gained a new follower!`);
        }
      }
    );

    function followUser() {
      state.followers++;
    }

    function toggleFavourite(id) {
      console.log(`Favourite #${id}`);
    }

    function addTwoot(newTwootContent) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: newTwootContent,
      });
    }

    return {
      state,
      fullname,
      followUser,
      toggleFavourite,
      addTwoot
    };
  },
  mounted() {
    console.log("mounted");
    this.followUser();
  },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
}

h1 {
  margin: 0;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  margin-bottom: auto;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile__admin-no-badge {
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}


</style>>
