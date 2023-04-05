<template>
    <div id="nav">
        <RouterLink id="logo" to="/">Jullans resor</RouterLink>
        <RouterLink
            v-for="destination in destinations"
            :key="destination.id"
            :to="{name: 'destination.show', params: {id: destination.id, slug: destination.slug}}"
            >
                {{ destination.name }}
            </RouterLink>
    </div>
</template>

<script lang="ts">
import sourceData from '@/data.json'

export default {
    data() {
        return {
            destinations: sourceData.destinations
        }
    }
}
</script>