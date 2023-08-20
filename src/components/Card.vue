<!--Корзина-->
<template>
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
     <tr v-for="(book,index) in bookList">
	 <td><img style="width: 50px;" src="https://storage.yandexcloud.net/wr4img/305036_43_i_015.jpg" /></td>
	 <td>{{book.name}}</td>
	 <td>${{book.price}}</td>
	 <td><input type="number" min="0" v-model.num="book.num"> </td>
	 <td>${{(book.price*book.num).toFixed(2)}}</td>
	 <td><i class="el-icon" @click="delBook(book.id)">
	  <svg viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" data-v-ea893728=""><path fill="currentColor" d="M160 256H96a32 32 0 0 1 0-64h256V95.936a32 32 0 0 1 32-32h256a32 32 0 0 1 32 32V192h256a32 32 0 1 1 0 64h-64v672a32 32 0 0 1-32 32H192a32 32 0 0 1-32-32V256zm448-64v-64H416v64h192zM224 896h576V256H224v640zm192-128a32 32 0 0 1-32-32V416a32 32 0 0 1 64 0v320a32 32 0 0 1-32 32zm192 0a32 32 0 0 1-32-32V416a32 32 0 0 1 64 0v320a32 32 0 0 1-32 32z"></path></svg>
	 </i></td>
	</tr>
	<tr> <td colspan="6" style="text-align: right;"> Subtotal： ${{total()}} </td> </tr>
   </tbody>
  </table>
  <div style="display: flex;justify-content: flex-end;">
    <button type="button" class="btn btn-default">Checkout</button>
  </div>
</div>
</template>

<script>
export default {
  name: 'Card',
  props: ['itr', 'index'],
  data () {
    return {
      book: { }, 
      bookList: [{ id: 1, name: 'Brand 1/ Product 1', price: 88.9, num: 1 },
      { id: 2, name: 'Brand 2/ Product 2', price: 88.9, num: 1 },
      { id: 4, name: 'Brand 3/ Product 3', price: 88.9, num: 2 }] 
    }
  },
  methods:{
    addBook: function() {
      this.bookList.push({ 
        id: this.bookList.length + 1, 
        name: this.book.name, 
        price: this.book.price, 
        num: 1 
      })
	},
    total: function() {
        return this.bookList.reduce((total, item) => { 
          total += item.price * item.num; 
          return total; 
        }, 0).toFixed(2) 
    },
    delBook: function(id) {
        this.bookList = this.bookList.filter(item => item.id != id);
    }
  }
};
</script>

<style scoped>
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
