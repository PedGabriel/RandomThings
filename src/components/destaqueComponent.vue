<template>
  <section class="destaque">
      <div class="infoDoDestaque" v-if="produtoDestaque.id">
        <div class="textosDest">
          <h2>{{ produtoDestaque.title }}</h2>
          <p>{{ produtoDestaque.description }}</p>
          <button @click=$emit('haveClick')>Acessar página do produto</button>
        </div>
        <div class="imagemDestaque">
          <img :src="produtoDestaque.image" alt="Imagem do produto em destaque" />
        </div>
      </div>
    </section>
    <hr />
</template>
<script setup>
  defineEmits(['haveClick'])
  defineProps(['produto-destaque'])
</script>