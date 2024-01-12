<template>
  <div>
    <img :src="cargarimagen(n)" alt="No carga imagen">
    <p>{{ txt }}</p>
  </div>
</template>

<script>
export default {
  props: {
    img : String,
    n: Number, // Debes recibir n como prop
    txt:String
  },
  data() {
    return {
  
    };
  },

  methods: {
    cargarimagen(n) {
      return "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/" + n + ".svg";
    },
  },
};
</script>

<style>
img {
  height: 300px;
  width: 300px;
}
</style>
