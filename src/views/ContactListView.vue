<template>
    <div class="p-6">
        <div class="flex flex-row justify-between">
            <h1 class="text-red-500 text-lg font-bold">{{ title }}</h1>
            <button type="button"
                class="px-3 py-1.5 text-sm font-medium text-gray-700 transition-colors border border-indigo-500 rounded-md hover:bg-indigo-100 hover:text-gray-900 focus:relative"
                @click="openModalAdd()">Add contact</button>
        </div>
        <div class="flex flex-row justify-between">
            <label for="Search">
                <div class="flex flex-row items-center">
                    <span class="text-sm font-medium text-gray-700 mr-4">Search: </span>
                    <span class="inset-y-0 grid w-8 place-content-center">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="size-4">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                        </svg>
                    </span>
                    <div>
                        <input type="search" id="Search" v-model="searchQuery" placeholder="Search name or email..."
                            class="mt-0.5 p-2 w-full min-w-[500px] rounded border-gray-100 shadow-md sm:text-sm outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-gray-50" />
                    </div>
                </div>
            </label>
            <div class="flex gap-4 sm:gap-6 mb-6 p-4">
                <span class="text-sm font-medium text-gray-700"> Filters: </span>
                <details class="group relative">
                    <summary
                        class="flex items-center gap-2 border-b border-gray-300 pb-1 text-gray-700 transition-colors hover:border-gray-400 hover:text-gray-900 [&::-webkit-details-marker]:hidden">
                        <span class="text-sm font-medium">City</span>
                        <span class="transition-transform group-open:-rotate-180">
                            <svg xmlns="http://www.w3.org/2000/svg" class="size-4" fill="none" viewBox="0 0 24 24"
                                stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                                    d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                            </svg>
                        </span>
                    </summary>
                    <div
                        class="z-auto w-64 divide-y divide-gray-300 rounded border border-gray-300 bg-white shadow-sm group-open:absolute group-open:top-8 group-open:right-0">
                        <div class="flex items-center justify-between px-3 py-2">
                            <span class="text-sm text-gray-700">
                                {{ selectedCity ? selectedCity : '0 Selected' }}
                            </span>
                            <button type="button" class="text-sm text-gray-700 underline hover:text-gray-900"
                                @click="selectedCity = ''">
                                Reset
                            </button>
                        </div>
                        <fieldset class="p-3">
                            <legend class="sr-only">Cities</legend>
                            <div class="flex flex-col items-start gap-3">
                                <label v-for="(city, index) in cities" :key="index"
                                    class="inline-flex items-center gap-3">
                                    <input type="radio" :value="city" v-model="selectedCity"
                                        class="size-5 rounded border-gray-300 shadow-sm" />
                                    <span class="text-sm font-medium text-gray-700">{{ city }}</span>
                                </label>
                            </div>
                        </fieldset>
                    </div>
                </details>

                <details class="group relative">
                    <summary
                        class="flex items-center gap-2 border-b border-gray-300 pb-1 text-gray-700 transition-colors hover:border-gray-400 hover:text-gray-900 [&::-webkit-details-marker]:hidden">
                        <span class="text-sm font-medium">Country</span>
                        <span class="transition-transform group-open:-rotate-180">
                            <svg xmlns="http://www.w3.org/2000/svg" class="size-4" fill="none" viewBox="0 0 24 24"
                                stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                                    d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                            </svg>
                        </span>
                    </summary>
                    <div
                        class="z-auto w-64 divide-y divide-gray-300 rounded border border-gray-300 bg-white shadow-sm group-open:absolute group-open:right-0 group-open:top-8">
                        <div class="flex items-center justify-between px-3 py-2">
                            <span class="text-sm text-gray-700">
                                {{ selectedCountry ? selectedCountry : '0 Selected' }}
                            </span>
                            <button type="button" class="text-sm text-gray-700 underline hover:text-gray-900"
                                @click="selectedCountry = ''">
                                Reset
                            </button>
                        </div>
                        <fieldset class="p-3">
                            <legend class="sr-only">Countries</legend>
                            <div class="flex flex-col items-start gap-3">
                                <label v-for="(country, index) in countries" :key="index"
                                    class="inline-flex items-center gap-3">
                                    <input type="radio" :value="country" v-model="selectedCountry"
                                        class="size-5 rounded border-gray-300 shadow-sm" />
                                    <span class="text-sm font-medium text-gray-700">{{ country }}</span>
                                </label>
                            </div>
                        </fieldset>
                    </div>
                </details>
            </div>
        </div>
        <div>
            <table class="min-w-full max-w-full divide-y divide-gray-200 box-border overflow-x-auto">
                <thead>
                    <tr class="box-border">
                        <th class="w-[150px] text-red-500" scope="col">Id</th>
                        <th class="max-w-[150px] text-red-500" scope="col">Name</th>
                        <th class="max-w-[150px] text-red-500" scope="col">Email</th>
                        <th class="max-w-[150px] text-red-500" scope="col">Address</th>
                        <th class="max-w-[150px] text-red-500" scope="col">Phone</th>
                        <th class="max-w-[150px] text-red-500" scope="col">Country</th>
                        <th class="max-w-[150px] text-red-500" scope="col">City</th>
                        <th class="max-w-[150px] text-red-500" scope="col">Actions</th>
                    </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                    <tr v-for="(item, index) in getItems" :key="item.id">
                        <td class="max-w-[150px] text-center">{{ item.id }}</td>
                        <td class="max-w-[150px] text-center">{{ item.name }}</td>
                        <td class="max-w-[150px] text-center">{{ item.email }}</td>
                        <td class="max-w-[150px] text-center">{{ item.address }}</td>
                        <td class="max-w-[150px] text-center">{{ item.phone }}</td>
                        <td class="max-w-[150px] text-center">{{ item.country }}</td>
                        <td class="max-w-[150px] text-center">{{ item.city }}</td>
                        <td class="p-2 text-center">
                            <button type="button"
                                class="px-3 py-1.5 text-sm mr-4 font-medium text-gray-700 transition-colors border border-indigo-500 rounded-md hover:bg-indigo-100 hover:text-gray-900 focus:relative"
                                @click="openModalEdit(index)">Edit contact</button>
                            <button type="button"
                                class="px-3 py-1.5 text-sm font-medium text-gray-700 transition-colors border border-red-500 rounded-md hover:bg-red-100 hover:text-gray-900 focus:relative"
                                @click="deleteContact(index)">
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    <!-- Modal -->
    <div v-if="isModalOpen" class="fixed inset-0 z-50 grid place-content-center bg-black/50 p-4" role="dialog"
        aria-modal="true" aria-labelledby="modalTitle">
        <div class="w-[500px] max-w-md rounded-lg bg-white p-6 shadow-lg relative">
            <div class="flex items-start justify-between">
                <h2 id="modalTitle" class="text-xl font-bold text-gray-900 sm:text-2xl">
                    {{ modalMode === 'edit' ? 'Edit Contact' : 'Add Contact' }}
                </h2>

                <button type="button" @click="closeModal"
                    class="-me-4 -mt-4 rounded-full p-2 text-gray-400 transition-colors hover:bg-gray-50 hover:text-gray-600 focus:outline-none"
                    aria-label="Close">
                    <svg xmlns="http://www.w3.org/2000/svg" class="size-5" fill="none" viewBox="0 0 24 24"
                        stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>

            <div class="mt-4">
                <EditContact v-if="selectedContact && modalMode === 'edit'" :contact="selectedContact"
                    @update="saveEdited" @cancel="closeModal" />
                <AddContact v-if="modalMode === 'create'" @created="addNewContact($event)" />
            </div>
        </div>
    </div>

</template>

<script>
import EditContact from '@/components/EditContact.vue';
import AddContact from '@/components/AddContact.vue';
import { email } from '@vuelidate/validators';
export default {
    name: 'ContactListView',
    data() {
        return {
            title: 'Contact List',
            items: [
                {
                    id: 1,
                    name: "Alice Johnson",
                    email: "alice.johnson@example.com",
                    address: "123 Maple Street",
                    phone: "123-456-7890",
                    country: "USA",
                    city: "New York"
                },
                {
                    id: 2,
                    name: "Bob Smith",
                    email: "bob.smith@example.com",
                    address: "456 Oak Avenue",
                    phone: "987-654-3210",
                    country: "Canada",
                    city: "Toronto"
                },
                {
                    id: 3,
                    name: "Carol White",
                    email: "carol.white@example.com",
                    address: "789 Pine Road",
                    phone: "555-123-4567",
                    country: "UK",
                    city: "London"
                },
                {
                    id: 4,
                    name: "David Brown",
                    email: "david.brown@example.com",
                    address: "321 Elm Street",
                    phone: "444-555-6666",
                    country: "Australia",
                    city: "Sydney"
                },
                {
                    id: 5,
                    name: "Emily Davis",
                    email: "emily.davis@example.com",
                    address: "654 Spruce Lane",
                    phone: "333-444-5555",
                    country: "USA",
                    city: "Los Angeles"
                }
            ],
            isModalOpen: false,
            selectedContact: null,
            selectedIndex: 0,
            cities: [
                'New York',
                'Toronto',
                'London',
                'Sydney',
                'Los Angeles',
            ],
            countries: [
                'USA',
                'Canada',
                'Australia',
                'UK',
            ],
            selectedCity: "",
            selectedCountry: "",
            searchQuery: "",
            modalMode: "create"
        }
    },
    components: {
        EditContact,
        AddContact,
    },
    mounted() {

    },
    methods: {
        openModalAdd() {
            this.modalMode = "create";
            this.isModalOpen = true;
        },
        openModalEdit(index) {
            this.selectedIndex = index;
            this.selectedContact = this.items[index];
            this.modalMode = "edit";
            this.isModalOpen = true;
        },
        closeModal() {
            this.isModalOpen = false;
            this.selectedContact = null;
            this.selectedIndex = null;
            this.modalMode = null;
        },
        saveEdited(editedContact) {
            this.items[this.selectedIndex] = editedContact;
            this.closeModal();
        },
        deleteContact(index) {
            if (confirm('Are you sure you want to delete this contact?')) {
                this.items.splice(index, 1);
            }
        },
        addNewContact($event) {
            const maxId = Math.max(...this.items.map(contact => contact.id), 0);
            $event['id'] = maxId + 1;
            this.items.push($event);
            this.closeModal();
        }
    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
        getItems() {
            let result = [...this.items];

            if (this.selectedCity !== "") {
                result = result.filter(item => item.city === this.selectedCity);
            }

            if (this.selectedCountry !== "") {
                result = result.filter(item => item.country === this.selectedCountry);
            }

            if (this.searchQuery.trim() !== '') {
  result = result.filter(item =>
    item.name.toLowerCase().includes(this.searchQuery.trim().toLowerCase()) ||
    item.email.toLowerCase().includes(this.searchQuery.trim().toLowerCase())
  );
}


            return result;
        }
    }
}
</script>