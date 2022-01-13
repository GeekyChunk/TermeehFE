<template>
    <section class="section">
        <br /> <br /> <br />
        <div class="container">
            <div class="columns is-centered has-text-centered">
                <div class="column is-half has-text-centered">
                <div v-if="err != null">
                    <template v-if="err == 400">
                        Not Found
                    </template>
                </div>
                    <form  @submit.prevent="Login" class="box">
                        <h1 class="title i-3">
                           Login
                        </h1>
                        <b-field label="Username" horizontal>
                            <b-input v-model="login.username">
                            </b-input>
                        </b-field>
                        <b-field label="Password" horizontal>
                            <b-input v-model="login.password" type="password">
                            </b-input>
                        </b-field>
                        <button class="button is-primary">Login</button>
                    </form>
                </div>
            </div>
        </div>
    </section>

</template>

<script>
export default {
    data() {
        return {
            login: {
                username: "",
                password: ""
            },
            err: null
        }
    },
    methods: {
        async Login() {
            try {
                await this.$auth.loginWith('local', {data: {username: this.login.username, password: this.login.password}})
            } catch (err) {
                this.err = err.response.status
            }
        }
    }
}
</script>