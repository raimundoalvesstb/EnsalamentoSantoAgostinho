# 🏫 Sistema de Ensalamento — Escola Santo Agostinho (Curitiba-PR)

> **Documento de planejamento e especificação — Fase 1: Período da Tarde**
> Versão do documento: 1.0 · Idioma: Português do Brasil · Entrega final: **um único arquivo HTML**

---

## Sumário

1. [Visão geral](#1-visão-geral)
2. [Escopo da Fase 1](#2-escopo-da-fase-1)
3. [Requisitos funcionais](#3-requisitos-funcionais)
4. [Requisitos não funcionais](#4-requisitos-não-funcionais)
5. [Regras de negócio](#5-regras-de-negócio)
6. [Identidade visual](#6-identidade-visual-baseada-na-imagem-ensalamento)
7. [Interface e experiência de uso](#7-interface-e-experiência-de-uso)
8. [Arquitetura do arquivo único](#8-arquitetura-do-arquivo-único)
9. [Convenção de nomes remissivos e catálogo de funções](#9-convenção-de-nomes-remissivos-e-catálogo-de-funções)
10. [Modelo de dados](#10-modelo-de-dados)
11. [Algoritmos principais](#11-algoritmos-principais)
12. [Segurança](#12-segurança)
13. [Compatibilidade e responsividade](#13-compatibilidade-e-responsividade)
14. [Plano de implantação (desenvolvimento)](#14-plano-de-implantação-desenvolvimento)
15. [Plano de testes](#15-plano-de-testes)
16. [Publicação e execução local](#16-publicação-e-execução-local)
17. [Manutenção e atualização dos dados](#17-manutenção-e-atualização-dos-dados)
18. [Pendências e pontos a confirmar](#18-pendências-e-pontos-a-confirmar)
19. [Critérios de aceite](#19-critérios-de-aceite)
20. [ANEXO A — Dados oficiais transcritos (tarde)](#anexo-a--dados-oficiais-transcritos-tarde)
21. [ANEXO B — Siglas e glossário](#anexo-b--siglas-e-glossário)
22. [ANEXO C — Esqueleto do arquivo HTML](#anexo-c--esqueleto-do-arquivo-html)

---

## 1. Visão geral

### 1.1 Problema
Professores, coordenação e equipe de apoio precisam saber, **a qualquer momento**, em qual sala/turma um professor deve estar e, inversamente, quais professores atendem uma turma ao longo do período. Hoje essa informação está em um quadro impresso (grade de horários) e em um cartaz de salas por piso.

### 1.2 Solução
Um aplicativo web **offline-first**, em **um único arquivo HTML**, que:

- lê **data e hora do próprio dispositivo**;
- identifica automaticamente o **dia da semana** e o **horário de aula** em vigor;
- permite **buscar por professor** (mostra as turmas, na ordem do horário) ou **buscar por turma** (mostra os professores, na ordem do horário);
- coloca **em destaque a aula atual ou a mais próxima** e **esmaece o que já passou**;
- mostra **onde fica a sala** (piso, térreo/andar, TV interativa) conforme o cartaz de ensalamento;
- segue a **identidade visual do cartaz "ENSALAMENTO – 3º TRIMESTRE"**.

### 1.3 Princípios de projeto

| Princípio | Significado prático |
|---|---|
| **Arquivo único** | HTML + CSS + JS + SVG + dados no mesmo arquivo. |
| **Zero dependências externas** | Nenhuma fonte, imagem, biblioteca, CDN, API ou requisição de rede. |
| **Exatidão dos dados** | Os dados são transcritos do quadro oficial e validados por rotina automática. |
| **Simplicidade de manutenção** | Dados separados da lógica, em um bloco claramente identificado, editável por quem não programa. |
| **Código em português** | Funções, variáveis, comentários e interface em PT-BR, com nomes remissivos (que "remetem" ao que fazem). |
| **Funciona em qualquer tela** | De celulares de 4" a quadros interativos 4K. |

---

## 2. Escopo da Fase 1

### 2.1 Dentro do escopo
- Período da **tarde** (aulas das 13:00 às 17:20), segunda a sexta.
- Turmas: **6ºA, 6ºB, 7ºA, 7ºB, 7ºC, 7ºD, 8ºA, 8ºB, 8ºC, 9ºC** e a turma de **Robótica (tarde)**.
- Busca por **professor** e por **turma**.
- Destaque da aula atual/próxima, esmaecimento das aulas passadas.
- Localização das salas (piso) conforme cartaz da tarde.
- Painel geral "Agora na escola" (visão de todas as turmas no momento).
- Simulador de data/hora (para testes e conferência).

### 2.2 Fora do escopo (fases futuras)
- Período da **manhã** (o cartaz já prevê: 3A, 2B, 9B, 2A, 9A, 3C, 3B, 1A, 1B, 1C/2C — dados de horários ainda não fornecidos).
- Cadastro/edição de horários dentro da própria tela (a edição é feita no bloco de dados do HTML).
- Notificações, login, banco de dados, sincronização, impressão avançada.

---

## 3. Requisitos funcionais

Prioridade: **M** = Must (obrigatório) · **S** = Should (deveria) · **C** = Could (desejável).

| ID | Requisito | Prioridade |
|---|---|---|
| RF-01 | Ler data/hora do dispositivo e atualizar a cada 1 segundo (relógio) e reavaliar a aula atual a cada 15 segundos. | M |
| RF-02 | Identificar o dia da semana e o horário de aula (1ª a 5ª aula) ou situação (antes das aulas, intervalo, fim do expediente, sem aula hoje). | M |
| RF-03 | Buscar por **professor**: lista todas as aulas do professor no dia, com turma, disciplina, horário e sala/piso. | M |
| RF-04 | Buscar por **turma**: lista todas as aulas da turma no dia, com professor, disciplina, horário e sala/piso. | M |
| RF-05 | Destacar **a aula em andamento** (ou, se não houver, a **próxima**); aulas futuras em ordem cronológica; aulas passadas **esmaecidas** ao final. | M |
| RF-06 | Busca com **autocompletar**, tolerante a acentos, maiúsculas/minúsculas e parte do nome. | M |
| RF-07 | Alternar o dia consultado (Seg–Sex) manualmente, com botão "Hoje" para voltar ao dia real. | M |
| RF-08 | Mostrar a **localização da sala** (Piso 1, 2 ou 3; "TV Interativa") com as cores do cartaz. | M |
| RF-09 | Indicar **aula dupla/geminada** (mesmo professor, mesma turma, horários consecutivos). | S |
| RF-10 | Indicar **janelas** (horários sem aula do professor) com opção de mostrar/ocultar. | S |
| RF-11 | Painel **"Agora na escola"**: todas as turmas e o professor/disciplina do momento, agrupado por piso. | S |
| RF-12 | **Simulador** de data/hora (painel oculto e parâmetro na URL) para testes e conferência. | S |
| RF-13 | Mostrar **contagem regressiva** para o início/fim da aula (ex.: "começa em 12 min"). | C |
| RF-14 | Lembrar a última busca no dispositivo (com tolerância à falta de armazenamento). | C |
| RF-15 | Botão **"Tela cheia"** para quadros interativos. | C |
| RF-16 | Versão de **impressão** da grade do professor/turma. | C |

---

## 4. Requisitos não funcionais

| ID | Requisito |
|---|---|
| RNF-01 | **Arquivo único**: nenhum `<link>`, `<script src>`, `<img src>` externo; imagens apenas como **SVG inline**. |
| RNF-02 | **Sem rede**: nenhuma chamada `fetch`, `XMLHttpRequest`, `WebSocket`, `import()` ou service worker. |
| RNF-03 | **Português do Brasil** em toda a interface, comentários e identificadores (sem acentos nos identificadores). |
| RNF-04 | **Nomes remissivos** em todas as funções, constantes e elementos (ver seção 9). |
| RNF-05 | **Desempenho**: carregamento < 1 s em celular básico; arquivo final < 150 KB. |
| RNF-06 | **Acessibilidade**: contraste mínimo WCAG AA, foco visível, uso por teclado, `aria-live` para mudança de aula, alvos de toque ≥ 44 px, respeita `prefers-reduced-motion`. |
| RNF-07 | **Responsivo** de 320 px (celular de 4") até 3840 px (quadro interativo 4K). |
| RNF-08 | **Compatibilidade ampla**: JS em padrão **ES2017 (sem módulos, sem encadeamento opcional `?.`)** para rodar também em Android antigo, iOS 12+ e Chromebooks. |
| RNF-09 | **Segurança**: política CSP restritiva via `<meta>`, sem `innerHTML` com dados, sem `eval`. |
| RNF-10 | **Robustez**: o sistema nunca deve exibir tela em branco; erros são tratados com mensagem amigável em PT-BR. |
| RNF-11 | **Execução local** via `file://` e **GitHub Pages** via `https://`, com o mesmo comportamento. |

---

## 5. Regras de negócio

### 5.1 Calendário e horários

**RN-01 — Dias letivos.** Segunda a sexta. Sábado e domingo = "Sem aula hoje".

**RN-02 — Grade de horários da tarde** (configurável em `CONFIGURACAO.horarios`):

| Aula | Início | Fim (padrão) | Observação |
|:-:|:-:|:-:|---|
| 1ª | 13:00 | 13:50 | |
| 2ª | 13:50 | 14:40 | |
| 3ª | 14:40 | 15:30 | |
| — | 15:30 | 15:40 | **Intervalo (recreio)** |
| 4ª | 15:40 | 16:30 | |
| 5ª | 16:30 | 17:20 | |

> O quadro impresso informa **apenas o horário de início** (13:00, 13:50, 14:40, 15:40, 16:30). O **fim** foi deduzido (aulas de 50 min; intervalo de 10 min entre 14:40 e 15:40). Ver [pendência P-01](#18-pendências-e-pontos-a-confirmar).

**RN-03 — Intervalo de tempo de cada aula** é **fechado no início e aberto no fim**: `início ≤ agora < fim`. Exemplo: às 13:50:00 já é a 2ª aula.

### 5.2 Situação do momento (máquina de estados)

**RN-04 — Estados do dia** (calculados para o dia consultado):

| Estado | Condição (dia = hoje) | Aula em destaque |
|---|---|---|
| `SEM_AULA_HOJE` | Fim de semana ou data em `CONFIGURACAO.diasSemAula` | Nenhuma; sugerir o próximo dia letivo |
| `ANTES_DAS_AULAS` | agora < 13:00 | **1ª aula** ("Começa às 13:00") |
| `EM_AULA` | início ≤ agora < fim de uma aula | **Aula em andamento** |
| `INTERVALO` | 15:30 ≤ agora < 15:40 | **4ª aula** (próxima) com aviso "Intervalo" |
| `FIM_DO_PERIODO` | agora ≥ 17:20 | Nenhuma; tudo esmaecido; sugerir o próximo dia letivo |
| `CONSULTA_OUTRO_DIA` | O usuário escolheu um dia diferente de hoje | Nenhuma em destaque "ao vivo"; lista integral em ordem cronológica, sem esmaecimento (rótulo "Consulta de [dia]") |

**RN-05 — Classificação de cada aula** (no dia atual) em relação ao momento:

| Classe | Regra | Aparência |
|---|---|---|
| `EM_ANDAMENTO` | início ≤ agora < fim | Destaque máximo (cor viva, borda dourada, selo "AGORA") |
| `PROXIMA` | A primeira aula **com aula** do usuário-alvo que começa após agora (e nenhuma em andamento ou, no caso do intervalo/antes, a próxima) | Destaque (selo "PRÓXIMA") |
| `FUTURA` | início > agora e não é a `PROXIMA` | Normal |
| `PASSADA` | fim ≤ agora | **Esmaecida** (opacidade reduzida, sem sombra, texto cinza) |

> **Atenção:** quando há uma aula `EM_ANDAMENTO`, a `PROXIMA` recebe um destaque secundário (selo "A SEGUIR"), mas não o principal.

### 5.3 Busca e exibição

**RN-06 — Normalização de texto para busca.** Converter para minúsculas, remover acentos (`NFD` + remoção de marcas combinantes), remover espaços extras e pontuação. Comparação sempre sobre o texto normalizado. Se `String.prototype.normalize` não existir, usar tabela de substituição manual de acentos.

**RN-07 — Busca por professor.**
1. Compara o texto digitado com o **nome normalizado** de cada professor (contém).
2. Se houver **correspondência exata** (ex.: "Eliane"), ela é priorizada; os demais resultados parciais (ex.: "Eliane Pereira") aparecem como sugestões logo abaixo.
3. Se houver **mais de um** resultado, mostrar **lista de sugestões** (botões/chips) para o usuário escolher; nunca assumir.
4. Os professores **Eliane**, **Eliana** e **Eliane Pereira** são **pessoas diferentes** e jamais devem ser mesclados.

**RN-08 — Busca por turma.** Aceitar formatos como `7A`, `7 A`, `7º A`, `7ºA`, `7_A`, `7a`, `sétimo A`(opcional). Normalizar para o código canônico (`7A`). Robótica: aceitar `robotica`, `robótica`.

**RN-09 — Resultado por professor** (lista cronológica do dia):
`Horário · Turma · Disciplina · Sala (Piso) · Situação`.

**RN-10 — Resultado por turma** (lista cronológica do dia):
`Horário · Professor · Disciplina · Situação` + cabeçalho com a sala da turma (Piso).

**RN-11 — Ordenação** (para o dia de hoje):
1. Em destaque: aula `EM_ANDAMENTO`; se não houver, a `PROXIMA`.
2. Em seguida: demais aulas `FUTURA` em ordem **crescente de horário**.
3. Por último: aulas `PASSADA`, **esmaecidas**, em ordem **decrescente** (a mais recente primeiro) — ou cronológica, conforme `CONFIGURACAO.ordemPassadas`.

Para **outros dias** (consulta), ordem cronológica simples sem esmaecimento.

**RN-12 — Aula dupla (geminada).** Duas aulas consecutivas do mesmo professor na mesma turma são exibidas **mantendo os dois blocos**, com selo "Aula dupla (1/2)" e "(2/2)". A contagem regressiva usa o fim da aula individual.

**RN-13 — Janelas.** Horários em que o professor **não tem aula** são tratados como "Sem aula neste horário". Ficam **ocultos por padrão** e visíveis com a opção "Mostrar janelas". Se visíveis, seguem a mesma regra de esmaecimento.

**RN-14 — Professor sem aulas no dia.** Mensagem: "Este professor não tem aulas à tarde neste dia." (mostrar também os dias em que ele tem aula).

**RN-15 — Turma sem aula em algum horário** (ex.: Robótica só tem 1ª e 2ª aula na segunda): exibir apenas os horários com aula; demais, "—" quando o usuário ativar janelas.

### 5.4 Sala / localização

**RN-16 — Mapa de salas da tarde** (cartaz "Ensalamento 3º Trimestre"):

| Piso | Salas / Turmas (tarde) |
|---|---|
| **Piso 1** | **8A · 7C · 7A** |
| **Piso 2** | **7D · 6A · 6B · 7B** |
| **Piso 3 (TV Interativa)** | **9C · 8B · 8C** |
| Robótica | **Local a confirmar** (não consta no cartaz) |

**RN-17 — A sala pertence à turma**, não ao professor. Ao exibir a aula de um professor, a sala é a da turma daquela aula.

**RN-18 — Rótulos da sala** nos cartões: `Piso 1`, `Piso 2`, `Piso 3 · TV Interativa`, com as cores do piso (azul, verde, roxo — ver seção 6).

### 5.5 Disciplinas e códigos especiais

**RN-19 — Disciplinas** são exibidas pelo **nome por extenso** (tabela do Anexo B). A sigla original é mantida em `title`/atributo para conferência.

**RN-20 — Código "704".** Aparece na grade como disciplina com os professores Melissa e Simone. **Deve ser exibido exatamente como "704"** até que a escola informe o nome oficial ([pendência P-02](#18-pendências-e-pontos-a-confirmar)).

**RN-21 — Código "RPP"** (Robótica, Raphael) idem: exibir "RPP" até confirmação ([pendência P-03](#18-pendências-e-pontos-a-confirmar)).

### 5.6 Integridade dos dados

**RN-22 — Validação automática no carregamento** (`validarIntegridadeDosDados`):
- toda turma tem exatamente 5 horários por dia (permitido vazio);
- nenhum professor aparece em **duas turmas no mesmo dia/horário** (conflito);
- toda turma citada existe no mapa de salas (exceto Robótica);
- toda disciplina tem nome por extenso;
- nomes de professores sem espaços duplos.

Falhas **não** impedem o uso: são listadas no painel "Diagnóstico" (oculto; abre com `#diagnostico`) e no console.

**RN-23 — Fonte da verdade.** O bloco `DADOS_DA_GRADE` é a única fonte de horários. Nenhuma outra parte do código repete esses dados.

### 5.7 Relógio e fuso

**RN-24 — Hora do dispositivo.** Usar `new Date()` local. Não converter fuso (Curitiba usa o horário oficial de Brasília, UTC−3, sem horário de verão atualmente). Se o relógio do aparelho estiver errado, o simulador permite conferir o comportamento.

**RN-25 — Mudança de dia.** Se o aplicativo ficar aberto de um dia para o outro, ao detectar mudança de data, reinicia o dia consultado para "hoje".

**RN-26 — Aba em segundo plano.** Ao voltar ao primeiro plano (`visibilitychange`), recalcular imediatamente.

---

## 6. Identidade visual (baseada na imagem "ENSALAMENTO")

### 6.1 Elementos observados no cartaz

- Título **"ENSALAMENTO"** em letras grandes, azul-marinho com contorno, sobre faixa colorida.
- Faixa azul "**3º TRIMESTRE**" (texto branco) e frase "*Cada sala, uma nova oportunidade de aprender e crescer!*".
- Ilustrações: **maçã e livros**, **avião de papel**, **sol sorridente**, **mochila**, **lápis e caderno**, estrelinhas.
- Faixa azul-marinho "**MANHÃ**" com selo "**BOM DIA!**" e faixa **laranja** "**TARDE**".
- Marcadores de **piso** com degraus: **Piso 1 (azul)**, **Piso 2 (verde)**, **Piso 3 (roxo, com ícone de TV interativa)**.
- **Cartões brancos** de bordas arredondadas com borda azul, texto azul-marinho em negrito.
- Rodapé: "*ORGANIZAÇÃO HOJE, SUCESSO SEMPRE!*".
- Fundo claro, estilo **escolar, alegre e arredondado**.

### 6.2 Paleta de cores (variáveis CSS — valores aproximados a calibrar com conta-gotas)

| Variável | Uso | Valor sugerido |
|---|---|---|
| `--cor-titulo` | Título/textos principais | `#1F3A8A` |
| `--cor-azul-faixa` | Faixa "3º trimestre", bordas dos cartões | `#2563C9` |
| `--cor-azul-claro` | Fundos suaves | `#E6F0FF` |
| `--cor-amarelo-sol` | Destaque, estrelas, selo "AGORA" | `#FFC81E` |
| `--cor-laranja-tarde` | Faixa "TARDE" | `#F58A1F` |
| `--cor-piso1` | Piso 1 | `#2F6FD6` |
| `--cor-piso2` | Piso 2 | `#3BA94A` |
| `--cor-piso3` | Piso 3 | `#7B3FB5` |
| `--cor-fundo` | Fundo da página | `#F7FAFF` |
| `--cor-cartao` | Cartões | `#FFFFFF` |
| `--cor-esmaecido` | Aulas passadas | texto `#8A94A6` · opacidade `.55` |
| `--cor-erro` | Mensagens de erro | `#C62828` |

### 6.3 Tipografia

Sem fontes externas. Pilha de fontes do sistema, arredondada e legível:

```css
font-family: "Trebuchet MS", "Segoe UI", "Nunito", system-ui, -apple-system,
             "Roboto", "Helvetica Neue", Arial, sans-serif;
```

- Títulos: peso **800/900**, `letter-spacing` leve, contorno via `text-shadow` ou `paint-order` do SVG.
- Tamanhos fluidos com `clamp()` (ex.: `font-size: clamp(0.9rem, 2.5vw, 1.6rem)`).

### 6.4 Biblioteca de SVGs inline (toda a arte vai no HTML)

Cada ilustração é um `<symbol>` em um `<svg style="display:none">` e usada com `<use href="#...">` (com fallback `xlink:href` para navegadores antigos).

| ID do símbolo | Descrição |
|---|---|
| `icone-maca` | Maçã vermelha |
| `icone-livros` | Pilha de livros |
| `icone-aviao-papel` | Avião de papel |
| `icone-sol` | Sol sorridente (manhã/tarde) |
| `icone-mochila` | Mochila |
| `icone-lapis` | Lápis em copo |
| `icone-caderno` | Caderno |
| `icone-estrela` | Estrelinha |
| `icone-degraus` | Degraus (marcador de piso) |
| `icone-tv` | TV interativa |
| `icone-relogio` | Relógio |
| `icone-busca` | Lupa |
| `icone-professor` | Pessoa/quadro |
| `icone-turma` | Carteiras/grupo |
| `icone-sala` | Porta/sala |
| `icone-seta` | Seta |
| `icone-tela-cheia` | Expandir |

### 6.5 Componentes de interface

- **Cabeçalho "ENSALAMENTO"** (SVG inline com texto vetorial e faixa).
- **Faixa "TARDE"** laranja com ícone de mochila/sol.
- **Cartão de aula** (arredondado, borda azul): horário, turma/professor, disciplina, selo de piso.
- **Selos**: `AGORA` (amarelo), `A SEGUIR`/`PRÓXIMA` (azul), `INTERVALO` (laranja), `ENCERRADA` (cinza).
- **Marcador de piso** com degraus: cor do piso + número.
- **Rodapé** com a frase do cartaz.

---

## 7. Interface e experiência de uso

### 7.1 Estrutura da tela (mobile primeiro)

```
┌──────────────────────────────────────────┐
│  ☀  ENSALAMENTO · 3º TRIMESTRE   [⛶]     │  ← cabeçalho (SVG)
│  Cada sala, uma nova oportunidade...      │
├──────────────────────────────────────────┤
│  🕒 14:52:07 · Segunda-feira · 02/11/2026 │  ← relógio / data
│  Situação: 3ª aula em andamento (até 15:30)│
├──────────────────────────────────────────┤
│  [ Professor ]  [ Turma ]  [ Agora ]      │  ← abas
│  ┌────────────────────────────────┐ 🔍   │
│  │ Digite o nome do professor...  │      │
│  └────────────────────────────────┘      │
│  Seg Ter Qua Qui Sex   [Hoje]            │  ← seletor de dia
├──────────────────────────────────────────┤
│  ▌ AGORA                                  │
│  ┌──────────────────────────────────┐    │
│  │ 14:40–15:30 · 3ª aula            │    │  ← destaque
│  │ 7º A · Geografia                 │    │
│  │ 🔵 Piso 1                         │    │
│  └──────────────────────────────────┘    │
│  A SEGUIR                                 │
│  ┌ 15:40–16:30 · 6º B · Hist. · Piso 2 ┐ │
│  ENCERRADAS (esmaecidas)                  │
│  ┌ 13:00–13:50 · 9º C · ... ───────────┐ │
├──────────────────────────────────────────┤
│  ORGANIZAÇÃO HOJE, SUCESSO SEMPRE! ⭐     │
└──────────────────────────────────────────┘
```

### 7.2 Abas

1. **Professor** — campo de busca com sugestões + lista de professores (A–Z) para toque rápido.
2. **Turma** — grade de botões das turmas **agrupados por Piso** (como no cartaz) + campo de busca.
3. **Agora** — painel geral: todas as turmas, quem está nelas agora, agrupado por Piso 1/2/3 (útil em quadros interativos e telões).

### 7.3 Estados da interface

| Situação | Mensagem exibida |
|---|---|
| Nada digitado | "Escolha um professor ou uma turma para começar." |
| Nenhum resultado | "Não encontramos esse nome. Confira a escrita ou escolha da lista." |
| Vários resultados | "Encontramos mais de um. Toque no correto:" + chips |
| Fim de semana | "Hoje não há aulas. Próximo dia letivo: segunda-feira." |
| Antes das 13:00 | "As aulas da tarde começam às 13:00." |
| Intervalo | "Intervalo (15:30–15:40). A próxima aula começa às 15:40." |
| Após 17:20 | "As aulas da tarde terminaram." |
| Erro inesperado | "Ops! Algo deu errado. Recarregue a página." (com detalhes só no console) |

### 7.4 Interações

- Teclado: `/` foca a busca; `Esc` limpa; setas navegam nas sugestões; `Enter` seleciona.
- Toque: alvos ≥ 44×44 px; sem dependência de *hover*.
- Quadro interativo: botão de **tela cheia** e **escala de fonte** (A− / A+) com 3 níveis, aplicada via variável CSS.

---

## 8. Arquitetura do arquivo único

### 8.1 Organização do HTML

```
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
  <meta http-equiv="Content-Security-Policy" content="...">   ← seção 12
  <meta name="referrer" content="no-referrer">
  <meta name="theme-color" content="#1F3A8A">
  <title>Ensalamento · Escola Santo Agostinho</title>
  <link rel="icon" href="data:image/svg+xml,...">             ← ícone embutido (data URI)
  <style> /* 1. variáveis · 2. base · 3. layout · 4. componentes · 5. estados · 6. responsivo · 7. impressão */ </style>
</head>
<body>
  <svg style="display:none">  <!-- biblioteca de símbolos SVG --> </svg>
  <header> ... </header>
  <main> ... </main>
  <footer> ... </footer>
  <noscript>Este sistema precisa de JavaScript ativado.</noscript>
  <script>
    /* BLOCO 1: CONFIGURACAO              */
    /* BLOCO 2: DADOS_DA_GRADE (dados)    */
    /* BLOCO 3: utilitários               */
    /* BLOCO 4: regras de negócio         */
    /* BLOCO 5: renderização              */
    /* BLOCO 6: eventos e inicialização   */
  </script>
</body>
</html>
```

### 8.2 Camadas lógicas (dentro do `<script>`)

| Camada | Responsabilidade | Depende de |
|---|---|---|
| **Dados** | Constantes de configuração, grade, salas, disciplinas | — |
| **Utilitários** | Normalizar texto, formatar hora, criar elementos DOM seguros | — |
| **Regras** | Calcular situação do momento, classificar aulas, buscar, ordenar | Dados, Utilitários |
| **Visão** | Montar telas com `createElement`/`textContent` | Regras |
| **Controle** | Eventos, relógio, estado da aplicação, simulador | Todas |

### 8.3 Estado da aplicação (objeto único)

```js
var estadoDoSistema = {
  abaAtiva: 'professor',          // 'professor' | 'turma' | 'agora'
  diaConsultado: null,            // 1..5 (null = hoje)
  termoDigitado: '',
  professorSelecionado: null,     // chave normalizada
  turmaSelecionada: null,         // código canônico
  mostrarJanelas: false,
  escalaDaFonte: 1,               // 1 | 1.15 | 1.3
  momentoSimulado: null           // Date ou null
};
```

### 8.4 Ciclo de atualização

```
iniciarSistema()
 ├─ validarIntegridadeDosDados()
 ├─ construirIndicesDeBusca()
 ├─ ligarEventosDaInterface()
 ├─ iniciarRelogioDoSistema()  ──► a cada 1 s: atualizarRelogioNaTela()
 │                              └► a cada 15 s (ou na virada de minuto): reavaliarSituacaoEAtualizarTela()
 └─ renderizarTelaAtual()
```

---

## 9. Convenção de nomes remissivos e catálogo de funções

### 9.1 Regras de nomenclatura

- **Idioma:** português; **sem acentos nem cedilha** nos identificadores (`obterAulaAtual`, não `obterAulaAtuál`).
- **Estilo:** `camelCase` para funções e variáveis; `MAIUSCULAS_COM_SUBLINHADO` para constantes; `kebab-case` para classes CSS e IDs.
- **Verbos de ação claros:** `obter…`, `buscar…`, `calcular…`, `classificar…`, `renderizar…`, `atualizar…`, `validar…`, `normalizar…`, `formatar…`, `alternar…`.
- **Remissivo = o nome diz o que faz e o que retorna.** Proibido: `f1`, `tmp`, `dados2`, `x`.
- **Uma função, uma responsabilidade.** Funções puras (sem efeito colateral) sempre que possível, para facilitar testes.
- **Prefixos por camada:** `renderizar*` (visão), `ligar*` (eventos), `validar*` (integridade).
- **Classes CSS:** `.cartao-aula`, `.cartao-aula--agora`, `.cartao-aula--proxima`, `.cartao-aula--passada`, `.selo-piso--1`, `.faixa-tarde`, etc.
- **IDs de elementos:** `campo-de-busca`, `lista-de-resultados`, `relogio-do-sistema`, `situacao-do-momento`.

### 9.2 Catálogo de funções

| Função | Camada | Descrição | Retorno |
|---|---|---|---|
| `iniciarSistema()` | Controle | Orquestra a inicialização. | — |
| `obterMomentoAtual()` | Regras | Retorna `Date` do dispositivo ou o simulado. | `Date` |
| `obterDiaDaSemanaLetivo(data)` | Regras | 1=Seg … 5=Sex; `null` se fim de semana/sem aula. | `number\|null` |
| `converterHoraParaMinutos(hora)` | Util | `"13:50"` → `830`. | `number` |
| `formatarMinutosComoHora(min)` | Util | `830` → `"13:50"`. | `string` |
| `formatarDataPorExtenso(data)` | Util | "Segunda-feira, 2 de novembro de 2026". | `string` |
| `normalizarTextoParaBusca(texto)` | Util | Sem acento, minúsculo, sem espaços extras. | `string` |
| `normalizarCodigoDaTurma(texto)` | Util | `"7º a"` → `"7A"`. | `string\|null` |
| `calcularSituacaoDoMomento(momento)` | Regras | Estado do dia (RN-04) + aula atual/próxima. | `objeto` |
| `classificarAulaNoMomento(aula, momento)` | Regras | `EM_ANDAMENTO/PROXIMA/FUTURA/PASSADA` (RN-05). | `string` |
| `construirIndicesDeBusca()` | Regras | Cria índices por professor e por turma a partir de `DADOS_DA_GRADE`. | — |
| `listarProfessoresOrdenados()` | Regras | Professores únicos A–Z. | `array` |
| `buscarProfessoresPorTexto(texto)` | Regras | Sugestões de professores (RN-07). | `array` |
| `buscarTurmasPorTexto(texto)` | Regras | Sugestões de turmas (RN-08). | `array` |
| `obterAulasDoProfessor(chave, dia)` | Regras | Aulas do professor no dia. | `array` |
| `obterAulasDaTurma(codigo, dia)` | Regras | Aulas da turma no dia. | `array` |
| `obterSalaDaTurma(codigo)` | Regras | Piso, rótulo, TV (RN-16). | `objeto` |
| `marcarAulasDuplas(listaDeAulas)` | Regras | Identifica geminadas (RN-12). | `array` |
| `ordenarAulasParaExibicao(lista, situacao)` | Regras | RN-11. | `array` |
| `obterPanoramaAgoraNaEscola(momento)` | Regras | Painel geral (RF-11). | `objeto` |
| `calcularTempoRestanteParaAula(aula, momento)` | Regras | Minutos/segundos até início/fim. | `objeto` |
| `validarIntegridadeDosDados()` | Regras | RN-22. | `array de problemas` |
| `criarElementoSeguro(tag, atributos, texto)` | Util | Cria DOM sem `innerHTML`. | `Element` |
| `renderizarCabecalhoDoSistema()` | Visão | Título, relógio, situação. | — |
| `renderizarAbaDeProfessor()` | Visão | Tela da aba Professor. | — |
| `renderizarAbaDeTurma()` | Visão | Tela da aba Turma. | — |
| `renderizarAbaAgoraNaEscola()` | Visão | Painel geral. | — |
| `renderizarCartaoDeAula(aula, classe)` | Visão | Cartão individual. | `Element` |
| `renderizarMensagemDeEstadoVazio(tipo)` | Visão | Mensagens da seção 7.3. | — |
| `atualizarRelogioNaTela()` | Controle | Atualiza hora/data. | — |
| `reavaliarSituacaoEAtualizarTela()` | Controle | Recalcula e re-renderiza se mudou. | — |
| `ligarEventosDaInterface()` | Controle | Liga cliques, teclado, `visibilitychange`. | — |
| `alternarDiaConsultado(dia)` | Controle | Troca o dia (RF-07). | — |
| `alternarMostrarJanelas()` | Controle | RF-10. | — |
| `alternarTelaCheia()` | Controle | RF-15 com tratamento de falta de suporte. | — |
| `aplicarEscalaDaFonte(nivel)` | Controle | Ajusta `--escala-fonte`. | — |
| `lerPreferenciasSalvas()` / `salvarPreferencias()` | Controle | `localStorage` dentro de `try/catch` (RF-14). | — |
| `lerParametrosDaUrl()` | Controle | `#simular=…`, `#diagnostico`. | `objeto` |
| `abrirPainelDeSimulacao()` | Controle | RF-12. | — |
| `tratarErroInesperado(erro)` | Controle | Mensagem amigável (RNF-10). | — |

---

## 10. Modelo de dados

### 10.1 Entidades

```
CONFIGURACAO ─┬─ escola, trimestre, periodo, horarios[], diasSemAula[], ordemPassadas
SALAS        ─── turma → { piso, rotulo, tvInterativa }
DISCIPLINAS  ─── sigla → nome por extenso
PROFESSORES  ─── chave → nome de exibição
GRADE        ─── dia(1..5) → horário(0..4) → turma → "SIGLA|PROFESSOR"
```

### 10.2 Estruturas em JavaScript (modelo de referência)

```js
var CONFIGURACAO = {
  escola: 'Escola Santo Agostinho',
  cidade: 'Curitiba-PR',
  trimestre: '3º TRIMESTRE',
  periodo: 'TARDE',
  frase: 'Cada sala, uma nova oportunidade de aprender e crescer!',
  rodape: 'ORGANIZAÇÃO HOJE, SUCESSO SEMPRE!',
  ordemPassadas: 'recentePrimeiro',      // ou 'cronologica'
  diasSemAula: [],                       // ex.: ['2026-11-02', '2026-11-15'] (feriados/recessos, AAAA-MM-DD)
  horarios: [
    { numero: 1, inicio: '13:00', fim: '13:50' },
    { numero: 2, inicio: '13:50', fim: '14:40' },
    { numero: 3, inicio: '14:40', fim: '15:30' },
    // intervalo implícito: 15:30–15:40
    { numero: 4, inicio: '15:40', fim: '16:30' },
    { numero: 5, inicio: '16:30', fim: '17:20' }
  ],
  intervalo: { inicio: '15:30', fim: '15:40' }
};

var ORDEM_DAS_TURMAS = ['9C','6A','6B','7A','7B','7C','7D','8A','8B','8C','ROBOTICA'];

var SALAS_DAS_TURMAS = {
  '8A': { piso: 1, rotulo: 'Piso 1', tvInterativa: false },
  '7C': { piso: 1, rotulo: 'Piso 1', tvInterativa: false },
  '7A': { piso: 1, rotulo: 'Piso 1', tvInterativa: false },
  '7D': { piso: 2, rotulo: 'Piso 2', tvInterativa: false },
  '6A': { piso: 2, rotulo: 'Piso 2', tvInterativa: false },
  '6B': { piso: 2, rotulo: 'Piso 2', tvInterativa: false },
  '7B': { piso: 2, rotulo: 'Piso 2', tvInterativa: false },
  '9C': { piso: 3, rotulo: 'Piso 3 · TV Interativa', tvInterativa: true },
  '8B': { piso: 3, rotulo: 'Piso 3 · TV Interativa', tvInterativa: true },
  '8C': { piso: 3, rotulo: 'Piso 3 · TV Interativa', tvInterativa: true },
  'ROBOTICA': { piso: 0, rotulo: 'Sala de Robótica (a confirmar)', tvInterativa: false }
};
```

### 10.3 Formato de cada aula (após indexação)

```js
{
  dia: 1,                       // 1=Segunda … 5=Sexta
  numeroDaAula: 3,              // 1..5
  inicio: '14:40', fim: '15:30',
  turma: '7A',
  disciplinaSigla: 'GEO',
  disciplinaNome: 'Geografia',
  professorChave: 'eliane',
  professorNome: 'Eliane',
  sala: { piso: 1, rotulo: 'Piso 1' },
  aulaDupla: null | { parte: 1, total: 2 }
}
```

---

## 11. Algoritmos principais

### 11.1 Calcular a situação do momento

```text
função calcularSituacaoDoMomento(momento):
  diaLetivo ← obterDiaDaSemanaLetivo(momento)
  se diaLetivo = nulo: retornar { estado: 'SEM_AULA_HOJE', proximoDiaLetivo: ... }

  minutosAgora ← hora*60 + minuto   (segundos considerados para contagem regressiva)

  se minutosAgora < inicio(1ª aula):            estado ← 'ANTES_DAS_AULAS',  alvo ← 1ª aula
  senão se minutosAgora ≥ fim(5ª aula):         estado ← 'FIM_DO_PERIODO'
  senão se intervalo.inicio ≤ minutosAgora < intervalo.fim:
                                                estado ← 'INTERVALO',        alvo ← 4ª aula
  senão: achar aula n tal que inicio(n) ≤ agora < fim(n)
                                                estado ← 'EM_AULA',          atual ← n, seguinte ← n+1
  retornar { estado, diaLetivo, numeroAtual, numeroProximo, minutosAgora }
```

### 11.2 Classificar e ordenar a lista do usuário (professor ou turma)

```text
função ordenarAulasParaExibicao(lista, situacao):
  para cada aula em lista:
      aula.classe ← classificarAulaNoMomento(aula, situacao)

  emDestaque ← aulas com classe EM_ANDAMENTO (se vazio, a primeira com classe PROXIMA)
  futuras    ← aulas FUTURA ou PROXIMA restantes, ordem crescente de início
  passadas   ← aulas PASSADA (ordem conforme CONFIGURACAO.ordemPassadas)
  retornar emDestaque + futuras + passadas
```

**Nota:** a classe `PROXIMA` é calculada **por lista**: é a primeira aula **dessa lista** que começa depois de agora. Assim, se o professor não tem aula na 3ª, a "próxima" dele será a 4ª, mesmo que a 3ª esteja em andamento para outros.

### 11.3 Classificar uma aula

```text
função classificarAulaNoMomento(aula, minutosAgora):
  se minutosAgora ≥ aula.fimEmMinutos:        retornar 'PASSADA'
  se aula.inicioEmMinutos ≤ minutosAgora:     retornar 'EM_ANDAMENTO'
  retornar 'FUTURA'      // a primeira FUTURA da lista vira 'PROXIMA' na ordenação
```

### 11.4 Busca com normalização

```text
função normalizarTextoParaBusca(t):
  t ← minúsculas(t)
  se existe String.normalize: t ← t.normalize('NFD').replace(/[\u0300-\u036f]/g,'')
  senão: aplicar tabela manual de acentos
  t ← t.replace(/[^a-z0-9 ]/g,' ').replace(/\s+/g,' ').trim()
  retornar t
```

### 11.5 Normalizar turma

```text
entrada: "7º a", "7 A", "7a", "7_A", "7ºA"
passos : minúsculo → remover º ª ° _ - espaços → regex /^([6-9])([a-d])$/ → maiúsculo
saída  : "7A"
especial: "robotica" | "robótica" → "ROBOTICA"
```

---

## 12. Segurança

O requisito é **nenhuma chamada externa e nenhuma possibilidade de invasão**. Medidas:

### 12.1 Política de segurança de conteúdo (CSP) via `<meta>`

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none';
               script-src 'unsafe-inline';
               style-src 'unsafe-inline';
               img-src data:;
               font-src 'none';
               connect-src 'none';
               media-src 'none';
               object-src 'none';
               frame-src 'none';
               base-uri 'none';
               form-action 'none';">
```

> `'unsafe-inline'` é necessário porque script e estilo estão no próprio arquivo. Alternativa mais rígida (opcional): usar **hash SHA-256** do bloco de script/estilo — exige recalcular o hash a cada edição dos dados.

### 12.2 Boas práticas obrigatórias no código

| Medida | Como |
|---|---|
| Sem `innerHTML`/`outerHTML`/`document.write` com dados | Montar DOM com `createElement` + `textContent`. |
| Sem `eval`, `new Function`, `setTimeout("texto")` | Proibidos. |
| Sem rede | Nenhum `fetch`, `XMLHttpRequest`, `WebSocket`, `sendBeacon`, `import()`. |
| Sem recursos externos | Nenhum `<link>`, `<script src>`, `<img src="http…">`, `@import`, `url(http…)`. |
| Entrada do usuário | Campo de busca limitado a 40 caracteres; apenas usado em comparação de texto (nunca renderizado como HTML). |
| Parâmetros da URL | Só aceitar formato estrito (`#simular=AAAA-MM-DDTHH:MM`), validado por expressão regular; ignorar o resto. |
| Armazenamento local | Apenas preferências não sensíveis, em `try/catch`; sem dados pessoais. |
| Links | Nenhum link externo. Se houver, `rel="noopener noreferrer"`. |
| `referrer` | `<meta name="referrer" content="no-referrer">`. |
| Dados | Contêm apenas nome de professor, disciplina e turma (sem dados de alunos, CPFs, telefones). |

### 12.3 Limitações e cuidados no GitHub Pages
- O GitHub Pages **não permite configurar cabeçalhos HTTP** (por isso a CSP via `<meta>`). Não é possível aplicar `frame-ancestors` por `<meta>`; o risco de *clickjacking* é baixo (sem login/ação sensível).
- Proteger o **repositório**: ativar autenticação em dois fatores, exigir revisão de *pull request* na branch publicada e restringir quem pode editar.

---

## 13. Compatibilidade e responsividade

### 13.1 Alvos de dispositivo

| Categoria | Largura típica | Estratégia |
|---|---|---|
| Celular pequeno (4") | 320–360 px | 1 coluna; fonte mínima 14 px; cabeçalho compacto |
| Smartphone | 360–430 px | 1 coluna |
| Tablet retrato | 600–820 px | 2 colunas nos painéis |
| Tablet paisagem/notebook/Chromebook | 900–1366 px | Busca à esquerda, resultado à direita (layout em duas áreas) |
| Desktop | 1366–1920 px | Contêiner centralizado, máx. ~1200 px |
| Quadro interativo/TV | 1920–3840 px | Escala de fonte maior, painel "Agora" em grade de 3 colunas (Pisos 1, 2, 3) |

### 13.2 Técnicas CSS

- `meta viewport` com `viewport-fit=cover` e `env(safe-area-inset-*)` para iPhones com *notch*.
- **Mobile-first** com `@media (min-width: …)`: 480, 768, 1024, 1440, 1920 px.
- Unidades fluidas: `rem`, `%`, `clamp()`, `vw` (com limites), `min()`/`max()` com **fallback** declarado antes.
- **Altura:** usar `min-height: 100vh` seguido de `min-height: 100dvh` (fallback para navegadores sem `dvh`).
- Layout: **Flexbox** como base e **Grid** em melhoria progressiva (`@supports (display:grid)`), pois alguns Android antigos não suportam Grid completo.
- Não usar `gap` em Flexbox sem fallback (Safari antigo): usar margens.
- Evitar `:has()`, `@container`, `aspect-ratio` sem fallback, `inset`, `backdrop-filter`.
- `-webkit-text-size-adjust: 100%` e `touch-action: manipulation` (evita zoom por toque duplo).
- Sem *hover* como única forma de acesso a informação.
- `@media (prefers-reduced-motion: reduce)` desliga animações.
- `@media (orientation: landscape) and (max-height: 480px)` reduz cabeçalho (celular deitado).
- `@media print` mostra apenas a lista de resultados em preto e branco.

### 13.3 Técnicas JavaScript (compatibilidade)

- `var`/`function` ou `const`/`let` (ES2015 aceitável); **sem** `?.`, `??`, `import/export`, `async/await` obrigatório.
- Sem `Intl` obrigatório: nomes de dias/meses por **tabelas próprias** (garante PT-BR mesmo se o aparelho estiver em outro idioma).
- `Array.prototype.includes`/`find` com *polyfill* mínimo opcional.
- `requestAnimationFrame`/`setInterval` com `try/catch` no *loop*.
- `localStorage` sempre em `try/catch` (modo anônimo do iOS e `file://` em alguns navegadores pode bloquear).
- `Fullscreen API` com prefixos (`webkit`) e *fallback* silencioso (iPhone não suporta tela cheia de página).

### 13.4 Matriz de testes de ambiente

| Sistema | Navegadores |
|---|---|
| Android 7+ | Chrome, Samsung Internet, Firefox |
| iOS/iPadOS 12+ | Safari, Chrome (WebKit) |
| Windows 10/11 | Chrome, Edge, Firefox |
| ChromeOS | Chrome |
| Linux | Chrome/Chromium, Firefox |
| macOS | Safari, Chrome |
| Quadros interativos | Chrome/Edge embarcado (Android ou Windows) |

---

## 14. Plano de implantação (desenvolvimento)

Desenvolvimento em **7 etapas curtas**, cada uma com entrega verificável.

### Etapa 0 — Preparação (0,5 dia)
- [ ] Criar repositório no GitHub (ex.: `ensalamento-santo-agostinho`).
- [ ] Conferir o **Anexo A** com a grade impressa original (dupla conferência).
- [ ] Fechar as **pendências P-01 a P-10** (seção 18).
- [ ] Definir nome do arquivo principal (`index.html`).

### Etapa 1 — Esqueleto e identidade visual (1 dia)
- [ ] Estrutura HTML, CSP, `meta`s, ícone em *data URI*.
- [ ] Variáveis CSS (paleta), tipografia, base responsiva.
- [ ] Biblioteca de símbolos SVG e cabeçalho "ENSALAMENTO".
- [ ] Faixa "TARDE", marcadores de piso, cartões.
- **Entrega:** tela estática fiel ao cartaz.

### Etapa 2 — Dados e validação (0,5 dia)
- [ ] Inserir `CONFIGURACAO`, `SALAS_DAS_TURMAS`, `DISCIPLINAS`, `DADOS_DA_GRADE` (Anexo A).
- [ ] Implementar `construirIndicesDeBusca()` e `validarIntegridadeDosDados()`.
- **Entrega:** diagnóstico sem erros (ou com avisos conhecidos).

### Etapa 3 — Motor de tempo e regras (1 dia)
- [ ] `obterMomentoAtual`, `calcularSituacaoDoMomento`, `classificarAulaNoMomento`.
- [ ] Relógio e reavaliação periódica; tratamento de virada de dia e aba em segundo plano.
- [ ] Simulador de data/hora.
- **Entrega:** testes das RN-01 a RN-05 passando no simulador.

### Etapa 4 — Busca e telas (1,5 dia)
- [ ] Busca de professor com autocompletar e desambiguação (RN-07).
- [ ] Busca de turma (RN-08) e grade de turmas por piso.
- [ ] Renderização de cartões, ordenação, destaque e esmaecimento (RN-09 a RN-15).
- [ ] Painel "Agora na escola".
- **Entrega:** fluxo completo funcional.

### Etapa 5 — Responsividade, acessibilidade e polimento (1 dia)
- [ ] Testar de 320 px a 4K; ajustar *breakpoints*.
- [ ] Teclado, foco, `aria-live`, contraste.
- [ ] Tela cheia, escala de fonte, impressão.
- **Entrega:** checklist da seção 13 aprovado.

### Etapa 6 — Testes e homologação (1 dia)
- [ ] Executar o plano de testes (seção 15) em dispositivos reais.
- [ ] Homologação com 2–3 professores e a coordenação.
- [ ] Correções.

### Etapa 7 — Publicação (0,5 dia)
- [ ] Publicar no GitHub Pages; testar via `https://`.
- [ ] Testar o arquivo baixado em modo `file://` (celular, tablet, notebook).
- [ ] Gerar QR Code do endereço (fora do sistema) e divulgar.
- [ ] Registrar versão (`v1.0.0`) e *tag* no repositório.

**Estimativa total:** ~7 dias úteis de trabalho.

### Fluxo de trabalho recomendado
1. Trabalhar em um arquivo `ensalamento.html` na pasta do projeto.
2. A cada etapa, abrir diretamente no navegador (`file://`) e testar.
3. *Commit* ao final de cada etapa, com mensagem em português (ex.: `feat: busca por professor com autocompletar`).

---

## 15. Plano de testes

### 15.1 Casos de teste de tempo (usar o simulador)

| ID | Simulação | Resultado esperado |
|---|---|---|
| T-01 | Segunda 12:59 | `ANTES_DAS_AULAS`; 1ª aula em destaque ("Começa às 13:00") |
| T-02 | Segunda 13:00:00 | `EM_AULA`, 1ª aula **em andamento** |
| T-03 | Segunda 13:49:59 | 1ª ainda em andamento |
| T-04 | Segunda 13:50:00 | 2ª em andamento; 1ª **esmaecida** |
| T-05 | Segunda 15:29:59 | 3ª em andamento |
| T-06 | Segunda 15:30:00 | `INTERVALO`; 4ª em destaque como próxima |
| T-07 | Segunda 15:39:59 | `INTERVALO` |
| T-08 | Segunda 15:40:00 | 4ª em andamento |
| T-09 | Segunda 17:19:59 | 5ª em andamento |
| T-10 | Segunda 17:20:00 | `FIM_DO_PERIODO`; tudo esmaecido |
| T-11 | Sábado qualquer hora | `SEM_AULA_HOJE`; sugere segunda-feira |
| T-12 | Domingo 23:59 → Segunda 00:00 | Virada de dia reavalia |
| T-13 | Dia em `diasSemAula` | `SEM_AULA_HOJE` |

### 15.2 Casos de teste de dados (conferência com a grade impressa)

| ID | Consulta | Resultado esperado |
|---|---|---|
| D-01 | Segunda · 13:00 · turma 9C | História · Leonel |
| D-02 | Terça · 16:30 · turma 7A | Ensino Religioso · Eliane Pereira |
| D-03 | Quarta · 14:40 · turma 8A | Educação Digital · Volnei |
| D-04 | Quinta · 15:40 · turma 9C | Recomposição de Língua Portuguesa · Daniele |
| D-05 | Sexta · 13:00 · turma 8C | História · Paulo |
| D-06 | Segunda · Robótica | 13:00 e 13:50: RPP · Raphael (sem outras aulas) |
| D-07 | Professor "Ubirajara", Segunda | 7C (13:00 e 13:50), 9C (14:40), 7D (15:40), 7B (16:30) |
| D-08 | Professor "Eliane" ≠ "Eliana" ≠ "Eliane Pereira" | Três resultados distintos na busca "elian" |
| D-09 | Professor "Noemi", Quarta | 6A (13:00), 9C (13:50), 8B (14:40), 7C (15:40), 8C (16:30) |
| D-10 | Turma 6B, Terça 15:40 | História · Leonel (ver P-05) |

### 15.3 Casos de busca

| ID | Entrada | Esperado |
|---|---|---|
| B-01 | "AUREA" / "áurea" / "Aurea " | Mesma professora (Áurea) |
| B-02 | "mar" | Sugere Márcia |
| B-03 | "xyz" | "Não encontramos esse nome." |
| B-04 | "7º a" / "7A" / "7 a" | Turma 7A |
| B-05 | "<script>alert(1)</script>" | Tratado como texto; nada executa; "Nenhum resultado" |
| B-06 | Campo vazio | Mensagem de orientação |

### 15.4 Testes de interface e ambiente
- Larguras: 320, 360, 414, 600, 768, 1024, 1366, 1920, 3840 px; retrato e paisagem.
- Zoom do navegador 200 %.
- Rede desligada (modo avião) e DevTools → aba *Network* **sem nenhuma requisição**.
- Abrir via `file://`, GitHub Pages, e arquivo renomeado (`ensalamento.html`).
- Navegação só por teclado; leitor de tela (TalkBack/VoiceOver) lendo a aula em destaque.
- *Lighthouse*: Acessibilidade ≥ 90, Boas práticas ≥ 90.

---

## 16. Publicação e execução local

### 16.1 GitHub Pages
1. Criar repositório e enviar o arquivo como **`index.html`** na raiz.
2. *Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)`*.
3. Endereço resultante: `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.
4. Opcional: criar arquivo vazio `.nojekyll` na raiz (evita processamento desnecessário).

### 16.2 Execução local (sem internet)
- Baixar o arquivo e **abrir com duplo clique** (ou "Abrir com → navegador").
- **Android/iOS:** salvar o arquivo e abrir pelo navegador/gerenciador de arquivos; ou "Adicionar à tela inicial" quando acessado pelo Pages (o site continua funcionando mesmo sem rede após o primeiro carregamento, pois o navegador mantém a página em cache — sem *service worker*, o cache não é garantido; por isso recomenda-se também manter o arquivo salvo).
- **Quadros interativos:** salvar o arquivo na área de trabalho e definir como página inicial do navegador.
- O nome do arquivo é livre (`index.html`, `ensalamento.html`, `tarde.html`…): o sistema **não depende do próprio nome**.

### 16.3 Versionamento
- Constante `CONFIGURACAO.versao = '1.0.0'` e `dataDaGrade = 'AAAA-MM-DD'` exibidas discretamente no rodapé, para a equipe saber se o arquivo local está desatualizado.

---

## 17. Manutenção e atualização dos dados

### 17.1 Quando houver mudança de horário
1. Abrir o arquivo em editor de texto simples.
2. Localizar o bloco `/* ===== DADOS_DA_GRADE ===== */`.
3. Alterar **somente** a célula necessária (`"SIGLA|PROFESSOR"`).
4. Salvar, abrir no navegador e conferir o **painel de diagnóstico** (`#diagnostico`).
5. Atualizar `versao` e `dataDaGrade`; publicar.

### 17.2 Quando mudar o trimestre
- Alterar `CONFIGURACAO.trimestre`, `SALAS_DAS_TURMAS` (se as salas mudarem) e a grade.

### 17.3 Adicionar feriados/recessos
- Incluir datas em `CONFIGURACAO.diasSemAula` no formato `'AAAA-MM-DD'`.

### 17.4 Fase 2 (manhã)
- Duplicar a estrutura `DADOS_DA_GRADE` para `DADOS_DA_GRADE_MANHA`, incluir `horariosManha` e uma chave de período (`manha`/`tarde`); a interface já prevê o seletor de período (faixa **MANHÃ** azul-marinho/**TARDE** laranja).

---

## 18. Pendências e pontos a confirmar

Itens que dependem de confirmação da escola e que **não devem ser "adivinhados"** no sistema:

| ID | Pendência | Tratamento provisório |
|---|---|---|
| **P-01** | Horário de **término** das aulas e do intervalo (o quadro só mostra o início). | 50 min por aula; intervalo 15:30–15:40; fim 17:20. Tudo em `CONFIGURACAO.horarios`. |
| **P-02** | Significado da disciplina **"704"** (aparece com Melissa e Simone). | Exibir "704". |
| **P-03** | Significado de **"RPP"** (Robótica/Raphael). | Exibir "RPP". |
| **P-04** | **Local da sala de Robótica** (não consta no cartaz). | "Sala de Robótica (a confirmar)". |
| **P-05** | **Correções manuscritas** na grade: Segunda 15:40 · 6B (escrito à mão "HIST – LEONEL") e Terça 16:30 · 6B (anotação manuscrita sobre o texto impresso, parcialmente ilegível, aparentando "HIST – LEONEL"). | Adotados como **HIST · LEONEL**; conferir no original. |
| **P-06** | **Grafia oficial** dos nomes (acentos): Áurea, Márcia, Emanoel/Emanuel, Ubirajara, Lilian/Lílian, Daniele, Karine, Noemi, Volnei, Raphael. | Chave de busca sem acento; nome de exibição ajustável em `PROFESSORES`. Sugestão: **Áurea** e **Márcia** com acento. |
| **P-07** | Nomes completos/sobrenomes (Ex.: "Eliane" × "Eliana" × "Eliane Pereira") para evitar confusão. | Manter como na grade. |
| **P-08** | Existência de **aulas "REC MT"/"REC LP"** como disciplinas oficiais (Recomposição de Matemática/Língua Portuguesa). | Nome por extenso proposto no Anexo B. |
| **P-09** | Confirmar siglas: **REDA** (Redação), **E REL** (Ensino Religioso), **ED DIG** (Educação Digital), **EDFI** (Educação Física). | Nome por extenso proposto no Anexo B. |
| **P-10** | **Turmas**: 9º C aparece na tarde; confirmar se há 9º A/B à tarde (não constam). | Apenas as turmas da grade fornecida. |
| **P-11** | Calendário de **feriados/recessos** do trimestre. | Lista vazia em `diasSemAula`. |
| **P-12** | Dados das **turmas do 6º e 9º** na imagem do cartaz: 6A e 6B no Piso 2; 9C no Piso 3 — confirmar. | Conforme cartaz. |

---

## 19. Critérios de aceite

O sistema será considerado pronto quando:

- [ ] Em **um único arquivo HTML**, sem nenhuma requisição externa (verificado na aba *Network*).
- [ ] Todos os dados do **Anexo A** conferidos com o quadro impresso, sem divergência.
- [ ] A busca por professor e por turma retorna **exatamente** as aulas do dia, com turma/professor, disciplina, horário e piso corretos.
- [ ] A aula **em andamento** (ou a **próxima**) está em destaque e as **passadas esmaecidas**, em todos os casos T-01 a T-13.
- [ ] Visual coerente com o cartaz "ENSALAMENTO" (cores, faixas Manhã/Tarde, pisos, ilustrações em SVG).
- [ ] Funciona de **320 px a 4K**, retrato e paisagem, sem rolagem horizontal.
- [ ] Funciona em **Android, iOS, Windows, Linux, ChromeOS e macOS** nos navegadores da matriz 13.4.
- [ ] Funciona via **GitHub Pages** e via **arquivo local (`file://`)** com qualquer nome de arquivo.
- [ ] **100 % em português do Brasil** (interface, comentários, nomes de funções).
- [ ] Funções, constantes e IDs com **nomes remissivos**, conforme a seção 9.
- [ ] Sem `innerHTML` com dados, sem `eval`, CSP aplicada.
- [ ] Tratamento amigável de erros e de estados vazios.

---

# ANEXO A — Dados oficiais transcritos (tarde)

> **Fonte:** quadro impresso "TURMAS — TARDE" e cartaz "ENSALAMENTO · 3º TRIMESTRE".
> **Leitura da grade:** cada célula = `DISCIPLINA | PROFESSOR`. Linhas = horários (13:00, 13:50, 14:40, 15:40, 16:30). Colunas = turmas na ordem:
> `9C, 6A, 6B, 7A, 7B, 7C, 7D, 8A, 8B, 8C, ROBOTICA`.
> Siglas com espaço no original (L PORT, L ING, E REL, REC MT, REC LP, ED DIG) estão escritas **sem espaço** (`LPORT`, `LING`, `EREL`, `RECMT`, `RECLP`, `EDDIG`) para uso em código.

## A.1 Mapa de salas (cartaz)

| Período | Piso | Turmas |
|---|---|---|
| Tarde | **Piso 1** | 8A, 7C, 7A |
| Tarde | **Piso 2** | 7D, 6A, 6B, 7B |
| Tarde | **Piso 3 (TV Interativa)** | 9C, 8B, 8C |
| (Referência — manhã, Fase 2) | Piso 1 | 3A, 2B, 9B |
| (Referência — manhã, Fase 2) | Piso 2 | 2A, 9A, 3C, 3B |
| (Referência — manhã, Fase 2) | Piso 3 (TV Interativa) | 1A, 1B, 1C/2C |

## A.2 Horários de início (quadro)

| Aula | Início |
|:-:|:-:|
| 1ª | 13:00 |
| 2ª | 13:50 |
| 3ª | 14:40 |
| 4ª | 15:40 |
| 5ª | 16:30 |

## A.3 Grade — Bloco de dados para o sistema (`DADOS_DA_GRADE`)

```js
/* ===== DADOS_DA_GRADE ===== */
/* Ordem das colunas: 9C, 6A, 6B, 7A, 7B, 7C, 7D, 8A, 8B, 8C, ROBOTICA
   Cada dia tem 5 linhas (13:00, 13:50, 14:40, 15:40, 16:30). Célula vazia = sem aula. */
var DADOS_DA_GRADE = {

  // ---------- SEGUNDA-FEIRA (1) ----------
  1: [
    ['HIST|LEONEL','EDFI|DAVI','GEO|ELIANE','LPORT|ELIANA','CIEN|KARINE','MAT|UBIRAJARA','HIST|ELIANE PEREIRA','LPORT|AUREA','704|MELISSA','LING|NOEMI','RPP|RAPHAEL'],
    ['HIST|LEONEL','704|SIMONE','LING|NOEMI','LPORT|ELIANA','EREL|ELIANE PEREIRA','MAT|UBIRAJARA','EDFI|DAVI','LPORT|AUREA','CIEN|KARINE','704|MELISSA','RPP|RAPHAEL'],
    ['MAT|UBIRAJARA','MAT|LILIAN','LPORT|ELIANA','GEO|ELIANE','CIEN|KARINE','HIST|ELIANE PEREIRA','704|MELISSA','LING|NOEMI','REDA|AUREA','EDFI|DAVI',''],
    ['704|MELISSA','CIEN|EMANOEL','HIST|LEONEL','HIST|ELIANE PEREIRA','LING|NOEMI','REDA|ELIANA','MAT|UBIRAJARA','GEO|ELIANE','CIEN|KARINE','REDA|AUREA',''],
    ['CIEN|EMANOEL','HIST|LEONEL','704|SIMONE','MAT|LILIAN','MAT|UBIRAJARA','REDA|ELIANA','LING|NOEMI','704|MELISSA','EDFI|DAVI','REDA|AUREA','']
  ],

  // ---------- TERÇA-FEIRA (2) ----------
  2: [
    ['EDFI|DAVI','HIST|LEONEL','EREL|ELIANE PEREIRA','REDA|ELIANA','GEO|ELIANE','CIEN|KARINE','704|MELISSA','REDA|AUREA','HIST|PAULO','MAT|PEDRO',''],
    ['MAT|UBIRAJARA','LPORT|ELIANA','RECMT|VOLNEI','CIEN|KARINE','GEO|ELIANE','704|SIMONE','EREL|ELIANE PEREIRA','704|MELISSA','HIST|PAULO','MAT|PEDRO',''],
    ['704|MELISSA','EREL|LEONEL','RECMT|VOLNEI','MAT|LILIAN','LPORT|AUREA','EREL|ELIANE PEREIRA','MAT|UBIRAJARA','EDFI|DAVI','MAT|PEDRO','CIEN|KARINE',''],
    ['RECMT|VOLNEI','RECMT|LILIAN','HIST|LEONEL','704|SIMONE','EDFI|DAVI','LPORT|AUREA','LPORT|ELIANA','MAT|UBIRAJARA','704|MELISSA','CIEN|KARINE',''],
    ['RECMT|VOLNEI','RECMT|LILIAN','HIST|LEONEL','EREL|ELIANE PEREIRA','704|SIMONE','GEO|ELIANE','LPORT|ELIANA','MAT|UBIRAJARA','LPORT|AUREA','704|MELISSA','']
  ],

  // ---------- QUARTA-FEIRA (3) ----------
  3: [
    ['LPORT|DANIELE','LING|NOEMI','LPORT|ELIANA','HIST|ELIANE PEREIRA','CIEN|KARINE','EDFI|DAVI','MAT|UBIRAJARA','GEO|ELIANE','MAT|PEDRO','LPORT|AUREA',''],
    ['LING|NOEMI','RECLP|ELIANA','CIEN|EMANOEL','EDFI|DAVI','HIST|ELIANE PEREIRA','GEO|ELIANE','MAT|UBIRAJARA','EDDIG|VOLNEI','CIEN|KARINE','LPORT|AUREA',''],
    ['CIEN|EMANOEL','RECLP|ELIANA','GEO|ELIANE','MAT|LILIAN','HIST|ELIANE PEREIRA','MAT|UBIRAJARA','CIEN|KARINE','EDDIG|VOLNEI','LING|NOEMI','EDFI|DAVI',''],
    ['MAT|UBIRAJARA','MAT|LILIAN','CIEN|EMANOEL','GEO|ELIANE','REDA|ELIANA','LING|NOEMI','CIEN|KARINE','LPORT|AUREA','EDFI|DAVI','EDDIG|VOLNEI',''],
    ['MAT|UBIRAJARA','CIEN|EMANOEL','MAT|LILIAN','GEO|ELIANE','REDA|ELIANA','LPORT|AUREA','EDFI|DAVI','CIEN|KARINE','EDDIG|VOLNEI','LING|NOEMI','']
  ],

  // ---------- QUINTA-FEIRA (4) ----------
  4: [
    ['GEO|MARCIA','GEO|ELIANE','LPORT|ELIANA','LING|NOEMI','MAT|UBIRAJARA','LPORT|AUREA','REDA|DANIELE','CIEN|KARINE','MAT|PEDRO','HIST|PAULO',''],
    ['GEO|MARCIA','LING|NOEMI','LPORT|ELIANA','MAT|LILIAN','MAT|UBIRAJARA','CIEN|KARINE','REDA|DANIELE','HIST|PAULO','MAT|PEDRO','EDDIG|VOLNEI',''],
    ['MAT|UBIRAJARA','LPORT|ELIANA','MAT|LILIAN','CIEN|KARINE','LPORT|AUREA','GEO|ELIANE','GEO|MARCIA','LING|NOEMI','EDDIG|VOLNEI','MAT|PEDRO',''],
    ['RECLP|DANIELE','GEO|ELIANE','MAT|LILIAN','LPORT|ELIANA','EDFI|DAVI','HIST|ELIANE PEREIRA','LING|NOEMI','MAT|UBIRAJARA','GEO|MARCIA','MAT|PEDRO',''],
    ['RECLP|DANIELE','MAT|LILIAN','LING|NOEMI','REDA|ELIANA','GEO|ELIANE','MAT|UBIRAJARA','HIST|ELIANE PEREIRA','EDFI|DAVI','REDA|AUREA','GEO|MARCIA','']
  ],

  // ---------- SEXTA-FEIRA (5) ----------
  5: [
    ['LPORT|DANIELE','LPORT|ELIANA','EDFI|DAVI','CIEN|KARINE','LING|NOEMI','704|SIMONE','GEO|MARCIA','MAT|UBIRAJARA','LPORT|AUREA','HIST|PAULO',''],
    ['LPORT|DANIELE','LPORT|ELIANA','704|SIMONE','EDFI|DAVI','MAT|UBIRAJARA','LING|NOEMI','GEO|MARCIA','CIEN|KARINE','LPORT|AUREA','HIST|PAULO',''],
    ['EDFI|DAVI','704|SIMONE','MAT|LILIAN','LING|NOEMI','MAT|UBIRAJARA','CIEN|KARINE','LPORT|ELIANA','REDA|AUREA','HIST|PAULO','GEO|MARCIA',''],
    ['GEO|MARCIA','EDFI|DAVI','RECLP|ELIANA','MAT|LILIAN','704|SIMONE','MAT|UBIRAJARA','CIEN|KARINE','HIST|PAULO','LING|NOEMI','LPORT|AUREA',''],
    ['LING|NOEMI','MAT|LILIAN','RECLP|ELIANA','704|SIMONE','LPORT|AUREA','EDFI|DAVI','MAT|UBIRAJARA','HIST|PAULO','GEO|MARCIA','CIEN|KARINE','']
  ]
};
/* ===== FIM DE DADOS_DA_GRADE ===== */
```

## A.4 Disciplinas (sigla → nome por extenso)

```js
var DISCIPLINAS = {
  'HIST':  'História',
  'GEO':   'Geografia',
  'MAT':   'Matemática',
  'CIEN':  'Ciências',
  'LPORT': 'Língua Portuguesa',
  'LING':  'Língua Inglesa',
  'EDFI':  'Educação Física',
  'EREL':  'Ensino Religioso',
  'REDA':  'Redação',
  'RECMT': 'Recomposição de Matemática',
  'RECLP': 'Recomposição de Língua Portuguesa',
  'EDDIG': 'Educação Digital',
  '704':   '704',      // a confirmar (P-02)
  'RPP':   'RPP'       // a confirmar (P-03)
};
```

## A.5 Professores (chave de busca → nome de exibição)

```js
var PROFESSORES = {
  'AUREA':           'Áurea',
  'DANIELE':         'Daniele',
  'DAVI':            'Davi',
  'ELIANA':          'Eliana',
  'ELIANE':          'Eliane',
  'ELIANE PEREIRA':  'Eliane Pereira',
  'EMANOEL':         'Emanoel',
  'KARINE':          'Karine',
  'LEONEL':          'Leonel',
  'LILIAN':          'Lilian',
  'MARCIA':          'Márcia',
  'MELISSA':         'Melissa',
  'NOEMI':           'Noemi',
  'PAULO':           'Paulo',
  'PEDRO':           'Pedro',
  'RAPHAEL':         'Raphael',
  'SIMONE':          'Simone',
  'UBIRAJARA':       'Ubirajara',
  'VOLNEI':          'Volnei'
};
```
*(19 professores)*

## A.6 Conferência visual da grade (para revisão humana)

Legenda: `DISC/PROF`. Colunas: 9C · 6A · 6B · 7A · 7B · 7C · 7D · 8A · 8B · 8C · ROB.

### Segunda-feira

| Horário | 9C | 6A | 6B | 7A | 7B | 7C | 7D | 8A | 8B | 8C | ROB |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 13:00 | HIST/Leonel | EDFI/Davi | GEO/Eliane | LPORT/Eliana | CIEN/Karine | MAT/Ubirajara | HIST/Eliane Pereira | LPORT/Áurea | 704/Melissa | LING/Noemi | RPP/Raphael |
| 13:50 | HIST/Leonel | 704/Simone | LING/Noemi | LPORT/Eliana | EREL/Eliane Pereira | MAT/Ubirajara | EDFI/Davi | LPORT/Áurea | CIEN/Karine | 704/Melissa | RPP/Raphael |
| 14:40 | MAT/Ubirajara | MAT/Lilian | LPORT/Eliana | GEO/Eliane | CIEN/Karine | HIST/Eliane Pereira | 704/Melissa | LING/Noemi | REDA/Áurea | EDFI/Davi | — |
| 15:40 | 704/Melissa | CIEN/Emanoel | HIST/Leonel* | HIST/Eliane Pereira | LING/Noemi | REDA/Eliana | MAT/Ubirajara | GEO/Eliane | CIEN/Karine | REDA/Áurea | — |
| 16:30 | CIEN/Emanoel | HIST/Leonel | 704/Simone | MAT/Lilian | MAT/Ubirajara | REDA/Eliana | LING/Noemi | 704/Melissa | EDFI/Davi | REDA/Áurea | — |

### Terça-feira

| Horário | 9C | 6A | 6B | 7A | 7B | 7C | 7D | 8A | 8B | 8C |
|---|---|---|---|---|---|---|---|---|---|---|
| 13:00 | EDFI/Davi | HIST/Leonel | EREL/Eliane Pereira | REDA/Eliana | GEO/Eliane | CIEN/Karine | 704/Melissa | REDA/Áurea | HIST/Paulo | MAT/Pedro |
| 13:50 | MAT/Ubirajara | LPORT/Eliana | RECMT/Volnei | CIEN/Karine | GEO/Eliane | 704/Simone | EREL/Eliane Pereira | 704/Melissa | HIST/Paulo | MAT/Pedro |
| 14:40 | 704/Melissa | EREL/Leonel | RECMT/Volnei | MAT/Lilian | LPORT/Áurea | EREL/Eliane Pereira | MAT/Ubirajara | EDFI/Davi | MAT/Pedro | CIEN/Karine |
| 15:40 | RECMT/Volnei | RECMT/Lilian | HIST/Leonel | 704/Simone | EDFI/Davi | LPORT/Áurea | LPORT/Eliana | MAT/Ubirajara | 704/Melissa | CIEN/Karine |
| 16:30 | RECMT/Volnei | RECMT/Lilian | HIST/Leonel* | EREL/Eliane Pereira | 704/Simone | GEO/Eliane | LPORT/Eliana | MAT/Ubirajara | LPORT/Áurea | 704/Melissa |

### Quarta-feira

| Horário | 9C | 6A | 6B | 7A | 7B | 7C | 7D | 8A | 8B | 8C |
|---|---|---|---|---|---|---|---|---|---|---|
| 13:00 | LPORT/Daniele | LING/Noemi | LPORT/Eliana | HIST/Eliane Pereira | CIEN/Karine | EDFI/Davi | MAT/Ubirajara | GEO/Eliane | MAT/Pedro | LPORT/Áurea |
| 13:50 | LING/Noemi | RECLP/Eliana | CIEN/Emanoel | EDFI/Davi | HIST/Eliane Pereira | GEO/Eliane | MAT/Ubirajara | EDDIG/Volnei | CIEN/Karine | LPORT/Áurea |
| 14:40 | CIEN/Emanoel | RECLP/Eliana | GEO/Eliane | MAT/Lilian | HIST/Eliane Pereira | MAT/Ubirajara | CIEN/Karine | EDDIG/Volnei | LING/Noemi | EDFI/Davi |
| 15:40 | MAT/Ubirajara | MAT/Lilian | CIEN/Emanoel | GEO/Eliane | REDA/Eliana | LING/Noemi | CIEN/Karine | LPORT/Áurea | EDFI/Davi | EDDIG/Volnei |
| 16:30 | MAT/Ubirajara | CIEN/Emanoel | MAT/Lilian | GEO/Eliane | REDA/Eliana | LPORT/Áurea | EDFI/Davi | CIEN/Karine | EDDIG/Volnei | LING/Noemi |

### Quinta-feira

| Horário | 9C | 6A | 6B | 7A | 7B | 7C | 7D | 8A | 8B | 8C |
|---|---|---|---|---|---|---|---|---|---|---|
| 13:00 | GEO/Márcia | GEO/Eliane | LPORT/Eliana | LING/Noemi | MAT/Ubirajara | LPORT/Áurea | REDA/Daniele | CIEN/Karine | MAT/Pedro | HIST/Paulo |
| 13:50 | GEO/Márcia | LING/Noemi | LPORT/Eliana | MAT/Lilian | MAT/Ubirajara | CIEN/Karine | REDA/Daniele | HIST/Paulo | MAT/Pedro | EDDIG/Volnei |
| 14:40 | MAT/Ubirajara | LPORT/Eliana | MAT/Lilian | CIEN/Karine | LPORT/Áurea | GEO/Eliane | GEO/Márcia | LING/Noemi | EDDIG/Volnei | MAT/Pedro |
| 15:40 | RECLP/Daniele | GEO/Eliane | MAT/Lilian | LPORT/Eliana | EDFI/Davi | HIST/Eliane Pereira | LING/Noemi | MAT/Ubirajara | GEO/Márcia | MAT/Pedro |
| 16:30 | RECLP/Daniele | MAT/Lilian | LING/Noemi | REDA/Eliana | GEO/Eliane | MAT/Ubirajara | HIST/Eliane Pereira | EDFI/Davi | REDA/Áurea | GEO/Márcia |

### Sexta-feira

| Horário | 9C | 6A | 6B | 7A | 7B | 7C | 7D | 8A | 8B | 8C |
|---|---|---|---|---|---|---|---|---|---|---|
| 13:00 | LPORT/Daniele | LPORT/Eliana | EDFI/Davi | CIEN/Karine | LING/Noemi | 704/Simone | GEO/Márcia | MAT/Ubirajara | LPORT/Áurea | HIST/Paulo |
| 13:50 | LPORT/Daniele | LPORT/Eliana | 704/Simone | EDFI/Davi | MAT/Ubirajara | LING/Noemi | GEO/Márcia | CIEN/Karine | LPORT/Áurea | HIST/Paulo |
| 14:40 | EDFI/Davi | 704/Simone | MAT/Lilian | LING/Noemi | MAT/Ubirajara | CIEN/Karine | LPORT/Eliana | REDA/Áurea | HIST/Paulo | GEO/Márcia |
| 15:40 | GEO/Márcia | EDFI/Davi | RECLP/Eliana | MAT/Lilian | 704/Simone | MAT/Ubirajara | CIEN/Karine | HIST/Paulo | LING/Noemi | LPORT/Áurea |
| 16:30 | LING/Noemi | MAT/Lilian | RECLP/Eliana | 704/Simone | LPORT/Áurea | EDFI/Davi | MAT/Ubirajara | HIST/Paulo | GEO/Márcia | CIEN/Karine |

> **\*** = célula com correção manuscrita no original; conferir (pendência **P-05**). A Robótica só tem aulas na **segunda (13:00 e 13:50)** na grade fornecida.

---

# ANEXO B — Siglas e glossário

| Sigla (grade) | Código no sistema | Significado adotado |
|---|---|---|
| HIST | `HIST` | História |
| GEO | `GEO` | Geografia |
| MAT | `MAT` | Matemática |
| CIEN | `CIEN` | Ciências |
| L PORT | `LPORT` | Língua Portuguesa |
| L ING | `LING` | Língua Inglesa |
| EDFI | `EDFI` | Educação Física |
| E REL | `EREL` | Ensino Religioso |
| REDA | `REDA` | Redação |
| REC MT | `RECMT` | Recomposição de Matemática |
| REC LP | `RECLP` | Recomposição de Língua Portuguesa |
| ED DIG | `EDDIG` | Educação Digital |
| 704 | `704` | **A confirmar** |
| RPP | `RPP` | **A confirmar** (turma de Robótica) |

| Termo | Definição |
|---|---|
| **Ensalamento** | Distribuição de turmas/professores nas salas. |
| **Aula dupla / geminada** | Duas aulas consecutivas do mesmo professor na mesma turma. |
| **Janela** | Horário sem aula para o professor dentro do período. |
| **Aula atual** | A que está em andamento no momento (início ≤ agora < fim). |
| **Próxima aula** | A primeira aula que começa depois do momento atual. |
| **Esmaecida** | Aula já encerrada, exibida com menor destaque visual. |
| **Nome remissivo** | Nome de função/variável que "remete" claramente ao seu propósito. |
| **Simulador** | Recurso para testar o comportamento com data/hora diferentes da real. |

---

# ANEXO C — Esqueleto do arquivo HTML

> Estrutura mínima de partida para a Etapa 1. Todo o conteúdo visual e lógico entra neste único arquivo.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none'; script-src 'unsafe-inline'; style-src 'unsafe-inline'; img-src data:; connect-src 'none'; base-uri 'none'; form-action 'none'">
<meta name="referrer" content="no-referrer">
<meta name="theme-color" content="#1F3A8A">
<title>Ensalamento · Escola Santo Agostinho</title>
<style>
  :root{
    --cor-titulo:#1F3A8A; --cor-azul-faixa:#2563C9; --cor-azul-claro:#E6F0FF;
    --cor-amarelo-sol:#FFC81E; --cor-laranja-tarde:#F58A1F;
    --cor-piso1:#2F6FD6; --cor-piso2:#3BA94A; --cor-piso3:#7B3FB5;
    --cor-fundo:#F7FAFF; --cor-cartao:#FFFFFF; --escala-fonte:1;
  }
  html{ -webkit-text-size-adjust:100%; }
  body{ margin:0; background:var(--cor-fundo); color:var(--cor-titulo);
        font-family:"Trebuchet MS","Segoe UI",system-ui,-apple-system,"Roboto",Arial,sans-serif;
        font-size:calc(1rem * var(--escala-fonte)); min-height:100vh; min-height:100dvh; }
  .cartao-aula{ background:var(--cor-cartao); border:3px solid var(--cor-azul-faixa);
                border-radius:16px; padding:12px 14px; margin:0 0 10px; }
  .cartao-aula--agora{ border-color:var(--cor-amarelo-sol); box-shadow:0 0 0 4px rgba(255,200,30,.35); }
  .cartao-aula--proxima{ border-color:var(--cor-azul-faixa); }
  .cartao-aula--passada{ opacity:.55; filter:grayscale(.6); }
  @media (prefers-reduced-motion:reduce){ *{ animation:none !important; transition:none !important; } }
</style>
</head>
<body>
  <!-- Biblioteca de símbolos SVG -->
  <svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
    <symbol id="icone-sol" viewBox="0 0 64 64"><!-- ... --></symbol>
    <symbol id="icone-maca" viewBox="0 0 64 64"><!-- ... --></symbol>
    <!-- demais símbolos da seção 6.4 -->
  </svg>

  <header id="cabecalho-do-sistema"><!-- SVG do título ENSALAMENTO --></header>
  <main id="area-principal" aria-live="polite"></main>
  <footer id="rodape-do-sistema">ORGANIZAÇÃO HOJE, SUCESSO SEMPRE!</footer>
  <noscript>Este sistema precisa de JavaScript ativado para funcionar.</noscript>

<script>
(function () {
  'use strict';
  /* BLOCO 1: CONFIGURACAO, SALAS_DAS_TURMAS, DISCIPLINAS, PROFESSORES */
  /* BLOCO 2: DADOS_DA_GRADE (Anexo A.3)                               */
  /* BLOCO 3: utilitários (normalizar, formatar, criarElementoSeguro)  */
  /* BLOCO 4: regras de negócio (situação, classificação, busca)       */
  /* BLOCO 5: renderização                                             */
  /* BLOCO 6: eventos e iniciarSistema()                               */
  try { iniciarSistema(); } catch (erro) { tratarErroInesperado(erro); }
})();
</script>
</body>
</html>
```

---

*Fim do documento. Próximo passo sugerido: fechar as pendências P-01 a P-06 com a coordenação e iniciar a Etapa 1 (esqueleto e identidade visual).*
