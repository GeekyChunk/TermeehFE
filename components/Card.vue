<template>
  <div @click="() => {
      if (link != null) {
        $router.push(link)
      }
    }" :style="`max-width: ${maxW != null ? maxW : '40'}rem; width: 100%`" :class="className">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'BuefyCard',
  props: {
    maxW: {
      type: String,
      default: "40",
    },
    className: {
      type: String,
    },
    link: {
      type: String,
      default: null
    }
  }
}
</script>
