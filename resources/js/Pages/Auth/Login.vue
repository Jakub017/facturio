<script setup>
import { Head, Link, useForm } from "@inertiajs/vue3";
import PrimaryButton from "@/Components/PrimaryButton.vue";

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: "",
    password: "",
    remember: false,
});

const submit = () => {
    form.transform((data) => ({
        ...data,
        remember: form.remember ? "on" : "",
    })).post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
    <Head title="Log in" />

    <div class="font-sans flex h-screen p-4">
        <div class="hidden md:flex h-full w-1/2">
            <div class="h-full w-full rounded-md bg-primary-light"></div>
        </div>

        <div
            class="flex justify-center flex-col items-center w-full md:w-1/2 gap-4"
        >
            <form
                @submit.prevent="submit"
                class="grid grid-cols-12 gap-8 w-full max-w-[600px] p-4"
            >
                <div class="col-span-12 flex flex-col gap-2">
                    <h1 class="text-xl font-semibold">Zaloguj się</h1>
                    <p class="text-sm text-secondary-dark font-normal w-full">
                        Witaj ponownie! Kontroluj swój biznes, gdziekolwiek
                        jesteś.
                    </p>
                </div>

                <div class="gap-4 grid grid-cols-12 col-span-12">
                    <div class="flex flex-col gap-1 col-span-12">
                        <label class="form-label" for="email"
                            >Adres email</label
                        >
                        <div class="relative w-full">
                            <input
                                class="form-input pl-8"
                                id="email"
                                type="text"
                                v-model="form.email"
                            /><i
                                class="fa-solid fa-user text-primary absolute top-1/2 left-3 translate-y-[-50%]"
                            ></i>
                        </div>
                        <span class="form-error" v-if="form.errors.email">{{
                            form.errors.email
                        }}</span>
                    </div>

                    <div class="flex flex-col gap-1 col-span-12">
                        <label class="form-label" for="password">Hasło</label>
                        <div class="relative w-full">
                            <input
                                class="form-input pl-8"
                                id="password"
                                type="password"
                                v-model="form.password"
                            />
                            <i
                                class="fa-solid fa-lock text-primary absolute top-1/2 left-3 translate-y-[-50%]"
                            ></i>
                        </div>
                        <span class="form-error" v-if="form.errors.password">{{
                            form.errors.password
                        }}</span>
                    </div>

                    <div class="col-span-12">
                        <PrimaryButton
                            class="flex w-full text-center justify-center"
                            :type="'button'"
                            >Zaloguj się</PrimaryButton
                        >
                    </div>
                    <p
                        class="text-sm text-secondary-dark font-normal col-span-12"
                    >
                        Nie masz konta?
                        <Link
                            :href="route('register')"
                            class="text-primary font-semibold"
                            >Zarejestruj się</Link
                        >
                    </p>
                </div>
            </form>
        </div>
    </div>
</template>
