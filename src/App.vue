<template>
  <div class="corpo">
    <Menu :rotas="routes" />
    <transition name="pagina" mode="out-in">
      <router-view />
    </transition>
  </div>
</template>

<script>
import { routes } from "./routes";
import Menu from "./components/shared/menu/Menu";

export default {
  components: {
    Menu
  },
  data() {
    return {
      routes
    };
  }
};
</script>

<style>
.corpo {
  font-family: "Helvetica", sans-serif;
  width: 96%;
  margin: 0 auto;
}

.pagina-enter,
.pagina-leave-active {
  opacity: 0;
}

.pagina-enter-active,
.pagina-leave-active {
  transition: opacity 0.4s;
}
</style>
