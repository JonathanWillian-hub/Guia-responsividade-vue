<script setup>
import { useViewport } from '../composables/useViewport'
const { largura, breakpoint } = useViewport()
</script>

<template>
  <div class="indicador" role="status" aria-live="off">
    {{ largura }}px · {{ breakpoint }}
  </div>
</template>

<style scoped>
.indicador {
  position: fixed;
  right: var(--espaco-2);
  bottom: var(--espaco-2);
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.375rem 0.875rem;
  background: var(--cor-cota);
  color: #fff;
  font-family: var(--fonte-codigo);
  font-size: 0.8125rem;
  font-variant-numeric: tabular-nums;
  border-radius: var(--raio-total);
  box-shadow: var(--sombra-2);
  z-index: 10;
}
/* pontinho "ao vivo" */
.indicador::before {
  content: '';
  width: 0.45rem;
  height: 0.45rem;
  border-radius: 50%;
  background: #fff;
  opacity: 0.85;
}
</style>
