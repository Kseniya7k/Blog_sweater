<template>
    <div>
        <input type="text" placeholder="Введите логин" class="login" v-model="login">
        <input type="password" placeholder="Введите пароль" class="password" v-model="password">
        <button class="authorise" v-on:click="authorise">Войти</button>
        <button v-on:click="registration">Зарегистрироваться</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            login: '',
            password: ''
        }
    },
    methods: {
        authorise(login, password) {
            this.$emit('authorise', this.login, this.password)
            login = '';
            password = '';
        },
        registration(login, password) {
            const newUser = {
                id: new Date(),
                name: this.login,
                password: this.password,
            }
            this.$emit('registration', newUser)
            login = '';
            password = '';
        }
    }

}
</script>

<style>
    button {
        padding: 2px;
    }
    .login {
        margin-right: 5px;
    }
    .password {
        margin-right: 5px;
    }
    .authorise {
        margin: 5px 5px;
    }
</style>