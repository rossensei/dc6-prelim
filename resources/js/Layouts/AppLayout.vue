<script setup>
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import SidebarComponent from '@/Components/SidebarComponent.vue';
import { ref, provide } from 'vue';

const isCollapsed = ref(false)

const collapseSidebar = () => {
    isCollapsed.value = !isCollapsed.value;
}

const selectedColor = ref('')
provide('color', selectedColor)

const themeColors = ref([
    'Blue',
    'Red',
    'Green'
])
</script>

<template>
    <div>
        <div class="flex items-start min-h-screen bg-gray-50">
            <div 
                class="sticky top-0 z-10 min-h-screen duration-150" 
                :class="[ 
                    !isCollapsed ? 'w-64' : 'w-16',
                    selectedColor == 'Blue' ? 'bg-blue-600' : 'bg-black',
                    selectedColor == 'Red' ? 'bg-red-600' : 'bg-black',
                    selectedColor == 'Green' ? 'bg-green-600' : 'bg-black',
                    ]">
                <div class="relative p-4">
                    <!-- Trigger -->
                    <span @click="collapseSidebar" class="text-2xl absolute top-4 -right-8 text-gray-400 hover:text-gray-300">
                        <i class="fa-solid" :class="[!isCollapsed ? 'fa-circle-chevron-left' : 'fa-circle-chevron-right' ]"></i>
                    </span>

                    <SidebarComponent :isCollapsed="isCollapsed" />

                    <select v-model="selectedColor" id="color" class="rounded-lg text-sm mt-5">
                        <option value="">Select a color</option>
                        <option v-for="(color, index) in themeColors" :key="index" :value="color">{{ color }}</option>
                    </select>
                </div>
            </div>
            <div class="flex-1 min-h-screen">
                <!-- Page Heading -->
                <header class="" v-if="$slots.header">
                    <div class="flex justify-between items-center max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
                        <slot name="header" />

                        <div class="hidden sm:flex sm:items-center sm:ml-6">
                            <!-- Settings Dropdown -->
                            <div class="ml-3 relative">
                                <Dropdown align="right" width="48">
                                    <template #trigger>
                                        <span class="inline-flex rounded-md">
                                            <button
                                                type="button"
                                                class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150"
                                            >
                                                {{ $page.props.auth.user.name }}
    
                                                <svg
                                                    class="ml-2 -mr-0.5 h-4 w-4"
                                                    xmlns="http://www.w3.org/2000/svg"
                                                    viewBox="0 0 20 20"
                                                    fill="currentColor"
                                                >
                                                    <path
                                                        fill-rule="evenodd"
                                                        d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                                        clip-rule="evenodd"
                                                    />
                                                </svg>
                                            </button>
                                        </span>
                                    </template>
    
                                    <template #content>
                                        <DropdownLink :href="route('profile.edit')"> Profile </DropdownLink>
                                        <DropdownLink :href="route('logout')" method="post" as="button">
                                            Log Out
                                        </DropdownLink>
                                    </template>
                                </Dropdown>
                            </div>
                        </div>
                    </div>
                </header>

                <!-- Page Content -->
                <main>
                    <slot />
                </main>
            </div>
        </div>
    </div>
</template>