<template>
  <div class="container__box">
    <NuxtLink class="button--green" to="/fishing">Retour</NuxtLink>
    <form class="w-full max-w-lg" @submit.prevent="submitFish">
      <div class="flex flex-wrap -mx-3 mb-6">
        <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
          <label
            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-first-name"
          >
            Prise
          </label>
          <input
            id="grid-first-name"
            v-model="fish.type"
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-red-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
            type="text"
            placeholder="Marlin"
          />
          <p class="text-red-500 text-xs italic">Ne peut pas être vide.</p>
        </div>
        <div class="w-full md:w-1/2 px-3">
          <label
            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-last-name"
          >
            Poids estimé
          </label>
          <input
            id="grid-last-name"
            v-model.number="fish.estimateWeight"
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            type="number"
            placeholder="00.00 Kg"
          />
        </div>
        <div class="w-full md:w-1/2 px-3">
          <label
            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-last-name"
          >
            Tarif
          </label>
          <input
            id="grid-last-name"
            v-model.number="fish.price"
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            type="number"
            placeholder="00.00 €"
          />
        </div>
        <div class="btn mt-5 gap-2">
          <!-- component -->

          <label
            class="w-64 flex flex-col items-center px-4 py-1 bg-white text-blue rounded-lg shadow-lg tracking-wide uppercase border border-blue cursor-pointer hover:bg-blue hover:text-white"
          >
            <svg
              class="w-8 h-8"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
            >
              <path
                d="M16.88 9.1A4 4 0 0 1 16 17H5a5 5 0 0 1-1-9.9V7a3 3 0 0 1 4.52-2.59A4.98 4.98 0 0 1 17 8c0 .38-.04.74-.12 1.1zM11 11h3l-4-4-4 4h3v3h2v-3z"
              />
            </svg>
            <span class="mt-2 text-base leading-normal">Select a file</span>
            <input
              id="file-input"
              type="file"
              class="hidden"
              accept="image/*"
              @change="uploadImage($event)"
            />
          </label>

          <button
            class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded"
          >
            Envoyer
          </button>
          <button
            class="bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-4 border border-red-500 hover:border-transparent rounded"
          >
            Annuler
          </button>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
const moment = require('moment')
moment.locale('fr')
export default {
  data() {
    return {
      fish: {
        estimateWeight: '',
        type: '',
        price: '',
        fishingDate: '',
        boatName: 'Calipso',
        zone: 'Port de St Gille',
        dib: {
          amount: 0,
          claimed: '',
        },
      },
    }
  },
  methods: {
    submitFish() {
      console.log(this.fish)
      this.$axios
        .post('http://localhost:8080/api/fish', {
          type: this.fish.type,
          price: this.fish.price,
          estimateWeight: this.fish.estimateWeight,
          boatName: this.fish.boatName,
          zone: this.fish.zone,
          fishingDate: moment().format('LLLL'),
          dib: {
            amount: this.fish.dib.amount,
            claimed: this.fish.dib.claimed,
          },
        })
        .then(() => {
          console.log('Fish envoyé')
        })
        .then(() => {
          console.log('go fishing page')
          this.$router.push('/fishing')
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
}
</script>
<style scoped>
.container__box {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 50px;
}
.btn {
  width: 100%;
  display: flex;
  justify-content: center;
}
</style>
