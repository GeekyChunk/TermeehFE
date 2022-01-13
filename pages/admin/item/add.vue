<template>
    <section class="section">
        <br /> <br /> <br />
        <div class="container">
            <div class="columns is-centered has-text-centered">
                <div class="column is-half has-text-centered">
                    <form  @submit.prevent="onSubmit" class="box">
                        <h1 class="title i-3">
                            Add a Item
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
                       <b-field label="Title"
                            horizontal>
                            <b-input v-model="data.title" maxlength="30"></b-input>
                        </b-field>
                        
                        <b-field v-if="data.title" label="Slug" horizontal>
                            <b-input :value="slugy(data.title)" disabled>
                            </b-input>
                        </b-field>
                        
                        <b-field label="Price" horizontal>
                            <b-input v-model="data.price">
                            </b-input>
                        </b-field>

                        <b-field label="Description" horizontal>
                            <b-input maxlength="500" v-model="data.description" type="textarea"></b-input>
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
                        <button @click.prevent="() => $router.push('/admin/item')" class="button is-danger">Discard</button>
                        <button class="button is-success">Save</button>

                    </form>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import slugify from 'slugify'
export default {
    data() {
        return {
            file: null,
            data: {
                title: ""
            },
            err: {},
        }
    },
    methods: {
        async onSubmit(event) {
            let formData = new FormData();
            formData.append("thumbnail", this.file);
            formData.append("title", this.data.title);
            formData.append("price", Number(this.data.price));
            formData.append("slug", slugify(this.data.title.toLowerCase()));
            formData.append("description", this.data.description);
            try {
                await this.$axios.post("api/item/", formData, { headers: { "Content-Type": "multipart/form-data" } })
                this.$router.push('/admin/item')
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