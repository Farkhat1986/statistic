<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app>
      <div :style="image" :height="60">
        // sCs.COM //
      </div>
        
 
      <v-spacer />
      <v-btn to="/">
        ЛИГИ
      </v-btn>
      <v-btn to="/comands">
        КОМАНДЫ
      </v-btn>
      <v-btn to="/about">
        Инфо
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <div class="text-h3 text-center">{{ title }}</div>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="fixed" app >
      <span>&copy; Bayramov Farhat {{ new Date().getFullYear() }} </span>
      <v-spacer />
      <div>
    <v-btn>
      <NuxtLink to="/">Лиги</NuxtLink>
    </v-btn>
    <v-btn>
      <NuxtLink to="/comands">Команды</NuxtLink>
    </v-btn>
      </div>
    </v-footer>
  </v-app>
</template>

<script>
import ball from "@/components/football.jpg"
export default {
  
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      image: { backgroundImage: `url(${ball})` },
      items: [
        {
          icon: 'mdi-chart-bubble',
          title: 'Команды',
          to: '/comands',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Лиги',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Документация',
          to: '/about',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'SoccerStat',
    }
  },
}
</script>
