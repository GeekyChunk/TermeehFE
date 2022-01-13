<template>
    <section class="container section">
        <br /> <br /> <br />
        <b-button @click="() => {this.$router.push('/admin/item/add')}" class="mb-2 is-success">
            add
        </b-button>

        <template>
            <b-loading :is-full-page="true" v-model="loadin" :can-cancel="false">
            </b-loading>
        </template>

            <b-table :data="data">
              
                <b-table-column label="Thumbnail" v-slot="props">
                    <div style="width: 4rem">
                        <b-image :src="props.row.thumbnail" :rounded="true" ratio="2by2" />
                    </div>
                </b-table-column>


                <b-table-column field="title" label="Item Title">
                    <template v-slot="props">
                        {{ props.row.title }}
                    </template>
                </b-table-column>

                <b-table-column field="price" label="Item Price">
                    <template v-slot="props">
                        {{ props.row.price }}
                    </template>
                </b-table-column>

                <b-table-column field="descriptions" label="Description" centered v-slot="props">
                    <span>
                        {{ props.row.description }}
                    </span>
                </b-table-column>
                <b-table-column label="Actions" field="slug" v-slot="props">
                    <div class="buttons">
                        <b-button @click="Delete(props.row.slug)" class="is-danger">
                             <b-icon
                                icon="delete"
                                size="is-small"
                                type="is-white">
                            </b-icon>
                        </b-button>
                        <b-button @click="$router.push(`/admin/item/${props.row.slug}`)" class="is-success">
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
        let response =  await this.$axios.get('api/item/')
        this.data = response.data
    },
    methods: {
        async Refresh() {
            let response = await this.$axios.get('api/item/')
            this.data = response.data
        },
        Delete(slug) {
            this.loadin = true;
            this.$axios.delete(`api/item/${slug}/`)
            .then(() => {
                this.Refresh();
                this.loadin = false;
            })
            .catch(() => this.loading = false)
        }
    }
}
</script>