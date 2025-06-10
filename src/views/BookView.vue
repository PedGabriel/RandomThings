<script setup>
defineProps(['id', 'produto'])
</script>
<template>
  <h1>{{ produto.titulo }}</h1>
  <img :src="produto.imagem" alt="Imagem de produto" />
  <p>{{ produto.preco.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</p>
</template>
