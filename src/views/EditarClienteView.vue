<script setup>
import { onMounted, reactive } from 'vue'
import { FormKit } from '@formkit/vue'
import { useRoute, useRouter } from 'vue-router'
import ClienteService from '../services/ClienteService'
import RouterLink from '../components/UI/RouterLink.vue'
import Heading from '../components/UI/Heading.vue'

const route = useRoute()
const router = useRouter()

const { id } = route.params

// const formData = ref({})
// const formData = reactive({})
const formData = reactive({
    nombre: '',
    apellido: '',
    email: '',
    telefono: '',
    empresa: '',
    puesto: '',
    estado: 1
})

onMounted(() => {
    ClienteService.obtenerCliente(id)
        .then(({data}) => {
            formData.nombre = data.nombre
            formData.apellido = data.apellido
            formData.email = data.email
            formData.telefono = data.telefono
            formData.empresa = data.empresa
            formData.puesto = data.puesto
            formData.estado = data.estado

            // formData.value = data
            // Object.assign(formData, data)
        })
        .catch(error => console.log("Ocurrió un error: ", error))
})

const handleSubmit = (data) => {
    ClienteService.actualizarCliente(id, data)
        .then(() => router.push({ name: 'listado-clientes'}))
        .catch(error => console.log("Ocurrió un error: ", error))
}

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
            <RouterLink to="listado-clientes">
                Volver
            </RouterLink>
        </div>
        <Heading class="text-4xl font-extrabold text-slate-500">{{ titulo }}</Heading>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-2/3 py-20 px-6">
                <FormKit
                    type="form"
                    submit-label="Guardar cambios"
                    incomplete-message="No se pudo enviar, revisa los mensajes"
                    @submit="handleSubmit"
                    :value="formData"
                >

                    <FormKit
                        type="text"
                        label="Nombre"
                        name="nombre"
                        placeholder="Nombre de Cliente"
                        help="Coloca el Nombre del Cliente que deseas registrar"
                        validation="required"
                        :validation-messages="{ required: 'El Nombre del Cliente es obligatorio' }"
                        v-model="formData.nombre"
                    />

                    <FormKit
                        type="text"
                        label="Apellido"
                        name="apellido"
                        placeholder="Apellido de Cliente"
                        validation="required"
                        :validation-messages="{ required: 'El Apellido del Cliente es obligatorio' }"
                        v-model="formData.apellido"
                    />

                    <FormKit
                        type="text"
                        label="Email"
                        name="email"
                        placeholder="Email de Cliente"
                        validation="required|email"
                        :validation-messages="{ required: 'El Email del Cliente es obligatorio', email: 'Coloca un email válido' }"
                        v-model="formData.email"
                    />

                    <FormKit
                        type="text"
                        label="Teléfono"
                        name="telefono"
                        placeholder="Teléfono: XXX-XXX-XXXX"
                        validation="?matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}}/"
                        :validation-messages="{ matches: 'El formato no es válido' }"
                        v-model="formData.telefono"
                    />

                    <FormKit
                        type="text"
                        label="Empresa"
                        name="empresa"
                        placeholder="Empresa del Cliente"
                        v-model="formData.empresa"
                    />

                    <FormKit
                        type="text"
                        label="Puesto"
                        name="puesto"
                        placeholder="Puesto del Cliente"
                        v-model="formData.puesto"
                    />

                    <FormKit
                        type="radio"
                        label="Estado"
                        name="estado"
                        :options="[
                            { label: 'Activo', value: 1 },
                            { label: 'Inactivo', value: 0 },
                        ]"
                        help="¿Cuál es el estado del Cliente?"
                        v-model="formData.estado"
                    />

                </FormKit>
            </div>
        </div>
    </div>
</template>

<style>
.formkit-wrapper,
.formkit-fieldset {
    max-width: 100% !important;
}
</style>