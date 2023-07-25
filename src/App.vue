<script setup>
import { reactive, ref, watch } from 'vue'
import { uid } from 'uid'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/Paciente.vue'

const pacientes = ref( JSON.parse(localStorage.getItem('pacientes')) || [] )

const paciente = reactive({
    id: null,
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: '',
})

watch(pacientes, () => {
    guardarLocalStorage()
}, {
    deep: true
})

const guardarLocalStorage = () => {
    localStorage.setItem('pacientes', JSON.stringify(pacientes.value))
}

const guardarPaciente = () => {
    if (paciente.id) {
        const { id } = paciente
        const i = pacientes.value.findIndex( paciente => paciente.id === id )
        Object.assign( pacientes.value[i], {...paciente})
    } else {
        // Usamos el spread operator para pasar una copia del objeto paciente al array
        pacientes.value.push({
            ...paciente,
            id: uid()
        })
    }

    // Reiniciar el objeto
    Object.assign(paciente, {
        id: null,
        nombre: '',
        propietario: '',
        email: '',
        alta: '',
        sintomas: ''
    })
}

const actualizarPaciente = (id) => {
    const pacienteEditar = pacientes.value.filter( paciente => paciente.id === id)[0]
    Object.assign(paciente, pacienteEditar)
}

const eliminarPaciente = (id) => {
    pacientes.value = pacientes.value.filter( paciente => paciente.id !== id)
}

</script>

<template>
    <div class="container mx-auto mt-20">
        <Header />

        <div class="mt-12 md:flex">
            <Formulario
                v-model:nombre="paciente.nombre"
                v-model:propietario="paciente.propietario"
                v-model:email="paciente.email"
                v-model:alta="paciente.alta"
                v-model:sintomas="paciente.sintomas"
                @guardar-paciente="guardarPaciente"
                :id="paciente.id"
            />

            <div class="md:w-1/2 md:h-screen overflow-y-scroll">
                <h2 class="font-black text-3xl text-center">Administra tus pacientes</h2>

                <p class="text-lg mt-5 text-center mb-10">Información de <span
                class="text-indigo-600 font-bold">pacientes</span></p>

                <div v-if="pacientes.length > 0">
                    <Paciente 
                        v-for="paciente in pacientes" 
                        :key="paciente.id" 
                        :paciente="paciente"
                        @actualizar-paciente="actualizarPaciente"
                        @eliminar-paciente="eliminarPaciente"
                    />
                        
                </div>
                <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
            </div>
        </div>
    </div>
</template>
