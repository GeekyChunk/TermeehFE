<template>
    <section class="section">
        <br><br>
        <div class="container">
            <div class="box">
            <h1 class="title has-text-centered">
                پست ها
            </h1>
                <Row class="p-1 mx-2">
                    <Card v-for="highlight in highlights" :key="highlight.id" style="max-width: 10rem; width: 100%" class="column">
                        <div class="pressable" @click="() => highlight.opened = true">
                            <BImage  :src="highlight.picture" class="is-1by1" rounded>
                            </BImage>
                        </div>
                        <h6 class="has-text-centered">
                            {{ highlight.title}}
                        </h6>
                        <b-modal v-model="highlight.opened">
                            <p class="image is-4by3">
                                <img :src="highlight.picture">
                            </p>
                        </b-modal>
                    </Card>
                </Row>
                <hr />
                <Row>
                    <Card v-for="post in posts" :key="post.id" maxW="25" :link="`/blog/${post.id}`" className="box pressable m-2 p-0">
                        <div class="card-image">
                            <figure class="image is-4by3">
                                <img :src="post.picture" alt="Placeholder image">
                            </figure>
                        </div>
                    </Card>
                </Row>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            posts: [],
            highlights: []
        }
    },
    created() {
        this.$axios.get('api/post/')
        .then(resp => this.posts = resp.data)
        this.$axios.get('api/highlight/')
        .then(resp => {
            let highlights = resp.data
            for (let i = 0; i < highlights.length; i++) {
                highlights[i]["opened"] = false
            }
            this.highlights = highlights
        })
    }
}
</script>