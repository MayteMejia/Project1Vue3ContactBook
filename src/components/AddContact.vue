<template>
    <div>
        <form @submit.prevent="submit" novalidate>
            <div class="col-span-full">
                <label class="block text-sm/6 font-medium text-gray-900">Name</label>
                <div class="mb-2">
                    <input class="block w-full rounded-md bg-white border px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="contact.name" type="text"/>
                </div>
            </div>
            <div class="col-span-full">
                <label class="block text-sm/6 font-medium text-gray-900">Email</label>
                <div class="mb-2">
                    <input class="block w-full rounded-md bg-white border px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="contact.email" type="text"/>
                </div>
            </div>
            <div class="col-span-full">
                <label class="block text-sm/6 font-medium text-gray-900">Address</label>
                <div class="mb-2">
                    <input class="block w-full rounded-md bg-white border px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="contact.address" type="text"/>
                </div>
            </div>
            <div class="col-span-full">
                <label class="block text-sm/6 font-medium text-gray-900">Phone</label>
                <div class="mb-2">
                    <input class="block w-full rounded-md bg-white border px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="contact.phone" type="text"/>
                </div>
            </div>
            <div class="col-span-full">
                <label class="block text-sm/6 font-medium text-gray-900">Country</label>
                <div class="mb-2">
                    <input class="block w-full rounded-md bg-white border px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="contact.country" type="text"/>
                </div>
            </div>
            <div class="col-span-full">
                <label class="block text-sm/6 font-medium text-gray-900">City</label>
                <div class="mb-2">
                    <input class="block w-full rounded-md bg-white border px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" v-model="contact.city" type="text"/>
                </div>
            </div>
            <button type="submit" class="px-3 py-1.5 text-sm font-medium text-gray-700 transition-colors border border-indigo-500 rounded-md hover:bg-indigo-100 hover:text-gray-900 focus:relative">Save</button>
        </form>
    </div>
</template>

<script>
import { reactive } from 'vue'
import useVuelidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'
export default {
    name: 'NewContactView',
    data() {
        return {
            title: ' NewContact',
            contact: reactive({
                name: '',
                email: '',
                address: '',
                phone: '',
                country: '',
                city: ''
            }),
            variable$: null
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
    },
    created() {
        const rules = {
            contact: {
                name: { required },
                email: { required },
                address: { required },
                phone: { required },
                country: { required },
                city: { required },
            }
        }
        this.variable$ = useVuelidate(rules, { contact: this.contact })
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        async submit() {
            const isValid = await this.variable$.$validate()
            if (!isValid) {
                alert('Please complete the form correctly.')
                return
            }
            this.$emit('created', { ...this.contact });
        }
    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>