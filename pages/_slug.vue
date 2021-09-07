<template>
    <div>
        <div class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0">
            <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css" rel="stylesheet">
            <div class="max-w-4xl mx-auto sm:px-6 lg:px-8">
            <div class="mt-8 bg-white overflow-hidden shadow sm:rounded-lg p-6">
                <img :src="planet.image" alt="Planet image" class="rounded border" style="max-height: 300px; width: 100%;">
                <h2 class="text-2xl leading-7 font-semibold mt-4">
                Welcome to {{ planet.title }}
                </h2>
                <p class="mt-3 text-gray-600">
                {{ planet.description }} {{ planet.title }} is <a href="" target="_blank" class="text-green-500 hover:underline">{{ $data.distanceFromSun }}</a> from the sun, with a radius of <a href="" class="text-green-500 hover:underline">{{ $data.radius }}</a>.<br>
                </p>
                <h2 class="text-2xl leading-7 font-semibold mt-4">
                Check out other planets
                </h2>
                <button @click="showPlanets = !showPlanets" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">{{ showPlanets === true ? 'Hide planets' : 'Show planets' }}</button>
                <div v-if="showPlanets">
                    <LazyPlanets />
                </div>
                <p class="mt-4 pt-4 text-gray-800 border-t border-dashed">
                    <NuxtLink to="/"><code class="bg-gray-100 text-sm p-1 rounded border">Back to Home</code></NuxtLink>
                </p>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    head () {
        return {
            title: this.planet.title + ' | Nuxt Mission',
            htmlAttrs: {
                lang: 'en'
            },
            meta: [
                { charset: 'utf-8' },
                { name: 'viewport', content: 'width=device-width, initial-scale=1' },
                { hid: 'description', name: 'description', content: this.planet.description },
                { name: 'format-detection', content: 'telephone=no' }
            ],
            link: [
                { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
            ]
        }
  	},

    data () {
        return {
            showPlanets: false
        }
    },

    async asyncData ({ params }) {
        const planet = await fetch(`https://api.nuxtjs.dev/planets/${ params.slug }`).then((res) => {
            if (res.ok) {
                return res.json()
            }
            throw new Error(res.status)
        })
        return { planet }
    }
}
</script>
