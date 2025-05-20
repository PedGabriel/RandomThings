<script setup>
import { ref, onMounted } from 'vue'
import HeaderComponent from './components/headerComponent.vue'
import FooterComponent from './components/footerComponent.vue'
import CartNoPurchased from './components/cartNoPurchased.vue'
import DestaqueComponent from './destaqueComponent.vue';
import ProdutosComponent from './produtosComponent.vue';
import CartComponent from './components/cartComponent.vue'

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
  alert(
    "Eu teria feito algo maneiro aqui mas imaginei que teria que passar por diversos 'Object, object' tentando, então por enquanto não tem nada aqui mesmo. ",
  )
}

// produtos do carrinho e ativação

const carrinho = ref([])

let ativo = ref(false)

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
  carrinho.value.push(item)
  item.comprado = true
}

function retirarCarrinho(item) {
  item.comprado = false
  carrinho.value.splice(carrinho.value.indexOf(item), 1)
}

let tempArrayID = ref()

function verProdutoZerados(item) {
  if (item.quantidade == 0) {
    tempArrayID.value = item.id
    carrinho.value.splice(carrinho.value.indexOf(item), 1)
    for (const produto of produtos.value) {
      if (produto.id === tempArrayID.value) {
        produto.comprado = false
        produto.quantidade = 1
      }
    }
  }
}

//ver total

let total = ref(0)

function atualizarTotal() {
  total.value = 0
  for (const produto of carrinho.value) {
    total.value = produto.preco * produto.quantidade + total.value
  }
}

/*funções de resumo*/

function upAndSee(item) {
  atualizarTotal()
  verProdutoZerados(item)
}
</script>

<template>
  <HeaderComponent @click-icon="ativarDesetivar()" />

  <main>
    <div v-if="ativo == false">
      <DestaqueComponent
      :produto-destaque = produtoDestaque
      />

      <ProdutosComponent

      />
    </div>

    <section v-else-if="ativo == true && carrinho.length !== 0" class="carrinho">
      <CartComponent
      @click-icon="ativarDesetivar()"
      :carrinho="carrinho"
      :atualizar-total="atualizarTotal()"
      :upp-and-see="upAndSee()"
      />
    </section>

    <section class="carrinhoVazio" v-else-if="ativo == true && carrinho.length == 0">
      <CartNoPurchased />
    </section>

    <hr />
  </main>

  <FooterComponent />
</template>
