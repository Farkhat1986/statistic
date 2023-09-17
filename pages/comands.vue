<template>
  <div class="container mx-auto mt-8 text-center">
    <h1>КОМАНДЫ</h1>      
        <v-breadcrumbs>
            <v-breadcrumbs-item href="/">
                {{ items[0].title }}
            </v-breadcrumbs-item>
            <v-breadcrumbs-item>
                /
            </v-breadcrumbs-item>
            <v-breadcrumbs-item>
               {{ items[1].title }}
            </v-breadcrumbs-item>
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
                    title: 'лиги',
                },
                {
                    title: 'команды',
                },
            ],
        }
    }
}
</script>

