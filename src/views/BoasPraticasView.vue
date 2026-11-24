<script setup>
import SecaoGuia from '../components/SecaoGuia.vue'

const codigo = `<!-- ERRADO: sem :key (ou usando o índice), o Vue reaproveita
     os elementos pela POSIÇÃO e o texto digitado pode "pular" -->
<li v-for="animal in animais">
  {{ animal.nome }} <input />
</li>

<!-- CERTO: :key com um id único e que não muda.
     O Vue sabe exatamente qual item saiu da lista -->
<li v-for="animal in animais" :key="animal.id">
  {{ animal.nome }} <input />
</li>

<!-- Rotas com import(): a página só é baixada quando alguém entra nela -->
<!-- { path: '/desafio', component: () => import('./views/DesafioView.vue') } -->`

const fontes = [
  { nome: 'Vue.js — Mantendo o estado com key', url: 'https://vuejs.org/guide/essentials/list.html#maintaining-state-with-key' },
  { nome: 'Vue.js — Guia de estilo', url: 'https://vuejs.org/style-guide/' },
  { nome: 'Vue Router — Lazy loading de rotas', url: 'https://router.vuejs.org/guide/advanced/lazy-loading.html' },
]
</script>

<template>
  <SecaoGuia
    titulo="Boas práticas em projetos Vue"
    pergunta="Uma lista de animais é exibida com v-for, sem :key, e cada item tem um campo de texto. A pessoa digita algo no campo do segundo animal, e em seguida o primeiro animal é removido da lista. O que pode acontecer com o texto digitado, e por quê?"
    :codigo="codigo"
    linguagem="vue"
    :fontes="fontes"
  >
    <template #explicacao>
      <p>
        Um projeto Vue organizado é mais fácil de manter e carrega mais rápido. Algumas práticas que usamos
        neste próprio guia:
      </p>
      <ul>
        <li>
          <strong>Componentes pequenos e reutilizáveis:</strong> todas as seções usam o mesmo
          <code>SecaoGuia.vue</code>, que recebe título, pergunta e código por <em>props</em>.
        </li>
        <li>
          <strong>Uma única fonte de dados:</strong> a lista de seções fica na store do Pinia
          (<code>stores/guia.js</code>), e o menu e a página inicial leem dela.
        </li>
        <li>
          <strong>Rotas carregadas sob demanda:</strong> com <code>import()</code> no router, cada página só é
          baixada quando alguém entra nela. O primeiro carregamento fica mais leve.
        </li>
        <li>
          <strong>Estilos com escopo e tokens:</strong> <code>&lt;style scoped&gt;</code> evita que o CSS de um
          componente afete outro, e as cores e espaços ficam centralizados em <code>tokens.css</code>.
        </li>
        <li>
          <strong>Sempre usar <code>:key</code> no <code>v-for</code></strong>, com um valor único e estável,
          como um id.
        </li>
      </ul>
    </template>

    <template #resposta>
      <p>
        O texto pode <strong>"pular" para o animal errado</strong>. Sem <code>:key</code>, o Vue não sabe
        qual item é qual, então reaproveita os elementos da tela pela <strong>posição</strong>.
      </p>
      <p>
        Quando o primeiro animal sai, o Vue não apaga a primeira linha. Ele só troca os nomes: a linha 1 passa
        a mostrar o 2º animal, a linha 2 passa a mostrar o 3º, e assim por diante, até apagar a última linha.
        Só que o que foi digitado no campo fica guardado no próprio elemento da tela, e não nos dados do Vue.
        Então o texto continua na linha 2, que agora mostra o <strong>terceiro</strong> animal, e o animal em
        que a pessoa digitou aparece com o campo vazio.
      </p>
      <p>
        Com <code>:key="animal.id"</code>, o Vue identifica cada item, remove a linha certa e o texto fica com
        o animal certo. Usar o índice do <code>v-for</code> como key causa o mesmo problema, porque o índice
        também muda quando a lista muda.
      </p>
    </template>
  </SecaoGuia>
</template>
