<div align="center">

# <img src="../../assets/icons/04-linux.svg" width="30" height="30" valign="middle" /> 2. Navegação no Sistema de Arquivos

### Pós-Graduação em Desenvolvimento Web com TypeScript e Inteligência Artificial &ndash; UTFPR
**Disciplina:** 04 &bull; Linux para Desenvolvedores e DevOps &nbsp;|&nbsp; **Módulo:** M01 &bull; Tópico 02

<br>

[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](#)
[![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](#)
[![Terminal](https://img.shields.io/badge/CLI-Terminal-4D4D4D?style=for-the-badge&logo=gnometerminal&logoColor=white)](#)
[![AI Prompt Lab](https://img.shields.io/badge/Prompt%20Lab-IA%20%2B%20Terminal-6A5ACD?style=for-the-badge&logo=probot&logoColor=white)](#)

</div>

---

## <img src="../../assets/icons/nav.svg" width="20" height="20" valign="middle" /> Sumário

- [🧭 1.2 Navegação no Sistema de Arquivos](#-12-navegacao-no-sistema-de-arquivos)
  - [⚙️ Preparação do Cenário de Laboratório](#️-preparacao-do-cenario-de-laboratorio)
  - [💻 Comandos Utilizados na Aula](#-comandos-utilizados-na-aula)
    - [1. Verificando a Localização Atual (`pwd`)](#1-verificando-a-localizacao-atual-pwd)
    - [2. Listando Arquivos e Pastas com Detalhes e Ocultos (`ls`)](#2-listando-arquivos-e-pastas-com-detalhes-e-ocultos-ls)
    - [3. Navegando entre Diretórios: Absoluto e Relativo (`cd`)](#3-navegando-entre-diretorios-absoluto-e-relativo-cd)
- [🧪 Prompt Lab &bull; Comandos para Explorar com IA](#-prompt-lab--comandos-para-explorar-com-ia)
  - [📋 Prompt da Atividade](#-prompt-da-atividade)
  - [📊 Resposta Consolidada e Análise](#-resposta-consolidada-e-analise)
  - [🔍 Exemplos Práticos de `tree`, `head`, `tail` e `realpath`](#-exemplos-praticos-de-tree-head-tail-e-realpath)
- [📌 Próximos Tópicos da Disciplina](#-proximos-topicos-da-disciplina)

---

## 🧭 1.2 Navegação no Sistema de Arquivos

Neste módulo, exploramos como se orientar e transitar com eficiência pela estrutura hierárquica do Linux, diferenciando caminhos absolutos e relativos, inspecionando arquivos ocultos e compreendendo permissões e metadados com utilitários de listagem.

### ⚙️ Preparação do Cenário de Laboratório

Para criar o ambiente prático de testes simulando um projeto web com arquivos estáticos, código-fonte e logs, foi executado o seguinte comando composto:

```bash
mkdir -p ~/cenario-web/projeto-legado/{public,src,logs} && touch ~/cenario-web/projeto-legado/src/index.js ~/cenario-web/projeto-legado/public/index.html ~/cenario-web/projeto-legado/.env.example && clear && echo "=== Cenário M01-T02 Criado com Sucesso ==="
```

> [!NOTE]
> **O que este comando faz:**
> 1. `mkdir -p`: Cria recursivamente a pasta `~/cenario-web/projeto-legado/` e, através da expansão de chaves `{public,src,logs}`, gera as três subpastas simultaneamente.
> 2. `touch`: Cria os arquivos vazios `index.js`, `index.html` e o arquivo oculto `.env.example`.
> 3. `clear && echo ...`: Limpa a tela e emite a confirmação de que o cenário está pronto.

---

### 💻 Comandos Utilizados na Aula

#### 1. Verificando a Localização Atual (`pwd`)

O utilitário `pwd` (*Print Working Directory*) imprime na tela o caminho absoluto da pasta onde o terminal está posicionado:

```bash
# Exibe o caminho absoluto do diretório corrente
$ pwd
# Saída esperada: /home/aluno
```

> [!TIP]
> Em ambientes com links simbólicos (*symlinks*), use `pwd -P` para obter o caminho físico real em disco ou `pwd -L` para seguir a referência lógica.

---

#### 2. Listando Arquivos e Pastas com Detalhes e Ocultos (`ls`)

Evolução progressiva das flags de listagem do mais simples ao formato ideal para diagnóstico:

```bash
# 1. Listagem simples (apenas nomes de arquivos visíveis)
$ ls

# 2. Listagem longa (-l) e completa (-a), incluindo arquivos ocultos (iniciados com '.')
$ ls -la

# 3. Listagem longa (-l), completa (-a) e com tamanhos legíveis (-h: KB, MB, GB)
$ ls -lah
```

Exemplo de interpretação da saída de `ls -lah`:

```text
drwxr-xr-x 5 aluno aluno 4.0K out 19 15:10 .
drwxr-xr-x 3 aluno aluno 4.0K out 19 15:10 ..
-rw-r--r-- 1 aluno aluno    0 out 19 15:10 .env.example
drwxr-xr-x 2 aluno aluno 4.0K out 19 15:10 logs
drwxr-xr-x 2 aluno aluno 4.0K out 19 15:10 public
drwxr-xr-x 2 aluno aluno 4.0K out 19 15:10 src
```

| Elemento / Flag | Significado | Importância para o Desenvolvedor |
| :--- | :--- | :--- |
| `.` *(ponto)* | Representa o diretório atual | Usado em referências relativas (ex: `./index.js`). |
| `..` *(dois pontos)* | Representa o diretório pai (um nível acima) | Usado para subir na hierarquia de pastas. |
| `.env.example` | Arquivo oculto (começa com `.`) | Não aparece no `ls` comum; exige a flag `-a`. Configurações sensíveis (como `.env`, `.git/`) são sempre ocultas. |
| Flag `-l` | Formato longo (*long listing*) | Exibe permissões (`drwxr-xr-x`), proprietário, grupo, tamanho e data da última modificação. |
| Flag `-a` | Todos (*all*) | Revela arquivos de sistema e variáveis de ambiente ocultas. |
| Flag `-h` | Legível para humanos (*human-readable*) | Converte bytes brutos em unidades compreensíveis (`4.0K`, `12M`, `1.5G`). |

---

#### 3. Navegando entre Diretórios: Absoluto e Relativo (`cd`)

Sequência de navegação explorando referências absolutas, relativas, atalhos de sistema e retorno:

```bash
# 1. Navegação Absoluta: Acessa a pasta criada a partir da home do usuário (~)
$ cd ~/cenario-web/projeto-legado

# 2. Confirma a posição atual
$ pwd
# /home/aluno/cenario-web/projeto-legado

# 3. Inspeciona o conteúdo detalhado do projeto
$ ls -lah

# 4. Navegação Relativa: Sobe um nível para a pasta pai (..)
$ cd ..
$ pwd
# /home/aluno/cenario-web

# 5. Atalho de Home: Retorna diretamente para a pasta pessoal do usuário
$ cd ~
# (Dica: digitar apenas 'cd' sem argumentos produz o mesmo efeito)
$ pwd
# /home/aluno

# 6. Atalho de Retorno Rápido: Volta imediatamente para o diretório anterior
$ cd -
# Saída automática: /home/aluno/cenario-web
```

> [!TIP]
> **Resumo dos Operadores de Navegação no `cd`:**
> - `cd ~` ou `cd`: Vai para o diretório raiz do usuário (`/home/usuario`).
> - `cd ..`: Sobe um nível para o diretório pai.
> - `cd ../..`: Sobe dois níveis hierárquicos.
> - `cd -`: Funciona como o botão "Voltar" do navegador, alternando entre o diretório atual e o anterior (`$OLDPWD`).
> - `cd /`: Vai para a raiz absoluta do sistema operacional.

---

## 🧪 Prompt Lab &bull; Comandos para Explorar com IA

<div align="center">
  <img src="../../assets/icons/12-ai.svg" width="32" height="32" valign="middle" />
  <h3>Laboratório Prático de Engenharia de Prompt</h3>
</div>

Para explorar utilitários que ajudam a visualizar estruturas de diretórios complexas e inspecionar o início e fim de arquivos de configuração e logs sem a necessidade de abri-los em editores de texto.

### 📋 Prompt da Atividade

Copie o prompt estruturado abaixo e envie para o seu assistente de IA preferido:

> **Prompt:**  
> *"Atue como um mentor de Linux para desenvolvedores web. Explique os utilitários `tree`, `head`, `tail` e `realpath` no Ubuntu. Mostre: 1) O que cada um faz; 2) Como usar o comando `tree -L 2` para limitar níveis de profundidade de um projeto web; 3) Como usar `head` e `tail` para inspecionar um arquivo sem abri-lo por completo."*

---

### 📊 Resposta Consolidada e Análise

Abaixo está a síntese técnica dos comandos explorados no laboratório de IA:

| Utilitário | <img src="../../assets/icons/target.svg" width="16" height="16" valign="middle" /> O que faz? | <img src="../../assets/icons/code.svg" width="16" height="16" valign="middle" /> Exemplo de Uso Real (Dev Web) | <img src="../../assets/icons/tools.svg" width="16" height="16" valign="middle" /> Flag ou Opção Principal |
| :---: | :--- | :--- | :--- |
| `tree` | Exibe a estrutura de pastas e arquivos recursivamente em formato visual de árvore. | Compreender a arquitetura de pastas de um projeto novo antes de iniciar codificação ou deploy. | `-L <nível>` (profundidade) &bull; `-I 'node_modules'` (ignora pastas) |
| `head` | Imprime as primeiras linhas de um arquivo de texto (padrão: 10 primeiras linhas). | Inspecionar cabeçalhos de arquivos CSV, licenças ou os primeiros metadados de um script. | `-n <qtd>` (define a quantidade exata de linhas a exibir) |
| `tail` | Imprime as últimas linhas de um arquivo de texto (padrão: 10 últimas linhas). | Ler as últimas mensagens de erro registradas em arquivos de log de servidores e APIs. | `-n <qtd>` &bull; `-f` (acompanha atualizações em tempo real) |
| `realpath` | Converte qualquer caminho relativo, com symlinks ou pontos (`.`/`..`), no caminho absoluto canônico. | Descobrir o local físico exato de um arquivo referenciado em scripts de build ou contêineres. | `-e` (exige que todos os elementos do caminho existam) |

---

### 🔍 Exemplos Práticos de `tree`, `head`, `tail` e `realpath`

#### 1. Limitando a visualização com `tree -L 2`

Em projetos web modernos (Node.js, Next.js, NestJS), a quantidade de subpastas pode poluir o terminal. Com o `tree -L`, limitamos a profundidade:

```bash
# Limita a listagem a 2 níveis abaixo do diretório corrente
$ tree -L 2 ~/cenario-web/projeto-legado
```

Saída esperada:

```text
/home/aluno/cenario-web/projeto-legado
├── .env.example
├── logs
├── public
│   └── index.html
└── src
    └── index.js

3 directories, 3 files
```

> [!TIP]
> Em projetos reais, evite listar a pasta `node_modules` adicionando o parâmetro `-I`:
> ```bash
> tree -L 2 -I 'node_modules|.git'
> ```

---

#### 2. Inspecionando Arquivos com `head` e `tail` sem Abrir Editores

Evite abrir arquivos pesados de log ou de configuração com o `nano` ou `vim` apenas para checar dados rápidos:

```bash
# Ver as 5 primeiras linhas de um arquivo de configuração
$ head -n 5 package.json

# Ver as últimas 20 linhas de um arquivo de log de produção
$ tail -n 20 logs/error.log

# Monitoramento contínuo em tempo real (essencial durante testes de endpoints HTTP):
$ tail -f logs/access.log
```

---

#### 3. Resolvendo Caminhos Canônicos com `realpath`

Quando você está trabalhando em caminhos relativos cheios de `../` ou lidando com pastas vinculadas por links simbólicos:

```bash
# Converte o caminho relativo no caminho absoluto real em disco
$ realpath ../projeto-legado/src/../public/index.html
# /home/aluno/cenario-web/projeto-legado/public/index.html
```

---

## 📌 Próximos Tópicos da Disciplina

- 📖 [**1.1 &bull; Primeiros Comandos e Produtividade**](../1-terminal-e-sistema-de-arquivos/) &ndash; Identificação, flags, atalhos de terminal e histórico.
- 📖 [**1.3 &bull; Manipulação de Arquivos e Pastas**](../3-manipulacao-de-arquivos-e-pastas/) &ndash; Comandos `touch`, `mkdir -p`, `cp`, `mv`, `rm`, wildcards e redirecionamentos.

---

<div align="center">
  <p>
    <a href="../1-terminal-e-sistema-de-arquivos/README.md">
      <img src="../../assets/icons/nav.svg" width="16" height="16" valign="middle" />
      &nbsp;Voltar ao Tópico 1.1
    </a>
    &nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="../README.md">
      <img src="../../assets/icons/book.svg" width="16" height="16" valign="middle" />
      &nbsp;Módulo 04 (Linux)
    </a>
    &nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="../../README.md">
      <img src="../../assets/icons/calendar.svg" width="16" height="16" valign="middle" />
      &nbsp;Índice Geral do Curso
    </a>
  </p>
</div>
