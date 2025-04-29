<script setup>
import { ref, onMounted } from 'vue'

const produtos = ref([])
const produtoDestaque = ref({})

const linkFakeStore = 'https://fakestoreapi.com/products'

async function buscarProdutos() {
  try {
    const respostaStore = await fetch(linkFakeStore)
    const informacoes = await respostaStore.json()

    const aleatorio = informacoes[Math.floor(Math.random() * informacoes.length)]
    produtoDestaque.value = aleatorio

    produtos.value = informacoes.map((produto) => ({
      id: produto.id,
      titulo: produto.title,
      desc: produto.description,
      preco: Number(produto.price),
      imagem: produto.image,
      link: '#',
      favoritado: false,
      comprado: false,
      quantidade: 1,
    }))
  } catch (error) {
    console.error('Erro ao buscar produtos:', error)
  }
}
onMounted(() => {
  buscarProdutos()
})

const carrinho = ref([]);

let ativo = ref(false);

function ativarDesetivar() {
  if (ativo.value == false) {
    ativo.value = true
  } else {
    ativo.value = false
  }
  atualizarTotal()
}

function adicionarCarrinho(item) {
  carrinho.value.push(item);
  item.comprado = true;
}
function retirarCarrinho(item) {
  item.comprado = false;
  carrinho.value.splice(carrinho.value.indexOf(item), 1);
}
function verProdutoZerados(item) {
  if (item.quantidade == 0) {
    item.comprado = false;
    carrinho.value.splice(carrinho.value.indexOf(item), 1);
  }
}

let total = ref(0);

function atualizarTotal() {
  for (const produto of carrinho.value) {
    total.value = 0;
    total.value = produto.preco * produto.quantidade + total.value;
  }
}

</script>

<template>
  <header>
      <h1>RandomThings</h1>
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
      <span @click="ativarDesetivar()" class="fa-solid fa-cart-shopping"></span>
      <p>|</p>
      <span class="fa-solid fa-heart"></span>
      <p>|</p>
      <span class="fa-solid fa-user"></span>
    </div>
  </header>
  <hr />
  <main>
    <div v-if="ativo == false">
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
  </div>
  <section v-else>
    <h1>Carrinho:</h1>
    <ul>
      <li>
        Produto
      </li>
      <li>
        Quantidade
      </li>
      <li>
        Valor
      </li>
    </ul>
    <ul v-for="(produto, index) in carrinho" :key="index">
      <li v-if="produto.quantidade > 0">
        <div class="infosCarrinho">
          <img :src="produto.imagem" alt="Imagem de produto"/>
          <div>
            <h3>{{ produto.titulo }}</h3>
            <p>{{ produto.preco.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</p>
          </div>
        </div>
        <div class="quantidadesCarrinho">
          <button @click="produto.quantidade-- && verProdutoZerados(produto)">-</button>
          <p>{{ produto.quantidade }}</p>
          <button @click="produto.quantidade++">+</button>
        </div>
        <div class="totalProduto">
          {{ (produto.preco * produto.quantidade).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}
        </div>
      </li>
    </ul>
    <button @click="ativarDesetivar()">Retornar para loja</button>
    <div class="somaTotal">
      <p>{{ total }}</p>
    </div>
  </section>
  <hr />
  </main>
  <footer>

  </footer>
</template>

<style scoped>
/*Geral*/
header {
  margin: 2vw 10vw 3vw 10vw;
}
section {
  margin: 0 5vw 0 5vw;
}
footer {
  margin: 0 5vw 2vw 5vw;
}
hr {
  color: #f85525;
  text-decoration: none;
  border: solid;
  border-width: 0.34vw;
  margin: 1vw 0 1vw 0;
  margin: 1vw 0 1vw 0;
}

/*CABEÇALHO*/
header {
  display: flex;
  justify-content: center;
  font-size: 1.5rem;
  font-weight: 500;
}
h1{
  margin-right: 4vw;
  font-weight: 600;
  font-size: 1.7rem;
}
div.barraDePesquisa input {
  font-size: 1.2rem;
  background-color: white;
  border: 3px solid #121619;
}
div.abas ul {
  display: flex;
  justify-content: space-between;
  margin-right: 2vw;
  margin-left: 2vw;
}
div.abas ul li {
  margin-right: 1vw;
  margin-left: 1vw;
}
div.cards {
  display: flex;
  color: #f85525;
}
div.cards span {
  margin: 0 0.5vw 0 0.5vw;
  font-size: 1.8rem;
}

/*item em destaque*/

section.destaque div.infoDoDestaque {
  display: flex;
  justify-content: space-between;
  margin-top: 2vw;
  margin-bottom: 2vw;
  align-items: center;
  gap: 3vw;
}
section.destaque div.textosDest {
  width: 60%;
}
section.destaque div.imagemDestaque {
  width: 40%;
  display: flex;
  justify-content: center;
  align-items: center;
}
section.destaque img{
  max-width: 100%;
  max-height: 400px;
  border: 3px solid #f85525;
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
  background-color: #f85525;
  border-color: #121619;
  padding: 0.5vw 1vw 0.5vw 1vw;
  font-size: 1.2rem;
}
section.destaque button:hover {
  background-color: #c74721;
}

/*Produtos*/

section.produtos {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
section.produtos li {
  margin: 1vw;
  width: 240px;
  height: 340px;
  border: solid 3px #f85525;
  user-select: none;
  display: flex;
  flex-direction: column;
  align-items: center;
}
section.produtos li:hover {
  transform: scale(1.1);
  transition: 0.2s;
}
section.produtos img {
  object-fit: cover;
  width: 80%;
  height: 170px;
  margin-top: 0.5vw;
  box-shadow: 4px 4px 4px rgba(0, 0, 0, 0.178);
}
section.produtos h3 {
  margin: 1vw;
  font-weight: 500;
}
section.produtos p {
  margin: 0 1vw 1vw 1vw;
}
section.produtos div button {
  margin-right: 1vw;
  border-color: #121619;
  border: 1.5px solid;
  font-weight: 500;
}
section.produtos div button.botaoComprar {
  background-color: #f85525;
}
section.produtos div button.botaoComprado {
  background-color: rgb(204, 204, 204);
  color: #485055;
}
section.produtos div button:hover {
  transition: 0.2s;
  transform: scale(1.1);
}
section.produtos div span {
  margin-left: 1vw;
  color: rgb(255, 36, 36);
}
section.produtos div span:hover{
  transform: scale(1.2);
  transition: 0.2s;
}
</style>
