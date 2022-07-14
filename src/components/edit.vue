<template>
  <div>

    <div class="form">
        <form v-on:submit.prevent>
          <label>Nombre del Proyecto:</label>
            <input type="text"  placeholder="Proyecto a solicitar" v-model="dataEdit.nombre" name="nombre"/>

          <label>Categoria:</label>
            <select v-model="dataEdit.cat" name="cat">
              <option v-for="(x,index) in options" :key="index">{{x}}</option>
            </select>

          <label>Descripcion</label>
          <textarea v-model.trim="dataEdit.descripcion" name="descripcion"></textarea>

          <button type="button" @click="edit(dataEdit)" value="Guardar">Enviar solicitud</button>
        </form>
        
      <div><p v-for="(x,index) in errores" :key="index">{{x}}</p></div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'EditForm',
  data:function(){
    return {
      options: ["Arma de fuego", "Armadura", "Equipamento", "Arma mele", "Explosivo", "Vehiculos de guerra", "Vehiculos de transporte"],
      dataEdit:{nombre:this.$route.params.nombre,
                descripcion: this.$route.params.descripcion,
                cat: this.$route.params.cat,
                src: "",
                id:this.$route.params.id

      },
      errores:[],
      ls:[]
    }
  },

  methods:{

    edit:function(dataEdit){
      this.errores=[]
             
      if(this.dataEdit.nombre == "") {
      this.errores.push('El proyecto debe ser nombrado.');
      }else if(this.dataEdit.nombre.length < 3) {
        this.errores.push('El nombre debe tener al menos 3 caracteres.');
      }

      if(this.dataEdit.cat == ""){
        this.errores.push('El proyecto debe ser categorisado.');
      }

      if(this.dataEdit.descripcion == "") {
      this.errores.push('El proyecto debe ser descripto.');
      }else if(this.dataEdit.descripcion.length < 15 || this.dataEdit.descripcion.length > 350) {
        this.errores.push('La descripcion del proyecto debe tener entre 15 y 350 caracteres.');
      }
      
     if(this.errores.length == 0){

         switch (dataEdit.cat) {
          case "Arma de fuego":
            dataEdit.src = "imgs/bl/weapon.jpg";
            break;
          case "Armadura":
            dataEdit.src = "imgs/bl/armor.jpg";
            break;
          case "Arma mele":
            dataEdit.src = "imgs/bl/mele.jpg";
            break;
          case "Explosivo":
            dataEdit.src = "imgs/bl/ex.jpg";
            break;
          case "Equipamento":
            dataEdit.src = "imgs/bl/ex.jpg";
            break;
          case "Vehiculos de transporte":
            dataEdit.src = "imgs/bl/auto.jpg";
            break;
          case "Vehiculos de guerra":
            dataEdit.src = "imgs/bl/auto.jpg";
            break;
          default:
            dataEdit.src = "imgs/bl/weapon.jpg";
            break;
        }
      
      if(!localStorage.datos){
          this.ls=[]
        }else{
          this.ls=JSON.parse(localStorage.getItem("datos"))
        }

        for (var i=0; i < this.ls.length; i++){
          if (this.ls[i].id == this.dataEdit.id ) {
            this.ls.splice(i, 1);
          }
        }

        this.ls.push(dataEdit)
        localStorage.setItem("datos",JSON.stringify(this.ls))
      }
      
      this.$router.push('/ver');
    }
  },
}
</script>

