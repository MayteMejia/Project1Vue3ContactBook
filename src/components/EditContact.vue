<template>
    <div>
      <form @submit.prevent="issueEditedData" novalidate>
        <div class="mb-3">
          <label class="block text-sm/6 font-medium text-gray-900">Name</label>
          <input class="block w-full rounded-md bg-white px-3 py-1.5 border text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="edited.name" type="text" required />
        </div>
  
        <div class="mb-3">
          <label class="block text-sm/6 font-medium text-gray-900">Email</label>
          <input class="block w-full rounded-md bg-white px-3 py-1.5 border text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="edited.email" type="text" required />
        </div>
  
        <div class="mb-3">
          <label class="block text-sm/6 font-medium text-gray-900">Address</label>
          <input class="block w-full rounded-md bg-white px-3 py-1.5 border text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="edited.address" type="text" required />
        </div>
  
        <div class="mb-3">
          <label class="block text-sm/6 font-medium text-gray-900">Phone</label>
          <input class="block w-full rounded-md bg-white px-3 py-1.5 border text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="edited.phone" type="text" required />
        </div>
  
        <div class="mb-3">
          <label class="block text-sm/6 font-medium text-gray-900">Country</label>
          <input class="block w-full rounded-md bg-white px-3 py-1.5 border text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="edited.country" type="text" required />
        </div>
  
        <div class="mb-3">
          <label class="block text-sm/6 font-medium text-gray-900">City</label>
          <input class="block w-full rounded-md bg-white px-3 py-1.5 border text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="edited.city" type="text" required />
        </div>
        <button type="submit" class="px-3 py-1.5 text-sm font-medium text-gray-700 transition-colors border border-indigo-500 rounded-md hover:bg-indigo-100 hover:text-gray-900 focus:relative">Save Changes</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'EditContact',
    props: {
      contact: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        // Copia del objeto original para evitar modificarlo directamente
        edited: { ...this.contact }
      }
    },
    methods: {
      issueEditedData() {
        // Emitimos un evento con los datos modificados
        this.$emit('update', this.edited)
      }
    }
  }
  </script>
  