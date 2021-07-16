<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>

      <div class="user-profile__follower_count">
        <strong>Followers:</strong> {{ followers }}
      </div>
    </div>
    <form class="user-profile__create-tweet" @submit.prevent="createNewTweet">
      <label for="newTweet"><strong>New Tweet</strong></label>
      <textarea id="newTweet" rows="4" v-model="newTweetContent"></textarea>

      <div class="user-profile__create-tweet-type">
        <label for="newTweetType"><strong>Type :</strong></label>
        <!-- <select id="newTweetType" v-mode="selectedTweetType">
          <option
            :value="option.value"
            v-for="(option, index) in tweetTypes"
            :key="index"
            >{{ option.name }}
          </option>
        </select> -->
      </div>
      <button>
        Send Tweet
      </button>
    </form>
    <div class="user-profil__tweets-wrapper">
      <TweetItem
        v-for="tweet in user.tweets"
        :key="tweet.id"
        :username="user.username"
        :tweet="tweet"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem.vue";

export default {
  name: "UserProfile",
  components: { TweetItem },
  data() {
    return {
      newTweetContent: "",
      selectedTweetType: "instant",
      tweetTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant tweet" },
      ],
      followers: 0,
      user: {
        id: 1,
        username: "_GG",
        firstName: "Germain",
        lastName: "Grumel",
        email: "germaingrumel@outlook.fr",
        isAdmin: true,
        tweets: [
          { id: 1, content: "Tweeter is amazing!" },
          { id: 2, content: "Salut Vue JS" },
          { id: 3, content: "Germain Grml" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
        console.log(`oldFollowerCount`, oldFollowerCount);
        console.log(`newFollowerCount`, newFollowerCount);
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
      console.log(`Favourited tweet #${id}`);
    },
    createNewTweet() {
      if (this.newTweetContent && this.selectedTweetType !== "draft") {
        this.user.tweets.unshift({
          id: this.user.tweets.length + 1,
          content: this.newTweetContent,
        });
        this.newTweetContent = "";
      }
    },
  },
  //quand tu recharges la page ça trigger les fonctions suivantes
  mounted() {
    this.followUser();
  },
  // components: {
  //   HelloWorld
  // }
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
  background: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
.user-profile__admin-badge {
  background: darkblue;
  color: white;
  border-radius: 5px;
  text-align: center;
  width: 50px;
  padding: 5px;
}
.user-profile__create-tweet {
  border: 1px solid #dfe3e8;
  display: flex;
  flex-direction: column;
  padding: 20px;
}
/* .user-profil__tweets-wrapper{
} */

h1 {
  margin: 0;
}
</style>
