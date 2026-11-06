# 🏫 Ensalamento · Escola Santo Agostinho

[![Acessar Sistema Online](https://img.shields.io/badge/Acessar-Sistema_Web-2ea44f?logo=github&logoColor=white)](https://raimundoalvesstb.github.io/EnsalamentoSantoAgostinho/)
[![Versão](https://img.shields.io/badge/Vers%C3%A3o-2.1.0-blue.svg)]()
[![Base de Dados](https://img.shields.io/badge/Base_de_Dados-base.csv_Unificado-34A853?logo=csv&logoColor=white)]()
[![Tecnologias](https://img.shields.io/badge/Tecnologias-HTML5%20%7C%20CSS3%20%7C%20JavaScript-orange.svg)]()
[![Segurança](https://img.shields.io/badge/Seguran%C3%A7a-CSP%20Strict-blueviolet.svg)]()
[![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-yellow.svg)](./LICENSE)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Raimundo_Alves-%230077B5?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/raimundoalvesstb/)

> **Sistema digital simples, rápido e visual para consulta de salas, horários e professores da Escola Santo Agostinho.**  
> Criado para facilitar o dia a dia de professores, coordenadores, funcionários, alunos e famílias. Funciona direto no navegador do celular, computador, tablet ou TV da escola, sem precisar instalar nada, sem precisar de login e com dados unificados e independentes mantidos em arquivo local CSV.

---

## 🌐 Link de Acesso Rápido

Você pode usar o sistema agora mesmo pelo link público oficial:  
👉 **[https://raimundoalvesstb.github.io/EnsalamentoSantoAgostinho/](https://raimundoalvesstb.github.io/EnsalamentoSantoAgostinho/)**

---

## 🎥 Tutorial Passo a Passo em Vídeo

Assista ao tutorial completo e detalhado em vídeo (2m44s), com ritmo calmo, explicações na tela e rolagem minuciosa por todos os recursos do sistema:  
▶️ **[Baixar / Assistir Vídeo Tutorial (`demonstracao.mp4`)](./demonstracao.mp4)**

---

## 📖 Manual Prático: Como Usar o Sistema Passo a Passo

> [!NOTE]  
> **Não precisa ser especialista em informática!** O sistema foi desenhado para ser intuitivo: tudo o que você precisa está à distância de um ou dois cliques.

```
+-----------------------------------------------------------------------------------+
|  [Relógio em Tempo Real: 14:15]                    [A-] [A+] [Tela Cheia]         |
|  -------------------------------------------------------------------------------  |
|  [ 👨‍🏫 Professores ]         [ 🏫 Turmas ]                  [ ⏱️ Agora ]             |
|  -------------------------------------------------------------------------------  |
|  [ Seg ]  [ Ter ]  [ Qua* ]  [ Qui ]  [ Sex ]                                     |
|  -------------------------------------------------------------------------------  |
|  🔎 [ Digite o nome do professor ou turma...                                  ]  |
+-----------------------------------------------------------------------------------+
```

---

### 1. Entendendo a Tela Principal

Ao abrir a página, você verá de cima para baixo:

1. **Relógio Oficial da Escola (no topo):** Mostra a data, o dia da semana e a hora exata. Ele se atualiza sozinho a cada segundo.
2. **Botões de Acessibilidade (no canto superior direito):**
   * **`A-` e `A+`:** Se você achar as letras pequenas ou grandes demais, clique nestes botões para ajustar o tamanho do texto até ficar confortável para a sua visão. O sistema memoriza o tamanho escolhido no seu aparelho.
   * **Botão de Tela Cheia (⛶):** Amplia o sistema para a tela inteira, ideal para TVs ou monitores na sala dos professores ou na recepção.
3. **Faixa Dinâmica de Turno (Manhã / Tarde):**
   * **Identificação Autônoma:** O sistema reconhece automaticamente em que horário estamos. Até as 12:45 ele abre diretamente no **Turno da Manhã**; a partir das 12:45 ele comuta automaticamente para o **Turno da Tarde**.
   * **Troca Rápida de Turno:** Quer planejar ou consultar o outro turno? Basta clicar nos botões sutis **Manhã** ou **Tarde** dentro da faixa para alternar a qualquer momento.
   * **Sincronização em Tempo Real:** Um indicador no canto da faixa avisa quando os dados foram atualizados diretamente da planilha oficial.
4. **As 3 Abas Principais de Navegação:**
   * **👨‍🏫 Professores:** Para consultar a rotina de um(a) professor(a).
   * **🏫 Turmas:** Para ver as aulas de uma sala de aula específica.
   * **⏱️ Agora:** Para ver um resumo de todas as salas da escola neste exato minuto.
5. **Dias da Semana (Seg, Ter, Qua, Qui, Sex):**
   * O sistema seleciona **automaticamente o dia de hoje**.
   * Se quiser ver as aulas de amanhã ou de outro dia para planejar, basta dar um clique no dia desejado.

---

### 2. Como Encontrar a Aula de um(a) Professor(a)

Precisa localizar um professor ou saber em qual sala ele está dando aula? Siga um destes dois caminhos:

#### Opção A — Clicando no nome (Mais fácil):
1. Fique na aba **Professores**.
2. Você verá uma lista com botões com os nomes de todos os professores em ordem alfabética (ex: *Alana*, *Aline*, *Davi*, *Josy*, *Thiago*, etc.).
3. Basta dar **um clique no nome do professor**.
4. A tela mostrará imediatamente todos os horários e salas daquele professor no dia.

#### Opção B — Usando o campo de busca:
1. No campo onde diz **"Buscar professor, turma ou horário..."**, digite o nome de quem procura.
2. Não precisa se preocupar com acentos ou letras maiúsculas (digitar `davi` ou `Davi` dá o mesmo resultado).
3. Conforme você digita, o sistema já sugere as opções. Clique no resultado desejado.

---

### 3. Como Ler as Informações na Tela

Quando você seleciona um professor ou turma, aparecem **cartões coloridos** na tela. Cada cor tem um significado muito simples:

* 🟡 **Cartão Amarelo em Destaque com o selo "AGORA":**  
  Significa que a aula está **acontecendo neste exato momento**.  
  * Abaixo do cartão há um contador em tempo real: *"Termina em X minutos"* ou *"Faltam X minutos para o sinal"*.
* 🟢 **Cartão Verde com o selo "PRÓXIMA":**  
  É a **próxima aula** do professor naquele dia, com o horário certinho em que ela vai começar.
* ⚪ **Cartão Claro ou Cinza ("ENCERRADA"):**  
  Aulas que já aconteceram mais cedo e já foram finalizadas no dia.

#### 🗺️ O que significa o mapinha do andar que aparece no cartão?
Cada aula traz um desenho visual que mostra o corredor da escola:
1. **Selo do Piso à esquerda:** Indica com clareza em qual andar fica a sala (**PISO 1**, **PISO 2** ou **PISO 3**), acompanhado do ícone de escada.
2. **Quadradinhos das salas:** Representam todas as salas do corredor daquele andar.
3. **Sala em Destaque:** O quadradinho branco com borda bem visível e um marcador é **exatamente a sala onde a aula está acontecendo**. As outras salas do mesmo piso aparecem apagadinhas ao lado para você se orientar geograficamente no prédio.

---

### 4. Como Consultar as Aulas de uma Turma

Quer saber a programação de aulas de uma turma inteira?
1. Clique na aba **Turmas** no topo da tela.
2. O sistema agrupa automaticamente as turmas ativas de acordo com o turno e o andar:
   * **No Turno da Manhã (6 aulas · 07:30 às 12:45):**
     * **Piso 1:** 9º A e 9º B.
     * **Piso 2:** 2º A, 2º B, 2º C e 3º A.
     * **Piso 3:** Sala Interativa/Robótica, 3º B, 3º C, 1º A, 1º B e 1º C.
   * **No Turno da Tarde (5 aulas · 13:00 às 17:20):**
     * **Piso 1:** 8º A, 7º C e 7º A.
     * **Piso 2:** 7º D, 6º A, 6º B e 7º B.
     * **Piso 3:** Sala Interativa/Robótica, 9º C, 8º B e 8º C.
3. Clique sobre o botão da turma desejada (ex: **6º B** ou **1º A**).
4. O sistema exibirá todas as aulas do dia daquela turma em ordem:
   * O horário de cada aula.
   * A matéria que está sendo ensinada (ex: Matemática, Português, Física, Robótica).
   * O nome do(a) professor(a) responsável.
   * O mapinha do andar indicando a localização exata da sala.

---

### 5. Como Ver o que Está Acontecendo na Escola Inteira Agora (Aba "Agora")

Ideal para a coordenação, portaria, direção ou inspetoria que precisa saber rapidamente o panorama geral do colégio:
1. Dê um clique na aba **Agora**.
2. A tela mostrará todos os andares (Piso 1, Piso 2 e Piso 3) simultaneamente.
3. Em cada sala, você verá em tempo real:
   * Se a turma está **em aula** (mostrando a disciplina e o professor).
   * Se os alunos estão em **intervalo / recreio**.
   * Se o turno ainda não começou ou se as aulas do dia já foram encerradas.

---

### 6. Como Ver Horários Livres (Janelas de Professores)

Ao consultar um professor, logo abaixo do nome dele existe uma caixinha com o texto **"Mostrar janelas / horários livres"**:
* Se você marcar essa caixinha, o sistema exibirá também os horários em que o professor **não tem aula** naquele dia, facilitando agendar reuniões de pais, alinhamentos pedagógicos ou planejamentos de aula.

---

### 7. Como Imprimir a Grade de Horários

Se você quiser imprimir para colocar na pasta pedagógica ou colar no mural físico:
1. Abra a turma ou o professor que deseja imprimir.
2. Pressione as teclas **`Ctrl` + `P`** no teclado do computador (ou vá no menu do navegador e escolha **Imprimir**).
3. O sistema já possui um formato especial de impressão que remove automaticamente os botões, menus e fundos desnecessários, gerando uma folha A4 limpa e profissional.

---

## 🔒 Segurança, Privacidade e Confiabilidade

* **100% Gratuito e Livre de Propagandas:** Não há anúncios, pop-ups ou distrações.
* **Privacidade Total:** O sistema não solicita nem armazena nenhum dado pessoal, e-mail, telefone ou senha.
* **Funciona Offline:** Não depende de servidores complexos. Uma vez aberta a página, ela continua funcionando perfeitamente mesmo se a conexão cair temporariamente.
* **Segurança Reforçada (CSP Estrita):** Código protegido contra injeção de scripts maliciosos ou conexões externas desconhecidas.

---

## 🛠️ Arquitetura do Projeto (Para Desenvolvedores)

O projeto é estruturado em **arquivo único (*single-file architecture*)**, eliminando etapas de compilação, instalação de pacotes pesados ou dependências externas:

```
EnsalamentoSantoAgostinho/
├── index.html          # Sistema completo (HTML5 estruturado, CSS3 responsivo e JS nativo)
├── base.csv            # Base de dados oficial única (Ensalamento, Professores e Cronogramas)
├── demonstracao.mp4    # Vídeo tutorial passo a passo (MP4 720p HD didático)
├── README.md           # Documentação detalhada e manual de instruções
├── LICENSE             # Licença de código aberto MIT
└── .gitignore          # Arquivos excluídos do controle de versão (ignora Base.xlsx)
```

### Principais Características Técnicas (v2.1.0)

* **Base de Dados Unificada em `base.csv`:** Todas as informações de ensalamento (Manhã e Tarde), professores, disciplinas e cronogramas de aula residem no arquivo local `base.csv` no próprio repositório. O sistema lê os dados diretamente via requisição local (`same-origin`), garantindo independência total de serviços externos (como Google Drive/Docs), sem problemas de CORS ou quedas de conexão.
* **Fácil Manutenção Humana:** O arquivo `base.csv` é organizado de forma altiva em 5 seções numeradas com cabeçalhos legíveis (`#`), permitindo que a coordenação edite horários ou professores facilmente pelo Excel ou qualquer editor de texto.
* **Detecção Autônoma de Turno:** O sistema calcula de forma autônoma o turno ativo (Manhã: 07:30 às 12:45 | Tarde: 13:00 às 17:20) com corte inteligente às 12:45, adaptando salas, pisos e horários sem necessidade de intervenção do usuário.
* **Estratégia de Cache *Stale-While-Revalidate*:** O sistema armazena a versão mais recente dos dados no `localStorage` do navegador para abertura instantânea a 0ms (mesmo offline) e sincroniza silenciosamente em segundo plano com o `base.csv`.
* **Tecnologias Nativas:** HTML5 semântico, CSS3 moderno (Variáveis CSS, CSS Grid, Flexbox, `@media print`) e JavaScript Vanilla puro (compatível com todos os navegadores modernos e legados).
* **SVG Puro Integrado:** Todos os ícones e os mini-mapas dos corredores de cada andar são desenhados diretamente em código vetorial SVG embutido, sem dependência de fontes externas pesadas ou requisições adicionais de imagens.

---

## 🚀 Como Hospedar no seu Próprio GitHub Pages

1. Faça um **Fork** ou clone este repositório:
   ```bash
   git clone https://github.com/raimundoalvesstb/EnsalamentoSantoAgostinho.git
   ```
2. No seu GitHub, vá em **Settings** > **Pages**.
3. Na opção **Branch**, selecione `main` e a pasta `/(root)`. Clique em **Save**.
4. Em poucos segundos o seu endereço público estará ativo!

---

## 📄 Licença Livre (Open Source)

Este projeto está registrado sob a **[Licença MIT](./LICENSE)**. Você pode utilizar, adaptar, compartilhar e implementar esta solução livremente em qualquer escola, colégio ou instituição de ensino.

---

## 👨‍💻 Autor e Contato

Desenvolvido por **Raimundo Alves Santa Brigida**  
* 🐙 **GitHub:** [raimundoalvesstb/EnsalamentoSantoAgostinho](https://github.com/raimundoalvesstb/EnsalamentoSantoAgostinho)  
* 💼 **LinkedIn:** [linkedin.com/in/raimundoalvesstb](https://www.linkedin.com/in/raimundoalvesstb/)  

---

<div align="center">
  <b>Escola Santo Agostinho</b><br>
  <i>"Cada sala, uma nova oportunidade de aprender e crescer!"</i><br>
  <b>Organização hoje, sucesso sempre! ⭐</b>
</div>
