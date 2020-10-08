<template>
  <div>
    <h2>Mon Panier</h2>
    <div v-for="article in panier.articles" :key="article.id">
      <div>
        {{ giveName(article.id) }} {{ article.quantity }}
      </div>
      <select v-model="article.quantity" :onchange="updateQuantity(article)">
        <option value="0">0</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
    </select>
    </div>
  </div>
</template>

<script>
module.exports = {
  props: {
    articles: { type: Array, default: [] },
    panier: { type: Object }
  },
  data () {
    return {
      selected: ''
    }
  },
  async mounted () {
  },
  methods: {
    updateQuantity(article) {
      console.log(article)
      article.quantity = parseInt(article.quantity)
      if (article.quantity == 0) {
        this.$emit('remove-from-panier', article.id)
      }
      else {
        this.$emit('update-quantity', article)
      }
    },
    giveName (articleId) {
      return this.articles.find(article => article.id == articleId).name
    }
  }
}
</script>

<style scoped>
</style>
