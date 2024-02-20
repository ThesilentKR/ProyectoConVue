<template>
  <div class="zombie-card">
    <div class="zombie-image-container">
      <img :src="zombie.imagen" alt="Zombie Image" class="zombie-image">
    </div>
    <div class="zombie-details">
      <h2 class="zombie-name">{{ zombie.nombre }}</h2>
      <div class="zombie-description">{{ zombie.descripcion }}</div>
      <button @click="eliminarZombie" class="delete-button">Eliminar Zombie</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    zombie: {
      type: Object,
      required: true
    },
    onDelete: {
      type: Function,
      required: true
    }
  },
  methods: {
    eliminarZombie() {
      this.onDelete(this.zombie);
    }
  }
};
</script>

<style scoped>

.zombie-card {
  display: flex;
  align-items: center;
  background-image: url("https://e1.pxfuel.com/desktop-wallpaper/464/262/desktop-wallpaper-4-quality-left-4-dead-2-left-4-dead-2-base-background-l4d2.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  color: #ffffff; 
  border: 1px solid #3c3c3c;
  border-radius: 10px;
  padding: 15px;
  margin: 10px;
}

.zombie-image-container {
  flex-shrink: 0;
  margin-right: 15px;
  overflow: hidden;
  border-radius: 50%;
  width: 200px;
  height: 200px;
  background-color: #333; 
}

.zombie-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.zombie-details {
  flex-grow: 1;
}

.zombie-name {
  font-size: 18px;
  margin-bottom: 8px;
}

.zombie-description {
  max-width: 300px;
  max-height: 150px;
  overflow-y: auto; 
}

.delete-button {
  background-image: url("https://e1.pxfuel.com/desktop-wallpaper/464/262/desktop-wallpaper-4-quality-left-4-dead-2-left-4-dead-2-base-background-l4d2.jpg");
  color: #fff;
  padding: 8px 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}

</style>
