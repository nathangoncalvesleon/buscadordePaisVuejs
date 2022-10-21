<template>
  <div>
    <div>
      <h1>Bem vindo ao pesquisador de países!</h1>
      <p>Para começar, digite o nome de um país na barra de pesquisa.</p>

    </div>
    <div>
      <input type="text" v-model="search" placeholder="Digite o nome do país" />
      <button @click="searchCountry">Pesquisar</button>
      {{search.length > 0 ? searchCountry() : 'Nenhum país pesquisado'}}

    </div>


    <div v-if="search.length ===0" class="displayflag">

      <div v-for="flag in flags" :key="flag.name">
        <ul>
            <a :href='flag.maps.googleMaps' target="_blank">

            <img :src="flag.flags.png" alt="Bandeira" />
            </a>
        </ul>
      </div>


    </div>




    <div v-if="country">
      <h2>
        {{ country.altSpellings
        .filter((name) => name !== country.name)
        .join(", ") }}</h2>



      <p>Capital: {{ country.capital[0] }}</p>
      <p>População: {{ country.population }}</p>
      <p>Área: {{ country.area }} km²</p>
      <p>Região: {{ country.region }}</p>
      <p>Sub-região: {{ country.subregion }}</p>
      <p>Domínio: {{ country.topLevelDomain }}</p>
      <p>Moedas: {{ country.currencies
      
      }}</p>
      <p>Idiomas: {{ country.languages
      
      }}</p>
      <p>Fronteiras: {{ country.borders
      }}</p>

      <div>
        <h3>Bandeira</h3>
        <ul>
          <img :src="country.flags.png" alt="Bandeira" />

        </ul>
      </div>








    </div>









  </div>
</template>

<script>
export default {
  name: 'FindCountry',
  data() {
    return {
      search: '',
      flags: {

      },
      country: {

      },
      neighbors: [

      ],

    }
  },
  methods: {
    searchCountry() {
      fetch(`https://restcountries.com/v3.1/name/${this.search}`)
        .then(response => response.json())
        .then(data => {
          this.country = data[0]
          console.log(this.country)
        })

    },
    searchFlag() {
      fetch(`https://restcountries.com/v3.1/all`)
        .then(response => response.json())
        .then(data => {

          this.flags = data
          console.log(this.flags)





        })

    },

    

  },


  created() {
    this.searchCountry(),
      this.searchFlag()


  },





}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  text-align: center;
}

.displayflag {
  width: 100%;
  display: grid;
  flex-wrap: wrap;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 1rem;
  padding: 1rem;






}

img {
  width: 100%;
  display: grid;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  padding: 0;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  border: 1px solid #ccc;
  max-width: 300px;
  max-height: 300px;
  object-fit: cover;
  object-position: center;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto auto;
  grid-gap: 10px;
  grid-auto-flow: dense;
  grid-auto-columns: 1fr;
  grid-auto-rows: 1fr;
  grid-template-areas: "a b c"
    "d e f"
    "g h i";




  object-position: center;
}


input {
  width: 300px;
  height: 30px;
  border-radius: 5px;
  border: 1px solid #ccc;
  padding: 0 10px;
  margin-right: 15px;
}

button {
  width: 100px;
  height: 30px;
  border-radius: 5px;
  border: 1px solid #ccc;
  background-color: #ccc;
  cursor: pointer;
}

ul {
  list-style: none;
  flex-direction: row;
  display: grid;
  grid-gap: 10px;
  grid-auto-flow: dense;
  grid-auto-columns: 4fr;
  grid-auto-rows: 4fr;
  grid-template-areas: "a b c"
    "d e f"
    "g h i";

  justify-content: center;
  align-items: center;
  gap: 100px;
  margin: 0;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

li {
  margin: 10px 0;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 300px;
  text-align: center;
}
</style>
