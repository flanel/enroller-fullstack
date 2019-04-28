<template>
  <form @submit.prevent="enter()">
    <label>Login</label>
    <input type="text" v-model="user.login">
    <label>Hasło</label>
    <input type="password" v-model="user.password">
    <button type="submit">{{ labelOfTheButton }}</button>
  </form>
</template>

<script>
    export default {
        props: ["buttonLabel"],
        data() {
            return {
                user: {}
            };
        },
        methods: {
            enter(user) {
                this.$http.post('participants', user)
                    .then(response => {
                        // poszlo
                    })
                    .catch(response => {
                        // fail
                    });
            }
        },
        computed: {
            labelOfTheButton() {
                return this.buttonLabel || 'Zarejestruj się';
            }
        }
    };
</script>
