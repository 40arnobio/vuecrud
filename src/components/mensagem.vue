<template>
 <div class="mensagem-container">
   {{ msg }} 
 </div>
</template>

<script>
 export default{
    name: "mensagem",
    props:{
        msg : String
    }
 }
</script>
<style scoped>
.mensagem-container{
    color: green;
    border: 2px solid #444;
    border-radius: 5px;
    max-width: 400px;
    margin: 30px auto;
    padding: 10px;
    font-weight: 500;
    font-size: 1.5em;
}
</style>