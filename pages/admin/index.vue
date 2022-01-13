<template>
    <section class="section">
        <br><br>
        <div class="container">
            <Row>
                <Card className="column is-half box m-2">
                    <h1 class="title is-4 link has-text-centered">
                        Items
                    </h1>
                    <table class="table is-fullwidth">
                        <thead>
                            <tr>
                                <th>
                                    IMG
                                </th>
                                <th>
                                    Title
                                </th>
                                <th>
                                    Slug
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in items.slice(0, 3)" :key="String(item.slug)">
                                <td>
                                    <div style="width: 4.8rem">
                                        <b-image :src="item.thumbnail" ratio="5by3" />
                                    </div>
                                </td>
                                <td>
                                    {{ item.title }}
                                </td>
                                <td>
                                    <NuxtLink :to="`/admin/item/${item.slug}`">
                                        {{ item.slug }}
                                    </NuxtLink>
                                </td>
                            </tr>  
                        </tbody>
                    </table>
                    <BButton @click="() => $router.push('/admin/item')" class="is-warning is-fullwidth"> Manage </BButton>
                </Card>
                <Card className="column is-half box m-2">
                    <h1 class="title is-4 link has-text-centered">
                        Tops
                    </h1>
                    <table class="table is-fullwidth">
                        <thead>
                            <tr>
                                <th>
                                    Image
                                </th>
                                <th>
                                    name
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="top in tops.slice(0, 3)" :key="top.id">
                                <td>
                                    <div style="width: 4.8rem">
                                        <b-image :src="top.image" ratio="5by3" />
                                    </div>
                                </td>
                                <td>
                                    {{ top.name }}
                                </td>
                            </tr>  
                        </tbody>
                    </table>
                    <BButton @click="() => $router.push('/admin/top')" class="is-warning is-fullwidth"> Manage </BButton>
                </Card>
                <Card className="column is-half box m-2">
                    <h1 class="title is-4 link has-text-centered">
                        Posts
                    </h1>
                    <table class="table is-fullwidth">
                        <thead>
                            <tr>
                                <th>
                                    Image
                                </th>
                                <th>
                                    Title
                                </th>
                                <th>
                                    Caption
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="post in posts.slice(0, 3)" :key="post.id">
                                <td>
                                    <div style="width: 4.8rem">
                                        <b-image :src="post.picture" ratio="5by3" />
                                    </div>
                                </td>
                                <td>
                                    {{ post.title }}
                                </td>
                                <td>
                                    {{ post.caption.slice(0, 45) }}...
                                </td>
                            </tr>  
                        </tbody>
                    </table>
                    <BButton @click="() => $router.push('/admin/post')" class="is-warning is-fullwidth"> Manage </BButton>
                </Card>
                <Card className="column is-half box m-2">
                    <h1 class="title is-4 link has-text-centered">
                        Highlights
                    </h1>
                    <table class="table is-fullwidth">
                        <thead>
                            <tr>
                                <th>
                                    Image
                                </th>
                                <th>
                                    Title
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="highlight in highlights.slice(0, 3)" :key="highlight.id">
                                <td>
                                    <div style="width: 4.8rem">
                                        <b-image :src="highlight.picture" ratio="5by3" />
                                    </div>
                                </td>
                                <td>
                                    {{ highlight.title }}
                                </td>
                            </tr>  
                        </tbody>
                    </table>
                    <BButton @click="() => $router.push('/admin/highlight')" class="is-warning is-fullwidth"> Manage </BButton>
                </Card>
            </Row>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            items: [],
            tops: [],
            posts: [],
            highlights: []
        }
    },
    created() {
        this.$axios.get('api/top/')
        .then(resp => this.tops = resp.data)
        this.$axios.get('api/item/')
        .then(resp => this.items = resp.data)
        this.$axios.get('api/post/')
        .then(resp => this.posts = resp.data)
        this.$axios.get('api/highlight/')
        .then(resp => this.highlights = resp.data)
    }
}
</script>