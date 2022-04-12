<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Editar dados</div>
      <div class="card-body">
        <form v-on:submit.prevent="atualizarRegistro">
          <div class="form-group">
            <label for="nombre">Nome</label>
            <input
              type="text"
              name="nombre"
              v-model="empleado.nombre"
              id="nombre"
              class="form-control"
              aria-describedby="helpId"
            />
          </div>

          <div class="form-group">
            <label for="correo">Email</label>
            <input
              type="email"
              name="correo"
              v-model="empleado.correo"
              id="correo"
              class="form-control"
              aria-describedby="helpId"
            />
          </div>
          <br />
          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-success">Salvar</button>
            <router-link :to="{ name: 'Listar' }" class="btn btn-warning"
              >Cancelar</router-link
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      empleado: {},
    };
  },

  created: function () {
    this.consultarID();
  },

  methods: {
    consultarID() {
      fetch("http://localhost/vue/novo/api/?consultar=" + this.$route.params.id)
        .then((resposta) => resposta.json())
        .then((dadosResposta) => {
          console.log(dadosResposta);
          this.empleado = dadosResposta[0];
        })
        .catch(console.log);
    },

    atualizarRegistro() {
      let dadosEnviar = {
        id: this.$route.params.id,
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };
      fetch(
        "http://localhost/vue/novo/api/?actualizar=" + this.$route.params.id,{
          method: "POST",
          body: JSON.stringify(dadosEnviar),
        })

        .then(resposta => resposta.json())
        .then((dadosResposta) => {
        //  console.log(dadosResposta);
          window.location.href="../listar"
        })
        
    },
  },
};
</script>
