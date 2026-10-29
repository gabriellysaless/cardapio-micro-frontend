# 🍽️ Prática Cardápio — Micro Frontends

Projeto desenvolvido como exercício prático de **Micro Frontends**, com o objetivo de estudar a integração de aplicações independentes utilizando **Next.js** e **Module Federation**.

A aplicação simula um sistema de pedidos de restaurante, no qual o usuário pode visualizar um cardápio e adicionar produtos a uma lista de pedidos.

## 🚀 Tecnologias utilizadas

- **Next.js 14** — framework React para desenvolvimento das aplicações.
- **React 18** — construção de interfaces componentizadas.
- **TypeScript** — tipagem estática.
- **Module Federation** — integração dos micro frontends.
- **Webpack 5** — configuração e suporte à federação de módulos.
- **CSS Modules** — estilização isolada dos componentes.

## 🏗️ Arquitetura do projeto

O projeto é dividido em três aplicações independentes:

| Aplicação | Porta | Responsabilidade |
|---|---:|---|
| `container` | 3000 | Integra e exibe os micro frontends. |
| `micro-cardapio` | 3001 | Exibe os pratos disponíveis e permite adicioná-los ao pedido. |
| `micro-pedido` | 3002 | Recebe os produtos adicionados e exibe a lista do pedido. |

### Estrutura de pastas

```text
pratica-cardapio/
├── container/
│   ├── src/
│   │   ├── pages/
│   │   ├── styles/
│   │   └── remotes.d.ts
│   └── next.config.mjs
├── micro-cardapio/
│   ├── src/
│   │   ├── components/
│   │   └── styles/
│   └── next.config.mjs
└── micro-pedido/
    ├── src/
    │   ├── components/
    │   └── styles/
    └── next.config.mjs
```

## ⚙️ Como funciona

O `container` utiliza o Module Federation para carregar os componentes expostos pelas aplicações remotas `micro-cardapio` e `micro-pedido`.

A comunicação entre o catálogo e o pedido é feita por meio de eventos personalizados do navegador, utilizando `CustomEvent`.

O fluxo funciona da seguinte maneira:

1. O usuário seleciona um prato no cardápio.
2. O `micro-cardapio` dispara o evento `adicionarProduto`, enviando o produto no campo `detail`.
3. O `micro-pedido` escuta esse evento e recebe os dados enviados.
4. O estado do pedido é atualizado com `useState`.
5. A lista de produtos é renderizada novamente com o React.

Essa abordagem mantém as responsabilidades separadas: o catálogo envia os dados, o pedido os processa e o container integra as aplicações.

## 🎨 Interface

A interface utiliza um estilo simples e responsivo, com:

- Fundo em tons claros.
- Cartões com bordas arredondadas.
- Botões verdes para adicionar produtos.
- Organização em colunas em telas maiores.
- Layout adaptado para dispositivos menores.

A estilização é feita com CSS Modules, mantendo os estilos de cada aplicação separados.

## 💻 Como executar o projeto

### Pré-requisitos

- Node.js instalado.
- npm instalado.

### 1. Instale as dependências

Abra um terminal em cada uma das três pastas (`container`, `micro-cardapio` e `micro-pedido`) e execute:

```bash
npm install
```

### 2. Inicie as aplicações

Abra três terminais, um para cada aplicação.

**Terminal 1 — Cardápio**

```bash
cd micro-cardapio
npm run dev
```

**Terminal 2 — Pedido**

```bash
cd micro-pedido
npm run dev
```

**Terminal 3 — Container**

```bash
cd container
npm run dev
```

> Execute os comandos a partir da pasta raiz `pratica-cardapio`, ajustando o caminho caso seus terminais já estejam dentro de alguma das pastas.

### 3. Acesse a aplicação

Abra o navegador em:

[http://localhost:3000](http://localhost:3000)

As aplicações remotas precisam estar em execução nas portas configuradas para que o container consiga carregá-las.

## 📚 Conceitos praticados

- Arquitetura de Micro Frontends.
- Integração de aplicações com Module Federation.
- Exposição e consumo de módulos remotos.
- Comunicação entre aplicações por eventos personalizados.
- Utilização de `CustomEvent` e `event.detail`.
- Gerenciamento de estado com `useState`.
- Gerenciamento de eventos com `useEffect`.
- Organização de responsabilidades entre aplicações.
- Estilização com CSS Modules.

## 🎯 Objetivo de aprendizagem

Este projeto foi desenvolvido para consolidar conhecimentos sobre integração de aplicações front-end independentes, comunicação entre micro frontends e organização de uma aplicação baseada em responsabilidades separadas.

---

Desenvolvido como projeto de estudo durante a formação Full Stack da EBAC.