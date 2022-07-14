<template>
  <div>
    <h1>Datos guardados</h1>

<div v-if="local.length > 0 ">
  <ul class= "galeria">
    <li v-for="(x,index) in local" :key="x.id">
        <img v-bind:class="index % 2 == 0 ? 'left' : 'right' " v-bind:src="x.src" v-bind:alt="x.cat"/>
        <div class="title_ver">
          <h3>{{mayus(x.nombre)}}</h3>
          <router-link :to="'/editar/' + x.nombre + '/' + x.descripcion + '/' + x.cat + '/' + x.id">Editar </router-link>
          <a @click="borrar(x)"> Borrar</a>
        </div>
        <p>{{x.descripcion}}</p>            
    </li>
  </ul>
</div>
    <h2 v-else>{{sin_datos}}</h2>

  </div>
</template>

<script>
export default {
  name: 'VerCarga',
  data:function(){
      return {
        local:[],
        sin_datos: ""
      }
  },


      
mounted:function(){
    console.log("se monto")
    this.ver_local(); //para que nos muestre info, o desde localStorage o mensaje para que cargue datos el usuario
  },

  
  methods:{

    mayus:function(txt){
      txt = txt[0].toUpperCase() + txt.substring(1).replace("_", " ")
      return txt
    },

    ver_local:function(){
      
    if(localStorage.datos){
      this.local=JSON.parse(localStorage.getItem("datos"))  
    }else{  
      this.sin_datos = "No hay tramites pendientes"
    }
  },
    borrar:function(item){
              
      this.local= JSON.parse(localStorage.getItem ("datos"))

  for (let x=0; x < this.local.length; x++){
  
      if (this.local[x].id == item.id ) {
          let rta=confirm("Queres borrar " + this.local[x].titulo)
            if (rta==true){
              this.local.splice(x, 1);
            }
          
            
          }
      }
  

    localStorage.setItem("datos", JSON.stringify(this.local))

    this.ver_local();
    }
}
}
</script>