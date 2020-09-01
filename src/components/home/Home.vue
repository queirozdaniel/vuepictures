<template>
  <div class="corpo">
    <h1 class="texto-center">{{ titulo }}</h1>
    <input
      type="search"
      v-on:input="filtro = $event.target.value"
      class="filtro"
      placeholder="filtre por parte do título"
    />
    {{ filtro }}
    <ul class="lista_fotos">
      <li
        class="lista_fotos_item"
        v-for="(foto, index) of fotosComFiltro"
        :key="index"
      >
        <painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo" />
          <botao
            tipo="button"
            rotulo="Remover"
            :confirmacao="true"
            estilo="perigo"
            @botaoAtivado="remove(foto)"
          />
        </painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import ImagemResponsiva from "../shared/imagem-responsiva/ImagemResponsiva.vue";
import Botao from "../shared/botao/Botao.vue";

export default {
  components: {
    Painel,
    ImagemResponsiva,
    Botao
  },
  data() {
    return {
      titulo: "Vue Pictures",
      fotos: [],
      filtro: ""
    };
  },
  methods: {
    remove(foto) {
      alert("Removeu " + foto.titulo);
    }
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.titulo));
        return this.fotos;
      } else {
        return this.fotos;
      }
    }
  },
  created() {
    let promise = this.$http.get("http://localhost:3000/v1/fotos");
    promise
      .then(res => res.json())
      .then(
        fotos => (this.fotos = fotos),
        err => console.log(err)
      );
  }
};
</script>

<style>
.corpo {
  font-family: "Helvetica", sans-serif;
  width: 96%;
  margin: 0 auto;
}

.texto-center {
  text-align: center;
}

.lista_fotos {
  list-style-type: none;
}

.lista_fotos .lista_fotos_item {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
