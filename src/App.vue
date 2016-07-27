<template>
  <div id="app">    
    <city-select></city-select>   
    <p>
    地址：{{province}}-{{city}}-{{district}}
    </p>
    <p>
    代号：{{provinceCode}}-{{cityCode}}-{{districtCode}}
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
  },
  events:{
    provinceChange(province){        
      this.province = province && province.name;
      this.provinceCode = province && province.code;
    },
    cityChange(city){     
      this.city = city && city.name || '';
      this.cityCode = city && city.code || '';
    },
    districtChange(district){     
      this.district = district && district.name || '';
      this.districtCode = district && district.code || '';
    }
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
