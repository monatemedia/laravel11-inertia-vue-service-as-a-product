<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Product from '@/Components/Product.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/vue3';

defineProps(['products']);

const form = useForm({
    message: '',
});
</script>

<template>
    <Head title="Products" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Products</h2>
        </template>

        <!-- Form -->
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form @submit.prevent="form.post(route('products.store'), { onSuccess: () => form.reset() })">
                <textarea
                    v-model="form.message"
                    placeholder="What's on your mind?"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                ></textarea>
                <InputError :message="form.errors.message" class="mt-2" />
                <PrimaryButton class="mt-4">Product</PrimaryButton>
            </form>

            <!-- View Products Components -->
            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
            <Product
                v-for="product in products"
                :key="product.id"
                :product="product"
            />
            </div>
        </div>
    </AuthenticatedLayout>
</template>
