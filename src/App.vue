<template>
  <div class="bg-gray-50" id="inicio">
    <div class="py-12 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="lg:text-center">
          <h2
            class="
              text-3xl text-base text-red-600
              font-extrabold
              tracking-wide
              uppercase
            "
          >
            Busca tu Pokemon!!
          </h2>
          <div class="ml-3 inline-flex rounded-md shadow">
            <input type="input"  v-model="checked" />
            <input
              class="
                inline-flex
                items-center
                justify-center
                px-5
                py-3
                border border-transparent
                text-base
                font-medium
                rounded-md
                text-indigo-600
                bg-white
                hover:bg-indigo-50
              "
              type="button"
              v-on:click="puchamon"
              value="buscar"
            />
            
          </div>
          <div v-if="imagen">
            <p
              class="
                text-indigo-600
                mt-2
                font-semibold
                leading-8
                tracking-tight
                text-gray-900
                sm:text-4xl
              "
            >
            <img :src="imagen" class="inline-flex items-center" >
              
            </p>
          </div>
          <div  v-if="habi">
            <p
              class="
                text-indigo-600
                mt-2
                font-semibold
                leading-8
                tracking-tight
                text-gray-900
                sm:text-4xl
              "
            >
              {{ habi }}
            </p>
          </div>
          
          <div v-if="pokemon">
            <p
              class="
                text-indigo-600
                mt-2
                font-semibold
                leading-8
                tracking-tight
                text-gray-900
                sm:text-4xl
              "
            >
              {{ pokemon.name }}
            </p>
          </div>
          
        </div>
      </div>
    </div>
   
           
         
  </div>
</template>

<script >
import axios from "axios";
export default {
  name: "inicio",
  data() {
    return {
      checked: null,
      pokemon: null,
      nombre: null,
      imagen: null,
      habi: null,
    };
  },
  methods: {
    puchamon: function () {
      //${this.id}
      axios.get(`https://pokeapi.co/api/v2/pokemon/${this.checked}`).then((response) => {
        this.pokemon = response.data;
        console.log(this.pokemon);
        console.log("pato");
        const habilidades = response.data.abilities;
        console.log(habilidades);

        const habilidad = response.data.abilities[1].ability.name;
        console.log(habilidad);
        this.habi = habilidad;
        console.log(this.habi);

        const { name } = response.data;
        this.nombre = name;
       // console.log(nombre);

        const imagen = response.data.sprites.front_default;
        this.imagen=imagen;
        console.log(imagen);
      });
    },
  },
};
</script>
  

<style>
</style>
