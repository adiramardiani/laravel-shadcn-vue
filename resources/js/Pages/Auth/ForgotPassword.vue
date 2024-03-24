<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/components/InputError.vue';

import { CardContent, CardFooter } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';

import { Head, useForm } from '@inertiajs/vue3';

defineProps({
    status: {
        type: String
    }
});

const form = useForm({
    email: ''
});

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <GuestLayout>
        <Head title="Forgot Password" />

        <form @submit.prevent="submit">
            <CardContent class="grid gap-4">
                <div class="mt-4 text-sm text-gray-600 dark:text-gray-400">
                    Forgot your password? No problem. Just let us know your email address and we will email you a password reset
                    link that will allow you to choose a new one.
                </div>

                <div v-if="status" class="text-sm font-medium text-green-600 dark:text-green-400">
                    {{ status }}
                </div>

                <div class="grid gap-2">
                    <Label for="email">Email</Label>
                    <Input id="email" v-model="form.email" type="email" required autofocus autocomplete="username" />
                    <InputError :message="form.errors.email" />
                </div>
            </CardContent>
            <CardFooter>
                <Button class="w-full" :disabled="form.processing" type="submit">Email Password Reset Link</Button>
            </CardFooter>
        </form>
    </GuestLayout>
</template>
