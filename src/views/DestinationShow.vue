<template>
    <div>
        <section v-if="destination" class="destination">
            <h1>{{ destination.name }}</h1>
            <GoBack />
            <div class="destination-details">
                <img :src="`/images/${destination.image}`" :alt="destination.name">
                <p>{{ destination.description }}</p>
            </div>
        </section>
        <section class="experiences">
            <h2>Top Experiences in {{ destination.name }}</h2>
            <div class="cards">
                <RouterLink v-for="experience in destination.experiences" :key="experience.slug"
                    :to="{ name: 'experience.show', params: { experienceSlug: experience.slug } }">

                    <ExperienceCard :experience="experience" />

                </RouterLink>
            </div>
            <RouterView />
        </section>
    </div>
</template>
  
<script lang="ts">
import { RouteParams } from 'vue-router';
import sourceData from '@/data.json'
import ExperienceCard from '@/components/ExperienceCard.vue';
import GoBack from '@/components/GoBack.vue';

interface Destination {
    name: string;
    image: string;
    description: string;
}

export default {
    components: { ExperienceCard, GoBack },
    props: {
        id: { type: Number, required: true },
        slug: String,
        experienceSlug: String
    },
    // data() {
    //     return {
    //         destination: null as Destination | null
    //     }
    // },
    computed: {
        //   destinationId(): number {
        //     const id = this.$route.params.id;
        //     if (Array.isArray(id)) {
        //       return parseInt(id[0]);
        //     } else {
        //       return parseInt(id);
        //     }
        //   },
        destination(): any {
            return sourceData.destinations.find((destination => destination.id === this.id))
        }
    },

    //     async created() {
    //         this.initData()
    //         // this.$watch(() => this.$route.params, this.initData);
    //   },
    //     methods: {
    //       isDestination(json: any): json is Destination {
    //         return json &&
    //                typeof json.name === 'string' &&
    //                typeof json.image === 'string' &&
    //                typeof json.description === 'string';
    //       },
    //       async initData() {
    //         const response = await fetch(`https://travel-dummy-api.netlify.app/${this.$route.params.slug}`)

    //         const json = await response.json()
    //         if (this.isDestination(json)) {
    //           this.destination = json;
    //         }
    //       }
    //     }
};
</script>