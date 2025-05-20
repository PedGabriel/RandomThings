<template>
  <section class="produtos">
      <ul v-for="(produto, index) in produtos" :key="index">
        <li>
          <img :src="produto.imagem" alt="Imagem de produto" />
          <h3>{{ produto.titulo }}</h3>
          <p>{{ produto.preco.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</p>
          <div class="botaoOutrasAbas">
            <button class="botaoComprar" v-if="produto.comprado == false" @click="adicionarCarrinho(produto)">COMPRAR AGORA</button>
            <button class="botaoComprado" v-else @click="retirarCarrinho(produto)">COMPRADO</button>
            <span
              @click="produto.favoritado = true"
              v-if="produto.favoritado == false"
              class="fa-regular fa-heart"
            ></span>
            <span @click="produto.favoritado = false" v-else class="fa-solid fa-heart"></span>
          </div>
        </li>
      </ul>
    </section>
</template>
<script setup>
  
</script>