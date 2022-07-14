<template>
  <div>

    <div class="form">
        <form v-on:submit.prevent>
        
        <label>Nombre del Proyecto:</label>
          <input type="text" v-model.trim="form_obj.nombre" placeholder="Proyecto a solisitar" name="nombre"/>

        <label>Categoria:</label>
          <select v-model="form_obj.cat" name="cat">
            <option>Arma de fuego</option>
            <option>Armadura</option>
            <option>Equipamento</option>
            <option>Arma mele</option>
            <option>Explosivo</option>
            <option>Vehiculos de guerra</option>
            <option>Vehiculos de transporte</option>
          </select>

        <label>Descripcion</label>
        <textarea v-model.trim="form_obj.descripcion" name="descripcion"></textarea>

        <button type="button" @click="guardar(form_obj)" value="Guardar">Enviar solisitud </button>
        </form>
        
        <div><p v-for="(x,index) in errores" :key="index">{{x}}</p></div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'IngresarForm',
data:function(){
    return {
      form_obj:{
        nombre: "",
        cat: "",
        id: "",
        src: "",
        descripcion: ""
      },
      errores:[],

      ls:[]
    }

  },

  computed : {
    hayErrores: function(){
      return this.errores.length;
    }
  },

 methods:{
  guardar:function(form_obj){
      this.errores=[]
             
      if(this.form_obj.nombre == "") {
      this.errores.push('El proyecto debe ser nombrado.');
      }else if(this.form_obj.nombre.length < 3) {
        this.errores.push('El nombre debe tener al menos 3 caracteres.');
      }

      if(this.form_obj.cat == ""){
        this.errores.push('El proyecto debe ser categorisado.');
      }

      if(this.form_obj.descripcion == "") {
      this.errores.push('El proyecto debe ser descripto.');
      }else if(this.form_obj.descripcion.length < 15 || this.form_obj.descripcion.length > 350) {
        this.errores.push('La descripcion del proyecto debe tener entre 15 y 350 caracteres.');
      }
      
     if(this.errores.length == 0){

         switch (form_obj.cat) {
          case "Arma de fuego":
            form_obj.src = "imgs/bl/weapon.jpg";
            break;
          case "Armadura":
            form_obj.src = "imgs/bl/armor.jpg";
            break;
          case "Arma mele":
            form_obj.src = "imgs/bl/mele.jpg";
            break;
          case "Explosivo":
            form_obj.src = "imgs/bl/ex.jpg";
            break;
          case "Equipamento":
            form_obj.src = "imgs/bl/ex.jpg";
            break;
          case "Vehiculos de transporte":
            form_obj.src = "imgs/bl/auto.jpg";
            break;
          case "Vehiculos de guerra":
            form_obj.src = "imgs/bl/auto.jpg";
            break;
          default:
            form_obj.src = "imgs/bl/weapon.jpg";
            break;
        }
        console.log(form_obj.cat);
        console.log(form_obj.src);
             
          form_obj = Object.assign({}, form_obj, { id: new Date().getTime() });
          console.log(form_obj);
      
      if(!localStorage.datos){
          this.ls=[]
        }else{
          this.ls=JSON.parse(localStorage.getItem("datos"))
        }

        this.ls.push(form_obj)
        localStorage.setItem("datos",JSON.stringify(this.ls))
      }
      
      this.$router.push('/ver');
    }
  },
}
</script>