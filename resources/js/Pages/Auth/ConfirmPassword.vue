<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/components/InputError.vue';

import { CardContent, CardFooter } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';

import { Head, useForm } from '@inertiajs/vue3';

const form = useForm({
    password: ''
});

const submit = () => {
    form.post(route('password.confirm'), {
        onFinish: () => form.reset()
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Confirm Password" />

        <form @submit.prevent="submit">
            <CardContent class="grid gap-4">
                <div class="mt-4 text-sm text-gray-600 dark:text-gray-400">
                    This is a secure area of the application. Please confirm your password before continuing.
                </div>

                <div class="mt-6 grid gap-2">
                    <Label for="password">Password</Label>
                    <Input
                        id="password"
                        v-model="form.password"
                        type="password"
                        required
                        autocomplete="current-password"
                        autofocus
                    />
                    <InputError :message="form.errors.password" />
                </div>
            </CardContent>
            <CardFooter>
                <Button class="w-full" :disabled="form.processing" type="submit">Confirm</Button>
            </CardFooter>
        </form>
    </GuestLayout>
</template>
