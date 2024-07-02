<script setup>

</script>

<template>
  <div class="md:w-1/2 mb-12">
    
    <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>

    <p class="text-lg mt-5 text-center mb-10">
      Añade Pacientes y <span class="text-indigo-600 font-bold">Adminístralos</span>
    </p>
    
    <form
      class="bg-white shadow-md rounded-lg py-10 px-5"
    >

      <div class="mb-5">
        <label 
          class="block text-gray-700 uppercase font-bold mb-2 cursor-pointer" 
          for="mascota"
        >
          Nombre Mascota
        </label>
        <input
          id="mascota"
          type="text"
          placeholder="Nombre Mascota"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight cursor-pointer "
        />
      </div>

      <div class="mb-5">
        <label 
          class="block text-gray-700 uppercase font-bold mb-2 cursor-pointer" 
          for="propietario"
        >
          Nombre Propietario
        </label>
        <input
          id="propietario"
          type="text"
          placeholder="Nombre Propietario"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight cursor-pointer"
        />
      </div>

      <div class="mb-5">
        <label 
          class="block text-gray-700 uppercase font-bold mb-2 cursor-pointer" 
          for="email"
        >
          Email
        </label>
        <input
          id="email"
          type="email"
          placeholder="ejemplo@ejemplo.com"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight cursor-pointer"
        />
      </div>

      <div class="mb-5">
        <label 
          class="block text-gray-700 uppercase font-bold mb-2 cursor-pointer" 
          for="alta"
        >
          Alta
        </label>
        <input
          id="alta"
          type="date"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight cursor-pointer"
        />
      </div>

      <div class="">
        <label 
          class="block text-gray-700 uppercase font-bold mb-2 cursor-pointer" 
          for="sintomas"
        >
          Síntomas
        </label>
        <textarea
          id="sintomas"
          placeholder="Descripción de los Síntomas"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight cursor-pointer h-40"
        />
      </div>

      <input
        type="submit"
        class="bg-indigo-600 w-full mt-5 p-2 text-white uppercase font-bold hover:bg-indigo-800 cursor-pointer transition-color duration-500 ease-in-out"
        value="Agregar Paciente"
      >
      </input>

    </form>
  </div>
</template>

