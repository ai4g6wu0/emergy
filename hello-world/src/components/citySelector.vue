<template>
    <div>
        <select name="" id=""  v-model="cityChoosen" > 
            <option>請選擇</option>
            <option v-for="(city,index) in citys" v-bind:key='index' v-bind:value="city.name">{{city.name}}</option>
        </select>
        <select name="" id="" v-model="countyChoosen">
            <option>請選擇</option>
            <option v-for="(country,index) in countrys" v-bind:key='index' v-bind:value="country.name">{{country.name}}</option>
        </select>
    </div>
</template>


<script>
 import json from '@/assets/twcity.json'
export default {
    name:'cityChoose'  ,
    data(){
        return {
            twCity:json,
            cityChoosen:'請選擇',
            countyChoosen:'請選擇',
            countrys:[]
        }
    },
    computed:{
        citys:function(){
            var cityList=[];
            this.twCity.map(function(city){
            cityList.push({name:city.name})
         })
         return cityList;
        }, 
    },
    watch:{
           cityChoosen(cityName){
               console.log(cityName)
               var  countyList=[];
              this.twCity.map(function(city){
            if(cityName==city.name){
                countyList=city.districts
            }
         })
         this.countrys=countyList
        },
        countyChoosen(){
            this.$emit('chooseCity',this.cityChoosen,this.countyChoosen)
        },
    }
}


        
</script>