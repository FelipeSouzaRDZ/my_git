# GIT

---

### [Install Git](https://git-scm.com/install/windows)

### [Documentação Git](https://docs.github.com/pt/get-started)

---

### Git - Install:

```bash

git config --global user.name "UsuarioGit"
git config --global user.email seuEmail@gmail.com
```



# Conectando GitHub a sua máquina via SSH

### **1. Usar chave SSH**

Essa é a opção mais segura pra trabalhar com o github

### Passo a passo:

1. **Verifique se já tem uma chave SSH:**

```bash
ls ~/.ssh/id_rsa.pub
```

1. **Se não tiver, crie uma:**

```bash
ssh-keygen -t ed25519 -C "felipesouza.rdz@gmail.com"
```

(Aperte Enter várias vezes para aceitar os padrões, caso queira mudar leia cada passo)

1. **Copie a chave pública:**

```bash
cat ~/.ssh/id_ed25519.pub
```

1. **Adicione a chave ao GitHub:**
    - Vá em https://github.com/settings/keys
    - Clique em **"New SSH key"**
    - Cole o conteúdo da chave
2. **Clone usando o SSH:**

```bash
git clone git@github.com:seu-usuario/nome-do-repo.git
```

> Exemplo:
> 

```bash
git clone git@github.com:felipesouza/meu-repo-privado.git
```

---

# Manuseando códigos e realizando commit com o git

Com o acréscimo do **Passo 0**, o ciclo de desenvolvimento do grupo está completo. Esta estrutura cobre desde o nascimento do repositório até a entrega segura de código em equipe, simulando exatamente o ambiente de desenvolvimento de uma empresa de tecnologia.

# 📖 Documentação de Fluxo de Trabalho Git & GitHub

Este documento estabelece o padrão de colaboração, organização de ramificações (*branches*) e resolução de problemas para o nosso projeto de grupo.

## 🏗️ Fase 1: Configuração Inicial (Apenas uma vez)

### Passo 0: Criação e Clonagem do Repositório

Para iniciar o projeto, um dos integrantes deve centralizar o código na nuvem e os demais devem baixar a estrutura.

1. **No GitHub:**
    - Crie um novo repositório público ou privado.
    - Marque a opção de adicionar um arquivo `README.md`.
2. **No Terminal (Todas as pessoas do grupo):**
    - Clone o projeto para a sua máquina local:

git clone <URL_DO_REPOSITORIO_AQUI>

   `* Entre na pasta criada:
     ```bash
cd nome_do_repositorio`

- Verifique as branches existentes (a branch atual estará destacada com um **asterisco** ):Bash
    
    ```
    git branch
    ```

- Lista TODAS as branches (locais e remotas)

    ```
    git branch -a
    ```
    

`### Passo 0.1: Criando o Ambiente de Desenvolvimento (`development`)
Para não mexermos direto na versão final (`main`), criaremos uma branch intermediária de laboratório. **Apenas um integrante realiza esse passo:**

* **Pelo site do GitHub:** Clique no menu que indica `main` no canto superior esquerdo, digite `development` e selecione *"Create branch: development from 'main'"*.
* **Aviso para o restante do grupo:** Após a criação na nuvem, os outros integrantes precisam rodar o comando abaixo para atualizar seus terminais locais:
```
git fetch origin
```

## 🛠️ Fase 2: O Ciclo de Desenvolvimento Diário (GitHub Flow)

As branches locais são rascunhos descartáveis. Siga estes 5 passos **sempre** que for iniciar uma nova tarefa.

 `[main / development] ──> Criar branch (feature/*) ──> Fazer código & Commits 
                                                                 │
 [Excluir branch local] <── Atualizar local <── Pull Request (GitHub) <── Push`

### 1. Sincronizar o computador

Antes de escrever código, mude para a branch `development` e baixe as atualizações mais recentes do grupo.

Bash

# 

```
git checkout development
git pull origin development
```

### 2. Criar a sua Branch de Trabalho

Nunca faça alterações direto na `development` ou na `main`. Crie uma ramificação para a sua tarefa usando o padrão de nomes estabelecido.

Bash

# 

```
git checkout -b feature/nome-da-sua-tarefa
```

### 3. Codificar e Salvar Progresso (Commits)

Trabalhe nos arquivos do projeto. Ao finalizar etapas lógicas, salve o progresso localmente:

Bash

# 

```
git status                     # Opcional: para ver quais arquivos foram alterados
git add .                      # Prepara todos os arquivos modificados
git commit -m "Tipo: Descrição curta da alteração"
```

### 4. Enviar para a Nuvem

Envie sua branch de rascunho para o GitHub:

Bash

# 

```
git push origin feature/nome-da-sua-tarefa
```

### 5. Abrir o Pull Request (PR) e Revisar em Equipe

1. Acesse a página do projeto no GitHub e clique no botão amarelo **"Compare & pull request"**.
2. **Atenção à Base:** Certifique-se de que o destino final (base) do PR seja a branch `development` e não a `main`.
3. Adicione uma descrição do que foi feito e solicite a revisão dos outros integrantes do grupo.
4. **Aprovação e Merge:** Após a revisão visual e validação do grupo, clique no botão verde **"Merge pull request"**.
5. No próprio site, clique no botão roxo **"Delete branch"** para limpar a nuvem.

### 6. Descarte Local (Manter a casa limpa)

Volte ao seu terminal, atualize seu laboratório e apague a ramificação antiga que já foi integrada:

Bash

# 

```
git checkout development
git pull origin development
git branch -d feature/nome-da-sua-tarefa or git branch -D feature/nome-da-sua-tarefa
```

## 🏷️ Padrão de Nomenclatura de Branches

Para manter o repositório organizado, as branches de trabalho devem seguir rigorosamente a tabela abaixo (utilizando letras minúsculas e hifens):

| **Prefixo** | **Finalidade** | **Exemplo de Uso** |
| --- | --- | --- |
| `feature/` | Desenvolvimento de novas funções, telas ou lógicas. | `feature/funcao-calculo` |
| `bugfix/` | Correção de erros ou falhas encontrados no código. | `bugfix/ajuste-loop-infinito` |
| `refactor/` | Melhorias visuais, limpeza ou otimização de códigos existentes. | `refactor/reorganizacao-funcoes` |

## ⚡ Guia de Comandos Rápidos ("Colinha" de Bolso)

Configure a estratégia padrão do Git no seu terminal uma única vez para evitar travamentos de divergência:

Bash

# 

```
git config --global pull.rebase false
```

### Fluxo diário resumido:

Bash

# 

```
# 1. Iniciar o dia atualizado
git checkout development && git pull origin development

# 2. Visualizar as branches (a atual fica marcada com asterisco)
git branch

# 3. Criar uma nova branch local para a tarefa
git checkout -b refactor/add_info_readme_02   

# 4. Permitir visualizar o status da branch (ver o que foi alterado)
git status

# 5. Adicionar as modificações para o salvamento
git add .

# 6. Implementar na árvore de dependências as modificações com uma mensagem explicativa
git commit -m "code review"

# 7. Subir a branch rascunho para o ambiente na nuvem (GitHub)
git push origin refactor/add_info_readme_02

# [PAUSA]: Aqui o grupo faz a revisão e o Merge visual no site do GitHub.

# 8. Retornar para a branch de desenvolvimento após o merge na nuvem
git checkout development

# 9. Atualizar a branch de desenvolvimento local com o código novo do grupo
git pull origin development

# 10. Agora sim, com segurança, deletar a branch local que já foi usada
git branch -D refactor/add_info_readme_02
```

## 🛡️ Gerenciamento de Crises: Resolução de Conflitos

O conflito de merge acontece quando duas pessoas modificam as mesmas linhas de um mesmo arquivo. Caso o GitHub aponte um conflito no seu Pull Request (como visto no exemplo prático do arquivo `README.md` na imagem_eeed60.png), adote o procedimento visual abaixo:

1. Na página do seu Pull Request no GitHub, clique no botão **"Resolve conflicts"**.
2. Analise os blocos de código delimitados pelas marcações do Git (`<<<<<<<`, `=======`, `>>>>>>>`).
3. Use os atalhos azuis da interface para decidir o resultado:
    - **`Accept current change`:** Mantém o código que **você** enviou na sua branch.
    - **`Accept incoming change`:** Mantém o código que já estava na branch base do grupo (`development` ou `main`).
    - **`Accept both changes`:** Mantém ambas as linhas de código, empilhando uma sobre a outra.
4. Clique em **"Mark as resolved"** no canto superior direito da tela de conflitos da imagem_eeed60.png.
5. Finalize clicando em **"Commit merge"** para destravar o Pull Request.

# No caso de terem definido a branch development como principal

Como você configurou a branch `development` como a **default** (padrão) do projeto no GitHub, o processo de levar tudo para a `main` muda apenas um pequeno detalhe na hora de criar o Pull Request, mas o conceito visual continua o mesmo.

Esse momento de migrar o código da `development` para a `main` é o que o mercado chama de **Release** (Lançamento da versão estável).

Aqui está o passo a passo exato de como vocês devem fazer isso direto pelo site do GitHub:

## Passo 1: O Pull Request de Lançamento (No GitHub)

Como a `development` agora é a sua branch padrão, quando você clicar para criar um novo Pull Request, o GitHub vai achar que você quer enviar código *para* a `development`. Vocês vão inverter isso manualmente:

1. Acesse a página principal do repositório no **GitHub**.
2. Clique na aba **Pull Requests** e depois no botão verde **New pull request**.
3. Agora vem o "pulo do gato" nas caixas de seleção de branches:
    - **base:** Altere para **`main`** (destino do código sagrado).
    - **compare:** Altere para **`development`** (onde o código pronto de vocês está).
4. O GitHub vai listar todas as alterações e commits que o grupo fez ao longo do projeto. Clique em **Create pull request**.
5. Dê um título claro, como: `Release v1.0 - Projeto Finalizado` ou `Entrega Final do Projeto`.
6. Clique em **Create pull request** novamente.

## Passo 2: A Revisão Final e o Merge

Como esse é o código que o professor (ou o cliente) vai avaliar, é uma boa prática que os **3 integrantes do grupo olhem esse PR juntos** (pode ser numa chamada ou na mesma mesa) para garantir que está tudo certo.

1. Estando todos de acordo, clique no botão verde **Merge pull request** e depois em **Confirm merge**.
2. **⚠️ ATENÇÃO:** Desta vez, **NÃO clique no botão "Delete branch"** que aparece após o merge. A branch `development` não deve ser apagada, pois ela continuará sendo o laboratório de vocês caso precisem atualizar o projeto no futuro (versão 2.0, correção de bugs pós-entrega, etc.).

## Passo 3: Atualizando as máquinas locais (No Terminal)

Agora que a `main` lá no site do GitHub recebeu todo o projeto, vocês precisam atualizar os computadores de vocês para que a `main` local fique idêntica à da nuvem.

Todos os integrantes do grupo devem rodar estes comandos no terminal:

Bash

# 

```
# 1. Vá para a branch main local
git checkout main

# 2. Baixe o projeto finalizado da nuvem para o seu PC
git pull origin main
```

Pronto!
