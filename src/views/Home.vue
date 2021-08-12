/** submit.prevent keep form as it is after submiting it **/
<template>
  <div class="home">
    <h1>Adopt new best friend</h1>
    <p>Total Pets : {{ animalsCount }}</p>
    <p>Total Cats : {{ getAllCats.length }}</p>
    <p>Total Dogs : {{ getAllDogs.length }}</p>
    <button @click="toggleForm" class='btn btn-primary'>Add Pet</button>
    <b-form @submit.prevent="handleSubmit" v-if="showForm">
      <b-form-group id="input-group-2" label="Pet Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats','dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.age"
          placeholder="Enter Age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showForm: false,
      formData: {
        name: null,
        species: null,
        age: 0
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats',
      'getAllDogs'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    toggleForm () {
      this.showForm = !this.showForm
    },
    handleSubmit () {
      const { name, species, age } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      this.formData = {
        name: null,
        species: null,
        age: 0
      }
    }
  }
}
</script>
