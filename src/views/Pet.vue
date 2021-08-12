/** {{ pet().name }}**/
<template>
  <div>
    <h1>{{ animal.name }} ({{ $route.params.species }})</h1>
    <p>Age : {{ animal.age }} years old</p>
    <p>Breed : {{ animal.breed }}</p>
  </div>
</template>

//import { mapState } from 'vuex'
//   methods: {
//       pet() {
//           //this[this.cats,this.dogs] functions in computed
//           const animal = this[this.$route.params.species][this.$route.params.id]
//           return animal
//       }
//   },

<script>

export default {
  data () {
    return {
      animal: {}
    }
  },
  computed: {
    cats () {
      return this.$store.state.cats
    },
    dogs () {
      return this.$store.state.dogs
    }
    // ...mapState([
    //   'cats'
    // ])
  },
  mounted () {
    const animal = this[this.$route.params.species][this.$route.params.id]
    this.animal = animal
  }
}
</script>
