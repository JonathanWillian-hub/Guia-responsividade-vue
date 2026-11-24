<script setup>
import { ref, watch } from 'vue'
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { useGuiaStore } from './stores/guia'
import BreakpointIndicator from './components/BreakpointIndicator.vue'

const guia = useGuiaStore()
const route = useRoute()
const menuAberto = ref(false)

// toda vez que a rota muda: fecha o menu e marca a seção como visitada
watch(
  () => route.path,
  (caminho) => {
    menuAberto.value = false
    guia.marcarVisitada(caminho)
  },
  { immediate: true },
)
</script>

<template>
  <header class="topo">
    <RouterLink to="/" class="marca">Largura Livre</RouterLink>

    <button
      class="botao-menu"
      type="button"
      :aria-expanded="menuAberto"
      aria-controls="menu-principal"
      @click="menuAberto = !menuAberto"
    >
      {{ menuAberto ? 'Fechar menu' : 'Abrir menu' }}
    </button>

    <nav id="menu-principal" :class="['menu', { aberto: menuAberto }]" aria-label="Seções do guia">
      <RouterLink v-for="secao in guia.secoes" :key="secao.to" :to="secao.to">
        {{ secao.texto }}
      </RouterLink>
    </nav>
  </header>

  <main class="conteudo">
    <!-- transição suave entre páginas (desligada se a pessoa pedir menos movimento) -->
    <RouterView v-slot="{ Component }">
      <Transition name="pagina" mode="out-in">
        <component :is="Component" />
      </Transition>
    </RouterView>
  </main>

  <BreakpointIndicator />
</template>

<style scoped>
/* ---------- CELULAR (base, sem media query) ---------- */
.topo {
  position: sticky;
  top: 0;
  z-index: 20;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: var(--espaco-1);
  padding: 0.75rem var(--espaco-2);
  background: rgb(22 36 58 / 0.96);
  color: var(--cor-fundo);
  box-shadow: 0 2px 12px rgb(22 36 58 / 0.18);
}
@supports (backdrop-filter: blur(8px)) {
  .topo { background: rgb(22 36 58 / 0.88); backdrop-filter: blur(8px); }
}
.marca {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  font-family: var(--fonte-titulo);
  font-size: 1.375rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  color: var(--cor-marca);
  text-decoration: none;
}
/* pequena "régua" ao lado do nome, lembrando a linha de cota */
.marca::before {
  content: '';
  width: 1.25rem;
  height: 0.75rem;
  border-left: 2px solid currentColor;
  border-right: 2px solid currentColor;
  background: linear-gradient(currentColor, currentColor) center / 100% 2px no-repeat;
}
.botao-menu {
  padding: 0.5rem 1rem;
  font: inherit;
  font-weight: 700;
  color: var(--cor-tinta);
  background: var(--cor-marca);
  border: 0;
  border-radius: var(--raio-total);
  cursor: pointer;
  transition: filter var(--transicao);
}
.botao-menu:hover { filter: brightness(1.05); }
.menu {
  display: none; /* escondido no celular: o botão abre */
  flex-direction: column;
  width: 100%;
  padding-top: var(--espaco-1);
}
.menu.aberto { display: flex; }
.menu a {
  padding: 0.75rem var(--espaco-1);
  color: var(--cor-fundo);
  text-decoration: none;
  border-top: 1px solid rgb(255 255 255 / 0.1);
  transition: background var(--transicao), color var(--transicao);
}
.menu a:hover { background: rgb(255 255 255 / 0.06); }
.menu a.router-link-active { color: var(--cor-marca); font-weight: 700; }

.conteudo {
  max-width: var(--largura-texto);
  margin: 0 auto;
  padding: var(--espaco-3) var(--espaco-2) var(--espaco-5);
}

/* transição entre páginas */
.pagina-enter-active,
.pagina-leave-active { transition: opacity 0.2s ease, transform 0.2s ease; }
.pagina-enter-from { opacity: 0; transform: translateY(0.5rem); }
.pagina-leave-to { opacity: 0; }

/* ---------- TABLET PARA CIMA ---------- */
@media (min-width: 48em) {
  .topo { padding: 0.75rem var(--espaco-4); }
  .botao-menu { display: none; }
  .menu {
    display: flex;
    flex-direction: row;
    width: auto;
    gap: 0.25rem;
    padding-top: 0;
  }
  .menu a {
    padding: 0.375rem 0.875rem;
    border-top: 0;
    border-radius: var(--raio-total);
  }
  .menu a:hover { background: rgb(255 255 255 / 0.1); }
  .menu a.router-link-active {
    color: var(--cor-tinta);
    background: var(--cor-marca);
  }
  .conteudo { padding-top: var(--espaco-4); }
}
</style>
