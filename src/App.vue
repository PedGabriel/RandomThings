<script setup>
import { ref, onMounted } from 'vue'

const produtos = ref([])
const produtoDestaque = ref({})

const linkFakeStore = 'https://fakestoreapi.com/products'

async function buscarProdutos() {
try {
  const respostaStore = await fetch(linkFakeStore)
  const informacoes = await respostaStore.json()

  const aleatorio = informacoes[Math.floor(Math.random() * informacoes.length)];
  produtoDestaque.value = aleatorio;

  produtos.value = informacoes.map((produto) => ({
    id: produto.id,
    titulo: produto.title,
    desc: produto.description,
    preco: produto.price,
    imagem: produto.image,
    link: '#',
  }))
  } catch (error) {
    console.error('Erro ao buscar produtos:', error);
  }
}
onMounted(() => {
  buscarProdutos()
})

</script>

<template>
  <header>
    <div class="logo">
      <p>Random Things</p>
    </div>
    <div class="barraDePesquisa">
      <input type="text" placeholder="Pesquisar" />
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
      <span class="fa-solid fa-cart-shopping"></span>
      <p>|</p>
      <span class="fa-solid fa-heart"></span>
      <p>|</p>
      <span class="fa-solid fa-user"></span>
    </div>
  </header>
  <hr />
  <main>
    <section class="destaque">
      <div class="infoDoDestaque" v-if="produtoDestaque.id">
        <div class="textosDest">
          <h2>{{ produtoDestaque.title }}</h2>
          <p>{{ produtoDestaque.description }}</p>
          <button>Acessar página do produto</button>
        </div>
        <div class="imagemDestaque">
          <img :src="produtoDestaque.image" alt="Imagem do produto em destaque" />
        </div>
      </div>
    </section>
    <hr />
    <section class="produtos">
      <ul v-for="(produto, index) in produtos" :key="index">
        <li>
          {{ produto }}
        </li>
      </ul>
    </section>
  </main>
</template>

<style scoped>

/*Geral*/
header{
  margin: 2vw 10vw 3vw 10vw;
}
section {
  margin: 0 5vw 0 5vw;
}
footer {
  margin: 0 5vw 2vw 5vw;
}
hr {
  color: #F85525;
  text-decoration: none;
  border: solid;
  border-width: 0.22vw;
  margin: 1vw 0 1vw 0;
  margin: 1vw 0 1vw 0;
}

/*CABEÇALHO*/
header {
  display: flex;
  justify-content: space-between;
  font-size: 1.5rem;
  font-weight: 500;
}
div.logo {
  display: flex;
}
div.barraDePesquisa input {
  font-size: 1.2rem;
}
div.abas ul{
  display: flex;
  justify-content: space-between;
}
div.abas ul li {
  margin-right: 1vw;
  margin-left: 1vw;
}
div.cards {
  display: flex;
  color: #F85525;
}
div.cards span {
margin: 0 0.5vw 0 0.5vw;
font-size: 1.8rem;
}

/*item em destaque*/

section.destaque div.infoDoDestaque {
  display: flex;
  justify-content: space-between;
}
section.destaque div.textosDest {
  width: 60%;
}
section.destaque h2 {
  font-size: 2rem;
  font-weight: 500;
  margin-bottom: 2vw;
}
section.destaque p {
  font-size: 1.5rem;
  line-height: 130%;
}
section.destaque button {
  margin-top: 2vw;
  background-color: #F85525;
  border-color: #121619;
  padding: 0.5vw 1vw 0.5vw 1vw;
  font-size: 1.2rem;
}
section.destaque button:hover {
  background-color: #c74721;
}
</style>
