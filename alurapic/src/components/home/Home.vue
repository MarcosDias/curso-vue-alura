<template>
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>

    <input type="search" class="filtro" placeholder="Filtre pelo título da foto"
      v-on:input="filtro = $event.target.value">

    <ul class="lista-fotos">
      <li class="lista-fotos-item"
        :key="index" v-for="(foto, index) of fotosComFiltro">

        <painel :titulo="foto.titulo">
          <img-responsiva :url="foto.url" :titulo="foto.titulo"/>
          <botao
            rotulo="Remover"
            tipo="button"
            estilo="padrao"
            :confirmacao="true"
            @botaoAtivado="remove(foto)"/>
        </painel>

      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import ImgResponsiva from "../shared/img-responsiva/ImagemResponsiva.vue";
import Botao from "../shared/botao/Botao.vue";

export default {
  components: {
    painel: Painel,
    "img-responsiva": ImgResponsiva,
    botao: Botao
  },

  data() {
    return {
      titulo: "Alurapic",
      fotos: [],
      filtro: ""
    };
  },

  methods: {
    remove(foto) {
      alert(foto.titulo);
    }
  },

  computed: {
    fotosComFiltro() {
      if (!!this.filtro) {
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos")
      .then(res => res.json())
      .then(fotos => (this.fotos = fotos), err => console.log(err));
  }
};
</script>

<style>
.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

.imagem-responsiva {
  width: 100%;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
