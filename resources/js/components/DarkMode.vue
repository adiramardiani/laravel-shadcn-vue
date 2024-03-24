<script setup>
import { useColorMode } from '@vueuse/core';
import { Button } from '@/components/ui/button';
import { Moon, Sun } from 'lucide-vue-next';
import { DropdownMenu, DropdownMenuContent, DropdownMenuItem, DropdownMenuTrigger } from '@/components/ui/dropdown-menu';

const mode = useColorMode();
</script>

<template>
    <DropdownMenu>
        <DropdownMenuTrigger as-child>
            <Button variant="outline">
                <Moon class="size-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
                <Sun class="absolute size-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
                <span class="sr-only">Toggle theme</span>
            </Button>
        </DropdownMenuTrigger>
        <DropdownMenuContent align="end">
            <DropdownMenuItem class="cursor-pointer" @click="mode = 'light'">Light</DropdownMenuItem>
            <DropdownMenuItem class="cursor-pointer" @click="mode = 'dark'">Dark</DropdownMenuItem>
            <DropdownMenuItem class="cursor-pointer" @click="mode = 'auto'">System</DropdownMenuItem>
        </DropdownMenuContent>
    </DropdownMenu>
</template>
