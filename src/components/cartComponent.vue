<template>
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
    <button class="retorno" @click="$emit('click-icon')">Retornar para loja</button>
    <div class="somaTotal">
      <p>Total da compra: <span>{{ total.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</span></p>
    </div>
  </div>
</template>
<script setup>
  defineEmits(['click-icon'])
  defineProps(['carrinho', 'upp-and-see', 'atualizar-total', 'total'])
</script>