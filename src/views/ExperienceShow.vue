<script lang="ts" setup>
import sourceData from '@/data.json';
import { computed, defineProps} from 'vue';

interface Props {
    id: number
    experienceSlug: string
}

const props = defineProps<Props>()
const destination = computed(() =>  sourceData.destinations.find(destination => destination.id === props.id))
const experience = computed(() =>  destination.value?.experiences.find(experience => experience.slug === props.experienceSlug))

</script>


<template>
    <section>
        <h1>{{ experience?.name }}</h1>
        <img :src="`/images/${experience?.image}`" :alt="experience?.name">
        <p>{{ experience?.description }}</p>
    </section>
</template>
