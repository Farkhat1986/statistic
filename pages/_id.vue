<template>   
    <div class="text-center">
        
        <h4>MAТЧИ</h4>
        <h1>{{compet.competition.name}}</h1>
        <div><img :src="compet.competition.emblem" :height="45"></div>
        <v-breadcrumbs>
        <v-breadcrumbs-item href="/">
            {{ items[0].title }}
        </v-breadcrumbs-item> 
        <v-breadcrumbs-item>
            /
        </v-breadcrumbs-item> 
        <v-breadcrumbs-item>
            {{compet.competition.name}}
        </v-breadcrumbs-item>
    </v-breadcrumbs>
        
        <div>    
            <v-data-table
            :headers="headers"
            :items="compet.matches"
            :items-per-page="7"
            class="elevation-1"
        >
        <template #top>
            <v-menu 
            ref="menu"
            v-model="showMenu">
            <template #activator="{ on, attrs }">
            <v-text-field
            v-model="date"
            clearable
            label="Дата с"
            readonly
            v-bind="attrs"
            v-on="on">
            </v-text-field>
            </template>

            <v-date-picker
            v-model="date"
            class="mt-4">
            </v-date-picker>
            </v-menu>
            
        </template>

        <template #[`item.utcDate`] = "{item}">
            {{ item.utcDate | formatDate }}
        </template>
        <template #[`item.homeTeam.crest`] = "{item}">
           <img :src="item.homeTeam.crest" :height="30">
        </template>
        <template #[`item.awayTeam.crest`] = "{item}">
           <img :src="item.awayTeam.crest" :height="30">
        </template>
        <template #[`item.df`] = "{item}">
           - {{ item.df }}
        </template>
            </v-data-table>
        </div>
   </div> 
</template>
<script>
  export default {
    filters: {
        formatDate: d => {
            const date = new Date(d);
            const options = { year: 'numeric', month: 'numeric', day: 'numeric'}
            return date.toLocaleString('ru-RU', options);

        }
    },
    
    
    data() {
        return {

            compet: [],
            date: '',
            items: [
                {
                title: 'лиги',
                },
                {
                title: '',
                },
            ],
            showMenu: false,
            headers: [
                      {text: 'Начало матча', value: 'utcDate', align: 'center'},
                      {text: 'Статус матча', value: 'status', align: 'center'},
                      {text: 'Домашняя команда', value: 'homeTeam.name', align: 'center'},
                      {text: 'Эмблема хозяев', value: 'homeTeam.crest', align: 'center'},
                      {text: 'Забили хозяева', value: 'score.fullTime.home', align: 'center'},
                      {text: '', value: 'df', align: 'center'},
                      {text: 'Забили гости', value: 'score.fullTime.away', align: 'center'},
                      {text: 'Эмблема гостей', value: 'awayTeam.crest', align: 'center'},
                      {text: 'Гостевая команда', value: 'awayTeam.name', align: 'center'},
            ]
        }
    },
    computed: {
        filteredCompet() {
            return this.date ? this.compet.filter(comp => new Date(comp.matches?.utcDate) > new Date(this.date)) : this.compet;
        }
    },
   
    async asyncData({ params, $axios }) {
          const compet = await $axios.$get(`api/competitions/${params.id}/matches`)
          return { compet }  
      }
  }
      
  </script>