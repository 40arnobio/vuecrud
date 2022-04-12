<template>
<div class="container">
  <router-link class="btn btn-success" to="/crear">Novo cadastro</router-link>
  <br><br>
  <div class="card">
    <div class="card-header">Mostrar dados</div>
    <div class="card-body">
      <table class="table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
            <th>Email</th>
            <th>Opções</th>
          </tr>
        </thead>
        <tbody>

          <tr v-for="empleado in empleados" :key="empleado.id">
            <td>{{ empleado.id }}</td>
            <td>{{ empleado.nombre }}</td>
            <td>{{ empleado.correo }}</td>
            <td class="btn-group">
            
              <router-link :to="{name:'Editar', params:{id:empleado.id} }" class="btn btn-info">Editar</router-link>
              <button type="button" v-on:click="excluirDados(empleado.id)" class="btn btn-warning" role="button">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      empleados: [],
    };
  },

  created: function () {
    this.consultarEmpleados();
  },

  methods: {
    consultarEmpleados() {
      fetch("http://localhost/vue/novo/api/")
        .then((resposta) => resposta.json())
        .then((dadosResposta) => {
         // console.log(dadosResposta);
          this.empleados = [];
          if (typeof dadosResposta[0].succss === "undefined") {
            this.empleados = dadosResposta;
          }
        })
        //.catch(console.log);
    },

    excluirDados(id){
      console.log(id);


      fetch("http://localhost/vue/novo/api/?delete="+id)
        .then(resposta => resposta.json())
        .then((dadosResposta) => {
        //  console.log(dadosResposta);
          window.location.href="listar"
        })
        //.catch(console.log);
    }
  }
}
</script>
