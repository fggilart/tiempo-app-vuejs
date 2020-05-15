<template>
  <div id="app">
   <main>
    <div class="caja-busqueda">
      <input
        type="text"
        class="barra-busqueda"
        placeholder="Buscar..."
        v-model="consulta"
        @keyup="obtenerTiempo"
      />
    </div>

  <div class="tiempo-contenedor" v-if="typeof tiempo.main != 'undefined'">

    <div class="caja-localizacion">
      <div class="localizacion">{{tiempo.name}}, {{tiempo.sys.country}}</div>
    </div>

    <div class="caja-tiempo">
      <div class="temperatura">{{  Math.round( tiempo.main.temp)  }}°C</div>
      <div> <img v-bind:src="'http://openweathermap.org/img/wn/'
      + tiempo.weather[0].icon +  '@2x.png'">
      </div>
    </div>

  </div>

   </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data (){
    return{
      api_key: '72102dd79a6ea0d4bee0a26e9c56cf28',
      url_base: 'https://api.openweathermap.org/data/2.5/weather?q=',
      consulta: '',
      tiempo: {},
    }
  },
  methods: {
    obtenerTiempo (){
       fetch(`${this.url_base}${this.consulta}&units=metric&appid=${this.api_key}`)
       .then(function (response){
         return response.json()
       })
       .then(this.establecerTiempo);
    },
    establecerTiempo(myJson){
      this.tiempo = myJson;
    }
  },
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
}

body{
  font-family: 'Rubik' , sans-serif;
  background-color: #b6b6b6;
  color: #404040;
}

#app {
  
}

main{
  padding: 30px;
}

.caja-busqueda{
  width: 100%;
  margin-bottom: 30px;
}

.caja-busqueda .barra-busqueda{
  width: 100%;
  padding: 15px;
  font-size: 20px;
  color: #404040;
  border-radius: 10px;
  border: none;
}

.caja-localizacion .localizacion{
  font-size: 30px;
  font-weight: 500;
  text-align: center;
}

.caja-tiempo{
  text-align: center;
}

.caja-tiempo .temperatura{
  font-size: 90px;
  font-weight: 700;
  margin: 20px 0;
}
</style>
