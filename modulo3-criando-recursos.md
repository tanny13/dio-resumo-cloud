# Módulo 3
*Este resumo contém o conteúdo do módulo 3, é abordado como criar e configurar o EC2 com sistema operacional Linux e Windows,  o armazenamento s3, o que é um serviço serveless, e o AWS lambda.*
## Guia rápido: Conexão em instâncias EC2 (Linux x Windows)

##  Linux (Amazon Linux / Ubuntu)
- [ ] Criar instância EC2 e selecionar uma **chave `.pem`** existente ou nova.  
- [ ] Garantir que a **porta 22 (SSH)** esteja liberada no Security Group.  
- [ ] Baixar a chave `.pem` (se nova).  
- [ ] Usar cliente SSH (MobaXterm, Git Bash ou terminal) para conectar:  
  ```bash
  ssh -i "minha-chave.pem" ec2-user@<IP-PÚBLICO>
- [ ] Acessar direto com usuário padrão (ec2-user, ubuntu, etc).
- [ ] Conectado!
      
## Windows Server
- [ ] Criar instância EC2 e selecionar uma chave .pem existente ou nova.
- [ ] Garantir que a porta 3389 (RDP) esteja liberada no Security Group.
- [ ] Baixar a chave .pem (se nova).
- [ ] No console AWS, usar a opção "Get Windows Password" para descriptografar a senha do Administrator com sua chave .pem.
- [ ] Abrir o cliente RDP do Windows e conectar com:
- [ ] Usuário: Administrator
- [ ] Senha: (a que foi descriptografada)
- [ ] Conectado!

| **Característica**        | **Linux (Amazon Linux / Ubuntu)**                 | **Windows Server**                                  |
|----------------------------|--------------------------------------------------|---------------------------------------------------|
| **Forma de acesso**        | SSH (porta 22)                                   | RDP (porta 3389)                                   |
| **Usuário padrão**         | `ec2-user`, `ubuntu`, etc.                       | `Administrator`                                    |
| **Autenticação inicial**   | Chave `.pem`                                     | Senha gerada automaticamente (criptografada)       |
| **Passo extra**            | Nenhum                                           | Precisa descriptografar senha usando chave `.pem`   |
| **Security Group padrão**  | Porta 22 (SSH) aberta                            | Precisa liberar porta 3389 (RDP)                   |
| **Experiência inicial**    | Login direto com chave                           | Precisa descriptografar senha + RDP client         |


## Amazon S3 (Simple Storage Service)
* É um serviço de armazenamento em nuvem da AWS.
* Armazena dados em objetos dentro de buckets (pastas virtuais).
* Altamente escalável, seguro e durável (99,999999999% de durabilidade 🤯).
###Casos de uso:
* Backup e recuperação de dados.
* Hospedagem de sites estáticos (HTML, CSS, JS).
* Armazenamento de arquivos (imagens, vídeos, logs).

## Serverless
* É um modelo de computação onde você não precisa gerenciar servidores.
* Você só escreve o código → a nuvem cuida da infraestrutura, escalabilidade e disponibilidade.
* Você paga apenas pelo uso (quando seu código roda, não pelo tempo ocioso).
* Exemplos de serviços serverless na AWS: Lambda, DynamoDB, API Gateway, S3 (quando usado para sites estáticos).

## AWS Lambda
* É o serviço serverless de execução de funções da AWS.
* Você escreve pequenas funções (em Python, Node.js, Java, etc) e o Lambda executa quando for chamado.
* Não precisa provisionar ou gerenciar servidores.
* Escala automaticamente → se 1 usuário ou 1 milhão chamarem sua função, o Lambda ajusta sozinho.
### Casos de uso:
* Processar uploads no S3 (ex: gerar miniaturas de imagens).
* Rodar APIs serverless junto com o API Gateway.
* Automação de tarefas (ex: reagir a eventos no DynamoDB, CloudWatch).

## AWS Lambda - Conceitos Importantes

| **Conceito**       | **Definição**                                                                 | **Exemplo Prático**                                                                 |
|---------------------|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| **Lambda Function** | O código que você escreve e armazena no serviço AWS Lambda.                  | Função em Python que processa imagens enviadas para o S3.                           |
| **Trigger**         | Evento que dispara a execução da Lambda Function.                           | Upload de arquivo no S3, requisição via API Gateway, agendamento no CloudWatch.     |
| **Runtime**         | Ambiente de execução que define a linguagem e versão suportada.             | Python 3.12, Node.js 20, Java 17.                                                   |
| **Execution Role**  | IAM Role (permissão) atribuída à Lambda para acessar recursos da AWS.       | Role com permissão `s3:GetObject` para ler arquivos em um bucket S3.                |

---

✨ **Resumo rápido:**  
- **Lambda Function** = o código.  
- **Trigger** = quem chama o código.  
- **Runtime** = onde o código roda.  
- **Execution Role** = o que o código pode acessar.  
