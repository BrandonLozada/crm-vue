<script setup>
import { FormKit } from '@formkit/vue'
import RouterLink from '../components/UI/RouterLink.vue'
import Heading from '../components/UI/Heading.vue'

defineProps({
    titulo: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink
                to="inicio"
            >
                Inicio
            </RouterLink>
        </div>
        <Heading class="text-4xl font-extrabold text-slate-500">{{ titulo }}</Heading>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-2/3 py-20 px-6">
                <FormKit
                    type="form"
                >

                <FormKit
                    type="text"
                    label="Nombre"
                    placeholder="Nombre de Cliente"
                    help="Coloca el Nombre del Cliente que deseas registrar"
                    validation="required"
                    :validation-messages="{ required: 'El Nombre del Cliente es obligatorio' }"
                />

                </FormKit>
            </div>
        </div>
    </div>
</template>

<style>
    .formkit-wrapper {
        max-width: 100%;
    }
</style>