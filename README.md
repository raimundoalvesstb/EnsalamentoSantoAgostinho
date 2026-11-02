# 🏫 Ensalamento · Escola Santo Agostinho

[![GitHub Pages](https://img.shields.io/badge/Deploy-GitHub%20Pages-blue?logo=github&logoColor=white)](https://raimundoalvesstb.github.io/EnsalamentoSantoAgostinho/)
[![Versão](https://img.shields.io/badge/Vers%C3%A3o-1.2.0-brightgreen.svg)]()
[![Tecnologias](https://img.shields.io/badge/Stack-HTML5%20%7C%20CSS3%20%7C%20JS%20Vanilla-orange.svg)]()
[![Segurança CSP](https://img.shields.io/badge/Seguran%C3%A7a-CSP%20Strict-blueviolet.svg)]()
[![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-yellow.svg)](./LICENSE)
[![Offline-First](https://img.shields.io/badge/Modo-100%25%20Offline--First-success.svg)]()

> Sistema web leve, intuitivo e responsivo para consulta ágil de salas, turmas e horários de aulas dos professores e alunos da **Escola Santo Agostinho**. Desenvolvido em arquivo único (*single-file*), sem dependências externas e pronto para hospedar no **GitHub Pages** ou executar diretamente em qualquer navegador.

---

## ✨ Principais Funcionalidades

### 1. 🔍 Consulta por Professor(a)
* **Lista Completa A-Z:** Chips clicáveis para seleção direta de qualquer professor(a).
* **Busca Global Inteligente:** Campo de pesquisa unificado com *autocomplete*, tolerante a acentos e maiúsculas/minúsculas. Pressione `/` no teclado para focar no campo de busca imediatamente.
* **Linha do Tempo da Aula:** Identificação visual automática da aula que está ocorrendo **AGORA**, da **PRÓXIMA** aula a seguir e das aulas já **ENCERRADAS**.
* **Contagem Regressiva em Tempo Real:** Exibe os minutos restantes para o início ou término de cada aula.
* **Visualização de Janelas:** Opção para exibir horários livres e intervalos entre aulas.

### 2. 👥 Consulta por Turma e Piso
* **Navegação Categorizada por Andares:**
  * **Piso 1:** Turmas 8º A, 7º C e 7º A.
  * **Piso 2:** Turmas 7º D, 6º A, 6º B e 7º B.
  * **Piso 3:** TV Interativa / Robótica, 9º C, 8º B e 8º C.
* Na consulta por turma, cada cartão identifica automaticamente o professor responsável por ministrar a aula no horário.

### 3. 🕒 Visão Panorâmica "Agora na Escola"
* Painel em tempo real da ocupação simultânea de todas as salas de aula divididas por andar.
* Indica com clareza se as turmas estão em aula, no intervalo ou com o expediente encerrado naquele momento.

### 4. 🗺️ Mini-Mapa SVG Dinâmico do Andar
* Cada box de aula inclui uma reprodução visual estilizada em **SVG puro** representando o corredor do piso:
  * **Badge do Andar:** Selo colorido com identificação do piso (`PISO 1`, `PISO 2` ou `PISO 3`) e ícone de escada/degraus.
  * **Salas do Corredor:** Disposição em sequência de todas as salas daquele piso.
  * **Destaque Visual da Sala:** A sala onde a aula ocorre recebe destaque nítido com fundo contrastante, borda ressaltada e marcador de localização, enquanto as salas vizinhas mantêm opacidade atenuada.
  * **Design Responsivo Adaptativo:** Largura total (100%) em smartphones e largura contida e harmoniosa em tablets, desktops e smart TVs.

### 5. ♿ Acessibilidade e Modos de Exibição
* **Controle de Escala de Fonte (A- / A+):** Ajuste fino do tamanho do texto (de 85% a 130%), persistido automaticamente no navegador via `localStorage`.
* **Modo Tela Cheia (Fullscreen):** Botão dedicado na barra superior, ideal para totens de autoatendimento, smart TVs e quiosques nos corredores.
* **Suporte a Redução de Movimento:** Respeita a preferência de acessibilidade do sistema (`prefers-reduced-motion`).
* **Modo de Impressão Limpo:** Folha de estilos `@media print` otimizada para impressão física da grade sem elementos de navegação ou botões.

### 6. 🧪 Simulador de Data e Hora Integrado
* Permite simular e testar o comportamento do ensalamento em qualquer dia da semana e horário.
* Acessível diretamente pelo parâmetro de URL `#simulador` ou `#diagnostico`.

---

## 🛠️ Arquitetura Técnica

```
EnsalamentoSantoAgostinho/
├── index.html       # Aplicação completa (HTML5 + CSS3 + JavaScript Vanilla)
├── README.md        # Documentação do projeto
├── LICENSE          # Licença de código aberto MIT
└── .gitignore       # Arquivos e pastas excluídos do versionamento
```

* **Single-File Architecture:** Todo o sistema reside no arquivo [`index.html`](./index.html). Não há necessidade de Node.js, Webpack, Vite ou bibliotecas de terceiros.
* **Zero Dependências:** Funciona 100% offline nativamente. Basta abrir o arquivo em qualquer navegador moderno (Chrome, Edge, Firefox, Safari).
* **Desempenho Extremo:** Carregamento instantâneo, renderização nativa de elementos DOM e zero requisições externas bloqueantes.

---

## 🔒 Segurança e Privacidade

O projeto foi construído seguindo diretrizes rigorosas de segurança na web:

1. **Content Security Policy (CSP) Estrita:**
   O cabeçalho meta CSP está configurado com a política de menor privilégio:
   ```html
   <meta http-equiv="Content-Security-Policy"
         content="default-src 'none'; script-src 'unsafe-inline'; style-src 'unsafe-inline'; img-src data:; connect-src 'none'; base-uri 'none'; form-action 'none'">
   ```
   * Bloqueia injeções de scripts externos maliciosos e impede conexões de rede não autorizadas.
2. **Zero Telemetria e Coleta de Dados:**
   * O sistema não possui rastreadores, analytics ou cookies.
   * As preferências de acessibilidade e aba ativa são mantidas exclusivamente no armazenamento local do usuário (`localStorage`).
3. **Prevenção contra XSS:**
   * Toda manipulação de interface utiliza métodos seguros do DOM (`textContent`, `createElementNS`, `setAttribute`), eliminando vulnerabilidades de injeção HTML.
4. **Política de Referrer Estrita:**
   * Definido como `no-referrer` para preservar a privacidade do usuário durante a navegação.

---

## 🚀 Como Executar e Hospedar

### Execução Local (Sem Servidor)
1. Clone este repositório:
   ```bash
   git clone https://github.com/raimundoalvesstb/EnsalamentoSantoAgostinho.git
   ```
2. Abra a pasta do projeto e dê um duplo clique no arquivo [`index.html`](./index.html).
3. O sistema funcionará imediatamente em seu navegador padrão.

### Hospedagem Gratuita no GitHub Pages
1. Acesse o repositório no GitHub: [raimundoalvesstb/EnsalamentoSantoAgostinho](https://github.com/raimundoalvesstb/EnsalamentoSantoAgostinho).
2. Clique na aba **Settings** (Configurações).
3. No menu lateral esquerdo, clique em **Pages**.
4. Na seção **Build and deployment** > **Branch**:
   * Selecione a branch `main`.
   * Selecione a pasta `/ (root)`.
   * Clique em **Save**.
5. O sistema estará disponível publicamente em:
   **[https://raimundoalvesstb.github.io/EnsalamentoSantoAgostinho/](https://raimundoalvesstb.github.io/EnsalamentoSantoAgostinho/)**

---

## 🤝 Como Contribuir

Contribuições da comunidade escolar e de desenvolvedores são bem-vindas:

1. Faça um **Fork** do repositório.
2. Crie uma branch para sua modificação:
   ```bash
   git checkout -b feature/minha-melhoria
   ```
3. Realize suas alterações mantendo o código limpo e dentro do arquivo único.
4. Salve suas alterações (*commit*):
   ```bash
   git commit -m "feat: Adiciona melhoria no sistema de busca"
   ```
5. Envie para o seu repositório (*push*):
   ```bash
   git push origin feature/minha-melhoria
   ```
6. Abra um **Pull Request** explicando as alterações realizadas.

---

## 📄 Licença Livre (Open Source)

Este projeto está licenciado sob a **Licença MIT** — você tem liberdade total para usar, estudar, modificar, distribuir e adaptar este software para qualquer instituição educacional ou privada.

Consulte o arquivo [`LICENSE`](./LICENSE) para o texto completo da licença.

---

<div align="center">
  <b>Escola Santo Agostinho</b><br>
  <i>"Cada sala, uma nova oportunidade de aprender e crescer!"</i><br>
  <b>Organização hoje, sucesso sempre! ⭐</b>
</div>
