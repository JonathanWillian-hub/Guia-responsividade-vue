<script setup>
import { ref } from 'vue'

// Dupla: troquem pela pergunta de vocês (que só se responde usando o guia)
const pergunta = 'No nosso laboratório de Grid, a partir de que largura (em px) aparecem 3 colunas?'
const respostaCerta = '704'

const tentativa = ref('')
const resultado = ref('') // '', 'certo' ou 'errado'

function conferir() {
  const limpo = tentativa.value.replace(/\D/g, '')
  resultado.value = limpo === respostaCerta ? 'certo' : 'errado'
}
</script>

<template>
  <article class="desafio">
    <h1>Desafio</h1>
    <p class="enunciado">{{ pergunta }}</p>

    <label for="resposta">Sua resposta</label>
    <div class="linha">
      <input id="resposta" v-model="tentativa" inputmode="numeric" @keyup.enter="conferir" />
      <button type="button" @click="conferir">Conferir</button>
    </div>

    <p v-if="resultado === 'certo'" class="certo" role="status">Certo! Você usou o guia direitinho.</p>
    <p v-else-if="resultado === 'errado'" class="errado" role="status">
      Ainda não. Volte ao laboratório de Flex e Grid e confira a conta.
    </p>
  </article>
</template>

<style scoped>
.desafio {
  padding: var(--espaco-3) var(--espaco-2);
  background: var(--cor-superficie);
  border: 1px solid var(--cor-borda);
  border-radius: var(--raio);
  box-shadow: var(--sombra-1);
}
.enunciado {
  padding: var(--espaco-2);
  margin-bottom: var(--espaco-3);
  border-left: 0.375rem solid var(--cor-marca);
  border-radius: var(--raio-p);
  background: var(--cor-marca-suave);
  font-size: 1.125rem;
}
label { display: block; margin-bottom: var(--espaco-1); font-weight: 700; }
.linha { display: flex; gap: var(--espaco-1); flex-wrap: wrap; }
input {
  flex: 1 1 8rem;
  min-width: 0;
  padding: 0.75rem 1rem;
  font: inherit;
  border: 2px solid var(--cor-borda);
  border-radius: var(--raio-p);
  background: var(--cor-superficie);
  transition: border-color var(--transicao), box-shadow var(--transicao);
}
input:focus { border-color: var(--cor-azul); box-shadow: 0 0 0 3px rgb(35 71 214 / 0.15); outline: none; }
button {
  padding: 0.75rem 1.5rem;
  font: inherit;
  font-weight: 700;
  color: var(--cor-fundo);
  background: var(--cor-tinta);
  border: 0;
  border-radius: var(--raio-p);
  cursor: pointer;
  transition: transform var(--transicao), box-shadow var(--transicao);
}
button:hover { transform: translateY(-1px); box-shadow: var(--sombra-2); }
button:active { transform: translateY(0); }
.certo,
.errado {
  margin-top: var(--espaco-2);
  padding: 0.75rem var(--espaco-2);
  font-weight: 700;
  border-radius: var(--raio-p);
}
.certo { color: var(--cor-sucesso); background: var(--cor-sucesso-suave); }
.errado { color: var(--cor-cota); background: var(--cor-cota-suave); }

@media (min-width: 48em) {
  .desafio { padding: var(--espaco-4); }
}
</style>
