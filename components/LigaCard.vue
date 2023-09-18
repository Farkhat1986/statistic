<template >
    <v-item-group selected-class="bg-primary">
    <v-container>
      <v-card>
        <v-text-field v-model="search" label="Search" append-icon="mdi-magnify" @keyup.enter="getData()"></v-text-field>
        <v-row :style="image" >
          <v-col
            v-for="comp in competitions"
            :key="comp.id"
            cols="25"
            md="4">
            <v-item v-slot="{ selectedClass }">
                <v-card
                    :class="['d-flex align-center', selectedClass]"
                    light
                    height="300"
                    @click="getData()">
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
    </v-container>
    </v-item-group>     
 </template>
 
 <script>
import foot from "@/components/football2.jpg"
 export default {
     data() {
         return {
             competitions: [],
             search: '',
             image: { backgroundImage: `url(${foot})` },
         }
     },
     mounted() {
         this.getData();
     },
     methods: {
         getData() {
             this.$axios.$get('api/competitions/', {
                params: this.search
             })
             .then(res => {
                 this.competitions = res.competitions;        
             })
         },
     }
 
     
 }
 </script>

 