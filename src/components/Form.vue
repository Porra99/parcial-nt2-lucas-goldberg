<template>

<section class="src-components-form">
    <div class="jumbotron">
    
      <h1>Form</h1>
      <hr>
      <br>
    
      <vue-form :state="formState" @submit.prevent="enviar()">

        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            name="nombre" 
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.nombre"
            required
            :minlength="stringLengthMin"
            :maxlength="stringLengthMax"
            sin-espacios
          >
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>            
            <div slot="sin-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios
            </div>            
            <div slot="minlength" class="alert alert-danger mt-1">
              Como mínimo debe ingresar {{ stringLengthMin }} caracteres
            </div>            
            <div v-if="formData.nombre.length == stringLengthMax" class="alert alert-danger mt-1">
              Como máximo puede ingresar {{ stringLengthMax }} caracteres
            </div>            
          </field-messages>
        </validate>
        <br>
        
        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input 
            type="text" 
            id="apellido" 
            name="apellido" 
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.apellido"
            required
            :minlength="stringLengthMin"
            :maxlength="stringLengthMax"
            sin-espacios
          >
          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div> 
            <div slot="sin-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios
            </div>            
            <div slot="minlength" class="alert alert-danger mt-1">
              Como mínimo debe ingresar {{ stringLengthMin }} caracteres
            </div>            
            <div v-if="formData.apellido.length == stringLengthMax" class="alert alert-danger mt-1">
              Como máximo puede ingresar {{ stringLengthMax }} caracteres
            </div>                       
          </field-messages>

        </validate>
        <br>

        <validate tag="div">
          <label for="nota">Nota</label>
          <input 
            type="number" 
            id="nota" 
            name="nota" 
            class="form-control"
            autocomplete="off"
            v-model.number="formData.nota"
            required
            :min="notaMin"
            :max="notaMax"
          >
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>            
            <div slot="min" class="alert alert-danger mt-1">La nota debe ser mayor o igual a {{notaMin}}</div>            
            <div slot="max" class="alert alert-danger mt-1">La nota debe ser menor o igual a {{notaMax}}</div>            
          </field-messages>
        </validate>
        <br>

        <button class="btn btn-info btn-block my-3" :disabled="formState.$invalid" type="submit">Enviar</button>

      </vue-form>
      <br>
      <hr>

      <div v-if="registros.length">
        <table class="table table-dark">
          <tr>
            <th v-for="(col, index) in getCols" :key="index"> {{ col }}</th>
          </tr>
          
          <tr v-for="(registro, index) in registros" :key="index">
            <th v-for="(col, index) in getCols" :key="index" :style="{ color: getColor(registro[col]) }">{{ registro[col] }}</th>
          </tr>
          
          <tr :style="{ color: getColor(calcularProm()) }">
            <th>Promedio</th>
            <th>{{ calcularProm() }}</th>
          </tr>
        </table>
      </div >
      
    </div>
  </section>  

</template>

<script lang="js">

  export default  {
    name: 'src-components-form',
    apellido: 'src-components-form',
    props: [],
    mounted () {

    },
    data () {
      return {
        formData : this.getInicialData(),
        formState : {},
        stringLengthMin : 3,
        stringLengthMax : 15,
        notaMin : 0,
        notaMax : 10,
        registros : [],
        notas : [],
      }
    },
    methods: {
      getInicialData(){
        return{
          nombre: '',
          apellido: '',
          nota: 0,
        }
      },
      calcularProm(){
        let sum = 0;
        this.notas.forEach(nota => {        
          sum = sum + nota;
        });
        this.prom = sum/this.notas.length;
        return this.prom
      },

      getColor(nota){
        let color = ''
        if(nota <= 3) color = 'red'
        else if(nota <= 6) color = 'yellow'
        else if(nota <= 10) color = 'green'
        return color
      },

      enviar(){
        const cargar = {
          'Nombre y Apellido': this.formData.nombre +' ' + this.formData.apellido,
          nota: this.formData.nota,
        }
        this.registros.push(cargar)
        this.notas.push(cargar.nota)
        this.calcularProm()
        this.formData = this.getInicialData()
        this.formState._reset()
      },

    },
    computed: {
      getCols() {
        return Object.keys(this.registros[0])
      }
    }
}


</script>

<style scoped lang="css">
  .src-components-form {

  }
</style>
