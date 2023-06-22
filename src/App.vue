<template>
  <div class="container">
    <h2>
      Cena {{ number + 1 }} con el rey godo
      <span class="king-name">{{ king }}</span>
    </h2>

    <h3 class="text-price">
      Precio: <span class="price">{{ productos[number].precio }} €</span>
    </h3>

    <p
      class="king-horario"
      :style="{ backgroundColor: 'red' }"
      v-if="productos[number].finDeSemana"
    >
      (Solo fines de semana)
    </p>
    <p
      class="king-horario"
      :style="{ backgroundColor: 'green' }"
      v-else
    >
      (De lunes a domingo)
    </p>

    <div class="oferta-container-space">
      <div
        class="oferta-container"
        v-show="productos[number].precio < 100"
      >
        <p>
          Ahora con un 10% dto:<span class="oferta-price"
            >{{ newPrice }} €</span
          >
        </p>
        <img
          class="oferta-image"
          src="oferta.png"
          alt="Oferta"
        />
      </div>
    </div>

    <img
      class="king-image"
      :src="image"
      alt="Imagen del rey"
    />
    <button
      class="button"
      @click="handleClick"
    >
      Siguiente ({{ number + 1 }}/{{ total }})
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { productos } from "./datos";

let number = ref(0);
let total = productos.length;
const route = "https://www.html6.es/img/rey_";

const handleClick = () => {
  number.value++;

  if (number.value >= total) {
    number.value = 0;
  }
};

const king = computed(() => {
  const name = productos[number.value].nombre.toLowerCase();
  return name.substring(0, 1).toUpperCase() + name.substring(1);
});

const image = computed(() => {
  return `${route}${productos[number.value].nombre.toLowerCase()}.png`;
});

const newPrice = computed(() => {
  return (
    productos[number.value].precio -
    (productos[number.value].precio * 10) / 100
  ).toFixed(2);
});
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: black;
}

h2 {
  margin: 8px 0;
  color: white;
}

.container {
  width: 520px;
  background-color: #181818;
  border: 2px solid white;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: sans-serif;
  box-shadow: 0px 0px 4px 4px rgba(255, 255, 255, 0.2);
  padding: 20px;
}

.king-name {
  color: #6dd856;
}

.text-price {
  margin: 8px 0;
  color: white;
}

.price {
  color: #6dd856;
}

.oferta-price {
  color: #6dd856;
  font-size: 1.2rem;
  margin-left: 4px;
}

.king-horario {
  padding: 8px;
  border-radius: 4px;
  color: white;
}

.oferta-container-space {
  height: 40px;
}

.oferta-container {
  margin: 4px 0;
  display: flex;
  justify-items: center;
  align-items: center;
  color: white;
}

.oferta-image {
  margin-left: 8px;
  width: 60px;
}

.king-image {
  width: 300px;
  margin: 8px;
}

.button {
  margin-top: 8px;
  padding: 12px 16px;
  width: 200px;
  font-size: 1.2rem;
  border-radius: 12px;
  background-color: #0000af70;
  border: none;
  color: white;
}
.button:hover {
  cursor: pointer;
  background-color: #0000af90;
}
</style>
