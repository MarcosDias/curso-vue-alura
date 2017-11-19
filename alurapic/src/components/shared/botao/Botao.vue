<template>
  <button
    class="botao botao-perigo"
    :type="tipo"
    @click="disparaAcao()">{{rotulo}}</button>
</template>

<script>
export default {
  props: {
    tipo: {
      required: true,
      type: String
    },

    rotulo: {
      required: true,
      type: String
    },

    confirmacao: {
      required: false,
      default: false,
      type: Boolean
    },

    estilo: {
      required: false,
      default: "padrao",
      type: String
    }
  },

  computed: {
    estiloDoBotao() {
      if (this.estilo == "padrao") return "botao botao-padrao";

      if (this.estilo == "perigo") return "botao botao-perigo";
    }
  },

  methods: {
    disparaAcao() {
      if (this.confirmacao) {
        if (confirm("Confirma operacao?")) {
          this.$emit("botaoAtivado");
        }
        return;
      }
      this.$emit("botaoAtivado");
    }
  }
};
</script>

<style scoped>
.botao {
  display: inline-block;
  padding: 10px;
  border-radius: 3px;
  margin: 10px;
  font-size: 1.2em;
}

.botao-perigo {
  background: firebrick;
  color: white;
}

.botao-padrao {
  background: darkcyan;
  color: white;
}
</style>
