<script setup>
import { ref } from 'vue'

const produtos = ref([
  {
    id: 1,
    titulo: 'Metallica (Remastered)',
    desc: 'The Black Album is one of the most commercially successful and critically acclaimed records of all time, with global sales of over 35 million, and contains a series of unrelenting singles, "Enter Sandman," "The Unforgiven", "Nothing Else Matters,"Wherever I May Roam," and "Sad But True."',
    preco: 234.4,
    capa: 'https://m.media-amazon.com/images/I/61Xk1PckmfL._AC_UL320_.jpg',
    link: 'https://www.amazon.com.br/Metallica-Remastered-Disco-Vinil/dp/B097C6KBV8/ref=lp_7791937011_1_9?pf_rd_p=721161a6-b78b-47dc-9717-91545f5eca72&pf_rd_r=M2Q70Y7MAC6TF05FCQTG&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&ufe=app_do%3Aamzn1.fos.6a09f7ec-d911-4889-ad70-de8dd83c8a74',
  },
  {
    id: 2,
    titulo: 'Livro 2',
    desc: 'Descrição breve 2',
    preco: 99.9,
    capa: 'https://placehold.co/600x400.png',
  },
  {
    id: 3,
    titulo: 'Livro 3',
    desc: 'Descrição breve 3',
    preco: 9.9,
    capa: 'https://placehold.co/600x400.png',
  },
  {
    id: 4,
    titulo: 'Livro 4',
    desc: 'Descrição breve 4',
    preco: 199.9,
    capa: 'https://placehold.co/600x400.png',
  },
  {
    id: 5,
    titulo: 'Livro 5',
    desc: 'Descrição breve 5',
    preco: 29.9,
    capa: 'https://placehold.co/600x400.png',
  },
])

let numeroProdutos = ref(produtos.value.length)
let numeroAleatorio = 0

function numeroArray() {
  numeroAleatorio = Math.floor(Math.random() * numeroProdutos.value)
}
numeroArray()
</script>

<template>
  <header>
    <div class="logo">
      <p>Vynil Records</p>
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
      <div class="infoDoDestaque" v-for="(produto, index) in produtos.slice(0, 1)" :key="index">
        <div class="textosDest">
          <h2>{{ produtos[0].titulo }}</h2>
          <p>{{ produtos[0].desc }}</p>
          <button >Acessar página do produto</button>
        </div>
        <div class="imagemDestaque">
          <img :src="produtos[0].capa" alt="" />
        </div>
      </div>
    </section>

    <hr />
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
