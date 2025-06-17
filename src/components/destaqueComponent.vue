<template>
  <section class="destaque">
      <div class="infoDoDestaque">
        <div class="textosDest">
          <p>{{ produto-destaque }}</p>
<!--
          <h2>{{ produtoDestaque.title }}</h2>
          <p>{{ produtoDestaque.description }}</p>
-->
          <button @click="$emit('clickDestaque')">Acessar página do produto</button>
        </div>
        <div class="imagemDestaque">
          <!--
          <img :src="produtoDestaque.image" alt="Imagem do produto em destaque" />
          -->
        </div>
      </div>
    </section>
</template>
<script setup>
  defineEmits(['click-destaque'])
  defineProps(['produto-destaque'])
</script>
