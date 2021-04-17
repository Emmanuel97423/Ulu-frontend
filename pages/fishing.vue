<template>
  <div>
    <div class="text-4xl">Fishing page</div>
    <div class="links">
      <NuxtLink class="button--green" to="/postOneFish"
        >Envoyé poisson</NuxtLink
      >
    </div>
    <CardFish
      :key="componentKey"
      :fishies="fishies"
      @refreshCardFish="refresh"
    ></CardFish>
  </div>
</template>
<script>
import CardFish from '@/components/fishing/CardFish'
export default {
  name: 'FishingPage',
  components: {
    CardFish,
  },
  async asyncData({ $axios }) {
    const fishies = await $axios.$get('http://localhost:8080/api/fishies')
    return { fishies }
  },
  data() {
    return {
      componentKey: 0,
      timer: '',
    }
  },
  created() {
    this.refresh()
    this.timer = setInterval(this.refresh, 15000)
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
  },
  beforeDestroy() {
    this.cancelAutoUpdate()
  },
  methods: {
    refresh() {
      this.$nuxt.refresh()
    },

    cancelAutoUpdate() {
      clearInterval(this.timer)
    },
  },
}
</script>
<style scoped></style>
