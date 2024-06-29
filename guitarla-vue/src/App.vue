<script setup>
  import { ref, reactive, onMounted, watch } from 'vue'
  import { db } from './data/guitarras'
  import Header from './components/Header.vue'
  import Guitarra from './components/Guitarra.vue'
  import Footer from './components/Footer.vue'

  const guitarras = ref([])
  const carrito = ref([])
  const guitarra = ref({})

  watch(carrito, () => {
    guardarLocalStorage()
  }, { deep: true })
  
  onMounted(() => {
    guitarras.value = db;
    guitarra.value = db[3];
    if (localStorage.getItem('carrito')) {
      carrito.value = JSON.parse(localStorage.getItem('carrito'))
    }
  })

  const agregarCarrito = (guitarra) => {
    const existeCarrito = carrito.value.findIndex( producto => producto.id === guitarra.id )
    if (existeCarrito !== -1) {
      if ( carrito.value[existeCarrito].cantidad >= 5 ) return
      carrito.value[existeCarrito].cantidad++
      return
    }
    guitarra.cantidad = 1
    carrito.value.push(guitarra)
  }

  const decrementarCantidad = guitarra => {
    const producto = carrito.value.findIndex( producto => producto.id === guitarra.id )
    if (carrito.value[producto].cantidad > 1) {
      carrito.value[producto].cantidad--
    }
  }

  const incrementarCantidad = guitarra => {
    const producto = carrito.value.findIndex( producto => producto.id === guitarra.id )
    if (carrito.value[producto].cantidad >= 5) return
    carrito.value[producto].cantidad++
  }

  const eliminarProducto = guitarra => {
    carrito.value = carrito.value.filter( producto => producto.id !== guitarra.id )
  }

  const vaciarCarrito = () => {
    carrito.value = []
  }

  const guardarLocalStorage = () => {
    localStorage.setItem('carrito', JSON.stringify(carrito.value))
  }
  
</script>

<template>
  
  <Header 
    :carrito="carrito"
    :guitarra="guitarra"
    @decrementar-cantidad="decrementarCantidad"
    @incrementar-cantidad="incrementarCantidad"
    @eliminar-producto="eliminarProducto"
    @agregar-carrito="agregarCarrito"
    @vaciar-carrito="vaciarCarrito"
  />
  
  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">

      <Guitarra
        v-for="guitarra in guitarras"
        :guitarra="guitarra"
        @agregar-carrito="agregarCarrito"
      />

    </div>
  </main>

  <Footer />
  
</template>

