<template>
    <section class="p-3">
        <br /> <br /> <br />
        <div class="container box has-background-grey-lighter is-centered">
            <h1 class="title is-3 has-text-centered">
                گالری
            </h1>
            <hr />
            <div v-if="items.length != 0" class="columns is-mobile is-centered">
                <b-carousel style="width: 35rem">
                    <b-carousel-item v-for="item in tops" :key=item.slug>
                        <div class="card">
                            <div class="card-image">
                                <figure class="image is-3by2">
                                    <a><img :src="item.image"></a>
                                </figure>
                            </div>
                            <div class="card-content">
                                <div class="content">
                                    <p class="title is-6">{{ item.name }}</p>
                                    <p class="subtitle is-7"></p>
                                </div>
                            </div>
                        </div>
                    </b-carousel-item>
                </b-carousel>
            </div>
        <br>
        <h2 class="title is-3 has-text-centered">
            محصولات
        </h2>
        <hr />
        <div v-if="items.length !=0" class="columns is-mobile is-multiline is-centered">
            <div v-for="i in items" :key="i.slug" style="width: 22rem" class="column is-narrow has-text-centered">
                <NuxtLink :to="`/gallery/${i.slug}`">
                    <div class="card has-background-primary">
                        <div class="card-image">
                            <figure class="image is-4by2">
                                <a><img :src="i.thumbnail"></a>
                            </figure>
                            </div>
                        <div class="card-content">
                            <div class="content">
                                <p class="title is-6 has-text-white pb-2">{{ i.title }}</p>
                                <p class="subtitle is-6 has-text-white">
                                    <span class="has-text-right"> {{ i.price }} </span>
                                    <span>
                                        تومن
                                    </span>
                                </p>
                            </div>
                        </div>
                    </div>
                </NuxtLink>
            </div>
        </div>
    </div>

    <br />
    </section>
</template>

<script>
export default {
    data() {
        return {
            items: [],
            tops: []
        }
    },
    created() {
        this.$axios.get("api/item/")
        .then(resp => this.items = resp.data)
        this.$axios.get("api/top/")
        .then(resp => this.tops = resp.data)
    }
}
</script>