<template>
  <div id="app" v-cloak>
    <h1>Doom Slayer shop</h1>
    <nav><!-- borrar este id que esta solo para el style-->
      <ul>
        <li><router-link to="/">Menu</router-link></li>
        <li><router-link to="/ingresar">Solicitar armas</router-link></li>
        <li><router-link to="/Ver">Ver armas solisitadas</router-link></li>
      </ul>
    </nav>
    <router-view/>
  </div>

</template>
