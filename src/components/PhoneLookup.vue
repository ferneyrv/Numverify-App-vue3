<template>
  <div class="min-h-screen flex items-center justify-center bg-gradient-to-r from-blue-50 to-blue-100">
    <div class="bg-white shadow-xl rounded-3xl p-8 w-full max-w-lg">
      <h1 class="text-4xl font-extrabold text-gray-800 mb-6 text-center">Búsqueda de teléfono</h1>
      
      <input
        v-model="phoneNumber"
        type="text"
        placeholder="Enter phone number"
        class="w-full p-4 mb-5 border border-gray-200 rounded-lg text-gray-700 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-400 transition duration-300"
      />
      
      <button
        @click="lookupPhoneNumber"
        class="w-full bg-blue-500 text-white py-3 px-6 rounded-lg font-semibold hover:bg-blue-600 transition duration-300 ease-in-out shadow-lg"
      >
        Buscar
      </button>

      <div v-if="phoneData" class="mt-8 bg-gray-50 p-6 rounded-lg shadow-md">
        <h2 class="text-2xl font-semibold mb-4 text-gray-800">Información del teléfono</h2>
        <div class="space-y-2">
          <p><strong class="text-gray-600">Número:</strong> {{ phoneData.number }}</p>
          <p><strong class="text-gray-600">País:</strong> {{ phoneData.country_name }}</p>
          <p><strong class="text-gray-600">Empresa Telefonia:</strong> {{ phoneData.carrier }}</p>
          <p><strong class="text-gray-600">Tipo de linea:</strong> {{ phoneData.line_type }}</p>
        </div>
      </div>
    </div>
  </div>
</template>



<script>
import axios from 'axios';

export default {
  data() {
    return {
      phoneNumber: '',
      phoneData: null,
      apiKey: '1578f764ba8918bd9d8db929fba181bc',
    };
  },
  methods: {
    async lookupPhoneNumber() {
      try {
        const response = await axios.get(
          `http://apilayer.net/api/validate?access_key=${this.apiKey}&number=${this.phoneNumber}`
        );
        this.phoneData = response.data;
      } catch (error) {
        console.error('Error al recuperar los datos del teléfono:', error);
      }
    },
  },
};
</script>

<style scoped>
.min-h-screen {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
</style>
