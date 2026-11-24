<script setup>
import SecaoGuia from '../components/SecaoGuia.vue'

const codigo = `<!-- 1. No <head>: diz ao celular "use a sua largura real" -->
<meta name="viewport" content="width=device-width, initial-scale=1" />

<style>
  /* 2. Mobile-first: estilo base pensado para telas pequenas */
  .menu { display: none; }

  /* 3. Só vale quando a janela tiver 48em (768px) ou mais.
     Sem a meta viewport, o celular finge ter ~980px
     e esta regra seria aplicada até no celular! */
  @media (min-width: 48em) {
    .menu { display: flex; }
  }
</style>`

const fontes = [
  { nome: 'MDN — Meta tag viewport', url: 'https://developer.mozilla.org/pt-BR/docs/Web/HTML/Viewport_meta_tag' },
  { nome: 'MDN — Usando media queries', url: 'https://developer.mozilla.org/pt-BR/docs/Web/CSS/CSS_media_queries/Using_media_queries' },
  { nome: 'web.dev — Responsive web design basics', url: 'https://web.dev/articles/responsive-web-design-basics' },
]
</script>

<template>
  <SecaoGuia
    titulo="Por que responsividade importa"
    pergunta="Um site tem media queries bem escritas, mas não tem a meta tag viewport. No celular, ele aparece como a versão de computador, só que minúscula. Por que isso acontece, e o que a meta viewport muda?"
    :codigo="codigo"
    linguagem="html"
    :fontes="fontes"
  >
    <template #explicacao>
      <p>
        Hoje a maioria das pessoas acessa sites pelo celular. Um site <strong>responsivo</strong> é aquele
        que se adapta a qualquer largura de tela: o mesmo HTML se reorganiza para caber num celular,
        num tablet ou num monitor grande, sem precisar dar zoom nem rolar para os lados.
      </p>
      <p>
        O <strong>viewport</strong> é a "janela" por onde a pessoa vê a página. No computador, é o tamanho
        da janela do navegador. No celular, ele depende de uma linha no HTML: a
        <code>&lt;meta name="viewport"&gt;</code>. É ela que faz o celular mostrar a página na largura
        real da tela.
      </p>
    </template>

    <template #resposta>
      <p>
        Quando os celulares surgiram, quase nenhum site era feito para eles. Por isso, sem a meta viewport,
        o navegador do celular <strong>finge ter uma tela de uns 980px</strong>, monta a página nessa largura
        e depois encolhe tudo para caber na tela. O resultado é a versão de computador em miniatura.
      </p>
      <p>
        As media queries perguntam "qual a largura do viewport?". Como o celular responde "980px", regras
        como <code>@media (min-width: 48em)</code> são aplicadas e as regras de celular nunca entram em ação,
        por mais bem escritas que estejam.
      </p>
      <p>
        Com <code>width=device-width, initial-scale=1</code>, o viewport passa a ter a largura real do
        aparelho (por exemplo, 390px) e a página não é encolhida. Aí as media queries recebem o número
        certo e o layout de celular aparece.
      </p>
    </template>
  </SecaoGuia>
</template>
