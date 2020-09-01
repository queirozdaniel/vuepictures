<template>
  <button
    @click="disparaAcao()"
    class="botao"
    :class="estiloBotao"
    :type="tipo"
  >
    {{ rotulo }}
  </button>
</template>

<script>
export default {
  props: {
    tipo: { type: String, required: true },
    rotulo: { type: String, required: true },
    confirmacao: { type: Boolean, required: true },
    estilo: { type: String, default: "padrao" }
  },
  methods: {
    disparaAcao() {
      if (this.confirmacao) {
        if (confirm("Deseja excluir item ?")) {
          this.$emit("botaoAtivado");
        }
        return;
      }
      this.$emit("botaoAtivado");
    }
  },
  computed: {
    estiloBotao() {
      if (this.estilo == "padrao") return "botao-padrao";
      if (this.estilo == "perigo") return "botao-perigo";
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
