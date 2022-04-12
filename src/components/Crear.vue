<template>
 <div class="container">
     <mensagem :msg="msg" v-show="msg" />
  <div class="card">
    <div class="card-header">
        Cadastrar dados
    </div>

    <div class="card-body">
    <form v-on:submit.prevent="agregarRegistro">
        <div class="form-group">
            <label for="">Nome</label>
            <input type="text"  v-model="empleado.nombre" id="nombre" class="form-control" 
            placeholder="" aria-describedby="helpId">
        </div>

        <div class="form-group">
            <label for="">Email</label>
            <input type="email"  v-model="empleado.correo" id="correo" class="form-control" 
            placeholder="" aria-describedby="helpId">
        </div>
        <br>
        <div class="btn-group" role="group" aria-label="">
        <input type="submit" class="btn btn-success">

        <router-link :to="{name:'Listar'}" class="btn btn-warning">Cancelar</router-link>
        </div>
    </form>
  </div>
  </div>
  </div>
</template>

<script>
import mensagem from './mensagem.vue';

export default {
    name: "Crear",
    data(){
        return{
            empleado:{},
            msg : null
        }
    },
    methods:{
        agregarRegistro(){
            console.log(this.empleado);

            let dadosEnviar = {
                nombre:this.empleado.nombre,
                correo:this.empleado.correo
            }

            fetch('http://localhost/vue/novo/api/?insert=1',{
               method:"POST",
               body:JSON.stringify(dadosEnviar)
              
           })

            .then(resposta => resposta.json())
            .then((dadosResposta) => {
            //  console.log(dadosResposta);
            //window.location.href="crear"
            this.msg = 'Cadastro Feito com sucesso';
		    //Limpa mensagem
            setTimeout(() => this.msg = "", 2000);
            
            this.empleado.nombre = "";
	        this.empleado.correo = "";
			
            })

        }
    },
    components:{
        mensagem
    }
}
</script>
