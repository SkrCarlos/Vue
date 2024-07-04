<script setup>
  import { ref } from 'vue';

  import Alerta from './Alerta.vue';

  const presupuesto = ref()

  const error = ref('')

  const definirPresupuesto = () => {
    if ( presupuesto.value <= 0) {
      error.value = 'El presupuesto no es válido'

      setTimeout(() => {
        error.value = ''
      }, 2000)
    }
  }
</script>

<template>
    <form 
      class="presupuesto"
      @submit.prevent="definirPresupuesto"
    >
      <Alerta 
        v-if="error"
      >
        {{ error }}
      </Alerta>

      <div class="campo">
        <label for="nuevo-presupuesto">Definir Presupuesto</label>
        <input 
          type="number" 
          id="nuevo-presupuesto" 
          name="nuevo-presupuesto"
          class="nuevo-presupuesto"
          placeholder="Añade tu presupuesto"
          min="0"
          v-model.number="presupuesto"
        />
      </div>

      <input type="submit" value="Definir Presupuesto">
    </form>
</template>

<style scoped>

  .presupuesto {
    width: 100%;
  }

  .campo {
    display: grid;
    gap: 2rem;
  }

  .presupuesto label {
    font-size: 2.2rem;
    text-align: center;
    color: var(--azul);
  }

  .presupuesto input[type="number"] {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 1.6rem;
    text-align: center;
  }

  .presupuesto input[type="submit"] {
    background-color: var(--azul);
    border: none;
    color: var(--blanco);
    padding: 1rem;
    font-size: 2rem;
    margin-top: 2rem;
    font-weight: 900;
    width: 100%;
    border-radius: 1rem;
    cursor: pointer;
    transition: background-color .3s ease;
  }

  .presupuesto input[type="submit"]:hover {
    background-color: var(--azul-fuerte);
  }
  
</style>
