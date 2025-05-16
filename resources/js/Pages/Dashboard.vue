<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { usePage } from '@inertiajs/vue3';
import { Head } from '@inertiajs/vue3';
import PostList from '@/Components/PostList.vue';
import PostForm from '@/Components/PostForm.vue';

const user = usePage().props.auth.user;

</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2
                class="text-xl font-semibold leading-tight text-gray-800"
            >
                Dashboard
            </h2>
        </template>
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div
                    class="overflow-hidden bg-white shadow-sm sm:rounded-lg"
                >
                    <div class="p-6 text-gray-900">
                        You're logged in!
                    </div>
                </div>

                <div v-if="user.is_admin ===true" class="mt-6 shadow-sm sm:rounded-lg p-6">
                    <PostForm />
                </div>

                <div class="mt-6 bg-white shadow-sm sm:rounded-lg p-6">
                    <PostList />
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
