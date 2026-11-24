<script setup>
import SecaoGuia from '../components/SecaoGuia.vue'

const codigo = `/* rem: relativo à fonte da raiz (padrão 16px, mas a pessoa pode mudar) */
body { font-size: 1rem; }          /* 16px no padrão */
h1   { font-size: 2.5rem; }        /* 40px no padrão */

/* px: fixo, ignora a configuração de fonte (evite para textos) */
.legenda { font-size: 12px; }

/* em: relativo à fonte do próprio elemento */
.botao { font-size: 1.25rem; padding: 0.5em 1em; } /* padding cresce junto */

/* %: relativo ao elemento pai */
.coluna { width: 50%; }

/* fr: fração do espaço que sobra no grid */
.grade { display: grid; grid-template-columns: 1fr 2fr; }

/* vw / vh / dvh: porcentagem da janela */
.capa { min-height: 100dvh; }      /* dvh desconta a barra do navegador no celular */
.titulo-capa { font-size: clamp(2rem, 6vw, 4rem); }

/* ch: largura do caractere "0" — ótimo para limitar linhas de texto */
p { max-width: 65ch; }`

const fontes = [
  { nome: 'MDN — Valores e unidades CSS', url: 'https://developer.mozilla.org/pt-BR/docs/Learn/CSS/Building_blocks/Values_and_units' },
  { nome: 'web.dev — Learn CSS: Sizing units', url: 'https://web.dev/learn/css/sizing' },
  { nome: 'W3C — WCAG 1.4.4 Redimensionar texto', url: 'https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html' },
]
</script>

<template>
  <SecaoGuia
    titulo="Unidades CSS"
    pergunta="Uma pessoa com baixa visão aumenta o tamanho da fonte nas configurações do navegador. O texto definido em px continua do mesmo tamanho, e o definido em rem aumenta. Por que essa diferença acontece?"
    :codigo="codigo"
    :fontes="fontes"
  >
    <template #explicacao>
      <p>
        Toda medida no CSS precisa de uma unidade. Algumas são <strong>absolutas</strong> (não mudam nunca)
        e outras são <strong>relativas</strong> (dependem de outra coisa: da fonte, do elemento pai ou da janela).
        Em site responsivo, as relativas são as mais usadas.
      </p>
      <ul>
        <li><code>px</code>: tamanho fixo. Bom para bordas finas, ruim para textos.</li>
        <li><code>rem</code>: múltiplo da fonte do <code>&lt;html&gt;</code> (normalmente 16px). <code>2rem</code> = 32px.</li>
        <li><code>em</code>: múltiplo da fonte do próprio elemento. Útil para espaçamentos que crescem com o texto.</li>
        <li><code>%</code>: porcentagem do elemento pai.</li>
        <li><code>fr</code>: uma fração do espaço livre num grid.</li>
        <li><code>vw</code> e <code>vh</code>: 1% da largura e da altura da janela.</li>
        <li><code>dvh</code>: como o <code>vh</code>, mas acompanha a barra do navegador do celular que aparece e some.</li>
        <li><code>ch</code>: largura do caractere "0". <code>65ch</code> deixa as linhas de texto num tamanho confortável de ler.</li>
      </ul>
    </template>

    <template #resposta>
      <p>
        O <code>px</code> é uma unidade <strong>absoluta</strong>: <code>20px</code> é sempre 20px, não importa
        o que a pessoa configurou. Já o <code>rem</code> é <strong>relativo à fonte da raiz</strong>
        (o elemento <code>&lt;html&gt;</code>), e essa fonte vem justamente da configuração do navegador.
      </p>
      <p>
        No padrão, 1rem = 16px. Se a pessoa muda a fonte para 24px, 1rem passa a valer 24px. Um título
        com <code>1.25rem</code> vai de 20px para 30px sozinho, enquanto um com <code>20px</code> fica parado.
      </p>
      <p>
        Por isso usamos <code>rem</code> para fontes e espaçamentos: o site respeita quem precisa de letras
        maiores, como pede a diretriz de acessibilidade WCAG 1.4.4. Neste guia, todos os espaços em
        <code>tokens.css</code> estão em rem por esse motivo.
      </p>
    </template>
  </SecaoGuia>
</template>
