<template>
    <div>
        <p v-if="$fetchState.pending" class="mt-4 pt-4 text-gray-800 border-t border-dashed">Loading planets..... ⏱</p>
        <p v-else-if="$fetchState.error" class="mt-4 pt-4 text-gray-800 border-t border-dashed">Unable to fetch planets 😢</p>
        <p v-for="planet in planets" :key="planet.slug" class="mt-4 pt-4 text-gray-800 border-t border-dashed">
          <NuxtLink :to="planet.slug"><code class="bg-gray-100 text-sm p-1 rounded border">{{ planet.title }}</code></NuxtLink>
        </p>
    </div>
</template>

<script>
export default {
    data () {
        return {
            planets: []
        }
    },

    async fetch () {
        this.planets = await fetch ('https://api.nuxtjs.dev/planets').then(res => res.json())
    }    
}
</script>
