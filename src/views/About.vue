<!--Корзина(удалить)-->
<template>
  <div class="about">
	<button class="button" @click="showdata">Добавить</button>
    <card
      v-for="(item, index) in custdet"
      :item="item"
      :index="index"
      :itr="item"
      :key="item.card"
      @removeelement="custdet.splice(index, 1)"><!--корзина(удалить)-->
    </card>
  </div>
</template>

<script>
import Card from '@/components/Card.vue'

export default {
  name: 'About',
  props: ['itr', 'index'],
  components: {
    Card
  },
  data() {
    return {
      card: '',
      custdet: [],
    }
  },
  methods :{
    showdata: function() {
      this.custdet.push({
        card: this.card,				 
      });
      this.card = "";
    }
  }
}
</script>
<style scoped>
.about{
	padding: 20px 15px 15px 15px;
	margin: 0 0 25px 0;
	width: auto;
}
.button {
	display: inline-block;
	color: #56595e;
	text-decoration: none;
	width: 150px;
	height: 35px;
	padding: .10em 2em;
	outline: none;
	border-style: solid none;
	border-color: #f1f6fa #000 #c6ced0;
	border-radius: 4px;
	background: linear-gradient(#fdfeff, #e9f1f4, #dde5e8);
	transition: 0.2s;
}
</style>