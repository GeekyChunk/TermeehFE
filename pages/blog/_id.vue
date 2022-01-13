<template>
    <section class="section">
        <br /> <br /> <br />
        <div class="container">
            <Row>
                <Card v-if="post" maxW="47" className="box p-0">
                    <div class="card-image">
                        <figure class="image is-4by3">
                            <img :src="post.picture" alt="Placeholder image">
                        </figure>
                    </div>
                    <div class="p-3">
                        <h1 class="title is-2 has-text-centered"> {{ post.title }} </h1>
                        <p class="is-size-4 has-text-centered">
                            <span v-html="post.caption" />
                        </p>
                    </div>
                </Card>
            </Row>
        </div>
    </section>
</template>

<script>
export default {
    async asyncData({ params }) {
        return {
            id: params.id,
            post: null,
        }
    },
    async created() {
        let data = (await this.$axios.get(`api/post/${this.id}/`)).data
        data.caption = data.caption.replace('\n', "<br />")
        this.post = data

    }
}
</script>