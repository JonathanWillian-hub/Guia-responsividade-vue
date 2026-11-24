<script setup>
import SecaoGuia from '../components/SecaoGuia.vue'

const codigo = `<!-- width e height: o navegador reserva o espaço ANTES de baixar a imagem.
     srcset + sizes: o navegador escolhe o arquivo do tamanho certo.
     loading="lazy": só baixa quando a imagem estiver perto de aparecer. -->
<img
  src="gato-800.jpg"
  srcset="gato-400.jpg 400w, gato-800.jpg 800w, gato-1600.jpg 1600w"
  sizes="(min-width: 48em) 44rem, 100vw"
  width="800"
  height="533"
  alt="Gato laranja dormindo no sofá"
  loading="lazy"
/>

<style>
  /* a imagem nunca fica mais larga que o espaço disponível
     e a altura acompanha, mantendo a proporção */
  img {
    max-width: 100%;
    height: auto;
  }
</style>`

const fontes = [
  { nome: 'MDN — Imagens responsivas', url: 'https://developer.mozilla.org/pt-BR/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images' },
  { nome: 'web.dev — Cumulative Layout Shift (CLS)', url: 'https://web.dev/articles/cls' },
  { nome: 'web.dev — Optimize CLS', url: 'https://web.dev/articles/optimize-cls' },
]
</script>

<template>
  <SecaoGuia
    titulo="Imagens responsivas"
    pergunta="Ao abrir uma página, o texto aparece primeiro. Quando a imagem termina de carregar, ela empurra o texto para baixo. Por que isso acontece quando a imagem não tem width e height no HTML? Qual métrica do Google mede esse problema?"
    :codigo="codigo"
    linguagem="html"
    :fontes="fontes"
  >
    <template #explicacao>
      <p>
        Uma imagem com largura fixa pode ficar maior que a tela do celular e "estourar" o layout.
        A regra <code>max-width: 100%; height: auto;</code> resolve isso: a imagem encolhe para caber
        no espaço e mantém a proporção.
      </p>
      <p>
        Além disso, não faz sentido o celular baixar uma foto enorme feita para monitores. Com
        <code>srcset</code> e <code>sizes</code> oferecemos vários tamanhos do mesmo arquivo, e o navegador
        escolhe o menor que fica nítido naquela tela. O <code>loading="lazy"</code> adia o download das imagens
        que ainda estão lá embaixo na página, e os atributos <code>width</code> e <code>height</code> evitam
        que o conteúdo "pule" enquanto a imagem carrega.
      </p>
    </template>

    <template #resposta>
      <p>
        Sem <code>width</code> e <code>height</code>, o navegador não sabe o tamanho da imagem até terminar de
        baixá-la. Então ele monta a página reservando <strong>altura zero</strong> para ela. Quando a imagem chega,
        ele descobre a altura, abre espaço e empurra tudo o que estava abaixo. É aquele "pulo" que faz a gente
        clicar no lugar errado.
      </p>
      <p>
        Com os dois atributos, o navegador calcula a proporção (por exemplo, 800 × 533) e já reserva o espaço
        certo, mesmo usando <code>height: auto</code> no CSS. A imagem aparece no buraco que já estava esperando
        por ela.
      </p>
      <p>
        O Google mede esse problema com o <strong>CLS (Cumulative Layout Shift)</strong>, uma das métricas
        Core Web Vitals. Ela soma o quanto o conteúdo se mexe sozinho durante o carregamento. Um bom valor é
        <strong>0,1 ou menos</strong>.
      </p>
    </template>
  </SecaoGuia>
</template>
