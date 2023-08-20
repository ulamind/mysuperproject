<!--Каталог(Лого)-->
<template>
  <div class="home">
    <!--<Select />-->
    <Catalog />
  </div>
</template>

<script>
import Catalog from '@/components/Catalog.vue'
//import Select from '@/components/Select.vue'

export default {
  name: 'Home',
  components: {
    Catalog,
	//Select
  }
}
</script>
<style>

</style>