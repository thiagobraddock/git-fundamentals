# Git Fundamentals

Guia passo a passo para iniciantes no Git — configuração, fluxo de trabalho local, trabalho com repositório remoto (GitHub) e uma tabela de comandos essenciais.

> Este README foi escrito para alguém que nunca usou Git antes. Siga os passos na ordem indicada.

## 1. Pré-requisitos

- Ter o Git instalado. Verifique com:

```bash
git --version
```

- Ter uma conta no GitHub (https://github.com). Crie uma se necessário.

## 2. Configuração inicial do Git (uma vez por máquina)

Configure seu nome de usuário e e-mail — estes serão usados em todos os commits:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@example.com"
```

Verifique a configuração:

```bash
git config --global --list
```

Opcional: configure o editor padrão usado pelo Git (ex.: VS Code):

```bash
git config --global core.editor "code --wait"
```

Configure credenciais para que o Git lembre seu login (macOS recomenda usar o credential helper do sistema):

```bash
git config --global credential.helper osxkeychain
```

Para autenticação com o GitHub recomenda-se usar SSH ou um token pessoal (PAT). Exemplo rápido com SSH:

```bash
ssh-keygen -t ed25519 -C "seu.email@example.com"
# Em seguida copie o conteúdo de ~/.ssh/id_ed25519.pub para as chaves SSH do GitHub
```

## 3. Inicializando um repositório local (trabalho somente local)

Se você já tem uma pasta com arquivos e quer transformá-la em repositório Git local (sem remote):

```bash
cd /caminho/para/seu/projeto
git init
```

Isso cria a pasta oculta `.git`. Agora adicione os arquivos e faça o primeiro commit:

```bash
git add .
git commit -m "Primeiro commit: adiciona projeto"
```

Observação: tudo acima funciona 100% sem um servidor remoto. Você pode fazer commits, criar branches e voltar no histórico localmente.

Se quiser trabalhar com um repositório remoto (opcional) — por exemplo para backup, colaboração ou deploy — veja a seção "Trabalhando com remotes (opcional)".

## 4. Fluxo de trabalho básico (diário)

1. Atualize seu repositório local a partir do remoto:

```bash
git pull
```

2. Crie uma nova branch para trabalhar em algo:

```bash
git checkout -b minha-feature
```

3. Faça alterações nos arquivos. Quando estiver pronto, adicione e faça commit:

```bash
git add arquivo1 arquivo2
git commit -m "Descrição curta do que foi feito"
```

4. Envie sua branch para o remoto:

```bash
git push -u origin minha-feature
```

5. Abra um Pull Request (PR) no GitHub para revisar e mesclar sua branch na `main`.

## 5. Trabalhando com remotes

Adicionar um remoto chamado `origin` (quando você criou o repositório localmente e quer ligar ao GitHub):

```bash
git remote add origin git@github.com:usuario/repo.git
git push -u origin main
```

Ver remotes configurados:

```bash
git remote -v
```

## 6. Resolvendo conflitos simples

Quando `git pull` informa que há conflitos, abra os arquivos afetados, procure marcas como `<<<<<<< HEAD` e escolha a versão correta. Depois:

```bash
git add arquivo-resolvido
git commit
# (ou git commit -m "Resolve conflito em ...")
```

## 7. Boas práticas

- Faça commits pequenos e com mensagens claras.
- Use branches para features e correções.
- Sincronize frequentemente (`git pull`) para evitar muitos conflitos.
- Adicione `.gitignore` para arquivos que não devem ir ao repositório (ex.: `node_modules/`, `.env`, `*.log`).

## 8. Tabela dos principais comandos

| Comando | O que faz | Exemplo de uso |
|---|---:|---|
| `git init` | Inicializa um repositório Git local | `git init` |
| `git clone <url>` | Clona um repositório remoto | `git clone git@github.com:usuario/repo.git` |
| `git status` | Mostra o estado atual (arquivos modif./staged) | `git status` |
| `git add <arquivo>` | Adiciona arquivos ao índice (staging) | `git add README.md` |
| `git add .` | Adiciona todas as mudanças atuais | `git add .` |
| `git commit -m "mensagem"` | Cria um commit com as mudanças staged | `git commit -m "Corrige bug X"` |
| `git log` | Mostra histórico de commits | `git log --oneline --graph` |
| `git branch` | Lista branches locais | `git branch` |
| `git branch <nome>` | Cria uma nova branch | `git branch minha-feature` |
| `git checkout <branch>` | Muda para outra branch | `git checkout main` |
| `git checkout -b <branch>` | Cria e muda para nova branch | `git checkout -b minha-feature` |
| `git merge <branch>` | Mescla outra branch na atual | `git merge minha-feature` |
| `git pull` | Baixa e faz merge do remoto para local | `git pull origin main` |
| `git push` | Envia commits para o remoto | `git push origin minha-feature` |
| `git remote -v` | Mostra remotes configurados | `git remote -v` |
| `git reset HEAD <arquivo>` | Remove arquivo do staging (undo `git add`) | `git reset HEAD app.js` |
| `git revert <commit>` | Reverte um commit criando novo commit | `git revert abc1234` |
| `git reset --hard <commit>` | Volta o estado do branch para um commit (perigoso) | `git reset --hard abc1234` |
| `git stash` | Guarda temporariamente mudanças não commitadas | `git stash save "WIP"` |
| `git stash pop` | Restaura o último stash | `git stash pop` |

## 9. Exemplos rápidos (cenários)

- Criar um novo repositório local e subir para o GitHub:

```bash
mkdir meu-projeto
cd meu-projeto
git init
echo "# Meu Projeto" > README.md
git add .
git commit -m "Primeiro commit"
git remote add origin git@github.com:usuario/meu-projeto.git
git push -u origin main
```

- Atualizar seu branch `main` local com o remoto e aplicar mudanças:

```bash
git checkout main
git pull origin main
```

## 10. Recursos adicionais

- Documentação oficial do Git: https://git-scm.com/docs
- Guia interativo: https://learngitbranching.js.org/
- Ajuda do Git local: `git help <comando>` (ex.: `git help commit`)

---

Se quiser, eu posso:

- Adicionar um arquivo `.gitignore` inicial para o seu projeto.
- Traduzir este README para inglês.
- Incluir exemplos com GitHub Desktop ou VS Code.

Diga o que prefere.
