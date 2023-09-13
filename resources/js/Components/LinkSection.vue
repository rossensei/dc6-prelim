<script setup>
import { Link } from '@inertiajs/vue3';

defineProps({
    isCollapsed: Boolean
})
</script>

<template>
    <div class="flex flex-col space-y-3 mt-4" :class="{ 'items-center' : isCollapsed }">
        <Link href="/dashboard" class="px-2 py-1.5 rounded-lg text-sm text-white hover:bg-white hover:text-black duration-75 space-x-2">
            <i class="fa-solid fa-gauge"></i>
            <span v-show="!isCollapsed" class="text-sm">Dashboard</span>
        </Link>
        <Link href="/clients" class="px-2 py-1.5 rounded-lg text-sm text-white hover:bg-white hover:text-black duration-75 space-x-2">
            <i class="fa-solid fa-users"></i>
            <span v-show="!isCollapsed" class="text-sm">Clients</span>
        </Link>
    </div>
</template>