<div align="center">

# <img src="../../assets/icons/04-linux.svg" width="30" height="30" valign="middle" /> 1. Terminal e Sistema de Arquivos

### Pós-Graduação em Desenvolvimento Web com TypeScript e Inteligência Artificial &ndash; UTFPR
**Disciplina:** 04 &bull; Linux para Desenvolvedores e DevOps &nbsp;|&nbsp; **Módulo:** M01 &bull; Tópico 01

<br>

[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](#)
[![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](#)
[![Terminal](https://img.shields.io/badge/CLI-Terminal-4D4D4D?style=for-the-badge&logo=gnometerminal&logoColor=white)](#)
[![AI Prompt Lab](https://img.shields.io/badge/Prompt%20Lab-IA%20%2B%20Terminal-6A5ACD?style=for-the-badge&logo=probot&logoColor=white)](#)

</div>

---

## <img src="../../assets/icons/nav.svg" width="20" height="20" valign="middle" /> Sumário

- [⚡ 1.1 Primeiros Comandos e Produtividade](#-11-primeiros-comandos-e-produtividade)
  - [⚙️ Preparação do Ambiente](#️-preparacao-do-ambiente)
  - [💻 Comandos Utilizados na Aula](#-comandos-utilizados-na-aula)
    - [1. Identificando Usuário, Máquina e Sistema](#1-identificando-usuario-maquina-e-sistema)
    - [2. Executando Comandos com Opções (Flags)](#2-executando-comandos-com-opcoes-flags)
    - [3. Atalhos de Produtividade no Terminal](#3-atalhos-de-produtividade-no-terminal)
    - [4. Consultando o Histórico Recente](#4-consultando-o-historico-recente)
- [🧪 Prompt Lab &bull; Comandos para Explorar com IA](#-prompt-lab--comandos-para-explorar-com-ia)
  - [📋 Prompt da Atividade](#-prompt-da-atividade)
  - [📊 Resposta Consolidada e Análise](#-resposta-consolidada-e-analise)
- [📌 Próximos Tópicos da Disciplina](#-proximos-topicos-da-disciplina)

---

## ⚡ 1.1 Primeiros Comandos e Produtividade

Este módulo introduz os conceitos fundamentais de operação na linha de comando (**CLI**), identificação de ambiente, sintaxe de opções (*flags*) e atalhos essenciais para maximizar a produtividade no terminal Linux.

### ⚙️ Preparação do Ambiente

Antes de iniciar a sessão prática ou gravação de aulas, o terminal foi limpo e sinalizado com o seguinte comando encadeado:

```bash
clear && echo "=== Ambiente de Gravação M01-T01 Pronto ==="
```

> [!NOTE]
> O operador `&&` (*AND lógico*) executa o comando à direita (`echo`) somente se o comando anterior (`clear`) finalizar com código de sucesso (`exit status 0`).

---

### 💻 Comandos Utilizados na Aula

#### 1. Identificando Usuário, Máquina e Sistema

Comandos essenciais para reconhecer quem você é, onde está e qual é o sistema operacional em execução:

```bash
# 1. Exibe o nome de login do usuário atual
$ whoami
# Saída esperada: aluno (ou seu usuário ativo)

# 2. Exibe o nome de rede do computador (hostname)
$ hostname
# Saída esperada: dev-machine / ubuntu-server

# 3. Informa o nome do Kernel do sistema operacional
$ uname -s
# Saída esperada: Linux

# 4. Imprime todas as informações disponíveis do sistema (Kernel, versão, arquitetura e SO)
$ uname -a
# Saída esperada: Linux dev-machine 6.8.0-45-generic #45-Ubuntu SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

| Comando | Descrição | Utilidade para o Desenvolvedor |
| :--- | :--- | :--- |
| `whoami` | Exibe o nome do usuário ativo na sessão | Evita executar comandos críticos no usuário errado (ex: validar se está como `root`). |
| `hostname` | Nome da máquina na rede | Confirma em qual servidor ou contêiner você está conectado antes de rodar deploys. |
| `uname -s` | Nome do Kernel do SO | Verificação rápida de ambiente em scripts de automação. |
| `uname -a` | Diagnóstico completo do sistema operacional | Identifica se a arquitetura é `x86_64` ou `aarch64` (ARM) para compilar imagens Docker. |

---

#### 2. Executando Comandos com Opções (Flags)

Demonstração do comando `date` e como as opções (*flags*) modificam o formato padrão de saída:

```bash
# Data e hora no formato padrão do sistema operacional
$ date
# Exemplo: seg 19 out 2026 15:00:00 -03

# Formatação customizada com especificadores de data (Ano-Mês-Dia)
$ date +"%Y-%m-%d"
# Exemplo: 2026-10-19

# Formato internacional padronizado ISO-8601
$ date --iso-8601
# Exemplo: 2026-10-19
```

> [!TIP]
> **Convenção de Flags no Linux:**
> - **Opções curtas:** Iniciam com um único hífen `-` (ex: `-s`, `-a`).
> - **Opções longas:** Iniciam com dois hífens `--` (ex: `--iso-8601`, `--help`).
> - **Formatos customizados:** Comandos como `date` aceitam strings precedidas pelo sinal `+` (ex: `+"%H:%M:%S"`).

---

#### 3. Atalhos de Produtividade no Terminal

Atalhos de teclado do Bash que agilizam o dia a dia e evitam digitação desnecessária:

| Ação | Como Executar | Comportamento Prático |
| :--- | :--- | :--- |
| **Autocompletar** | Digite `whoa` e pressione <kbd>Tab</kbd> | O shell completa automaticamente para `whoami`. Se houver mais de uma opção, pressione <kbd>Tab</kbd> duas vezes para ver a lista. |
| **Interromper Comando** | Execute `sleep 20` e pressione <kbd>Ctrl</kbd> + <kbd>C</kbd> | Envia o sinal `SIGINT` (Signal Interrupt) ao processo em primeiro plano, cancelando-o imediatamente. |
| **Limpar a Tela** | Pressione <kbd>Ctrl</kbd> + <kbd>L</kbd> | Limpa visualmente a tela do terminal instantaneamente, mantendo a linha digitada ativa (equivalente rápido ao comando `clear`). |

---

#### 4. Consultando o Histórico Recente

Visualização dos comandos executados na sessão atual:

```bash
# Exibe apenas os últimos 5 comandos executados no histórico
history 5
```

> [!TIP]
> **Dicas de Histórico:**
> - Digite `!!` para repetir o último comando executado (ex: `sudo !!` roda o comando anterior com privilégios de superusuário).
> - Pressione <kbd>Ctrl</kbd> + <kbd>R</kbd> para ativar a busca reversa interativa no histórico por palavras-chave.

---

## 🧪 Prompt Lab &bull; Comandos para Explorar com IA

<div align="center">
  <img src="../../assets/icons/12-ai.svg" width="32" height="32" valign="middle" />
  <h3>Laboratório Prático de Engenharia de Prompt</h3>
</div>

O **Prompt Lab** incentiva o uso intencional de Inteligência Artificial para aprofundar tópicos apresentados em aula, descobrindo flags avançadas e contextos práticos de uso para o desenvolvimento web.

### 📋 Prompt da Atividade

Copie o prompt estruturado abaixo e envie para o seu assistente de IA de preferência (*ChatGPT, Claude, Gemini ou Copilot*):

> **Prompt:**  
> *"Atue como um mentor sênior de Linux para desenvolvedores web. Explique os comandos `which`, `type`, `history` e `clear`. Para cada um, apresente: 1) O objetivo prático em uma frase; 2) Um exemplo de uso real no dia a dia de um dev web; 3) A principal flag ou atalho relacionado no Ubuntu."*

---

### 📊 Resposta Consolidada e Análise

Abaixo está o resumo técnico estruturado gerado a partir do laboratório de prompt:

| Comando | <img src="../../assets/icons/target.svg" width="16" height="16" valign="middle" /> Objetivo Prático | <img src="../../assets/icons/code.svg" width="16" height="16" valign="middle" /> Exemplo de Uso Real (Dev Web) | <img src="../../assets/icons/tools.svg" width="16" height="16" valign="middle" /> Principal Flag ou Atalho |
| :---: | :--- | :--- | :--- |
| `which` | Identifica onde o sistema localiza um executável no `PATH`. | Verificar qual versão do Node.js está ativa (ex: `/usr/bin/node` vs `~/.nvm/versions/node/v20/bin/node`). | `-a` (lista todos os executáveis com esse nome no `PATH`) |
| `type` | Descreve a natureza de um comando (se é executável, *shell builtin*, *alias* ou função). | Descobrir se um comando como `cd` ou `test` é um comando nativo do shell ou um binário compilado externo. | `-t` (retorna apenas a palavra-chave: `builtin`, `alias`, `file`) |
| `history` | Recupera e inspeciona comandos executados anteriormente no terminal. | Reencontrar um comando longo de migração de banco de dados (`npx prisma migrate dev`) rodado dias atrás. | `-c` (limpa histórico) &bull; `!5` (roda o 5º comando) &bull; <kbd>Ctrl</kbd> + <kbd>R</kbd> |
| `clear` | Limpa o buffer de visualização do terminal corrente. | Organizar e limpar a janela do terminal antes de gravar uma demonstração ou executar comandos críticos. | <kbd>Ctrl</kbd> + <kbd>L</kbd> (atalho de teclado equivalente universal) |

> [!NOTE]
> **Diferença entre `which` e `type`:**
> - O `which` procura apenas binários executáveis nas pastas do seu `PATH`.
> - O `type` é um comando nativo do Bash (*builtin*) que reconhece *aliases*, funções e comandos integrados do shell, fornecendo um diagnóstico mais preciso.

---

## 📌 Próximos Tópicos da Disciplina

- 📖 [**1.2 &bull; Navegação no Sistema de Arquivos**](../2-navegacao-no-sistema-de-arquivos/) &ndash; Comandos `pwd`, `cd`, `ls -lah` e a hierarquia `/`.
- 📖 **1.3 &bull; Manipulação de Arquivos e Pastas** &ndash; Comandos `touch`, `mkdir -p`, `cp`, `mv`, `rm` e redirecionamentos.

---

<div align="center">
  <p>
    <a href="../README.md">
      <img src="../../assets/icons/nav.svg" width="16" height="16" valign="middle" />
      &nbsp;Voltar para o Módulo de Linux
    </a>
    &nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="../../README.md">
      <img src="../../assets/icons/book.svg" width="16" height="16" valign="middle" />
      &nbsp;Voltar ao Índice do Repositório
    </a>
  </p>
</div>
