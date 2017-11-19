<template>
  <nav>
    <ul>
      <li :key="index" v-for="(rota, index) in rotas">
        <router-link :to="rota.path ? rota.path : '/'">
          {{rota.titulo}}
        </router-link>
      </li>
    </ul>
  </nav>
</template>
<script>
export default {
  props: {
    rotas: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>

</style>
