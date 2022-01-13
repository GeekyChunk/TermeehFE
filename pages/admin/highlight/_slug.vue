<template>
    <section class="section">
        <br /> <br /> <br />
        <div class="container">
            <div class="columns is-centered has-text-centered">
                <div class="column is-half has-text-centered">
                   <form @submit.prevent="Update" class="card p-2 is-centered has-text-centered">
                       <b-image class="m-5 mb-5" :src="data.picture" horizontal rounded>
                       </b-image>
                       <b-field label="Name"
                            horizontal>
                            <b-input v-model="data.title" maxlength="30"></b-input>
                        </b-field>
                        
                        <b-field label="Thumbnail" horizontal>
                            <b-upload v-model="file" class="file-label">
                                <span class="file-cta  has-background-primary has-text-white">
                                    <b-icon class="file-icon" icon="upload"></b-icon>
                                    <span class="file-label">Thumbnail</span>
                                </span>
                                <span class="file-name" v-if="file">
                                    {{ file.name }}
                                </span>
                            </b-upload>
                        </b-field>
                        <button @click.prevent="() => $router.push('/admin/top')" class="button is-danger">Discard</button>
                        <button type="submit" class="button is-success"> Update </button>
                   </form>
                </div>
            </div>
        </div>
    </section>

</template>


<script>
import slugify from 'slugify'

export default {
    async asyncData({ params }) {
      const slug = params.slug
      return {
          slug,
          file: null,
          err: null,
          data: {},
        }
    },
    async created() {
        let resp = await this.$axios.get(`/api/highlight/${this.slug}`)
        this.data = resp.data
    },
    methods: {
        Update(event) {
            let formData = new FormData
            if (this.file != null) {
                formData.append('picture', this.file)
            }
            formData.append('title', this.data.title)
            this.$axios.patch(`api/highlight/${this.slug}/`, formData, { headers: { "Content-Type": "multipart/form-data; boundary=<calculated when request is sent>" } })
            .then(response => {
                this.$router.push('/admin/highlight')
            })
            .catch(err => {
                console.log(err.response)
            })
        },
        slugy(title) {
            return slugify(title.toLowerCase())
        }
    }
}
</script>