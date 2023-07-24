<script setup>
import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue';
import { reactive, ref } from 'vue';

const pacientes = ref([]);

const paciente = reactive({
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: '',
})

const guardarPaciente = () => {
    // Usamos el spread operator para pasar una copia al array
    pacientes.value.push({...paciente})

    // Reiniciar el objeto
    paciente.nombre = ''
    paciente.propietario = ''
    paciente.email = ''
    paciente.alta = ''
    paciente.sintomas = ''
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
            />

            <div class="md:w-1/2 md:h-screen overflow-y-scroll">
                <h2 class="font-black text-3xl text-center">Administra tus pacientes</h2>

                <p class="text-lg mt-5 text-center mb-10">Información de <span
                class="text-indigo-600 font-bold">pacientes</span></p>

                <div v-if="pacientes.length > 0">
                    <Paciente v-for="paciente in pacientes" :key="paciente.id" :paciente="paciente"/>
                        
                </div>
                <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
            </div>
        </div>
    </div>
</template>
