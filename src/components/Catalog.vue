<!--Каталог(справа)-->
<template>
  <div class="containers">
    <div class="box span-row">
	  <div style="text-align: left;">All Brands</div>	
	  <select v-model="selectedBrandId" class="form-select">
		<option v-for="brand in brands" :value="brand.id" :key="brand.id">{{ brand.title }}</option>
	  </select>
    </div>

    <div class="box"><h3 style="text-align: left;">
	   ={{ getTotalQuantity() }}
	  <br>Catalog</h3>
    </div>

    <div class="box span-col">
	  <div class="section" v-for="brand in brands" :key="brand.id">
		<ul v-if="selectedBrandId === brand.id" v-for="product in getProductsByBrandId(brand.id)" :key="product.id">
		  <li class="col-md-11 col-6 mb-2">
			<div class="card-body" style="text-align: left;" @click="addToCart(product)">		  
			  <img class="card-img-top" :src="product.image">
			  <h5 class="card-title"><a href="#">{{ product }}</a></h5>
			</div>
			<div class="card-text">
			  Brand <br>
			  ${{ product.price }}
			</div>
		  </li>
		</ul>
	  </div>
    </div>
  </div>
   =
<div style="width: 800px; margin: 50px auto;">
  <h2 style="text-align: left;">Shopping Cart</h2>
  <table class="table">
   <thead> <tr>
   <th></th>
   <th>Item</th>
   <th>Price</th>
   <th>Qty</th>
   <th>Total</th>
   <th></th>
   </tr></thead>
   <tbody>
      <tr v-for="item in cartItems" :key="item.id">
        <td><img style="width: 50px;" :src="item.image"></td>
        <td>Brand {{item.brand}}/{{item.title}}</td>
        <td>${{ item.price }}</td>
		<td><input type="number" min="0" v-model.quantity="item.quantity"></td>
		<td>${{(item.price*item.quantity).toFixed(2)}}</td>
		<td><i class="el-icon" @click="removeFromCart(item)">
		  <svg viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" data-v-ea893728=""><path fill="currentColor" d="M160 256H96a32 32 0 0 1 0-64h256V95.936a32 32 0 0 1 32-32h256a32 32 0 0 1 32 32V192h256a32 32 0 1 1 0 64h-64v672a32 32 0 0 1-32 32H192a32 32 0 0 1-32-32V256zm448-64v-64H416v64h192zM224 896h576V256H224v640zm192-128a32 32 0 0 1-32-32V416a32 32 0 0 1 64 0v320a32 32 0 0 1-32 32zm192 0a32 32 0 0 1-32-32V416a32 32 0 0 1 64 0v320a32 32 0 0 1-32 32z"></path></svg>
		</i></td>
      </tr>
      <tr> <td colspan="6" style="text-align: right;"> Subtotal： ${{ cartTotal.toFixed(2) }}</td> </tr>
   </tbody>
  </table>
  <div style="display: flex;justify-content: flex-end;">
    <button type="button" class="btn btn-default">Checkout</button>
  </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Catalog',
  data () {
    return {
      brands: [],	  
	  selectedCatalogs: [],
	  selectedBrandId: '',
      products: [],
      cartItems: [],
    }
  },
  mounted () {
    this.fetchProducts();
    this.fetchBrands();
  },
  methods: {
    fetchBrands () {
      axios.get('https://raw.githubusercontent.com/fe-side/vue-test/master/assets/brands.json')
        .then(response => {
          this.brands = response.data
          console.log(response.data,'select');
        })
        .catch(error => {
          console.error(error);
        });		
    },
    fetchProducts () {
      //axios.get('https://raw.githubusercontent.com/fe-side/vue-test/master/assets/products.json')
	  //берём только цвет/размер по id
      axios.get('https://raw.githubusercontent.com/fe-side/vue-test/master/assets/level3/products.json')
        .then(response => {
          this.products = response.data.map((result) => {
          return {
            title: result.title,
            price: result.regular_price.value,
            image: 'https://raw.githubusercontent.com/fe-side/vue-test/master/assets/' + result.image,
			brand: result.brand,
			id: result.id,
			//color: result.configurable_options.values.value,
			//size: result.configurable_options.values.label
          };
        }); 
          console.log(response.data,'catalog');
        })
        .catch(error => {
          //console.log(error);
        });
      console.log('modal')		
    },
	//Добавить
    addToCart(product) {
      const cartItem = this.cartItems.find(item => item.id === product.id);
      if (cartItem) {
        cartItem.quantity++;
      } else {
        this.cartItems.push({ ...product, quantity: 1 });
      }
    },
	//Удалить
    removeFromCart(item) {
      const index = this.cartItems.indexOf(item);
      this.cartItems.splice(index, 1);
    },
    getCountByBrandNewId (id) {
      return this.getProductsByBrandId(id).length
    },
    getProductsByBrandId (id) {
      return this.products.filter(product => product.brand === id)
    },
	//Корзина
    getTotalQuantity() {
      return this.cartItems.reduce((total, item) => total + item.quantity, 0);
    }
  },
  computed: {
	//Итого
    cartTotal() {
      return this.cartItems.reduce((total, item) => total + (item.price * item.quantity), 0);
    }
  }
}
</script>
<style>
.containers {
  display: grid;
  grid-template-columns: 2fr 6fr 0fr;
  grid-auto-rows: minmax(40px, auto);
  grid-auto-flow: column;
  gap: 10px;
  padding: 2em 1em;
  max-width: 100%;
}
.section {
  width: 85%;
}
ul {
  padding: 0!important;
  margin: 0!important;
  width: 240px;
  display: inline-block;
}
.section .mb-2 {
  margin: 0!important;
}
li {
  list-style-type: none;
}
.card-img-top {
  width: 220px!important;
  height: 250px;
  border: 1px solid rgba(0,0,0,.03);
  border-radius: 2px;
  cursor: pointer;
  background: rgba(0,0,0,.03);
}
.card-body {
  padding: 10px 0 0!important;
}
.card-title {
  margin: 10px 0 4px!important;
}
.card-title a {
  color: #0F1111;
  text-decoration: none;
}
.card-title a:active, .card-title a:hover {
  color: #C7511F;
}
.span-row {
  grid-row: auto / span 2;
  text-align: right;
  padding: 6px 30px;
  border-right: 1px ridge silver;
}
.span-col {
  grid-column: auto / span 2;
  text-align: left;
}
/*card*/
.el-icon {
    height: 1em;
    width: 1em;
    line-height: 1em;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    position: relative;
    font-size: 20px;
	cursor: pointer;
}
.table {
    width: 100%;
    max-width: 100%;
    margin-bottom: 20px;
}
.table>tbody>tr>td, 
.table>tbody>tr>th, 
.table>tfoot>tr>td, 
.table>tfoot>tr>th, 
.table>thead>tr>td, 
.table>thead>tr>th {
    padding: 8px;
    line-height: 1.42857143;
    vertical-align: top;
    border-top: 1px solid #ddd;
}
.table>thead>tr>th {
    vertical-align: bottom;
    border-bottom: 2px solid #ddd;
}
.table>caption+thead>tr:first-child>td, 
.table>caption+thead>tr:first-child>th, 
.table>colgroup+thead>tr:first-child>td, 
.table>colgroup+thead>tr:first-child>th, 
.table>thead:first-child>tr:first-child>td, 
.table>thead:first-child>tr:first-child>th {
    border-top: 0;
}
.table>thead:first-child>tr:first-child>th {
    border-bottom: 0;
}
.table>tbody>tr:first-child>td {
    border-top: 0;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}
.table>tbody>tr>td, 
.table>tbody>tr>th, 
.table>tfoot>tr>td, 
.table>tfoot>tr>th, 
.table>thead>tr>td, 
.table>thead>tr>th {
    padding: 8px;
    line-height: 1.42857143;
    vertical-align: top;
    border-top: 1px solid #ddd;
}
input[type=number] {
    width: 35px;
}
</style>