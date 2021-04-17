<template>
  <!--<div class="m-12">
    <h2>Fish Card component</h2>
    <div class="button--green" @click="getAllFish()">Voir poissons</div>
    <div class="flex flex-row flex-wrap">
      <div
        class="container mx-auto px-4 m-5 border-8 rounded-2xl w-1/6"
        v-for="fish in fishies"
        :key="fish.id"
      >
        {{ fish }}
      </div>
    </div>
  </div>-->
  <div
    class="flex flew-row flex-wrap items-center justify-center max-w-7xl mx-auto"
  >
    <div
      v-for="fish in fishies.slice().reverse()"
      :key="fish._id"
      class="max-h-screen"
    >
      <div class="max-w-sm w-full py-6 px-3">
        <div class="bg-white shadow-xl rounded-lg overflow-hidden">
          <div
            class="bg-cover bg-center h-56 p-4"
            :style="{
              'background-image': `url(${require('@/assets/images/IMG_2390.jpg')})`,
            }"
          >
            <div class="flex justify-end">
              <svg
                class="h-6 w-6 text-white fill-current"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path
                  d="M12.76 3.76a6 6 0 0 1 8.48 8.48l-8.53 8.54a1 1 0 0 1-1.42 0l-8.53-8.54a6 6 0 0 1 8.48-8.48l.76.75.76-.75zm7.07 7.07a4 4 0 1 0-5.66-5.66l-1.46 1.47a1 1 0 0 1-1.42 0L9.83 5.17a4 4 0 1 0-5.66 5.66L12 18.66l7.83-7.83z"
                ></path>
              </svg>
            </div>
          </div>
          <div class="p-4">
            <p class="uppercase tracking-wide text-sm font-bold text-gray-700">
              {{ fish.type }} • {{ fish.estimateWeight }} kg
            </p>
            <p class="text-xs tracking-wide font-bold text-gray-700">
              Pêché le <em>{{ fish.fishingDate }}</em>
            </p>
            <p class="text-3xl text-gray-900">{{ fish.price }} €</p>
            <p class="text-gray-700">{{ fish.zone }}</p>
          </div>
          <div class="flex border-t border-gray-300 text-gray-700"></div>

          <Dib :fish="fish" @refreshDib="refreshCardFish"></Dib>
          <div class="px-4 pt-3 pb-4 border-t border-gray-300 bg-gray-100">
            <div
              class="text-xs uppercase font-bold text-gray-600 tracking-wide"
            >
              Bâteau
            </div>
            <div class="flex items-center pt-2">
              <div
                class="bg-cover bg-center w-10 h-10 rounded-full mr-3"
                :style="{
                  'background-image': `url(${require('@/assets/images/T5CTW7XDXKLAORLE7JVJCJP2ZA.jpg')})`,
                }"
              ></div>
              <div>
                <p class="font-bold text-gray-900">{{ fish.boatName }}</p>
                <p class="text-sm text-gray-700">
                  Mat. {{ fish.boatMatricule }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Dib from './Dib'
export default {
  components: {
    Dib,
  },
  props: {
    fishies: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      id: '',
      dib: {
        amount: '',
        claimed: '',
      },
    }
  },
  methods: {
    refreshCardFish() {
      this.$emit('refreshCardFish')
    },
  },
}
</script>

<style scoped>
.button--green {
  cursor: pointer;
}
.container {
  display: flex;
  flex-direction: column;
  width: 50%;
  height: 50%;
  border: 1px solid black;
}
</style>
