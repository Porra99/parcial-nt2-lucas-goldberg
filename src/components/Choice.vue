<template>

  <section class="src-components-choice">
    <div class="jumbotron">
      <h1>Multiple Choice</h1>
      <table class="table table-dark" v-if="multipleChoice.length > 0">
        <tr>
          <th v-for="(col, index) in getCols" :key="index"> {{ col }}</th>
        </tr>
        
        <tr v-for="(choice, index) in multipleChoice" :key="index">
          <th v-for="(col, index) in getCols" :key="index">{{ choice[col] }}</th>
        </tr>
      </table>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-choice',
    props: [],
    mounted () {

    },
    data () {
      return {
        multipleChoice: [
          {numero: 1, respuesta: "C"},
          {numero: 2, respuesta: "C"},
          {numero: 3, respuesta: "B"}
        ]
      }
    },
    methods: {

    },
    computed: {
      getCols() {
        return Object.keys(this.multipleChoice[0])
      }
    }
}


</script>

<style scoped lang="css">
  .src-components-choice {

  }
</style>
