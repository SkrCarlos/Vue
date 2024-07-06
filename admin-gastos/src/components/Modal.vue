<script setup>

  import cerrarModal from '../assets/img/cerrar.svg'

  const emit = defineEmits(['cerrar-modal'])

  const props = defineProps({
    modal: {
      type: Object,
      required: true
    }
  })

</script>

<template>
    
    <div class="modal">
      <div class="cerrar-modal">
        <img 
          :src="cerrarModal" 
          alt="Cerrar Modal"
          @click="$emit('cerrar-modal')"
        >
      </div>

      <div 
        class="contenedor centrar contenedor-formulario"
        :class="[modal.animar ? 'animar' : 'cerrar']">
        <form class="nuevo-gasto">
          <legend>Añadir Gasto</legend>

          <div class="campo">
            <label for="nombre">Nombre Gasto:</label>
            <input 
              type="text"
              id="nombre"
              name="nombre"
              placeholder="Ej. Transporte"
            >
          </div>

          <div class="campo">
            <label for="cantidad">Cantidad:</label>
            <input 
              type="text"
              id="cantidad"
              name="cantidad"
              placeholder="Ej. 300"
            >
          </div>

          <div class="campo">
            <label for="cateogria">Categoría:</label>
            <select 
              name="categoria" 
              id="categoria"
            >
              <option value="">-- Seleccione --</option>
              <option value="ahorro">Ahorro</option>
              <option value="comida">Comida</option>
              <option value="casa">Casa</option>
              <option value="gastos">Gastos Varios</option>
              <option value="ocio">Ocio</option>
              <option value="salud">Salud</option>
              <option value="suscripciones">Suscripciones</option>
            </select>
          </div>

          <input 
            type="submit" 
            value="Agregar Gasto"
          >

        </form>
      </div>

    </div>

</template>

<style scoped>
  .modal {
    position: absolute;
    background-color: rgb(0, 0, 0, 0.9);
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .cerrar-modal {
    position: absolute;
    top: 3rem;
    right: 3rem;
    cursor: pointer;
  }
  .cerrar-modal img {
    width: 3rem;
    transition: all 0.7s ease;
  }
  .cerrar-modal img:hover {
    transform: rotate(180deg);
  }

  .contenedor-formulario {
    transition-property: all;
    transition-duration: 0.3s;
    transition-timing-function: ease-in;
    opacity: 0;
  }
  .contenedor-formulario.animar {
    opacity: 1;
  }
  .contenedor-formulario.cerrar {
    opacity: 0;
  }

  .centrar {
    width: 100%;
    height: 80%;
    display: grid;
    place-items: center;
  }

  .nuevo-gasto {
    background-color: var(--blanco);
    padding: 3rem;
    border-radius: 1.2rem;
    width: 90%;
    max-width: 50rem;
    margin: 10rem auto 0 auto;
  }
  .nuevo-gasto legend {
    font-size: 3rem;
    color: var(--azul);
    margin-bottom: 2rem;
  }
  .campo {
    display: grid;
    gap: 1rem;
    margin-bottom: 3rem;
  }
  .campo:last-child {
    margin-bottom: 0;
  }
  .nuevo-gasto input,
  .nuevo-gasto select {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    border: none;
    padding: 1rem;
    font-size: 2rem;
  }
  .nuevo-gasto label {
    font-size: 2.2rem;
    color: var(--azul);
  }
  .nuevo-gasto input[type="submit"] {
    background-color: var(--azul);
    color: var(--blanco);
    font-size: 2rem;
    padding: 1rem 2rem;
    border: none;
    border-radius: 1rem;
    cursor: pointer;
    transition: all 0.5s ease;
    float: right;
    width: 100%;
  }
  .nuevo-gasto input[type="submit"]:hover {
    background-color: var(--azul-fuerte);
  }
  @media (min-width: 768px) {
    .nuevo-gasto input[type="submit"] {
      width: auto;
    }
  }



</style>
