<template>
    <section class="container section">
        <br /> <br /> <br />
        <b-button @click="() => {this.$router.push('/admin/top/add')}" class="mb-2 is-success">
            add
        </b-button>

        <template>
            <b-loading :is-full-page="true" v-model="loadin" :can-cancel="false">
            </b-loading>
        </template>

            <b-table :data="data">
              
                <b-table-column label="Image" v-slot="props">
                    <div style="width: 4rem">
                        <b-image :src="props.row.image" :rounded="true" ratio="2by2" />
                    </div>
                </b-table-column>


                <b-table-column field="title" label="Name">
                    <template v-slot="props">
                        {{ props.row.name }}
                    </template>
                </b-table-column>

            

                <b-table-column field="slug" label="Slug">
                    <template v-slot="props">
                        <NuxtLink :to="`/admin/top/${props.row.id}`">
                            {{ props.row.name }}
                        </NuxtLink>
                    </template>
                </b-table-column>

                <b-table-column label="Actions" field="id" v-slot="props">
                    <div class="buttons">
                        <b-button @click="Delete(props.row.id)" class="is-danger">
                             <b-icon
                                icon="delete"
                                size="is-small"
                                type="is-white">
                            </b-icon>
                        </b-button>
                        <b-button @click="$router.push(`/admin/top/${props.row.id}/`)" class="is-success">
                             <b-icon
                                icon="pencil"
                                size="is-small"
                                type="is-white">
                            </b-icon>
                        </b-button>
                    </div>
                </b-table-column>
            </b-table>
    </section>
</template>

<script>
export default {

    data() {
        return {
            data: [],
            loadin: false,
        }
    },
    async created() {
        let response =  await this.$axios.get('api/top/')
        this.data = response.data
    },
    methods: {
        async Refresh() {
            let response = await this.$axios.get('api/top/')
            this.data = response.data
        },
        Delete(slug) {
            this.loadin = true;
            this.$axios.delete(`api/top/${slug}/`)
            .then(() => {
                this.Refresh();
                this.loadin = false;
            })
            .catch(() => this.loading = false)
        }
    }
}
</script>