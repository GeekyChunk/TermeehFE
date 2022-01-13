<template>
    <nav class="navbar is-fixed-top is-primary">
        <div class="container">
            <div class="navbar-brand">
                <NuxtLink class="navbar-item" to="/">
                    <img src="~/assets/termeeh.png" alt="Logo">
                </NuxtLink>

                <div class="navbar-burger" @click="showNav = !showNav" :class="{ 'is-active': showNav }">
                    <span></span>
                    <span></span>
                    <span></span>
                </div>
            </div>
            <!--
            Using the v-bind: directive to reactively update the class attribute 'is-active' based on the showNav property.
            -->
            <div class="navbar-menu" :class="{ 'is-active': showNav }">
                <div class="navbar-start">
                    <NuxtLink class="navbar-item" to="/gallery">
                        گالری
                    </NuxtLink>
                    <NuxtLink class="navbar-item" to="/blog">
                        پست ها
                    </NuxtLink>
                    <template v-if="$auth.user && $auth.user.is_staff">
                        <NuxtLink class="navbar-item" to="/admin">
                            پنل ادمین
                        </NuxtLink>
                    </template>
                </div>
                <div class="navbar-end">
                    <div class="navbar-item">
                         <div class="buttons">
                            <NuxtLink class="button is-success" v-if=" $auth.loggedIn && $auth.user" to="/auth">
                                    {{ $auth.user.username }}
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>

<script>

export default {
    props: ['prp'],
    data() {
        return {
            showNav: false
        }
    },
    methods: {
        close (e) {
            if (!this.$el.contains(e.target)) {
                this.showNav = false
            }
        }
    },
    mounted () {
        document.addEventListener('click', this.close)
    },
    beforeDestroy () {
        document.removeEventListener('click',this.close)
    }
}
</script>
