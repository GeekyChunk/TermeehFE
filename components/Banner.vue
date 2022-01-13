<template>
    <div>
        <section class="hero is-large">
        <img src="~/assets/bg.png" class="hero-background is-transparent">
        <div class="hero-body">
            <div class="container has-text-centered">
            <h1 style="font-size: 400%" class="title is-2 has-text-grey-dark pb-2">
                گالری ترمه
            </h1>
            <p class="subtitle is-2">
                <NuxtLink to="/gallery">
                    <b-button class="is-primary title is-4">
                        گالری
                    </b-button>
                </NuxtLink>
                <b-button class="is-danger title is-4">
                    ثبت درخواست
                </b-button>
                
            </p>
            </div>
        </div>
        </section>

    </div>
</template>

<style scoped>
.hero-background {
    position: absolute;
    object-fit: cover;
    object-position: center center;
    width: 100%;
    height: 100%;
}
.is-transparent {
      opacity: 0.7;
}
</style>