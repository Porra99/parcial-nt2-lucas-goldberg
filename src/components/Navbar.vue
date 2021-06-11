<template>

 <section class="src-componentes-navbar">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      
      <router-link to="/">
        <a class="navbar-brand" href="#">Inicio</a>
      </router-link>

      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link to="/form">
              <a class="nav-link" href="#">Notas</a>
            </router-link>
          </li>
          <li class="nav-item">
            <router-link to="/choice">
              <a class="nav-link" href="#">Choice</a>
            </router-link>
          </li>
        </ul>
      </div>
    </nav>
  </section>


</template>

<script lang="js">

  export default  {
    name: 'Navbar',
    props: [],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-navbar {

  }
</style>
