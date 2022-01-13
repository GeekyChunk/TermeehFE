<template>
    <section class="container section">
        <br /> <br /> <br />
        <div style="backgroundColor: #e3e3e3!important" class="box mt-5 p-5 has-text-centered ">

            <div class="columns">
                <div class="column">
                    <div class="columns is-mobile">
                        <div class="column has-text-left">
                            {{ profile.last_name }}
                        </div>

                        <div class="column has-text-right">
                            نام خانوادگی
                        </div>
                    </div>
                </div>

                <div class="column">
                    <div class="columns is-mobile">
                        <div class="column has-text-left">
                            {{ profile.first_name }}
                        </div>

                        <div class="column has-text-right">
                            نام
                        </div>
                    </div>
                </div>
            </div>

            <div class="columns">
                <div class="column">
                    <div class="columns is-mobile">
                        <div class="column has-text-left">
                            {{ profile.username }}
                        </div>

                        <div class="column has-text-right">
                            نام کاربری
                        </div>
                    </div>
                </div>

                <div class="column">
                    <div class="columns is-mobile">
                        <div class="column has-text-left">
                            {{ profile.email }}
                        </div>

                        <div class="column has-text-right">
                            ایمیل
                        </div>
                    </div>
                </div>
            </div>
            <b-button @click="() => {
                    this.$auth.logout();
                    this.$router.push('/');
                }" class="is-danger">
                خروج
            </b-button>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            profile: this.$auth.user
        }
    },
    methods : {
        async refresh() {
            this.$auth.setUser(await this.$axios.get('/api/user/'))
        }
    },
}
</script>
