<script setup>
defineProps({
  codigo: { type: String, required: true },
  linguagem: { type: String, default: 'css' },
})
</script>

<template>
  <div class="caixa">
    <div class="barra" aria-hidden="true">{{ linguagem }}</div>
    <pre class="codigo" :data-lang="linguagem" tabindex="0"><code>{{ codigo }}</code></pre>
  </div>
</template>

<style scoped>
.caixa {
  max-width: 100%;
  border-radius: var(--raio);
  overflow: hidden; /* deixa o canto arredondado também no <pre> */
  box-shadow: var(--sombra-2);
  background: var(--cor-tinta);
}
.barra {
  padding: 0.4rem var(--espaco-2);
  font-family: var(--fonte-codigo);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--cor-marca);
  background: rgb(255 255 255 / 0.05);
  border-bottom: 1px solid rgb(255 255 255 / 0.08);
}
.codigo {
  margin: 0;
  padding: var(--espaco-2);
  color: #e3e9e5;
  font-size: 0.8125rem;
  line-height: 1.7;
  max-width: 100%;
  overflow-x: auto; /* rola só dentro do bloco, nunca a página */
}
</style>
