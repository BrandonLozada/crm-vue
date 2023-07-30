<script setup>
import { onUnmounted } from 'vue'
import axios from 'axios'
import RouterLink from '../components/UI/RouterLink.vue'
import Heading from '../components/UI/Heading.vue'

onUnmounted(()=> {
    axios.get('http://localhost:4000/clientes')
        .then(respuesta => {
            console.log("respuesta", respuesta)
        })
})

defineProps({
    titulo: {
        type: String,
        required: true
    }
})
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
        <Heading class="text-4xl font-extrabold text-slate-500">{{ titulo }}</Heading>
    </div>
</template>