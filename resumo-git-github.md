# Resumos git e github

*Repositório para armazenar resumos sobre git e github do curso de 
versionamento de código.*

# Resumos das aulas
## Configurações Iniciais
*Usados apenas ao usar o git em uma maquina*
|***Comando*** |***Resumo***|
|:---|:---|
|`git config --global user.name` |Define o nome que será associado aos seus commits|
|`git config --global user.email`|Define o email que será associado aos seus commits|


## Iniciar Projetos
*Estes comandos são usados para versionar um projeto*
|***Comando*** |***Resumo***|
|:---|:---|
|`mkdir`|Cria uma nova pasta no diretório atual|
|`git touch`| Cria um ou mais de um arquivo vazio no diretório atual|
|`git init`  |Inicia um novo Repositório no git no diretório atual  
|`git clone` |Cria uma cópia exata de um Repositório remoto para a sua maquina local|

## Fluxo de Trabalho
*Para fazer alterações, os mais usados no dia a dia*
|***Comando*** |***Resumo***|
|:---|:---|
|`git status`|Mostra o estado atual do seu diretório|
|`git add` |Adiciona um arquivo modificado a Staging Area|
|`git add .`|Adiciona todos os arquivos modificados a Staging area|
|`git commit -m"mensagem"`|Salva permanentemente as alterações da Staging Area, a mensagem é obrigatória e deve descrever oque foi feito|
|`git diff`|Mostra as diferenças exatas entre oque foi modificado nos arquivos e oque está salvo ultimo commit|
|`git rm`|Remover arquivos de um reposiório|
|`rm -rf .git`|Reverte o git init do diretório atual e os commits feitos no diretório em questão|
|`git mv`|Renomeia arquivos de um diretório ou o nome do próprio diretório| 

## Trabalhando com Branches
*Trabalhar em novas funcionalidades de forma isolada*
*Correções de bugs de forma isolada*|
|***Comando*** |***Resumo***|
|:---|:---|
|`git branch` |Lista as branches existentes no seu Repositório|  
|`git branch [nome-da-branch]` |Cria uma nova branch|
|`git checkout [nome-da-branch]`|Muda para a branch especificada|
|`git merge [nome-da-branch]`|Junta e mescla as alterações da branch especificada a branch atual|

## Colaborando com Repositórios Remotos
*Sincronizar trabalho pessoal com de outros desenvolvedores*
|***Comando*** |***Resumo***|
|:---|:---|
|`git remote -v`|Lista os Repositórios remotos configurados para os projetos|
|`git fetch`|Baixa as atualizações de um Repositório remoto, mas não integra ao trabalho local|
|`git pull`|Baixa as atualizações do Repositório remoto e tenta mesclar elas a branch atual|
|`git push`|Envia os commits locais para um repositório remoto|

## Visualizando o histórico
*Explorar o passado do projeto em questão*
|***Comando*** |***Resumo***|
|:---|:---|
|`git log`|Mostra os histórico de commits da branch atual do mais recente ao mais antigo|
|`git log --oneline`|Para um visualizção mais compacta|
|`git log --graph --oneline --all`|Para ver o histórico de todas as branches de forma gráfica|

```mermaid
flowchart TD
    subgraph INI[🔹 Inicialização]
        A[git init]
        B[git clone URL]
    end

    subgraph COM[📝 Commit]
        C[git status]
        D[git add .]
        E[git commit -m 'msg']
        F[git log --oneline]
    end

    subgraph BR[🌿 Branch]
        J[git branch]
        K[git branch nome]
        L[git checkout nome]
        M[git merge nome]
    end

    subgraph REM[☁️ Repositório Remoto]
        G[git remote add origin URL]
        H[git push -u origin main]
        I[git pull origin main]
    end

    %% Fluxo principal
    A --> C
    B --> C
    C --> D --> E --> F
    E --> G --> H --> I

    %% Branch connections
    E --> J --> K --> L
    L --> M
    M --> E


