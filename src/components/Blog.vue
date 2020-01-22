<template>
    <div>
        <ul>
            <Data
            v-for="citation of citations"
            v-bind:citation ="citation"
            v-on:remove-text="removeText"
            v-on:transform-citation="transformCitation"
            />
        </ul>
    </div>
</template>

<script>
import Data from '@/components/Data'
export default {
    props: ['citations'],
    methods: {
        removeText(id) {
            this.$emit('remove-text', id)
        },
        transformCitation(citation) {
            console.log(citation.title)
            this.$emit('transform-citation',citation.title)
        }
    },
    components: {
        Data
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>