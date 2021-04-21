<template>
  <Menu :openCloseForm="openCloseForm" :showForm="showForm" />
  <TweetForm :showForm="showForm" :reloadTweets="reloadTweets" :openCloseForm="openCloseForm"/>
  <TweetList :tweets="tweets" />
</template>

<script>
import { ref } from "vue";
import Menu from "./components/Menu";
import TweetForm from "./components/TweetForm";
import useFormTweet from "./hooks/useFormTweet";
import TweetList from "./components/TweetList";
import { getTweetsApi } from "./api/tweet";

export default {
  name: "App",
  components: {
    Menu,
    TweetForm,
    TweetList,
  },
  setup() {
    let tweets = ref(getTweetsApi().reverse());

    const reloadTweets = () => {
      tweets.value = getTweetsApi().reverse();
    }
    
    return {
      ...useFormTweet(),
      reloadTweets,
      tweets
    };
  },
};
</script>

<style lang="scss"></style>
