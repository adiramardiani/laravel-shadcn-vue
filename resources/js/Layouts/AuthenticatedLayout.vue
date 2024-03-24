<script setup>
import { Link } from '@inertiajs/vue3';
import ApplicationLogo from '@/components/ApplicationLogo.vue';

import { Menu, Search } from 'lucide-vue-next';

import { Sheet, SheetContent, SheetTrigger } from '@/components/ui/sheet';
import { Avatar, AvatarFallback } from '@/components/ui/avatar';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';

import DarkMode from '@/components/DarkMode.vue';

import {
    DropdownMenu,
    DropdownMenuContent,
    DropdownMenuItem,
    DropdownMenuLabel,
    DropdownMenuSeparator,
    DropdownMenuTrigger
} from '@/components/ui/dropdown-menu';
</script>

<template>
    <div>
        <div class="min-h-screen bg-gray-100 dark:bg-gray-900">
            <header class="sticky top-0 flex h-16 items-center gap-4 border-b bg-background px-4 md:px-6">
                <nav
                    class="mx-auto hidden max-w-7xl flex-col gap-6 text-lg font-medium md:flex md:flex-row md:items-center md:gap-5 md:text-sm lg:gap-6"
                >
                    <Link :href="route('dashboard')" class="flex items-center gap-2 text-lg font-semibold md:text-base">
                        <ApplicationLogo class="size-10" />
                        <span class="sr-only">Laravel</span>
                    </Link>
                    <Link
                        :href="route('dashboard')"
                        :active="route().current('dashboard')"
                        class="transition-colors hover:text-foreground"
                        :class="[route().current('dashboard') ? 'text-foreground' : 'text-muted-foreground']"
                    >
                        Dashboard
                    </Link>
                    <Link
                        :href="route('profile.edit')"
                        :active="route().current('profile.edit')"
                        class="transition-colors hover:text-foreground"
                        :class="[route().current('profile.edit') ? 'text-foreground' : 'text-muted-foreground']"
                    >
                        Profile
                    </Link>
                    <a
                        href="https://www.shadcn-vue.com"
                        target="_blank"
                        class="text-muted-foreground transition-colors hover:text-foreground"
                    >
                        ShadcnVue
                    </a>
                </nav>
                <Sheet>
                    <SheetTrigger as-child>
                        <Button variant="outline" size="icon" class="shrink-0 md:hidden">
                            <Menu class="h-5 w-5" />
                            <span class="sr-only">Toggle navigation menu</span>
                        </Button>
                    </SheetTrigger>
                    <SheetContent side="left">
                        <nav class="grid gap-6 text-lg font-medium">
                            <Link :href="route('dashboard')" class="flex items-center gap-2 text-lg font-semibold">
                                <ApplicationLogo class="size-8" />
                                <span class="sr-only">Laravel</span>
                            </Link>
                            <Link
                                :href="route('dashboard')"
                                :active="route().current('dashboard')"
                                class="hover:text-foreground"
                                :class="[route().current('dashboard') ? '' : 'text-muted-foreground']"
                            >
                                Dashboard
                            </Link>
                            <Link
                                :href="route('profile.edit')"
                                :active="route().current('profile.edit')"
                                class="hover:text-foreground"
                                :class="[route().current('profile.edit') ? '' : 'text-muted-foreground']"
                            >
                                Profile
                            </Link>
                            <a href="https://www.shadcn-vue.com" target="_blank" class="hover:text-foreground">ShadcnVue</a>
                        </nav>
                    </SheetContent>
                </Sheet>
                <div class="flex w-full items-center gap-4 md:ml-auto md:gap-2 lg:gap-4">
                    <form class="ml-auto flex-1 sm:flex-initial">
                        <div class="relative">
                            <Search class="absolute left-2.5 top-2.5 h-4 w-4 text-muted-foreground" />
                            <Input
                                type="search"
                                placeholder="Search anything..."
                                class="pl-8 sm:w-[300px] md:w-[200px] lg:w-[300px]"
                            />
                        </div>
                    </form>
                    <DarkMode />
                    <DropdownMenu>
                        <DropdownMenuTrigger as-child>
                            <Button variant="secondary" size="icon" class="rounded-full">
                                <Avatar class="h-5 w-5">
                                    <AvatarFallback>MC</AvatarFallback>
                                </Avatar>
                                <span class="sr-only">Toggle user menu</span>
                            </Button>
                        </DropdownMenuTrigger>
                        <DropdownMenuContent align="end">
                            <DropdownMenuLabel>{{ $page.props.auth.user.name }}</DropdownMenuLabel>
                            <DropdownMenuSeparator />
                            <DropdownMenuItem as-child>
                                <Link :href="route('profile.edit')" class="cursor-pointer">Profile</Link>
                            </DropdownMenuItem>
                            <DropdownMenuSeparator />
                            <DropdownMenuItem as-child>
                                <Link :href="route('logout')" method="post" as="button" class="w-full cursor-pointer">
                                    Log Out
                                </Link>
                            </DropdownMenuItem>
                        </DropdownMenuContent>
                    </DropdownMenu>
                </div>
            </header>

            <!-- Page Heading -->
            <header v-if="$slots.header" class="bg-white shadow dark:bg-gray-800">
                <div class="mx-auto max-w-7xl px-4 py-6 sm:px-6 lg:px-8">
                    <slot name="header" />
                </div>
            </header>

            <!-- Page Content -->
            <main>
                <slot />
            </main>
        </div>
    </div>
</template>
