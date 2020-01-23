<template>
    <form class="add" @submit.prevent="OnSubmit">
        <input class="add" type="text" v-model="title">
        <button type="submit">Добавить</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        OnSubmit() {
            if (this.title.trim()) {
                const newPost = {
                    date: new Date().getTime(),
                    title: this.title,
                }

                this.$emit('add-post', newPost)
                this.title = ''
            }
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
        margin-bottom: 10px;
    }
    input {
        width: 600px;
        padding: 0;
    }
    button {
        width: 80px;
        height: 30px;
        margin-left: 10px;
        font-weight: bold;
    }
    .add {
        padding-right: 20px;
        display: flex;
        justify-content: center;
    }

</style>