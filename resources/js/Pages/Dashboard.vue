<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import Card from '@/Components/Card.vue';
import { Head, Link } from '@inertiajs/vue3';

const prop = defineProps({
    clientCount: Number
})
</script>

<template>
    <Head title="Dashboard" />

    <AppLayout>
        <template #header>
            <h2 class="font-semibold text-2xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <!-- <Link href="/clients" class="block max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700">
                    <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ prop.clientCount }}</h5>
                    <p class="font-normal text-gray-700 dark:text-gray-400">Total Clients</p>
                </Link> -->

                <Card :clientCount="clientCount"/>
            </div>
        </div>
    </AppLayout>
</template>
