<template>
  <div class="contenido">
    <!-- Título -->
    <div class="titulo">
      <h1> Random Gif Cat </h1>
    </div>

    <!-- Filtros -->
    <div class="Filtros">
      <!-- input Mensaje -->
      <p class="instruccion">
        Título:
        <input
          v-model="mensaje"
          class="mensajeInput altoInput"
          type="text"
          placeholder="Mensaje"
        />
      </p>
      <!-- Filtro Fotográfico -->
      <p class="instruccion">
        Filtro:
        <select v-model="filtroSclt" class="filtroFoto altoInput">
          <option disabled selected> Selecciona </option>
          <option
            @click="filtroSclt = elemento"
            v-for="elemento in filtros"
            :key="elemento"
            :value="elemento"
          >
            {{ elemento }}
          </option>
        </select>
      </p>
      <!-- Color letra -->
      <div class="instruccion">
        <p class="color">
          Color:
          <select class="colorFuente altoInput" v-model="colorSclt">
            <option disabled selected> Selecciona </option>
            <option
              @click="colorSclt = elemento"
              v-for="elemento in colores"
              :key="elemento"
              :value="elemento"
            >
              {{ elemento }}
            </option>
          </select>
        </p>
        <!-- Círculo de Color -->
        <div
          :style="{ 'background-color': this.colorSclt }"
          class="bolitaColor"
        ></div>
      </div>
      <!-- Tamaño letra -->
      <p class="instruccion">
        Tamaño:
        <input
          v-model.number="tamano"
          class="tamanoFuente altoInput"
          type="number"
          min="1"
        />
      </p>
    </div>
    <!-- Resultado imagen -->
    <div class="gif">
      <!-- Botón Generador -->
      <button @click="gatito" class="btnGatito"> Genera tu anvorguesito </button>
      <!-- gif imagen -->
      <div>
        <img v-if="imagenRes" :src="imagenRes" alt="Gatito" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // Componente App
  name: "App",
  data() {
    return {
       // Defino la propiedad "mensaje" para almacenar el "título" ingresado en el input en un string vacío
      mensaje: "",
       // Defino la propiedad "filtros" con un array que contenga los filtros a utilizar
      filtros: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
       // Defino la propiedad "colores" con un array con los colores para aplicar en la fuente
      colores: ["red", "green", "yellow", "blue", "black", "gray"],
       // Defino la propiedad "filtroSclt" un string llamado Selecciona para que aparezca este nombre en el select de Filtros
      filtroSclt: "Selecciona",
       // Defino la propiedad "colorSclt" un string llamado Selecciona para que aparezca este nombre en el select de Color de fuente
      colorSclt: "Selecciona",
       // Defino la propiedad "tamano" con el valor null, que tomará el valor indicado en el input de tipo number
      tamano: null,
       // Defino la propiedad "imagenRes" con un string vacío donde se almacenará la imagen generada
      imagenRes: "",
    };
  },
  methods: {
      // Método "gatito" 
    gatito() {
      // A la URL de la API gatitos le concateno cada propiedad que corresponde, que a su vez será generada de forma dinámica según la selección del usuario
      this.imagenRes = `https://cataas.com/cat/gif/says/${this.mensaje}?filter=${this.filtroSclt}&color=${this.colorSclt}&size=${this.tamano}`;
    },
  },
};
</script>

<style>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "cabin", sans-serif;
}

.contenido {
  max-width: 500px;
  margin: auto;
}

.titulo {
  text-align: center;
  padding: 40px 0 20px 0;
  background-color: #add8e6;
  color: #394854;
  font-size: 18px;
  font-weight: 700;
}

.altoInput {
  padding: 2px 0;
}

.Filtros {
  padding: 10px;
  background-color: #f08080;
}

.instruccion {
  margin: 20px 0;
  text-align: left;
  padding-left: 45px;
  color: #394854;
  font-size: 16px;
  font-weight: 400;
}

.color {
  display: inline-block;
  align-items: center;
}

.bolitaColor {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin-left: 10px;
  display: inline-block;
}

.gif {
  padding: 20px 0 50px 0;
  background-color: #add8e6;
  text-align: center;
}

.btnGatito {
  margin-bottom: 20px;
  padding: 5px 10px;
  color: #394854;
  font-size: 16px;
  font-weight: 500;
  border-radius: 5px;
  border-color: rgba(73, 73, 73, 0.247);
  cursor: pointer;
}

</style>
