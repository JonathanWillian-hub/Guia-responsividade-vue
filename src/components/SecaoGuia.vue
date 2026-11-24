<script setup>
import CodigoExemplo from './CodigoExemplo.vue'

defineProps({
  titulo: { type: String, required: true },
  pergunta: { type: String, required: true },
  codigo: { type: String, required: true },
  linguagem: { type: String, default: 'css' },
  fontes: {
    type: Array, // [{ nome: 'MDN', url: 'https://...' }]
    required: true,
    validator: (lista) => lista.length > 0,
  },
})
</script>

<template>
  <article class="secao">
    <h1>{{ titulo }}</h1>

    <!-- 1. Explicação curta -->
    <section class="bloco">
      <h2>Em poucas palavras</h2>
      <slot name="explicacao" />
    </section>

    <!-- 2. Exemplo de código comentado -->
    <section class="bloco">
      <h2>Exemplo</h2>
      <CodigoExemplo :codigo="codigo" :linguagem="linguagem" />
    </section>

    <!-- Laboratório (opcional) -->
    <section v-if="$slots.laboratorio" class="bloco laboratorio">
      <h2>Laboratório</h2>
      <slot name="laboratorio" />
    </section>

    <!-- 3. Pergunta-guia respondida -->
    <section class="bloco">
      <h2>Pergunta-guia</h2>
      <p class="enunciado">{{ pergunta }}</p>
      <slot name="resposta" />
    </section>

    <!-- 4. Fontes consultadas -->
    <footer class="bloco fontes">
      <h2>Fontes consultadas</h2>
      <ul>
        <li v-for="fonte in fontes" :key="fonte.url">
          <a :href="fonte.url" target="_blank" rel="noopener">{{ fonte.nome }}</a>
        </li>
      </ul>
    </footer>
  </article>
</template>

<style scoped>
/* minmax(0, 1fr): impede que um filho largo (código) estique a página */
.secao {
  display: grid;
  grid-template-columns: minmax(0, 1fr);
  gap: var(--espaco-4);
}
/* título da página com um traço de marca-texto embaixo */
.secao > h1 {
  padding-bottom: var(--espaco-2);
  margin-bottom: 0;
  border-bottom: 2px solid var(--cor-borda);
}
.bloco h2 {
  display: inline-block;
  margin-bottom: var(--espaco-2);
  padding: 0 0.15em;
  /* efeito marca-texto, como num caderno */
  background: linear-gradient(transparent 58%, var(--cor-marca) 58%, var(--cor-marca) 90%, transparent 90%);
}
.enunciado {
  position: relative;
  padding: var(--espaco-2) var(--espaco-2) var(--espaco-2) 3.25rem;
  margin-bottom: var(--espaco-2);
  border-left: 0.375rem solid var(--cor-marca);
  border-radius: var(--raio-p);
  background: var(--cor-marca-suave);
  font-weight: 700;
}
/* ícone de interrogação desenhado só com CSS */
.enunciado::before {
  content: '?';
  position: absolute;
  left: var(--espaco-2);
  top: var(--espaco-2);
  display: grid;
  place-items: center;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  background: var(--cor-tinta);
  color: var(--cor-marca);
  font-family: var(--fonte-titulo);
  font-size: 0.9rem;
  line-height: 1;
}
.laboratorio {
  padding: var(--espaco-3) var(--espaco-2);
  background: var(--cor-superficie);
  border: 1px solid var(--cor-borda);
  border-radius: var(--raio);
  box-shadow: var(--sombra-1);
}
.fontes {
  padding-top: var(--espaco-3);
  border-top: 2px solid var(--cor-borda);
}
.fontes ul { margin: 0; padding: 0; list-style: none; display: grid; gap: var(--espaco-1); }
.fontes a::after { content: ' ↗'; font-size: 0.85em; }

@media (min-width: 48em) {
  .laboratorio { padding: var(--espaco-3); }
}
</style>
