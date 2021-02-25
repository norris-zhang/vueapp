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
        </div>
        <div class="user-profile__twoots-wrapper">
            <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" @favourite="toggleFavourite"/>
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
                username: "nzhang",
                firstName: "Norris",
                lastName: "Zhang",
                email: "nzhang@bravurasolutions.com",
                isAdmin: true,
                twoots: [
                    { id: 1, content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime, ea enim, a eligendi saepe consequuntur nihil sapiente nemo eaque necessitatibus unde cumque distinctio atque soluta porro corporis officia. Odio, error!' },
                    { id: 2, content: 'I am not a long text.' }
                ]
            }
        }
    },
    watch: {
        followers(newFollowers, oldFollowers) {
            if (newFollowers > oldFollowers) {
                console.log(`${this.fullname} gained a new follower!`);
            }
        }
    },
    computed: {
        fullname() {
            return `${this.user.firstName} ${this.user.lastName}`
        }
    },
    methods: {
        followUser() {
            this.followers++;
        },
        toggleFavourite(id) {
            console.log(`Favourite #${id}`);
        }
    },
    mounted() {
        console.log('mounted');
        this.followUser();
    }
}
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
    border: 1px solid #DFE3E8;
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
</style>>
