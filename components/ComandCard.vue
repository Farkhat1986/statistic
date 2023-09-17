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
    </v-card>
    <v-pagination class="ma-5" :length="totalPage" v-model="page" 
    total-visible="7"
    @input="getDataTeams()"></v-pagination>

</v-container>
</v-item-group>   
 
 </template>
 
 
 <script>
 export default {
     data() {
         return {
            
             teams: [],
             page: 1,
             totalPage: 10,
             limit: 6,
         }
     },
     
     mounted() {
         this.getDataTeams();
        
     },
     methods: {
         getDataTeams() {
             this.$axios.$get('api/teams/', {
                params: {
                    limit: this.limit,
                    offset: (this.page - 1) * this.limit,
                }
             })
             .then(res => {
                 this.teams = res.teams;
                 console.log(res)
                 const { data } = res;
                this.totalPage = Math.ceil(data.count/this.limit)
                const leagaName = matches.map((compet) => {
                if (compet.homeTeam.id.toString() === teamId) {
                    return {name: compet.homeTeam.name};
                } else {
                    return { name: compet.awayTeam.name};
                }
            },
                 
             }
             
             )
         },
         
     }
 
     
 }
 </script>