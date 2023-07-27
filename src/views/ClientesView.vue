<script setup>
import RouterLink from '../components/UI/RouterLink.vue'
import Heading from '../components/UI/Heading.vue'

</script>

<template>
    <div>
        <div class="flex justify-end">
            <RouterLink
                to="agregar-cliente"
            >
                Agregar Cliente
            </RouterLink>
        </div>
        <Heading class="text-4xl font-extrabold text-slate-500">Listado de Clientes</Heading>
    </div>
</template>