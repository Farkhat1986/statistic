<template>
    <v-item-group selected-class="bg-primary">
        
    <v-container>
    <v-card>
        <v-row>
            <v-col
                v-for="team in teams" :key="team.id"
                cols="25"
                md="4">
                 <v-item v-slot="{ selectedClass, toggle }">
                    <v-card
                    :class="['d-flex align-center', selectedClass]"
                    light
                    height="300"
                    @click="toggle"
                    >
                        <div class="text-h5 flex-grow-1 text-center"
                        >
                        <a :href="`mat/${team.id}`">{{ team.name }}</a>
                        <div>
                            
                        <div>{{team.id}}</div>
                        </div>
                        <div>{{ team.founded }}</div>
                        <div>{{ team.shortName }}</div>
                        <img :src="team.crest" :height="90">

                        </div>
                    </v-card>

                 </v-item>

            </v-col>
        </v-row>
        <div class="text-center">
    <v-pagination
      v-model="page"
      total-items="totalPages"
      :length="8"
      :total-visible="8"
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
            
             teams: [],
             page: 1,
             
         }
     },
     computed: {
        totalPages() {
            return this.teams / 10 + 1;
        }
     },
     mounted() {
         this.getDataTeams();
        
     },
     methods: {
         getDataTeams() {
             this.$axios.$get('api/teams/')
             .then(res => {
                 this.teams = res.teams;
             })
         },
         
     }
 
     
 }
 </script>
 <style >
 </style>