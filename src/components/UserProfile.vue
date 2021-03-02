<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ fullname }}</h1>
      <div class="user-profile__admin-badge" v-if="followers > 5">Admin</div>
      <div class="user-profile__admin-no-badge" v-else>&nbsp;</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <button @click="followUser">Follow</button>
      <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>

        <div class="user-profile__create-twoot-type">
          <label for="newTwootType"><strong>Type: </strong></label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button>Twoot!</button>
      </form>
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
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
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
      },
    };
  },
  watch: {
    followers(newFollowers, oldFollowers) {
      if (newFollowers > oldFollowers) {
        console.log(`${this.fullname} gained a new follower!`);
      }
    },
  },
  computed: {
    fullname() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourite #${id}`);
    },
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== 'draft') {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent
        });
      }
      this.newTwootContent = '';
    }
  },
  mounted() {
    console.log("mounted");
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

h1 {
  margin: 0;
}

.user-profile__create-twoot {
  padding-top: 20px;
  display: flex;
  flex-direction: column;
}

.user-profile__create-twoot textarea {
  width: 100%;
}
</style>>
