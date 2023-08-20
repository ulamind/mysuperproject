<!--Селект(слева)-->
<template>
  <!--<select v-model="selectedCatalogs" multiple @change="myFunction()">
    <option v-for="brand in brands" v-bind:value="brand">{{brand.title}}</option>
  </select>
  <h3>Catalog</h3>
  <ul>
    <li v-for="brand in selectedCatalogs">{{brand.title}} - {{brand.sort}}</li>
  </ul>-->
  <aside>
    <ul>
      <!--<li v-for="brand in selectedCatalogs"><a href="">{{brand.title}} - {{brand.sort}}a link</a></li>-->
      <li v-for="brand in brands" v-bind:value="brand"><a href="">{{brand.title}}</a></li>
    </ul>
  </aside>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Select',
  data () {
    return {
      brands: [],
	  selectedCatalogs: []
    }
  },
  mounted () {
    this.fetchBrands()
  },
  methods: {
    fetchBrands () {
      axios.get('https://raw.githubusercontent.com/fe-side/vue-test/master/assets/brands.json')
        .then(response => {
          this.brands = response.data
          console.log(response.data,'select');
        })
    },
    myFunction: function () {
      console.log("Aloha");
    }
  }
}
</script>
<style>
aside {
	width: 20%;
	max-width: 10rem;
}
</style>
