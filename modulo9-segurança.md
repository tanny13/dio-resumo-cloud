# Segurança na AWS
*É Baseada em modelo de responsabilidade compartilhada, onde tanto a aws quanto os usuários têm papeis especificos*
## Práticas recomendadas de segurança na nuvem
### Controle de identidade e acesso (IAM)
* Use princípio do menor privilégio: dê apenas as permissões necessárias.
* Habilite MFA (autenticação multifator) para usuários sensíveis.
* Prefira roles em vez de usuários com chaves permanentes, especialmente para serviços.
* Revise permissões regularmente.
### Gestão de credenciais
* Nunca use credenciais padrão ou compartilhadas.
* Use AWS Secrets Manager ou SSM Parameter Store para gerenciar senhas e chaves.
* Rotacione credenciais e chaves periodicamente.
### Proteção de dados
* Habilite criptografia em repouso (S3, EBS, RDS) e em trânsito (TLS/HTTPS).
* Use KMS para gerenciar chaves de criptografia de forma centralizada.
* Faça backups regulares e valide a recuperação.
### Monitoramento e auditoria
* Use CloudTrail para registrar todas as ações na conta AWS.
* Use CloudWatch para monitorar métricas e criar alertas.
* Ative AWS Config para rastrear mudanças de configuração e compliance.
### Rede e perímetro
* Segmente recursos com VPCs, subnets privadas e públicas.
* Use Security Groups e NACLs para controlar tráfego.
* Evite expor recursos críticos diretamente à internet.
### Segurança de aplicações
* Atualize sistemas operacionais e dependências regularmente.
* Faça scans de vulnerabilidade.
*  Habilite logging de aplicações e análise de eventos suspeitos.
### Planejamento e resposta
* Tenha plano de resposta a incidentes.
* Teste recuperação de desastres periodicamente.

## Criptografia de dados na AWS
*A AWS oferece recursos para proteger dados em repouso, em trânsito e em uso, garantindo confidencialidade, integridade e conformidade.*
### Criptografia em repouso
* Amazon S3, EBS, RDS, DynamoDB, Redshift → suportam criptografia nativa.
* Pode ser feita com:
	* AWS Managed Keys (SSE-S3, SSE-KMS) → gerenciadas 	automaticamente.
	* Customer Managed Keys (CMKs via KMS) → você controla 	e rotaciona.
	* Server-Side Encryption (SSE) → AWS criptografa antes 	de salvar no disco.
	* Client-Side Encryption → o cliente criptografa antes 	de enviar.
### Criptografia em trânsito
* Usa TLS/SSL (HTTPS) para tráfego entre clientes e serviços.
* VPNs e Direct Connect também suportam criptografia para conexões de rede privadas.
* Certificados digitais podem ser gerenciados pelo AWS Certificate Manager (ACM).
### Criptografia em uso
* Nitro Enclaves: isolamento seguro para processar dados sensíveis.
* Confidential Computing: protege dados enquanto estão sendo processados (camada mais avançada).
### AWS Key Management Service (KMS)
* Serviço central de gerenciamento de chaves de criptografia.
* Permite criar, armazenar, rotacionar e auditar o uso de chaves.
* Integra-se com praticamente todos os serviços da AWS.
### Resumo final:
* Repouso → S3, EBS, RDS com KMS.
* Trânsito → TLS/SSL, VPN, ACM.
* Uso → Nitro Enclaves.
* KMS é o cérebro que gerencia tudo isso.

## AWS WAF: Firewall de aplicativos da web
### O que é?
* O AWS WAF é um firewall de aplicativos da web que protege suas aplicações contra ataques comuns da camada 7 (HTTP/HTTPS), como:
	* SQL Injection
	* Cross-Site Scripting (XSS)
	* Bots maliciosos e scraping
	* Exploração de vulnerabilidades conhecidas
### Como funciona?
* Você cria regras e condições (WAF Rules) que definem o que bloquear, permitir ou monitorar.
* Pode usar Managed Rules da AWS ou parceiros (já prontas para ameaças comuns).
* Funciona integrado com serviços como:
	* Amazon CloudFront (CDN)
	* Application Load Balancer (ALB)
	* API Gateway
	* AppSync
### Recursos principais
* Rate-based rules → limitam requisições de IPs suspeitos.
* Geo-blocking → restringe acesso por região geográfica.
* Bot Control → identifica e bloqueia tráfego automatizado.
* Visibilidade → integra com CloudWatch para monitoramento.
### Benefícios
* Proteção contra ataques da web sem precisar mexer no código da aplicação.
* Escalabilidade automática (acompanha o tráfego da AWS).
* Regras customizáveis + pacotes prontos.
* Reduz riscos de downtime e violação de dados.
### Resumo rápido:
*O AWS WAF é o escudo da camada de aplicação: fica entre a internet e sua aplicação, filtrando requisições maliciosas e deixando passar só tráfego legítimo.*