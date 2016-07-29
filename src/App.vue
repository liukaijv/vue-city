<template>
  <div id="app">    
    <city-select :province.sync="province" :city.sync="city" :district.sync="district"></city-select>   
    <p>
    地址：{{province}}-{{city}}-{{district}}
    </p>   
  </div>
</template>

<script>
import citySelect from './components/city-select.vue';

export default { 
  data(){
    return {
      province:'',
      city:'',
      district:'',
      provinceCode:'',
      cityCode:'',
      districtCode:''
    }
  }, 
  components:{
    citySelect
  } 
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
