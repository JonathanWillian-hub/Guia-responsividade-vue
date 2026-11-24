<script setup>
import { RouterLink } from 'vue-router'
import { useGuiaStore } from '../stores/guia'
import CotaLarga from '../components/CotaLarga.vue'

const guia = useGuiaStore()
</script>

<template>
  <section class="inicio">
    <CotaLarga />
    <h1>Largura Livre</h1>
    <p class="lead">
      O número acima é a largura da sua janela agora. Estique, encolha, gire o celular: ele muda.
      Um site responsivo é um site que aguenta qualquer número.
    </p>

    <ul class="indice">
      <li v-for="secao in guia.secoes" :key="secao.to">
        <RouterLink :to="secao.to">
          <strong>{{ secao.texto }}</strong>
          <span>{{ secao.resumo }}</span>
          <em v-if="guia.visitadas.includes(secao.to)">visitada</em>
        </RouterLink>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.lead { font-size: 1.125rem; max-width: 36rem; color: var(--cor-tinta-suave); }
.indice {
  list-style: none;
  margin: var(--espaco-4) 0 0;
  padding: 0;
  display: grid;
  gap: var(--espaco-2);
  counter-reset: secao; /* numeração 01, 02, 03... feita pelo CSS */
}
.indice li { counter-increment: secao; }
.indice a {
  position: relative;
  display: grid;
  gap: 0.25rem;
  height: 100%;
  padding: var(--espaco-2) var(--espaco-2) var(--espaco-2) 4rem;
  color: var(--cor-tinta);
  background: var(--cor-superficie);
  border: 1px solid var(--cor-borda);
  border-radius: var(--raio);
  box-shadow: var(--sombra-1);
  text-decoration: none;
  transition: transform var(--transicao), box-shadow var(--transicao), border-color var(--transicao);
}
.indice a::before {
  content: counter(secao, decimal-leading-zero);
  position: absolute;
  left: var(--espaco-2);
  top: var(--espaco-2);
  font-family: var(--fonte-codigo);
  font-size: 0.875rem;
  font-weight: 400;
  color: var(--cor-cota);
}
.indice a::after {
  content: '→';
  position: absolute;
  right: var(--espaco-2);
  top: var(--espaco-2);
  color: var(--cor-tinta-suave);
  transition: transform var(--transicao);
}
.indice a:hover {
  transform: translateY(-2px);
  border-color: var(--cor-marca);
  box-shadow: var(--sombra-2);
}
.indice a:hover::after { transform: translateX(3px); }
.indice strong { font-family: var(--fonte-titulo); font-size: 1.125rem; padding-right: var(--espaco-3); }
.indice span { color: var(--cor-tinta-suave); font-size: 0.9375rem; }
.indice em {
  justify-self: start;
  margin-top: 0.25rem;
  padding: 0.1rem 0.6rem;
  font-size: 0.75rem;
  font-style: normal;
  font-weight: 700;
  color: var(--cor-sucesso);
  background: var(--cor-sucesso-suave);
  border-radius: var(--raio-total);
}
.indice em::before { content: '✓ '; }

@media (min-width: 48em) {
  .indice { grid-template-columns: repeat(2, minmax(0, 1fr)); }
}
</style>
