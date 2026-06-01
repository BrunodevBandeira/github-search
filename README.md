# 🔍 GitHub Search

Uma aplicação web para buscar perfis e repositórios do GitHub, construída com **Vue 3** + **Vite**.

![Vue 3](https://img.shields.io/badge/Vue-3.x-42b883?style=flat-square&logo=vue.js&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5.x-646cff?style=flat-square&logo=vite&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES2022-f7df1e?style=flat-square&logo=javascript&logoColor=black)
![GitHub API](https://img.shields.io/badge/GitHub_API-REST-181717?style=flat-square&logo=github&logoColor=white)

---

## ✨ Funcionalidades

- 🔎 Busca de usuários pelo username do GitHub
- 👤 Exibe perfil completo: avatar, nome, bio, seguidores e seguindo
- 📦 Lista até 30 repositórios públicos ordenados por estrelas
- 🌐 Abre o repositório diretamente no GitHub ao clicar
- ⚡ Requisições paralelas com `Promise.all` para carregamento rápido
- 🎨 Design escuro com efeito glassmorphism e grid animado

---

## 🖼️ Preview

> Tela de busca

![Search Page](https://placehold.co/860x420/061E47/68A4F1?text=GitHub+Search+—+Search+Page&font=montserrat)

> Tela de resultados

![Results Page](https://placehold.co/860x420/061E47/68A4F1?text=GitHub+Search+—+Results+Page&font=montserrat)

---

## 🚀 Como rodar

### Pré-requisitos

- [Node.js](https://nodejs.org/) 18+
- npm 9+

### Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/github-search.git
cd github-search

# Instale as dependências
npm install

# Rode em modo de desenvolvimento
npm run dev
```

Acesse: **http://localhost:5173**

### Build para produção

```bash
npm run build
npm run preview
```

---

## 🗂️ Estrutura do projeto

```
github-search/
├── index.html                  # Entry point do Vite
├── vite.config.js
├── package.json
└── src/
    ├── main.js                 # Monta o app Vue
    ├── App.vue                 # Estado global + lógica de busca
    ├── assets/
    │   └── main.css            # Estilos globais (body, grid bg, glow)
    └── components/
        ├── SearchPage.vue      # Tela de busca
        └── ResultsPage.vue     # Tela de resultados e repositórios
```

---

## 🛠️ Tecnologias

| Tech | Uso |
|---|---|
| [Vue 3](https://vuejs.org/) | Framework reativo com Composition API (`<script setup>`) |
| [Vite](https://vitejs.dev/) | Bundler e dev server ultrarrápido |
| [GitHub REST API](https://docs.github.com/en/rest) | Dados de usuários e repositórios |
| Google Fonts | Syne (sans-serif) · DM Mono (monospace) |

---

## 🔌 API utilizada

```
GET https://api.github.com/users/{username}
GET https://api.github.com/users/{username}/repos?per_page=30&sort=stars
```

> A API pública do GitHub tem limite de **60 requisições/hora** por IP sem autenticação.

---

## 📄 Licença

MIT © [Bruno Bandeira](https://github.com/seu-usuario)
