# 🚀 Sistema de Pedidos para Açaí - Vue.js + JSON Server 🍧

📌 **Projeto full front-end com integração a uma API REST simulada**

Desenvolvi um sistema completo de pedidos de açaí utilizando Vue.js no front-end, com integração a uma API REST mockada via JSON Server. O sistema permite aos usuários personalizarem seus pedidos de forma dinâmica e intuitiva, com gerenciamento de status para facilitar o controle no atendimento.

---

## 🧩 Funcionalidades implementadas:

### ✅ **Tela inicial com formulário de pedidos customizável, incluindo:**
- Nome do cliente
- Seleção de tamanho (P, M, G, etc.)
- Escolha da base (açaí tradicional, zero, cupuaçu...)
- Seleção múltipla de frutas e cremes com checkbox
- Campo de observações adicionais
- Feedback visual com componente de alerta (`Mensagem.vue`)

### ✅ **Envio de pedidos com POST para a API e exibição de mensagem de sucesso**

### ✅ **Listagem e gerenciamento dos pedidos recebidos, com:**
- Exibição de todos os pedidos registrados via GET
- Botões para atualizar o status (ex: de "Solicitado" para "Pronto" ou "Cancelado")
- Renderização dinâmica dos ingredientes e observações
- Filtro por status planejado

### ✅ **Componentização organizada:**
- `NavBar.vue`, `Footer.vue`, `Mensagem.vue`, `Hero.vue`, `Form.vue`, `Pedidos.vue`

### ✅ **Estilização completa com CSS puro, focando em uma interface amigável, limpa e responsiva:**
- Layout centralizado
- Botões com estados ativos
- Formulário bem espaçado e organizado por seções
- Estilo visual refinado com a fonte **Poppins** (Google Fonts)

### ✅ **Comunicação com API via Axios**
- CRUD básico simulando integração real
- Separação das rotas: `/ingredientes`, `/bases`, `/tamanhos`, `/pedidos`, `/status`

---

## 💻 Tecnologias utilizadas:
- **Vue.js 3** (Composition API com Options API)
- **Axios** para requisições HTTP
- **JSON Server** como back-end fake RESTful
- **HTML5 + CSS3**
- **Font Awesome** para ícones
- **Google Fonts** - Poppins
- Estrutura modularizada com boas práticas de componentização

---

## 📦 Sobre a API JSON Server:

A estrutura do banco de dados simulado inclui os seguintes endpoints:

- `/ingredientes`: Frutas e cremes
- `/bases`: Opções de base
- `/tamanhos`: Tamanhos disponíveis
- `/pedidos`: Registro e atualização de pedidos
- `/status`: Status possíveis de pedidos

---

## 📈 Próximos passos:
- Implementar autenticação com **Firebase** ou **Auth0**
- Adicionar sistema de usuários e login para controle de pedidos
- Criar dashboard com gráficos em tempo real (ex: pedidos por hora, sabores mais escolhidos)
- Adaptar o projeto para dispositivos móveis (**mobile first**)
