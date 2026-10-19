<div align="center">

# <img src="../../assets/icons/04-linux.svg" width="30" height="30" valign="middle" /> 3. Manipulação de Arquivos e Pastas

### Pós-Graduação em Desenvolvimento Web com TypeScript e Inteligência Artificial &ndash; UTFPR
**Disciplina:** 04 &bull; Linux para Desenvolvedores e DevOps &nbsp;|&nbsp; **Módulo:** M01 &bull; Tópico 03

<br>

[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](#)
[![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](#)
[![Terminal](https://img.shields.io/badge/CLI-Terminal-4D4D4D?style=for-the-badge&logo=gnometerminal&logoColor=white)](#)
[![AI Prompt Lab](https://img.shields.io/badge/Prompt%20Lab-IA%20%2B%20Terminal-6A5ACD?style=for-the-badge&logo=probot&logoColor=white)](#)

</div>

---

## <img src="../../assets/icons/nav.svg" width="20" height="20" valign="middle" /> Sumário

- [📁 1.3 Manipulação de Arquivos e Pastas](#-13-manipulacao-de-arquivos-e-pastas)
  - [⚙️ Preparação do Cenário de Laboratório](#️-preparacao-do-cenario-de-laboratorio)
  - [💻 Comandos Utilizados na Aula](#-comandos-utilizados-na-aula)
    - [1. Acessando a Pasta de Trabalho](#1-acessando-a-pasta-de-trabalho)
    - [2. Criando a Estrutura de Pastas do Site em Cascata (`mkdir -p`)](#2-criando-a-estrutura-de-pastas-do-site-em-cascata-mkdir--p)
    - [3. Criando, Copiando e Movendo Arquivos (`touch`, `cp`, `mv`)](#3-criando-copiando-e-movendo-arquivos-touch-cp-mv)
    - [4. Exclusão Consciente e Localização (`rm`, `find`)](#4-exclusao-consciente-e-localizacao-rm-find)
    - [5. Limpeza dos Cenários (Opcional)](#5-limpeza-dos-cenarios-opcional)
- [🧪 Prompt Lab &bull; Comandos para Explorar com IA](#-prompt-lab--comandos-para-explorar-com-ia)
  - [📋 Prompt da Atividade](#-prompt-da-atividade)
  - [📊 Resposta Consolidada e Análise](#-resposta-consolidada-e-analise)
  - [🔍 Aprofundamento Prático: `stat`, `file` e `ln -s`](#-aprofundamento-pratico-stat-file-e-ln--s)
- [📌 Próximos Tópicos da Disciplina](#-proximos-topicos-da-disciplina)

---

## 📁 1.3 Manipulação de Arquivos e Pastas

Neste módulo, praticamos as operações fundamentais do ciclo de vida de arquivos e pastas no Linux: criação de estruturas em cascata, cópia de templates de configuração, movimentação e renomeação de código-fonte, remoção consciente e busca refinada por padrões e tipos.

### ⚙️ Preparação do Cenário de Laboratório

Para simular o fluxo de trabalho real de um desenvolvedor inicializando um projeto web a partir de templates, foi executado o seguinte comando composto:

```bash
mkdir -p ~/cenario-projeto/templates && echo "PORT=3000" > ~/cenario-projeto/templates/env.example && touch ~/cenario-projeto/app.temp.js && clear && echo "=== Cenário M01-T03 Criado com Sucesso ==="
```

> [!NOTE]
> **O que este comando realiza:**
> 1. `mkdir -p ~/cenario-projeto/templates`: Cria a pasta raiz do cenário e a subpasta `templates` em cascata.
> 2. `echo "PORT=3000" > ...`: Usa o redirecionamento de saída `>` para criar o arquivo `env.example` preenchido com a variável de ambiente.
> 3. `touch ~/cenario-projeto/app.temp.js`: Cria um arquivo de script temporário vazio.
> 4. `clear && echo ...`: Limpa o terminal e emite a notificação de ambiente pronto.

---

### 💻 Comandos Utilizados na Aula

#### 1. Acessando a Pasta de Trabalho

Navegação até o diretório raiz do laboratório recém-criado:

```bash
cd ~/cenario-projeto
```

---

#### 2. Criando a Estrutura de Pastas do Site em Cascata (`mkdir -p`)

Criação da árvore de diretórios do frontend e backend da aplicação em uma única linha:

```bash
mkdir -p meu-site/src meu-site/public/css
```

> [!TIP]
> A flag `-p` (*parents*) assegura que:
> - O diretório pai `meu-site/` seja criado caso ainda não exista.
> - O comando seja **idempotente** (não quebra nem gera erro se alguma das pastas já existir).

---

#### 3. Criando, Copiando e Movendo Arquivos (`touch`, `cp`, `mv`)

Ciclo de vida de arquivos do projeto: criação de documentação, cópia de template de ambiente e renomeação do ponto de entrada da aplicação.

```bash
# 1. Cria o arquivo de documentação vazio na raiz do site
$ touch meu-site/README.md

# 2. Copia o template de variáveis de ambiente para a raiz do site como um arquivo oculto (.env)
$ cp templates/env.example meu-site/.env

# 3. Inspeciona a pasta meu-site para confirmar a cópia e criação
$ ls -la meu-site
```

Saída esperada em `meu-site/`:
```text
drwxr-xr-x 4 aluno aluno 4.0K out 19 15:20 .
drwxr-xr-x 4 aluno aluno 4.0K out 19 15:20 ..
-rw-r--r-- 1 aluno aluno   10 out 19 15:20 .env
drwxr-xr-x 3 aluno aluno 4.0K out 19 15:20 public
-rw-r--r-- 1 aluno aluno    0 out 19 15:20 README.md
drwxr-xr-x 2 aluno aluno 4.0K out 19 15:20 src
```

```bash
# 4. Move e renomeia simultaneamente o arquivo temporário para dentro da pasta src/ com o nome server.js
$ mv app.temp.js meu-site/src/server.js

# 5. Confirma a movimentação dentro de src/
$ ls -la meu-site/src
```

Saída esperada em `meu-site/src/`:
```text
drwxr-xr-x 2 aluno aluno 4.0K out 19 15:20 .
drwxr-xr-x 4 aluno aluno 4.0K out 19 15:20 ..
-rw-r--r-- 1 aluno aluno    0 out 19 15:20 server.js
```

| Comando | Sintaxe | O que faz no exemplo |
| :--- | :--- | :--- |
| `touch` | `touch <arquivo>` | Cria um novo arquivo vazio ou atualiza o timestamp de acesso. |
| `cp` | `cp <origem> <destino>` | Copia `templates/env.example` preservando o original e criando `.env`. |
| `mv` | `mv <origem> <destino>` | Move `app.temp.js` da pasta raiz para `meu-site/src/` já renomeando para `server.js`. |

---

#### 4. Exclusão Consciente e Localização (`rm`, `find`)

Remoção pontual de arquivos e utilização do utilitário `find` para localizar recursos por extensão ou tipo:

```bash
# 1. Remove o arquivo README.md de meu-site/
$ rm meu-site/README.md

# 2. Localiza todos os arquivos com extensão .js recursivamente dentro de meu-site/
$ find meu-site -name "*.js"
# Saída: meu-site/src/server.js

# 3. Localiza apenas arquivos regulares (-type f) ignorando diretórios
$ find meu-site -type f
# Saída:
# meu-site/.env
# meu-site/src/server.js
```

> [!CAUTION]
> Ao usar `rm`, lembre-se de que não existe lixeira no terminal padrão. Verifique sempre o caminho antes de pressionar <kbd>Enter</kbd>.

---

#### 5. Limpeza dos Cenários (Opcional)

Ao finalizar os laboratórios práticos dos tópicos 2 e 3, remova as pastas de teste para manter sua home organizada:

```bash
rm -rf ~/cenario-web ~/cenario-projeto
```

> [!WARNING]
> A combinação `-rf` (*recursive + force*) remove diretórios e todo o seu conteúdo sem pedir confirmação. Tenha certeza absoluta de que os caminhos especificados são exatamente as pastas de teste.

---

## 🧪 Prompt Lab &bull; Comandos para Explorar com IA

<div align="center">
  <img src="../../assets/icons/12-ai.svg" width="32" height="32" valign="middle" />
  <h3>Laboratório Prático de Engenharia de Prompt</h3>
</div>

Para operações avançadas de auditoria de metadados, identificação de tipos reais de arquivos e criação de links simbólicos essenciais para esteiras de deploy contínuo (**CI/CD**).

### 📋 Prompt da Atividade

Copie o prompt estruturado abaixo e envie para o seu assistente de IA preferido (*ChatGPT, Claude, Gemini ou Copilot*):

> **Prompt:**  
> *"Atue como um especialista Linux focado em desenvolvimento web. Explique os comandos `stat`, `file` e `ln -s` no Ubuntu. Mostre: 1) O que faz cada comando; 2) Para que serve criar um link simbólico (`ln -s`) em deploys de aplicações web; 3) Como o comando `file` identifica o tipo real de um arquivo independentemente de sua extensão."*

---

### 📊 Resposta Consolidada e Análise

Abaixo está o resumo técnico estruturado resultante do laboratório:

| Utilitário | <img src="../../assets/icons/target.svg" width="16" height="16" valign="middle" /> O que faz? | <img src="../../assets/icons/code.svg" width="16" height="16" valign="middle" /> Exemplo de Uso Real (Dev Web) | <img src="../../assets/icons/tools.svg" width="16" height="16" valign="middle" /> Flag ou Opção Principal |
| :---: | :--- | :--- | :--- |
| `stat` | Exibe metadados detalhados de baixo nível (inode, blocos, permissões em octal, datas de acesso/modificação/change). | Auditar quando um arquivo de log ou certificado SSL foi alterado pela última vez. | `-c "%a %n"` (exibe permissão octal, ex: `644 .env`) |
| `file` | Analisa os *magic numbers* do cabeçalho do arquivo e determina seu tipo MIME real, ignorando a extensão. | Validar segurança em uploads de usuários (ex: garantir que um `avatar.png` não seja um script malicioso PHP/Bash). | `-b` (modo breve) &bull; `-i` (exibe o formato MIME type padrão) |
| `ln -s` | Cria links simbólicos (*symlinks*), que funcionam como atalhos transparentes apontando para outro arquivo ou pasta. | Apontar o diretório `current/` para a versão mais recente em deploys com zero *downtime*. | `-f` (força a sobrescrita de link existente) &bull; `-n` (trata diretório como arquivo normal) |

---

### 🔍 Aprofundamento Prático: `stat`, `file` e `ln -s`

#### 1. Inspecionando Metadados com `stat`

Enquanto o `ls -l` resume as informações, o `stat` exibe a radiografia completa do inode do sistema de arquivos:

```bash
$ stat meu-site/.env
```

Exemplo de saída detalhada:
```text
  File: meu-site/.env
  Size: 10          Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d  Inode: 1442019     Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/ aluno)   Gid: ( 1000/ aluno)
Access: 2026-10-19 15:20:10.000000000 -0300
Modify: 2026-10-19 15:20:10.000000000 -0300
Change: 2026-10-19 15:20:10.000000000 -0300
 Birth: 2026-10-19 15:20:10.000000000 -0300
```

> [!NOTE]
> Observe as três datas cruciais: **Access** (última leitura), **Modify** (última alteração de conteúdo) e **Change** (última alteração de metadados/permissões).

---

#### 2. Para que serve criar um link simbólico (`ln -s`) em Deploys Web?

A criação de links simbólicos (`ln -s`) é o pilar da estratégia de **Zero-Downtime Deployment** (deploys sem indisponibilidade).

Em servidores de produção (utilizando Nginx, PM2 ou Docker), a estrutura comumente adotada é:

```text
/var/www/meu-app/
├── releases/
│   ├── release-20261010-v1.0.0/
│   └── release-20261019-v1.1.0/
└── current -> /var/www/meu-app/releases/release-20261019-v1.1.0/
```

- O servidor web (ex: Nginx) sempre aponta para o diretório `/var/www/meu-app/current`.
- Quando uma nova versão fica pronta, o deploy simplesmente atualiza o ponteiro do symlink de forma atômica:

```bash
# Atualização atômica do link para a nova versão
ln -sfn /var/www/meu-app/releases/release-20261019-v1.1.0 /var/www/meu-app/current

# Em caso de bug em produção, o rollback é instantâneo:
ln -sfn /var/www/meu-app/releases/release-20261010-v1.0.0 /var/www/meu-app/current
```

---

#### 3. Como o comando `file` identifica o tipo real de um arquivo?

Ao contrário do Windows, o Linux não confia cegamente na extensão do arquivo (`.png`, `.jpg`, `.pdf`). O comando `file` lê os primeiros bytes do arquivo conhecidos como **Magic Numbers** (assinatura binária):

```bash
# Exemplo 1: Criando um script shell disfarçado com extensão .jpg
$ echo '#!/bin/bash\necho "exploit"' > avatar.jpg

# Inspecionando o arquivo:
$ file avatar.jpg
# Saída: avatar.jpg: POSIX shell script, ASCII text executable

# Exibindo o MIME Type exato (ideal para pipelines de upload em Node.js):
$ file --mime-type -b avatar.jpg
# Saída: text/x-shellscript
```

> [!IMPORTANT]
> Em aplicações web com upload de arquivos, **nunca** confie apenas no cabeçalho `Content-Type` enviado pelo cliente nem na extensão do arquivo. Utilizar verificações de assinatura mágica como o utilitário `file` previne ataques de Execução Remota de Código (*RCE*).

---

## 📌 Próximos Tópicos da Disciplina

- 📖 [**1.1 &bull; Primeiros Comandos e Produtividade**](../1-terminal-e-sistema-de-arquivos/) &ndash; Identificação, flags, atalhos e histórico.
- 📖 [**1.2 &bull; Navegação no Sistema de Arquivos**](../2-navegacao-no-sistema-de-arquivos/) &ndash; Comandos `pwd`, `cd`, `ls -lah`, `tree` e FHS.
- 📖 **2 &bull; Permissões, Logs e Editores** &ndash; Comandos `chmod`, `chown`, leitura de logs em `/var/log` e editores de texto no terminal.

---

<div align="center">
  <p>
    <a href="../2-navegacao-no-sistema-de-arquivos/README.md">
      <img src="../../assets/icons/nav.svg" width="16" height="16" valign="middle" />
      &nbsp;Voltar ao Tópico 1.2
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
