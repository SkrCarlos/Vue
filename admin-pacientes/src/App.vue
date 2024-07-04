<script setup>
  import { ref, reactive, onMounted, watch } from 'vue'

  import { uid } from 'uid'
  
  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import Paciente from './components/Paciente.vue'

  const pacientes = ref([])

  const paciente = reactive({
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
  })

  const guardarPaciente = () => {

    if ( paciente.id ){  // Existe id, actualiza
      const { id } = paciente
      const i = pacientes.value.findIndex(p => p.id === id)
      pacientes.value[i] = { ...paciente }
    } else { // No existe id, crea
      pacientes.value.push({ 
        ...paciente, 
        id: uid()
      })
    }

    
    paciente.id = null
    paciente.nombre = ''
    paciente.propietario = ''
    paciente.email = ''
    paciente.alta = ''
    paciente.sintomas = ''

  }

  const actualizarPaciente = id => {
    const pacienteEditar = pacientes.value.find(p => p.id === id)
    Object.assign(paciente, pacienteEditar)
  }

  const eliminarPaciente = id => {
    pacientes.value = pacientes.value.filter(p => p.id !== id)
  }

  const guardarLocalStorage = () => {
    localStorage.setItem('pacientes', JSON.stringify(pacientes.value))
  }

  onMounted(() => {
    if (localStorage.getItem('pacientes')) {
      pacientes.value = JSON.parse(localStorage.getItem('pacientes'))
    }
  })

  watch(pacientes, () => {
    guardarLocalStorage()
  }, { deep: true })

</script>

<template>
  <div class="container mx-auto mt-15">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario 
        v-model:nombre="paciente.nombre"
        v-model:propietario ="paciente.propietario"
        v-model:email ="paciente.email"
        v-model:alta ="paciente.alta"
        v-model:sintomas ="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
        :id="paciente.id"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>

        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Paciente 
            v-for="paciente in pacientes"
            :paciente="paciente"
            @actualizar-paciente="actualizarPaciente"
            @eliminar-paciente="eliminarPaciente"
          />
        </div>

        <p v-else class="text-center mt-20 text-2xl">No Hay Pacientes Aún</p>
        

      </div>
    </div>
    
  </div>
  
</template>


