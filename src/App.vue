<template>

    <nav class="navbar navbar-expand navbar-light bg-light">
        <div class="nav navbar-nav">
            <router-link class="nav-link" to="/crear">Create</router-link>
            <router-link class="nav-link" to="/listar">Listar</router-link>
            <router-link class="nav-link" to="/teste">Teste</router-link>
        </div>
    </nav>
    <br>
  <router-view/>
</template>


