<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';

import { CardContent, CardFooter } from '@/components/ui/card';
import { Button } from '@/components/ui/button';

import { Head, Link, useForm } from '@inertiajs/vue3';
import { computed } from 'vue';

const props = defineProps({
    status: {
        type: String
    }
});

const form = useForm({});

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');
</script>

<template>
    <GuestLayout>
        <Head title="Email Verification" />

        <form @submit.prevent="submit">
            <CardContent class="grid gap-4">
                <div class="mt-4 text-sm text-gray-600 dark:text-gray-400">
                    Thanks for signing up! Before getting started, could you verify your email address by clicking on the link we
                    just emailed to you? If you didn't receive the email, we will gladly send you another.
                </div>

                <div v-if="verificationLinkSent" class="text-sm font-medium text-green-600 dark:text-green-400">
                    A new verification link has been sent to the email address you provided during registration.
                </div>
            </CardContent>
            <CardFooter class="flex items-center justify-between">
                <Button :disabled="form.processing" type="submit">Resend Verification Email</Button>
                <Link :href="route('logout')" method="post" as="button" class="ml-auto inline-block text-sm underline">
                    Log Out
                </Link>
            </CardFooter>
        </form>
    </GuestLayout>
</template>
