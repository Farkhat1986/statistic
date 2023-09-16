<template>
  <div class="container mx-auto mt-8 text-center">
      <h1>КОМАНДЫ</h1>
      <NuxtLink to="/" >
          Лиги
      </NuxtLink>
      /
      <NuxtLink to="/comands" >
          Команды
      </NuxtLink>
      
      <v-breadcrumbs v-for="item in items" :key="item.title" :item="item">
   
      <a href="/">{{ item.title }}</a>
      <a href="/comands">{{ item.title }}</a>

    </v-breadcrumbs>
      <ComandCard />
  </div>
</template>

<script>
export default {   
    data() {
        return {
            items: [
                {
                    title: 'her',
                    disabled: false,
                    to: 'comands'
                },
                {
                    title: 'her2',
                    disabled: false,
                    to: '/'
                },

            ],
        }
    }
}
</script>

