<template>
    <div>
        <h1>口罩在那</h1>
    <span><font>縣市</font></span>
    <citySelector v-on:chooseCity='chooseCity'></citySelector>
   <table>
       <tr>
           <td>
               名稱
           </td>
           <td>
               住址
           </td>
           <td>
               剩餘成人口罩
           </td>
           <td>
               剩餘兒童口罩
           </td>
           <td>
               更新時間
           </td>
            <td>
               Map
           </td>
       </tr>
        <tr v-for='(data,index) in targetLocation' v-bind:key='index'>
           <td>
               {{data.properties.name}}
           </td>
           <td>
                {{data.properties.address}}
           </td>
           <td>
                {{data.properties.mask_adult}}
           </td>
           <td>
                {{data.properties.mask_child}}
           </td>
             <td>
                {{data.properties.updated}}
           </td>
           <td>
              <a  v-bind:href="'https://www.google.com.tw/maps/search/'+data.properties.name+'/@'+data.geometry.coordinates[1]+','+data.geometry.coordinates[0]+',17z'">Map </a>
           </td>
       </tr>
   </table>
    </div>
</template>

<script>

export default {
    name:'maskcomponent',
    data(){
        return {
            maskinfo:[],
            city:{},
            targetLocation:[]
           
        }
    },components:{
          citySelector:()=>import('@/components/citySelector.vue'),
          
    },
    methods:{
        chooseCity:function(city,country){
                this.city.city=city;
                this.city.country=country;
                var city=   city.concat(country)
                var maskLocations=this.maskinfo.features;
                var ctargetLocation=[];
                maskLocations.map(function(maskLocation){
                    var address=maskLocation.properties.address;
                    var res =address.indexOf(city);
                    if(res!=-1){
                        ctargetLocation.push(maskLocation)
                    }
                })
                this.targetLocation=ctargetLocation;
        }
    }
    ,
    created(){
        function postData(url) {
            return fetch(url).then(response => {
                if (!response.ok) throw new Error(response.statusText)
                return response.json()
            })
        }
        postData('https://raw.githubusercontent.com/kiang/pharmacies/master/json/points.json', {}).then(responseData => {
            
            this.maskinfo=responseData;
        }).catch(error => console.log(error))
    },

}
</script>