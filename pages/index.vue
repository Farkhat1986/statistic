<template>
    <div class="container mx-auto mt-8 text-center">
        <h1>ЛИГИ</h1>
        <v-breadcrumbs>
            <v-breadcrumbs-item>
                {{ items[0].title }}
            </v-breadcrumbs-item>        
        </v-breadcrumbs>
        <LigaCard />
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
            ]
        }
    }
}
</script>
