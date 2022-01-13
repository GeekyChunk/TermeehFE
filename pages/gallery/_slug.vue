<template>
  <div class="bg-img p-5">
    <br /> <br /> <br />
      <section class="box container">
          <div v-if="data" class="mt-5 p-5 columns is-centered has-text-centered">
            <b-image class="column has-text-centered mr-3" style="max-width: 25rem" :src="data.thumbnail"  horizontal/>
            
            <div class="column p-0">
              <div class="columns">
                
                <div class="column">
                  <div class="columns is-mobile">
                    <div class="column is-size-5 has-text-left">
                      {{ data.price }}
                    </div>
                    <div class="column title is-5 has-text-right">
                      قیمت
                    </div>
                  </div>
                </div>
                
                <div class="column">
                  <div class="columns is-mobile">
                    <div class="column is-size-5 has-text-left">
                      {{ data.title }}
                    </div>
                    <div class="column title is-5 has-text-right">
                      :نام
                    </div>
                  </div>
                </div>
              </div>

              <hr />

              <div class="columns">
                <div class="column p-0">
                  <div class="has-text-right">
                    <div class="title is-5">
                      :توضیحات
                    </div>
                    <div class="is-size-6 has-text-centered">
                      <span v-html="data.description" />
                    </div>
                  </div>
                </div>
              </div>
              <hr />
              <BButton @click="() => $router.push('/gallery/')" class="is-danger"> بازگشت </BButton>
            </div>
          </div>
      </section>
  </div>
</template>

<script>
  export default {
    async asyncData({ params }) {
      const slug = params.slug
      return {
        slug,
        data: null,
      }
    },
    async created() {
      let data = await this.$axios.$get(`api/item/${this.slug}`)
      data.description =  data.description.replace('\n', "<br />")
      this.data = data
    }
  }
</script>

