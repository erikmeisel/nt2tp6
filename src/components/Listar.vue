<template lang="html">

  <section class="src-components-listar">
    <button class="btn btn-success my-3 mr-3" type="button" @click="leerAsyn()">Actualizar Async Await</button> 
    <button class="btn btn-warning my-3" type="button" @click="leerThenCatch()">Actualizar then catch</button>

    <div v-if="personas.length==0" class="alert alert-warning mt-1">No hay usuarios disponibles</div>            

    <table class="table" v-else>
      <tr class="bg-success text-white">
          <th>Nombre</th>
          <th>Edad</th>
          <th>E-Mail</th>
          <th></th>
      </tr>
      <tr class="bg-info text-white" v-for="(persona,index) in personas" :key="index">
          <td>{{ persona.nombre }}</td>
          <td>{{ persona.edad }}</td>
          <td>{{ persona.email }}</td>
          <td><button class="btn btn-warning" type="button" @click="borrar(persona.id)">Borrar</button></td>
      </tr>
    </table>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'src-components-listar',
    props: [],
    mounted () {
      this.leerThenCatch()
    },
    data () {
      return {
        URL:"https://609dbea233eed80017957098.mockapi.io/tp6clientes",
        personas:[]
      }
    },
    methods: {
      async leerAsyn() {
        console.log("async await")
        try {
          let respuesta = await this.axios(this.URL)
          console.log(respuesta)
          this.personas = respuesta.data
        } catch(error){
          console.error(error)
        } 
      },
      leerThenCatch() {
          console.log("then catch")
          this.axios(this.URL).then( respuesta => {
            console.log(respuesta)
            this.personas = respuesta.data
          }).catch(error => console.error(error))
      },
      borrar(id) {
        this.axios.delete(this.URL+"/"+id).then(respuesta => {
          console.log(respuesta)
          let i = this.personas.indexOf(it => it.id == id)
          this.personas.splice(i,1)
        }).catch(error => console.error(error))
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-listar {
    margin: 1em
  }
</style>
