<script setup>
import { Text } from 'vue';


</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>

        <p class="text-lg mt-5 text-center mb-10">Añade pacientes y <span
                class="text-indigo-600 font-bold">adminístralos</span></p>

        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10">
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">Nombre Mascota</label>
                <input type="text" id="mascota" placeholder="Nombre de la mascota" class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400">
            </div>
            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">Nombre propietario</label>
                <input type="text" id="propietario" placeholder="Nombre del propietario" class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400">
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">Email de contacto</label>
                <input type="email" id="email" placeholder="Email de contacto" class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400">
            </div>
            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">Fecha de alta</label>
                <input type="date" id="alta" class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400">
            </div>
            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">Síntomas</label>
                <textarea id="sintomas" placeholder="Describe los síntomas" class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400 h-40" />
            </div>

            <input type="submit" value="Registrar paciente" class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-400 cursor-pointer transition-colors rounded-md">
        </form>
    </div>
</template>
