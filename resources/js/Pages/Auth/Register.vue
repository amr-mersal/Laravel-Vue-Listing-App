<script setup>
import Container from "../../components/Container.vue";
import Title from "../../components/Title.vue";
import TextLink from "../../components/TextLink.vue";
import InputField from "../../components/InputField.vue";
import PrimaryBtn from "../../components/PrimaryBtn.vue";
import { useForm } from "@inertiajs/vue3";
import ErrorMessages from "../../components/ErrorMessages.vue";

const form = useForm({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
});

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <Head title="-Register" />
    <Container class="w-1/2">
        <div class="mb-8 text-center">
            <Title>Register A New Account</Title>
            <p>
                Already have an account ?
                <TextLink routeName="login" label="Login" />
            </p>
        </div>
        <!-- error -->
        <ErrorMessages :errors="form.errors" />
        <form class="space-y-6" @submit.prevent="submit">
            <InputField label="Name" icon="id-badge" v-model="form.name" />

            <InputField label="Email" icon="at" v-model="form.email" />

            <InputField
                label="Password"
                type="password"
                icon="key"
                v-model="form.password"
            />

            <InputField
                label="Confirm Password"
                type="password"
                icon="key"
                v-model="form.password_confirmation"
            />

            <p class="text-slate-500 text-sm dark:text-slate-400">
                By creating an account, you agree to our Terms of Service and
                Privacy Policy.
            </p>
            <PrimaryBtn :disabled="form.processing"> Register </PrimaryBtn>
        </form>
    </Container>
</template>
