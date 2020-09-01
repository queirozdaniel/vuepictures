<template>
  <div>
    <h1>{{titulo}}</h1>
    <img :src="foto.url" :alt="foto.titulo" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: "Vue Pictures",
      foto: {
        url:
          "https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/dog-puppy-on-garden-royalty-free-image-1586966191.jpg?crop=1.00xw:0.669xh;0,0.190xh&resize=768:*",
        titulo: "Doginho fofo",
      },
    };
  },
};
</script>

<style>
</style>
