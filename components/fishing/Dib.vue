<template>
  <div>
    <div class="flex flex-row m-3">
      <div class="flex-1 inline-flex items-center">
        <button
          class="mr-3 bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded"
          @click="addDib()"
        >
          Enchérir
        </button>
      </div>
      <div>
        <label
          for="price"
          class="block text-sm font-medium text-gray-700"
        ></label>
        <div class="mt-1 relative rounded-md shadow-sm">
          <div
            class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none"
          >
            <span class="text-gray-900 sm:text-sm"> € </span>
          </div>
          <input
            id="price"
            v-model.number="dib.amount"
            type="number"
            name="price"
            class="focus:ring-indigo-500 focus:border-indigo-500 block w-full py-2 px-8 sm:text-sm border-gray-300 rounded-md"
            placeholder="0.00"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dib',
  props: {
    fish: {
      type: Object,
      required: true,
    },
  },
  data() {
    return { user: { id: 'userId' }, dib: { amount: '', claimed: 'UserId' } }
  },
  methods: {
    addDib() {
      this.$axios
        .put('http://localhost:8080/api/fish/' + this.fish._id, {
          _id: this.fish._id,
          price: this.fish.price,
          dib: {
            amount: this.dib.amount,
            claimed: this.dib.claimed,
          },
        })
        .then(() => {
          this.$emit('refreshDib')
          console.log(this.dib)
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
}
</script>

<style scoped></style>
