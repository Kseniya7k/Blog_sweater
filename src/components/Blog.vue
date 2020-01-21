<template>
    <div>
        <ul>
            <Data
            v-for="citation of citations"
            v-bind:citation ="citation"
            v-on:remove-text="removeText"
            @enable-editing="enableEditing"
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
        enableEditing(newVal) {
            this.$emit('enable-editing', newVal);
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