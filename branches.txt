Branch no Git

Uma branch é como uma linha do tempo paralela no seu projeto.
Ela permite que você trabalhe em novas funcionalidades ou correções sem mexer diretamente na branch principal (geralmente a main ou master).

🔹 Por que usar branches?

Trabalhar em novas features de forma isolada.

Corrigir bugs sem atrapalhar o código principal.

Colaborar em equipe sem bagunçar o repositório central.

Facilitar testes antes de integrar o código à branch principal.

| ***Comando***                    | ***Resumo***                                            |
| :------------------------------- | :------------------------------------------------------ |
| `git branch`                     | Lista todas as branches existentes                      |
| `git branch nome-da-branch`      | Cria uma nova branch                                    |
| `git checkout nome-da-branch`    | Muda para a branch especificada                         |
| `git checkout -b nome-da-branch` | Cria e já muda para a nova branch                       |
| `git merge nome-da-branch`       | Mescla a branch especificada na branch atual            |
| `git branch -d nome-da-branch`   | Deleta uma branch já mesclada                           |
| `git switch nome-da-branch`      | Alternativa moderna ao `checkout` para trocar de branch |
| `git switch -c nome-da-branch`   | Cria e muda para a nova branch (atalho)                 |

git checkout -b nova-feature
(cria e muda para a branch nova-feature)

git add .
git commit -m "Implementa nova feature"
(Faz alterações, adiciona e commita:)

git checkout main
(Volta para a branch main:)

git merge nova-feature
(Mescla as alterações da branch criada com a main)

git branch -d nova-feature
(Deleta a branch criada)
