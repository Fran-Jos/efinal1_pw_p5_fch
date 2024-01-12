<template>
  <div class="valor">
    <h1>Puntaje:{{ puntaje }}</h1>
    <h1>Intento:{{ intento }}</h1>
  </div>
  <div class="compo1">
    <Cuadrado n="1" :txt="txt" />
    <Cuadrado n="2" :txt="txt"/>
    <Cuadrado n="3" :txt="txt"/>
  </div>
  <button @click="jugar">JUGAR</button>
</template>

<script>

import Cuadrado from "./components/Cuadrado.vue";
export default {
  name: "App",
  components: {
    Cuadrado,
  },
  data(){
    return{
      puntaje:0,
      intento:0,
      txt : null,
      img: null
    }
  },
  methods: {
    methods: {
    async consumirApi() {
      for (let index = 0; index < 3; index++) {
        const { answer, image } = await fetch("https://yesno.wtf/api").then(
          (r) => r.json()
        );
        this.consumir.push({ answer, image });
      }
      if (this.p === true) {
        const { answer, image } = this.consumir[0];
        this.url1 = image;
        this.nom1 = answer;
      }
      if (this.p) {
        const { answer, image } = this.consumir[1];
        this.url2 = image;
        this.nom2 = answer;
      }
      if (this.p) {
        const { answer, image } = this.consumir[2];
        this.url3 = image;
        this.nom3 = answer;
      }

      if (this.nom1 === this.nom2 === this.nom3) {
        this.puntaje = this.puntaje + 5;
        return this.puntaje;
      } else if (
        this.nom1 === this.nom2 ||
        this.nom1 === this.nom3 ||
        this.nom2 === this.nom3
      ) {
        this.puntaje = this.puntaje + 2;
        return this.puntaje;
      }
      this.consumir=[];
    }
    
  },
async consumirApi() {

      const { answer, image } = await fetch("https://yesno.wtf/api").then(
        (respuesta) => respuesta.json()
      );
      this.respuesta = answer==='yes'?"SI!":"NO!";
      this.img = image;
      this.txt = answer;
    },

    jugar() {
      this.intento++;
      this.consumirApi();
    },
 
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.compo1,
.valor {
  display: grid;
  justify-content: center;
  align-items: center;
  padding: 15px 15px;
}
.compo1 {
  grid-template-columns: repeat(3, 500px);
}
.valor {
  grid-template-columns: repeat(2, 500px);
}
button {
  height: 200Ppx;
  width: 130px;
  font-size: 30px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
</style>