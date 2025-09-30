# Gerenciamento e governança na AWS

## AWS CloudWatch
* Responsável por monitorar os recursos da AWS, todas as aplicações executadas dentro da AWS
* Ao acessar a pagina do CloudWatch ja vai ser exibida automaticamente todas a métricas de todos os produtos que estão sendo utilizados
* Também é possível usar essas métricas para criar alarmes que notificam ou façam alterações automaticamente nos recursos que esta sendo monitorado
* Métricas: coleta e armazena métricas de serviços da AWS (EC2, RDS, Lambda, S3, etc.) e também de aplicações customizadas.
* Alarmes: você pode definir limites para métricas (ex.: CPU > 80%) e disparar ações automáticas (notificações no SNS, auto scaling, etc.).
* Logs: centraliza, armazena e analisa logs de aplicações, sistemas operacionais e serviços AWS.
* Dashboards: cria painéis visuais personalizados para acompanhar métricas e eventos.
* Eventos (EventBridge): detecta mudanças no ambiente e aciona respostas automatizadas (ex.: executar uma Lambda ao detectar erro).
* Insights: possui ferramentas para análise de logs (CloudWatch Logs Insights) e monitoramento de aplicações (CloudWatch Application Insights).

## AWS CloudTrail
* O CloudTrail é o serviço da AWS focado em auditoria, segurança e conformidade. Ele registra todas as ações feitas dentro da conta AWS — seja por usuários, serviços, aplicações ou pela própria AWS.
* Registro de atividades: grava quem fez o quê, quando, de onde e como (ex.: “usuário X iniciou uma instância EC2 às 15h”).
* Eventos de API: cada chamada de API (pela CLI, SDK, console ou serviço) é registrada.
* Logs: os registros ficam disponíveis no CloudTrail console, podem ser enviados para S3 e analisados com Athena ou CloudWatch Logs.
* Segurança: ajuda a detectar atividades suspeitas ou não autorizadas.
* Auditoria & compliance: facilita gerar relatórios para normas como ISO, GDPR, HIPAA etc.
* Insights: recurso extra que analisa automaticamente padrões incomuns de uso.

## AWS CloudFormation
* O AWS CloudFormation é o serviço da AWS usado para provisionar e gerenciar infraestrutura como código (IaC). Em vez de criar recursos manualmente no console, você descreve tudo em templates (YAML ou JSON), e o CloudFormation cuida de criar, configurar e atualizar automaticamente.
* Infraestrutura como código: descreve recursos como EC2, S3, RDS, VPC etc. em arquivos versionáveis.
* Automação: cria e atualiza ambientes inteiros com um único comando.
* Padrões reutilizáveis: você pode usar os mesmos templates para replicar ambientes (ex.: dev, teste, produção).
* Gerenciamento de dependências: ele entende a ordem de criação (ex.: cria a VPC antes das instâncias EC2).
* Stacks: os recursos são organizados em pilhas (stacks), fáceis de criar, atualizar e excluir.
* Rollback automático: se algo falhar, ele reverte para o estado anterior.

## AWS Identity and Access Management (IAM)
* O IAM é o serviço da AWS que cuida de identidade e controle de acesso. Ele define quem pode fazer o quê, em qual recurso, e de que forma dentro da sua conta AWS.
* Usuários: contas individuais para pessoas ou aplicações.
* Grupos: conjunto de usuários com as mesmas permissões.
* Funções (Roles): identidades temporárias usadas por serviços ou aplicações (ex.: uma Lambda acessando um bucket S3).
* Políticas: documentos em JSON que descrevem permissões (ex.: “permitir leitura em S3”).
* Autenticação multifator (MFA): camada extra de segurança para usuários.
* Princípio do menor privilégio: dar somente as permissões mínimas necessária

## AWS Policies e Roles
### AWS Policies
* São documentos em JSON que definem permissões (quem pode fazer o quê, em qual recurso e em quais condições).
* São anexadas a usuários, grupos ou roles.
* Tipos principais:
	* Managed Policies: prontas da AWS ou criadas por você, 	reutilizáveis.
	* Inline Policies: políticas únicas, criadas direto 	dentro de um usuário/grupo/role.
### AWS Roles
* São identidades de acesso temporário com permissões definidas por políticas.
* Diferente de usuários, não têm senha ou chave de acesso.
* São assumidas por:
	* Serviços AWS (ex.: Lambda acessando DynamoDB).
	* Usuários de outra conta AWS (cross-account access).
	* Aplicações que precisam de credenciais temporárias 	via STS.