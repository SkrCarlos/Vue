<script setup>

  import { reactive } from 'vue'

  import Alerta from './Alerta.vue'

  const alerta = reactive({
    tipo: '',
    mensaje: ''
  })

  const emit = defineEmits([
    'update:nombre', 
    'update:propietario', 
    'update:email', 
    'update:alta', 
    'update:sintomas',
    'guardar-paciente'
  ])

  const props = defineProps({
    nombre: {
      type: String,
      required: true
    },
    propietario: {
      type: String,
      required: true
    },
    email: {
      type: String,
      required: true
    },
    alta: {
      type: String,
      required: true
    },
    sintomas: {
      type: String,
      required: true
    },
    id: {
      type: [String, null],
      required: false
    }
  })

  const validar = () => {
  
    if (Object.values(props).includes('')) {
      alerta.tipo = 'error'
      alerta.mensaje = 'Todos los campos son obligatorios'
      return
    }

    emit('guardar-paciente')

    alerta.tipo = 'success'
    alerta.mensaje = 'Paciente agregado correctamente'

    setTimeout(() => {
      alerta.tipo = ''
      alerta.mensaje = ''
    }, 1500)
      
  }


</script>

<template>
  <div class="md:w-1/2 mb-12">
    
    <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>

    <p class="text-lg mt-5 text-center mb-10">
      Añade Pacientes y <span class="text-indigo-600 font-bold">Adminístralos</span>
    </p>
    
    <form
      class="bg-white shadow-md rounded-lg py-10 px-5"
      @submit.prevent="validar"
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
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
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
          :value="propietario"
          @input="$emit('update:propietario', $event.target.value)"
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
          :value="email"
          @input="$emit('update:email', $event.target.value)"
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
          :value="alta"
          @input="$emit('update:alta', $event.target.value)"
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
          :value="sintomas"
          @input="$emit('update:sintomas', $event.target.value)"
        />
      </div>

      <input
        type="submit"
        class="bg-indigo-600 w-full mt-5 p-2 text-white uppercase font-bold hover:bg-indigo-800 cursor-pointer transition-color duration-500 ease-in-out"
        :value=" id ? 'Editar Paciente' : 'Agregar Paciente'"
      >
      </input>

      <Alerta 
        v-if="alerta.mensaje"
        :alerta="alerta" 
        />

    </form>
  </div>
</template>

