<template>
  <div>
    <SearchJokes @search-text="searchText" />
    <Joke
      v-for="joke in jokes"
      :id="joke.id"
      :key="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import Joke from '../../components/Joke'
import SearchJokes from '../../components/SearchJokes'

export default {
  components: {
    Joke,
    SearchJokes,
  },

  data() {
    return {
      jokes: [],
      loading: false,
    }
  },
  head() {
    return {
      title: 'Jokes',
    }
  },
  async created() {
    const config = {
      headers: {
        Accept: 'application/json',
      },
    }
    try {
      const jokeObj = await this.$axios.$get(
        'https://icanhazdadjoke.com/search',
        config
      )
      this.jokes = jokeObj.results
    } catch (error) {
      // eslint-disable-next-line
        console.warn(error);
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: 'application/json',
        },
      }

      const res = await this.$axios.$get(
        `https://icanhazdadjoke.com/search?term=${text}`,
        config
      )
      this.jokes = res.results
    },
  },
}
</script>

<style></style>
