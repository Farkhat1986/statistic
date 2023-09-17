<template>
    <v-item-group selected-class="bg-primary">
    <v-container>
      <v-card>
        <v-row>
          <v-col
            v-for="comp in competitions"
            :key="comp.id"
            cols="25"
            md="4">
            <v-item v-slot="{ selectedClass, toggle }">
                <v-card
                    :class="['d-flex align-center', selectedClass]"
                    light
                    height="300"
                    @click="toggle">
                        <div class="text-h5 flex-grow-1 text-center">   
                            <img :src="comp.emblem" :height="90">
                            <div>
                                <a :href="`${comp.id}`">{{comp.name}}</a>
                            </div>
                        </div>   
                </v-card>
            </v-item>
            
            </v-col>
            
        </v-row>
        
      </v-card>
      <v-pagination class="ma-5" v-model="page" :length="totalPages" total-visible="3" @input="getData()"></v-pagination>
    </v-container>
    </v-item-group>     
 </template>
 
 <script>
 export default {
     data() {
         return {
             competitions: [],
             page: 1,
             totalPages: 3,
             limit: 6,
         }
     },
     mounted() {
         this.getData();
     },
     methods: {
         getData() {
             this.$axios.$get('api/competitions/', {
                params: {
                    limit: this.limit,
                    offset: (this.page - 1) * this.limit,
                }
             })
             .then(res => {
                 this.competitions = res.competitions;
                 console.log(res)
                 const { data } = res;
                 this.totalPages = Math.ceil(data.count/this.limit)        
             })
         },
     }
 
     
 }
 </script>
 