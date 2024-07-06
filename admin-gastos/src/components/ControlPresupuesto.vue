<script setup>
  import imagen from '../assets/img/grafico.jpg'
  import { formatearCantidad } from '../helpers'

  const props = defineProps({
    presupuesto: {
      type: Number,
      required: true
    },
    disponible: {
      type: Number,
      required: true
    },
    gastado: {
      type: Number,
      required: true
    },
  })
  
</script>

<template>
    <div class="dos-columnas">
      <div class="contenedor-grafico">
        <img 
          :src="imagen" 
          alt="Grafica">
      </div>

      <div class="contenedor-presupuesto">
        <button class="reset-app">
          Resetear App
        </button>
        <p>
          <span>Presupuesto:</span> {{ formatearCantidad(props.presupuesto) }} 
        </p>
        <p>
          <span>Disponible: </span> {{ formatearCantidad(props.disponible) }}
        </p>
        <p>
          <span>Gastado: </span> {{ formatearCantidad(props.gastado) }}
        </p>
      </div>
    </div>
</template>

<style scoped>
  .dos-columnas {
    display: flex;
    flex-direction: column;
  }
  .dos-columnas > :first-child {
    margin-bottom: 3rem;
  }
  @media (min-width: 768px) {
    .dos-columnas {
      flex-direction: row;
      gap: 4rem;
      align-items: center;
    }
    .dos-columnas > :first-child {
      margin-bottom: 0rem;
    }
  }

  .contenedor-presupuesto {
    width: 100%;
  }

  .reset-app {
    background-color: #db2777;
    border: none;
    padding: 1.5rem 1rem;
    width: 100%;
    cursor: pointer;
    color: var(--blanco);
    transition: all .3s ease;
    font-weight: 900;
    text-transform: uppercase;
    border-radius: 1rem;
  }
  .reset-app:hover {
    background-color: #be185d;
  }

  .contenedor-presupuesto p {
    font-size: 2.4rem;
    text-align: center;
    color: var(--gris-oscuro);
  }
  @media (min-width: 768px) {
    .contenedor-presupuesto p{
      text-align: left;
    }
  }
  .contenedor-presupuesto span{
    font-weight: 900;
    color: var(--azul);
  }

</style>
