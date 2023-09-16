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
        <div class="text-center">
    <v-pagination
      v-model="page"
      :length="6"
      :total-visible="6"
      prev-icon="mdi-menu-left"
      next-icon="mdi-menu-right"
    >

</v-pagination>
  </div>
      </v-card>
    </v-container>
    </v-item-group>     
 </template>
 
 <script>
 export default {
     data() {
         return {
             competitions: [],
             page: 1,
             items: [
        {
          title: 'Команды',
          disabled: false,
          to: '/comands',
        },
        {
          title: 'Лиги',
          disabled: false,
          to: '/',
        },
        
      ],
         }
     },
     mounted() {
         this.getData();
     },
     methods: {
         getData() {
             this.$axios.$get('api/competitions/')
             .then(res => {
                 this.competitions = res.competitions;
                
             })
         }
     }
 
     
 }
 </script>
 