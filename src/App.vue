<template>
  <div class="pokemons">
    <div class="cards">
      <Card v-for="starter in starters" :key="starter.id" @click="fetchEvolutions(starter)"> 
        <template v-slot:title>
          {{ starter.name }}
        </template>

        <template v-slot:content>
          <img :src="starter.sprite" :alt="starter.name">
        </template>

        <template v-slot:description>
          <p class="power">Power</p>
          <div class="tag" v-for="(type, i) in starter.types" :key="i">
            {{ type }}
          </div>
        </template>  
      </Card>
    </div>
    
    <hr />
    <h1>Pokemon Evolutions</h1>
    <div class="cards">
      <Card v-for="evolution in evolutions" :key="evolution.id"> 
        <template v-slot:title>
          {{ evolution.name }}
        </template>

        <template v-slot:content>
          <img :src="evolution.sprite" :alt="evolution.name">
        </template>

        <template v-slot:description>
          <p class="power">Power</p>
          <div class="tag" v-for="(type, i) in evolution.types" :key="i">
            {{ type }}
          </div>
        </template>  
      </Card>
    </div>
  </div>
</template>

<script>
const api = 'https://pokeapi.co/api/v2/pokemon'
const STARTER_IDS = [1, 4, 7, 10, 13, 16]

import Card from './components/Card'
export default {
  name: 'App',
  components: {
    Card
  },
  data() {
    return {
      starters: [],
      evolutions: []
    }
  },
  async created() {
    const starters = await this.fetchData(STARTER_IDS)
    this.starters = starters
  },
  methods: {
    async fetchEvolutions(pokemon) {
      const evolutions = await this.fetchData([pokemon.id + 1, pokemon.id + 2])
      this.evolutions = evolutions
    },

    async fetchData(ids) {
      const responses = await Promise.all(ids.map(id => window.fetch(`${api}/${id}`)))
      const data = await Promise.all(responses.map(res => res.json()))
      return data.map(datum => ({
        id: datum.id,
        name: datum.name,
        sprite: datum.sprites.other['official-artwork'].front_default,
        types: datum.types.map(type => type.type.name)
      }))
      // console.log(this.starters)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
.power {
  text-transform: uppercase;
  font-size: 10px;
  margin: 5px;
}
.cards {
  display: flex;
  justify-content: center;
  align-items: center;
}
h1 {
  text-align: center;
}
hr {
  margin: 50px 0;
  border: none;
  border-bottom: 1px solid #cccccc;
}
</style>
