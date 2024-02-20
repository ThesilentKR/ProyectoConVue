<template>
  <div id="app">
    <div class="container">
      <h1 class="app-title">Left 4 Dead Zombie Wiki</h1>
      <button @click="toggleFormVisibility" class="toggle-button">
        {{ showForm ? 'Ocultar Formulario' : 'Mostrar Formulario' }}
      </button>
      <form v-if="showForm" @submit.prevent="agregarZombie" class="zombie-form">
        <label for="nombre">Nombre:</label>
        <input v-model="nuevoZombie.nombre" id="nombre" required maxlength="50">

        <label for="descripcion">Descripción:</label>
        <textarea v-model="nuevoZombie.descripcion" id="descripcion" required maxlength="200"></textarea>

        <label for="imagen">URL de la Imagen:</label>
        <input v-model="nuevoZombie.imagen" id="imagen" required>

        <button type="submit">Añadir Zombie</button>
      </form>
    </div>

    <div class="zombies-container">
      <ZombieCard
        v-for="zombie in zombies"
        :key="zombie.id"
        :zombie="zombie"
        :onDelete="eliminarZombie"
      />
    </div>
  </div>
</template>

<script>
import ZombieCard from "@/components/ZombieCard.vue";

export default {
  components: {
    ZombieCard
  },
  data() {
    return {
      showForm: false,
      zombies: [
        { id: 1, nombre: "Boomer", descripcion: "El Boomer es un infectado especial extremadamente hinchado. Su mutación le ha dado la capacidad de producir inmensas cantidades de bilis que intentará vomitar sobre los supervivientes, cegándolos.", imagen: "https://steamuserimages-a.akamaihd.net/ugc/1854932942788014010/58C6407FA074FB1AB2E2A888C1371D8F18B7A5FF/?imw=637&imh=358&ima=fit&impolicy=Letterbox&imcolor=%23000000&letterbox=true" },
        { id: 1, nombre: "Spitter", descripcion: "En general, su ácido causa el mayor daño total que puede llegar a causar cualquier infectado jugable, pero al mismo tiempo es el ataque menos fiable, ya que solo dura durante un corto periodo.", imagen: "https://steamuserimages-a.akamaihd.net/ugc/1660105383878826746/D15FF27047CCC353C0AE32A4C72587C36CB298B3/?imw=637&imh=358&ima=fit&impolicy=Letterbox&imcolor=%23000000&letterbox=true" },
        { id: 1, nombre: "Hunter", descripcion: "El Hunter parece haber sido un practicante de parkour antes de mutar a causa de la Gripe verde vistiendo una sudadera desteñida con una capucha azul y pantalones de color marrón.", imagen: "https://pa1.aminoapps.com/6431/ad3761afc519b35d16c31a06f9ce599af19d3e82_00.gif" },
        ],
      nuevoZombie: {
        nombre: "",
        descripcion: "",
        imagen: ""
      }
    };
  },
  methods: {
    toggleFormVisibility() {
      this.showForm = !this.showForm;
    },
    agregarZombie() {
      if (this.nuevoZombie.nombre && this.nuevoZombie.descripcion && this.nuevoZombie.imagen) {
        this.zombies.push({
          id: Date.now(),
          nombre: this.nuevoZombie.nombre,
          descripcion: this.nuevoZombie.descripcion,
          imagen: this.nuevoZombie.imagen
        });

        this.nuevoZombie = { nombre: "", descripcion: "", imagen: "" };
        this.showForm = false; 
      }
    },
    eliminarZombie(zombie) {
      this.zombies = this.zombies.filter(z => z !== zombie);
    }
  }
};
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-image: url("https://i.gifer.com/85OQ.gif");
  background-repeat: no-repeat;
  background-size: cover;
  color: #ffffff;
  font-family: "Press Start 2P", system-ui;
  font-style: normal;
}

#app {
  text-align: center;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.container {
  max-width: 600px;
  margin: 20px auto;
}

.app-title {
  color: #e8482a;
}

.zombie-form {
  background-image: url("https://e1.pxfuel.com/desktop-wallpaper/464/262/desktop-wallpaper-4-quality-left-4-dead-2-left-4-dead-2-base-background-l4d2.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  text-align: left;
}

.zombie-form label {
  display: block;
  margin-bottom: 8px;
}

.zombie-form input,
.zombie-form textarea {
  width: 100%;
  padding: 8px;
  margin-bottom: 16px;
  box-sizing: border-box;
}

.zombie-form button {
  background-image: url("https://e1.pxfuel.com/desktop-wallpaper/464/262/desktop-wallpaper-4-quality-left-4-dead-2-left-4-dead-2-base-background-l4d2.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.zombies-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.toggle-button {
  margin-bottom: 10px;
  background-image: url("https://e1.pxfuel.com/desktop-wallpaper/464/262/desktop-wallpaper-4-quality-left-4-dead-2-left-4-dead-2-base-background-l4d2.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  color: #fff;
  padding: 8px 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}
</style>
