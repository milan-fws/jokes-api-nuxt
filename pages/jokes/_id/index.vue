<template>
  <div>
    <nuxt-link to="/jokes">Back to jokes</nuxt-link>
    <h2>{{ joke }}</h2>
  </div>
</template>

<script>
export default {
  data() {
    return {
      joke: '',
    }
  },
  head() {
    return {
      title: this.joke,
    }
  },
  async created() {
    const config = {
      headers: {
        Accept: 'application/json',
      },
    }
    const joke = await this.$axios.$get(
      `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
      config
    )
    this.joke = joke.joke
  },
}
</script>

<style></style>
