<script setup>
import { ref } from "vue";


const produtos = ref([
    {
        id: 1,
        titulo: 'Livro 1',
        resenha: 'Descrição breve 1',
        preco: 49.9,
        capa: 'https://placehold.co/600x400.png',
    },
    {
        id: 2,
        titulo: 'Livro 2',
        resenha: 'Descrição breve 2',
        preco: 99.9,
        capa: 'https://placehold.co/600x400.png',
    },
    {
        id: 3,
        titulo: 'Livro 3',
        resenha: 'Descrição breve 3',
        preco: 9.9,
        capa: 'https://placehold.co/600x400.png',
    },
    {
        id: 4,
        titulo: 'Livro 4',
        resenha: 'Descrição breve 4',
        preco: 199.9,
        capa: 'https://placehold.co/600x400.png',
    },
    {
        id: 5,
        titulo: 'Livro 5',
        resenha: 'Descrição breve 5',
        preco: 29.9,
        capa: 'https://placehold.co/600x400.png',
    }
]);

</script>

<template>
<header>
  <div class="logo">
    <img src="https://cdn.shopify.com/s/files/1/0287/4323/7725/files/Everything_You_Should_Know_About_Vinyl_Record_Sizes_2048x2048.jpg?v=1631557061" alt="Logo">
  </div>
  <div class="barraDePesquisa">
    <input type="text" placeholder="Pesquisar">
  </div>
  <div class="abas">
    <ul>
      <li>
        <a href="#">Termos</a>
      </li>
      <li>
        <a href="#">Equipe</a>
      </li>
      <li>
        <a href="#">Envio</a>
      </li>
      <li>
        <a href="#">Devoluções</a>
      </li>
    </ul>
  </div>
  <div class="cards">
    <span class="fa-solid fa-cart-shopping"></span><p>|</p>
    <span class="fa-solid fa-heart"></span><p>|</p>
    <span class="fa-solid fa-user"></span>
  </div>
</header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
}
div.logo {

}
div.logo img {
  width: 10vw;
}
div.cards {
  display: flex;
  color: #F85525;
}
div.cards p {
margin: 0 0.5vw 0 0.5vw;
}

</style>
