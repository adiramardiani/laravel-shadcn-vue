<script setup>
import InputError from '@/components/InputError.vue';

import { Dialog, DialogContent, DialogDescription, DialogFooter, DialogHeader, DialogTitle } from '@/components/ui/dialog';
import { CardHeader, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';

import { useForm } from '@inertiajs/vue3';
import { nextTick, ref } from 'vue';

const confirmingUserDeletion = ref(false);
const passwordInput = ref(null);

const form = useForm({
    password: ''
});

const confirmUserDeletion = () => {
    confirmingUserDeletion.value = true;

    nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onError: () => passwordInput.value.focus(),
        onFinish: () => form.reset()
    });
};

const closeModal = () => {
    confirmingUserDeletion.value = false;

    form.reset();
};
</script>

<template>
    <section>
        <CardHeader>
            <h2 class="text-lg font-medium text-gray-900 dark:text-gray-100">Delete Account</h2>

            <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">
                Once your account is deleted, all of its resources and data will be permanently deleted. Before deleting your
                account, please download any data or information that you wish to retain.
            </p>
        </CardHeader>
        <CardContent>
            <Button variant="destructive" @click="confirmUserDeletion">Delete Account</Button>
        </CardContent>
        <Dialog v-model:open="confirmingUserDeletion">
            <DialogContent>
                <DialogHeader>
                    <DialogTitle>Are you sure you want to delete your account?</DialogTitle>
                    <DialogDescription>
                        Once your account is deleted, all of its resources and data will be permanently deleted. Please enter your
                        password to confirm you would like to permanently delete your account.
                    </DialogDescription>
                </DialogHeader>
                <div class="grid gap-4">
                    <div class="grid gap-2">
                        <Label for="password" class="sr-only">Password</Label>
                        <Input
                            id="password"
                            ref="passwordInput"
                            v-model="form.password"
                            type="password"
                            placeholder="Password"
                            @keyup.enter="deleteUser"
                        />
                        <InputError :message="form.errors.password" />
                    </div>
                </div>
                <DialogFooter class="gap-2">
                    <Button variant="outline" @click="closeModal">Cancel</Button>
                    <Button variant="destructive" :disabled="form.processing" @click="deleteUser">Delete Account</Button>
                </DialogFooter>
            </DialogContent>
        </Dialog>
    </section>
</template>
