<template>

<div class="relative overflow-x-auto shadow-md sm:rounded-lg">
    <div class="flex justify-end mb-4">
            <div class="inline-flex items-end px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150">
                <router-link :to="{ name: 'companies.create' }" class="text-sm font-medium">Create company</router-link>
            </div>
        </div>
    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Company Name
                </th>
                <th scope="col" class="px-6 py-3">
                    Email
                </th>
                <th scope="col" class="px-6 py-3">
                    Address
                </th>
                <th scope="col" class="px-6 py-3">
                    Website
                </th>
                <th scope="col" class="px-6 py-3">
                    <span class="sr-only">Actions</span>
                </th>
            </tr>
        </thead>
        <tbody>
            <template v-for="item in companies" :key="item.id">
            <tr class="bg-white dark:bg-gray-800">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                    {{ item.name }}
                </th>
                <td class="px-6 py-4">
                    {{ item.email }}
                </td>
                <td class="px-6 py-4">
                    {{ item.address }}
                </td>
                <td class="px-6 py-4">
                    {{ item.website }}
                </td>
                <td class="px-6 py-4 text-right">
                    <router-link :to="{ name: 'companies.edit', params: { id: item.id } }" 
                    class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150">
                        Edit
                    </router-link>
                    <button @click="deleteCompany(item.id)" 
                    class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150"
                    >Delete</button>
                </td>
            </tr>
            </template>
        </tbody>
    </table>
</div>
</template>

<script>
import useCompanies from "../../composables/companies";
import { onMounted } from "vue";

export default {
    setup() {
        const { companies, getCompanies, destroyCompany } = useCompanies()

        onMounted(getCompanies)

        const deleteCompany = async (id) => {
            if (!window.confirm('Are you sure?')){
                return 
            }
            await destroyCompany(id);
            await getCompanies();
        }
        
        return {
            companies,
            deleteCompany,
        }
    }
}
</script>