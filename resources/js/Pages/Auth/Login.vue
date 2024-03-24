<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/components/InputError.vue';

import { CardContent, CardFooter } from '@/components/ui/card';
import { Checkbox } from '@/components/ui/checkbox';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';

import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean
    },
    status: {
        type: String
    }
});

const form = useForm({
    email: '',
    password: '',
    remember: false
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password')
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <form @submit.prevent="submit">
            <CardContent class="grid gap-4">
                <div v-if="status" class="mt-4 text-sm font-medium text-green-600">
                    {{ status }}
                </div>

                <div class="grid gap-2">
                    <Label for="email">Email</Label>
                    <Input id="email" v-model="form.email" type="email" required autofocus autocomplete="username" />
                    <InputError :message="form.errors.email" />
                </div>
                <div class="grid gap-2">
                    <div class="flex items-center">
                        <Label for="password">Password</Label>
                        <Link
                            v-if="canResetPassword"
                            :href="route('password.request')"
                            class="ml-auto inline-block text-sm underline"
                        >
                            Forgot your password?
                        </Link>
                    </div>
                    <Input id="password" v-model="form.password" type="password" required autocomplete="current-password" />
                    <InputError :message="form.errors.password" />
                </div>
                <div class="grid gap-2">
                    <div class="flex items-center space-x-2">
                        <Checkbox id="remember" v-model:checked="form.remember" name="remember" />
                        <label
                            for="remember"
                            class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
                        >
                            Remember me
                        </label>
                    </div>
                </div>
            </CardContent>
            <CardFooter>
                <Button class="w-full" :disabled="form.processing" type="submit">Sign in</Button>
            </CardFooter>
        </form>
    </GuestLayout>
</template>
