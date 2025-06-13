<script setup>

import DestaqueComponent from '../components/destaqueComponent.vue';


import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

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


function botaoPaginaDestaque() {
alert("Eu teria feito algo maneiro aqui mas imaginei que teria que passar por diversos 'Object, object' tentando, então por enquanto não tem nada aqui mesmo. ")
}

// produtos do carrinho e ativação

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


// modificar produtos do carrinho

function adicionarCarrinho(item) {
  carrinho.value.push(item);
  item.comprado = true;
}

function retirarCarrinho(item) {
  item.comprado = false;
  carrinho.value.splice(carrinho.value.indexOf(item), 1);
}

let tempArrayID = ref();

function verProdutoZerados(item) {
  if (item.quantidade == 0) {
    tempArrayID.value = item.id;
    carrinho.value.splice(carrinho.value.indexOf(item), 1);
    for (const produto of produtos.value) {
      if (produto.id === tempArrayID.value) {
        produto.comprado = false;
        produto.quantidade = 1;
      }
    }
  }
}


//ver total

let total = ref(0);

function atualizarTotal() {
  total.value = 0;
  for (const produto of carrinho.value) {
    total.value = produto.preco * produto.quantidade + total.value;
  }
}


/*funções de resumo*/

function upAndSee(item) {
  atualizarTotal()
  verProdutoZerados(item)
}


const router = useRouter();

function openBook(id) {
  router.push({ name: 'Book', params: { id } })
}

</script>

<template>
  <hr />
  <main>
    <div v-if="ativo == false">

      <DestaqueComponent
      @clickDestaque = "botaoPaginaDestaque()"
      :produtoDestaque = "produtoDestaque.value"
      />

    <hr />
    <section class="produtos">
      <ul v-for="(produto, index) in produtos" :key="index">
        <li @click="openBook(produto.id)">
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
  <section v-else-if="ativo == true && carrinho.length !== 0" class="carrinho">
    <h1>Carrinho:</h1>
    <ul class="catProdutosComprados">
      <li>
        Produto:
      </li>
      <li class="quantidade">
        Quantidade:
      </li>
      <li class="valor">
        Valor:
      </li>
    </ul>
    <ul v-for="(produto, index) in carrinho" :key="index">
      <li v-if="produto.quantidade > 0" class="itensNoCarrinho">
        <div class="infosCarrinho">
          <img :src="produto.imagem" alt="Imagem de produto"/>
          <div class="nomeEPreco">
            <h3>{{ produto.titulo }}</h3>
            <p>{{ produto.preco.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</p>
          </div>
        </div>
        <div class="quantidadesCarrinho">
          <button @click="produto.quantidade-- && upAndSee(produto)">-</button>
          <p>{{ produto.quantidade }}</p>
          <button @click="produto.quantidade++ && atualizarTotal()">+</button>
        </div>
        <div class="totalProduto">
          {{ (produto.preco * produto.quantidade).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}
        </div>
      </li>
    </ul>
    <div class="fimCarrinho">
    <button class="retorno" @click="ativarDesetivar()">Retornar para loja</button>
    <div class="somaTotal">
      <p>Total da compra: <span>{{ total.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</span></p>
    </div>
  </div>
  </section>
  <section class="carrinhoVazio" v-else-if="ativo == true && carrinho.length == 0">
    <div>
      <p>Adicione novos produtos ao carrinho e eles aparecerão aqui!</p>
    </div>
    <button class="retorno" @click="ativarDesetivar()">Retornar para loja</button>
  </section>
  <hr />
  </main>
</template>
