<template>
    <section class="container has-text-centered">
        <br /> <br /> <br />
        <b-notification
            type="is-danger"
            aria-close-label="Close notification"
            role="alert"
            class="mt-5">
            Logged Out Redirecting...
        </b-notification>
    </section>
</template>

<script>
export default {
    created() {
        this.$auth.logout()
        this.$router.push('/')
    }
}
</script>