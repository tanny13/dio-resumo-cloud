# Aula sobre criação de grupos e adição de usuários 



*Nesta aula é abordado um pouco sobre politicas de permições, criação de grupos de usuários no console na AWS, e adição de usuários nos grupos, utilizando um lista de arquivo csv atraves do terminal bash do git e com scrip padronizado.*



* Para configurar o acesso atraves do cmd o git bash, é necessário criar uma chave de acesso no AWS, essa chave a chave de acesso secreta e a região seram necessário para configurar o acesso na AWS por meio do CLI.

### O comando para configurar o acesso por meio do terminal bash do git

`AWS configure` 

### Será solicitado:

* `AWS Access Key ID`

* `AWS Secret Access Key`

* `Default region name` *Neste caso foi utilizado o us-east-2*

* `Default output format [json]:` Json



## Criação de grupos e Usuários



* É recomendado que ao criar um acesso para um usuário novo adcioná-lo a um grupo no qual defina-se politicas de permições relacionadas ao setor ou área de trabalho, também recomenda-se que a permissão IAMUserschancePassword seja inclusa, pois no primeiro acesso o usuário novo terá que modificar a sua senha tornando-a pessoal e confidencial.

* Para automatizar a criação e adição de usuários nos grupos, recomenda-se a criação de arquivo CSV com nome do usuário, grupo de trabalho e senha padrão para otimização, na AWS a senha precisa ter no minimo oito caracteres, sendo composta por letra maiúscula, maiúscula, número e caracteres especiais.

* Para a adição de usuários aos grupos pode se utilizar um arquivo com o script padrão para facilitar e agilizar o processo.


## Script para executar o arquivo csv com a lista de usuários e o arquivo sh com o script para criar usuários e adcioná-los aos grupo no AWS



`bash scriptIAM.sh usuarios.csv` 

* *`scriptIAM.sh` *é o nome do arquivo que contém o script*

* `usuarios.csv` *é o nome do arquivo que contém a lsita de novos usuários*



## Script para criar usuários e adcioná-los nos grupos



`#!/bin/bash`



### Verifica se o argumento de entrada (nome do arquivo) foi fornecido

`if [ -z "$1" ]; then`

`&nbsp;   echo "Por favor, forneça o arquivo CSV como argumento."`

`&nbsp;   exit 1`

`fi`



### Armazena o nome do arquivo de entrada em uma variável

`INPUT="$1"`



### Verifica se o arquivo de entrada realmente existe no diretório

`if [ ! -f "$INPUT" ]; then`

`&nbsp;   echo "$INPUT arquivo não encontrado"`

`&nbsp;   exit 1`

`fi`



### Verifica se o utilitário dos2unix está instalado, pois é necessário para compatibilidade

`command -v dos2unix >/dev/null || { echo "utilitário dos2unix não encontrado. Por favor, instale dos2unix antes de executar o script."; exit 1; }`



### Converte o arquivo CSV para o formato Unix para evitar problemas de quebra de linha

`dos2unix "$INPUT"`



### Loop para ler cada linha do arquivo CSV e processar as informações

`while IFS= read -r line || \[ -n "$line" ]; do`

`&nbsp;`   

`&nbsp;`  
### Separa as informações usando o delimitador ';' e atribui a variáveis

`&nbsp;   usuario=$(echo "$line" | cut -d';' -f1)`

`&nbsp;   grupo=$(echo "$line" | cut -d';' -f2)`

`&nbsp;   senha=$(echo "$line" | cut -d';' -f3)`



`&nbsp;   echo "Processando usuário: $usuario..."`



`&nbsp;`   
### 1. Cria um usuário no IAM

`&nbsp;   aws iam create-user --user-name "$usuario"`

`&nbsp;`   

`&nbsp;`   
### 2. Define uma senha e solicita a redefinição no próximo login

`&nbsp;   aws iam create-login-profile --password-reset-required --user-name "$usuario" --password "$senha"`

`&nbsp;`   

`&nbsp;`   
### 3. Adiciona o usuário ao grupo especificado

`&nbsp;   aws iam add-user-to-group --group-name "$grupo" --user-name "$usuario"`



`done < "$INPUT"`



`echo "Usuários importados com sucesso."`



