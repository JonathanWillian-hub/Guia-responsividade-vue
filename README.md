# 📐 Largura Livre — Guia interativo de responsividade

![Vue 3](https://img.shields.io/badge/Vue-3-42b883?logo=vuedotjs&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-6-646cff?logo=vite&logoColor=white)
![Pinia](https://img.shields.io/badge/Pinia-3-ffd859)
![Netlify](https://img.shields.io/badge/deploy-Netlify-00c7b7?logo=netlify&logoColor=white)

Guia didático feito em **Vue 3** que explica, na prática, como construir sites responsivos.
Cada seção traz uma explicação curta, um exemplo de código comentado, uma pergunta-guia respondida
e as fontes consultadas. Algumas seções têm laboratórios interativos para testar os conceitos na hora.

### 🔗 [Acessar a aplicação](https://guiaresponsividade.netlify.app/#/)

> Dica: abra o site e redimensione a janela. O número gigante na página inicial mostra a largura atual em pixels,
> e o indicador no canto inferior direito mostra em qual breakpoint (celular, tablet ou desktop) você está.

---

## 📑 Sumário

- [Sobre o projeto](#-sobre-o-projeto)
- [Seções do guia](#-seções-do-guia)
- [Funcionalidades](#-funcionalidades)
- [Tecnologias](#-tecnologias)
- [Boas práticas aplicadas](#-boas-práticas-aplicadas)
- [Estrutura de pastas](#-estrutura-de-pastas)
- [Como rodar localmente](#-como-rodar-localmente)
- [Deploy](#-deploy)
- [Referências](#-referências)
- [Autores](#-autores)

---

## 💡 Sobre o projeto

O objetivo do **Largura Livre** é ensinar responsividade para quem está começando em desenvolvimento web,
usando o próprio site como exemplo: ele foi construído com as mesmas técnicas que explica
(mobile-first, unidades relativas, Flexbox, Grid e imagens responsivas).

A identidade visual lembra um **caderno quadriculado com desenho técnico**: a "linha de cota" vermelha
mede a largura da janela, e o amarelo funciona como marca-texto nos pontos importantes.

---

## 📚 Seções do guia

| # | Seção | Rota | Pergunta-guia (resumo) |
|---|-------|------|------------------------|
| 01 | Viewport | `/#/viewport` | Por que um site sem a meta viewport aparece minúsculo no celular? |
| 02 | Unidades CSS | `/#/unidades` | Por que texto em `rem` aumenta com a configuração do navegador e em `px` não? |
| 03 | Flexbox e Grid | `/#/flex-grid` | A partir de qual largura o grid passa de 1 para 2 colunas? *(com laboratório)* |
| 04 | Imagens responsivas | `/#/imagens` | Por que a imagem sem `width`/`height` empurra o texto? Qual métrica mede isso? |
| 05 | Boas práticas em Vue | `/#/boas-praticas` | O que acontece com um `v-for` sem `:key` quando um item é removido? |
| 06 | Desafio | `/#/desafio` | Pergunta final que só se responde usando o guia. |

Todas as seções (01 a 05) seguem o mesmo molde, definido no componente `SecaoGuia.vue`:

1. **Em poucas palavras** — explicação curta, para alguém do 1º semestre entender
2. **Exemplo** — código comentado
3. **Laboratório** *(opcional)* — experimento interativo
4. **Pergunta-guia** — situação real e sua resposta
5. **Fontes consultadas** — links das referências

---

## ✨ Funcionalidades

- **Medidor de largura ao vivo** na página inicial (linha de cota que acompanha o tamanho da janela)
- **Indicador de breakpoint** fixo no canto da tela (`celular`, `tablet` ou `desktop`)
- **Laboratório de Grid**: um controle deslizante muda a largura do contêiner e mostra quantas colunas
  o navegador criou com `repeat(auto-fit, minmax(14rem, 1fr))`
- **Marcação de seções visitadas** na página inicial (estado global com Pinia)
- **Desafio** com conferência automática da resposta
- **Menu responsivo**: botão "Abrir menu" no celular e menu horizontal a partir do tablet

---

## 🛠 Tecnologias

| Tecnologia | Uso no projeto |
|------------|----------------|
| [Vue 3](https://vuejs.org/) | Framework principal (Composition API com `<script setup>`) |
| [Vite](https://vite.dev/) | Servidor de desenvolvimento e build |
| [Vue Router](https://router.vuejs.org/) | Navegação entre as seções (modo hash) |
| [Pinia](https://pinia.vuejs.org/) | Estado global: lista de seções e seções visitadas |
| [Fontsource](https://fontsource.org/) | Fontes self-hosted: Bricolage Grotesque, Atkinson Hyperlegible e IBM Plex Mono |
| CSS puro | Sem frameworks de CSS: tokens com variáveis CSS e estilos `scoped` |
| [Netlify](https://www.netlify.com/) | Hospedagem da versão publicada |

---

## ✅ Boas práticas aplicadas

**Responsividade**
- **Mobile-first**: o CSS base é para celular e as media queries só *adicionam* regras para telas maiores
- Breakpoints em `em`: **48em (768px)** para tablet e **64em (1024px)** para desktop
- Meta tag `viewport` configurada no `index.html`
- `minmax(0, 1fr)` e `overflow-x: auto` nos blocos de código para nunca gerar rolagem horizontal na página

**Acessibilidade**
- Espaçamentos e fontes em `rem`, respeitando o tamanho de fonte escolhido pela pessoa
- Fonte **Atkinson Hyperlegible**, criada para pessoas com baixa visão
- Foco visível no teclado (`:focus-visible`) e atributos `aria-*` no menu
- Animações desligadas para quem ativou `prefers-reduced-motion`

**Organização e desempenho em Vue**
- Componentes reutilizáveis (`SecaoGuia`, `CodigoExemplo`, `CotaLarga`...)
- Lógica compartilhada em *composable* (`useViewport.js`)
- Rotas com `import()` dinâmico: cada página só é baixada quando alguém entra nela
- Cores, espaços e fontes centralizados em `tokens.css`

---

## 📁 Estrutura de pastas

```
guia-responsivo/
├── index.html                  # HTML base (com a meta viewport)
├── package.json
├── vite.config.js
└── src/
    ├── main.js                 # Cria o app e registra Pinia, Router e fontes
    ├── App.vue                 # Cabeçalho, menu e área das páginas
    ├── assets/
    │   ├── tokens.css          # Design tokens: cores, espaços, fontes, sombras
    │   └── base.css            # Estilos globais (tipografia, fundo quadriculado)
    ├── components/
    │   ├── SecaoGuia.vue       # Molde das seções (explicação, exemplo, pergunta, fontes)
    │   ├── CodigoExemplo.vue   # Bloco de código
    │   ├── CotaLarga.vue       # Medidor de largura da página inicial
    │   ├── BreakpointIndicator.vue
    │   └── labs/
    │       └── LabLargura.vue  # Laboratório interativo de Grid
    ├── composables/
    │   └── useViewport.js      # Largura da janela e breakpoint atual
    ├── router/
    │   └── index.js            # Rotas com carregamento sob demanda
    ├── stores/
    │   └── guia.js             # Store Pinia: seções e seções visitadas
    └── views/                  # Uma tela por seção
        ├── InicioView.vue
        ├── ViewportView.vue
        ├── UnidadesView.vue
        ├── FlexGridView.vue
        ├── ImagensView.vue
        ├── BoasPraticasView.vue
        └── DesafioView.vue
```

---

## 🚀 Como rodar localmente

**Pré-requisitos:** [Node.js](https://nodejs.org/) 18 ou superior e npm.

```bash
# 1. Clonar o repositório
git clone https://github.com/JonathanWillian-hub/Guia-responsividade-vue.git
cd Guia-responsividade-vue

# 2. Instalar as dependências
npm install

# 3. Rodar em modo de desenvolvimento
npm run dev
```

O site abre em **http://localhost:5173**.

| Comando | O que faz |
|---------|-----------|
| `npm run dev` | Inicia o servidor de desenvolvimento |
| `npm run build` | Gera a versão otimizada na pasta `dist/` |
| `npm run preview` | Abre localmente a versão gerada pelo build |

---

## 🌐 Deploy

A aplicação está publicada no **Netlify**: https://guiaresponsividade.netlify.app/#/

Configuração usada:

| Campo | Valor |
|-------|-------|
| Build command | `npm run build` |
| Publish directory | `dist` |

> O router usa o **modo hash** (`/#/rota`). Assim, ao atualizar a página em qualquer seção,
> o servidor sempre entrega o `index.html` e não aparece erro 404.

---

## 📖 Referências

- [MDN Web Docs](https://developer.mozilla.org/pt-BR/) — meta viewport, media queries, unidades CSS, Flexbox, Grid e imagens responsivas
- [web.dev](https://web.dev/) — fundamentos de design responsivo e Cumulative Layout Shift (CLS)
- [W3C — WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html) — critério 1.4.4, redimensionar texto
- [Documentação do Vue.js](https://vuejs.org/) e [Vue Router](https://router.vuejs.org/)

As fontes específicas de cada assunto estão listadas no fim de cada seção do site.

---

## 👥 Autores

Projeto desenvolvido em dupla para a disciplina de desenvolvimento web — **SENAI**.

| Nome | GitHub |
|------|--------|
| Jonathan Willian | [@JonathanWillian-hub](https://github.com/JonathanWillian-hub) |
| Gabriel Pinto| [@JonathanWillian-hub](https://github.com/JonathanWillian-hub) |
