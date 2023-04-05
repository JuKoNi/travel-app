<script setup lang="ts">
import { RouteParams } from 'vue-router';
import sourceData from '@/data.json'
import { computed, defineProps} from 'vue';
import ExperienceCard from '@/components/ExperienceCard.vue';
import GoBack from '@/components/GoBack.vue';

interface Props {
    name: string;
    image: string;
    description: string;
    id: number;
    required: true;
    slug: string;
    experienceSlug: string
}
const props = defineProps<Props>()
const destination = computed(() => sourceData.destinations.find((destination => destination.id === props.id)))
</script>

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
            <h2>Top Experiences in {{ destination?.name }}</h2>
            <div class="cards">
                <RouterLink v-for="experience in destination?.experiences" :key="experience.slug"
                    :to="{ name: 'experience.show', params: { experienceSlug: experience.slug } }">

                    <ExperienceCard :experience="experience" />

                </RouterLink>
            </div>
            <RouterView />
        </section>
    </div>
</template>
  
