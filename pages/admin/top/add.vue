<template>
    <section class="section">
        <br /> <br /> <br />
        <div class="container">
            <div class="columns is-centered has-text-centered">
                <div class="column is-half has-text-centered">
                    <form  @submit.prevent="onSubmit" class="box">
                        <h1 class="title i-3">
                            Add a Top Image
                        </h1>
                        <div class="mb-5" v-if="Object.keys(err) != 0">
                            <b-notification
                                v-for="error in Object.keys(err)"
                                :key="error"
                                type="is-danger is-light"
                                aria-close-label="Close notification"
                                role="alert">
                                {{ error }} : {{ err[error][0] }}
                            </b-notification>
                        </div>
                       <b-field label="Name"
                            horizontal>
                            <b-input v-model="data.name" maxlength="30"></b-input>
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
                        <button class="button is-success">Save</button>

                    </form>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            file: null,
            data: {},
            err: {},
        }
    },
    methods: {
        async onSubmit(event) {
            let formData = new FormData();
            formData.append("image", this.file);
            formData.append("name", this.data.name);
            try {
                await this.$axios.post("api/top/", formData, { headers: { "Content-Type": "multipart/form-data" } })
                this.$router.push('/admin/top')
            } catch (err) {
                this.err = err.response.data
            }        
        },
        slugy(text) {
            return slugify(text.toLowerCase())
        }

    }
}
</script>