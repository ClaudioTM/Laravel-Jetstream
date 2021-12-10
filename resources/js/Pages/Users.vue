<template>
    <app-layout title="Users">

    <div class="max-w-3xl mx-auto mt-10">

        <div class="flex justify-between mb-6">
            <h1 class="text-3xl">
                Users
            </h1>

            <input v-model="search" type="text" placeholder="Search..." class="border px-2 rounded-lg">

        </div>

        <div class="flex flex-col mb-7">
            <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                    <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
                        <table class="min-w-full divide-y divide-gray-200">
                            <tbody class="bg-white divide-y divide-gray-200">
                            <tr v-for="user in users.data" :key="user.id">
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <div class="flex items-center">
                                        <div>
                                            <div class="text-sm font-medium text-gray-900">
                                                {{ user.name }}
                                            </div>
                                        </div>
                                    </div>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-300 text-green-800">
                                         Active
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-red-300 text-red-800">
                                         Inactive
                                    </span>
                                </td>

                                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                                    <Link :href="`/users${user.id}/edit`" class="text-indigo-600 hover:text-indigo-900">Edit
                                    </Link>
                                </td>
                            </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>


<!--        <Pagination :links="users.links" class="mt-7" />-->


    </div>
    </app-layout>
</template>

<script setup>
import {Link} from "@inertiajs/inertia-vue3";
import Pagination from "./Shared/Pagination";
import { ref, watch } from "vue";
import AppLayout from "@/Layouts/AppLayout";
import {Inertia} from "@inertiajs/inertia";
import throttle from "lodash/throttle"

let props = defineProps({
    users: Object,
    filters: Object
});

let search = ref(props.filters.search);

watch(search, throttle(function (value) {
    Inertia.get('/users', { search: value }, {
        preserveState: true,
        replace: true
    });
}, 300));
</script>
