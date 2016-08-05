<template>
	<select v-model="province" :class="selectClass" @change="isChanging=true">
		<option value="">选择省</option>
		<option v-for="province in provinces" :value="province[valueType]">{{province.name}}</option>
	</select>
	<select v-model="city" :class="selectClass" @change="isChanging=true">
		<option value="">选择城市</option>
		<option v-for="city in cities" :value="city[valueType]">{{city.name}}</option>
	</select>
	<select v-model="district" :class="selectClass" @change="isChanging=true">
		<option value="">选择县/区</option>
		<option v-for="district in districts" :value="district[valueType]">{{district.name}}</option>
	</select>
	<slot><slot>	
</template>

<script>
	import citydata  from '../lib/citydata.json';
	export default {		
		ready(){					
			this.provinces=citydata;
			this.oldProvince = this.province;
			this.oldCity = this.city;
			this.oldDistrict = this.district;
			let seletedProvince = this.provinces.filter(function(item){
				return item[this.valueType] == this.province;
			}.bind(this));
			if(seletedProvince.length){
				this.cities = seletedProvince[0]['children'];				
			}
			let seletedCity = this.cities.filter(function(item){
				return item[this.valueType] == this.city;
			}.bind(this));
			if(seletedCity.length){
				this.districts = seletedCity[0]['children'];				
			}
		},
		props:{	
			province:{
				twoWay: true,
				default:''
			},
			city:{
				twoWay: true,
				default:''
			},
			district:{
				twoWay: true,
				default:''
			},
			selectClass:{
				type:String,
				default:'form-control'
			},
			valueType:{
				type:String,
				default:'name'
			}
		},
		data(){
			return {
				oldProvince:'',
				oldCity:'',
				oldDistrict:'',	
				provinces:[],	
				cities:[],
				districts:[]			
			}
		},	
		watch:{
			province(){					
				let seletedItem = this.provinces.filter(function(item){
					return item[this.valueType] == this.province;
				}.bind(this));			
				if(seletedItem.length){					
					this.cities = seletedItem[0]['children'];
					this.city = this.city == this.oldCity ? this.cities[0][this.valueType] : this.city;
				}else{
					this.city = '';
					this.cities = [];
				}		
				this.oldCity = this.city;	
				this.$dispatch('provinceChange',seletedItem[0]);			
			},
			city(){	
				let seletedItem = this.cities.filter(function(item){
					return item[this.valueType] == this.city;
				}.bind(this));	
				if(seletedItem.length){					
					this.districts = seletedItem[0]['children'];					
					this.district = this.district == this.oldDistrict ? this.districts[0][this.valueType] : this.district;
				}else{
					this.district = '';
					this.districts = [];
				}
				this.oldDistrict = this.district;				
				this.$dispatch('cityChange', seletedItem[0]);			
			},
			district(){				
				let seletedItem = this.districts.filter(function(item){
					return item[this.valueType] == this.district;
				}.bind(this));						
				this.$dispatch('districtChange',seletedItem[0]);
			}
		},
		computed:{

		}
	}
</script>
