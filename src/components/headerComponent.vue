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
      <span @click="$emit('click-icon')" class="fa-solid fa-cart-shopping"></span>
      <p>|</p>
      <span class="fa-solid fa-heart"></span>
      <p>|</p>
      <span class="fa-solid fa-user"></span>
    </div>
  </header>
  <hr />
</template>
<script setup>
  defineEmits(['click-icon'])
</script>