# Redes na AWS

## VPC (Virtual Private Cloud)

* É uma rede virtual isolada dentro da AWS onde se hospeda os recursos (EC2, RDS, Lambda, etc).
* Funciona rede privada pessoal na nuvem, onde o usúario contola os endereços IP, subnets, roteadores, firewalls e gateways.

### Principais características

* Isolamento: cada VPC é isolada das outras por padrão.
* Customização
* O bloco CIDR (faixa de IPs, ex: 10.0.0.0/16).
* Quantas subnets terá? e se são públicas ou privadas.
* Se terá acesso à internet (via Internet Gateway).
* Segurança: usa Security Groups (firewalls por instância) e Network ACLs (firewalls por subnet).
* Escalabilidade: suporta múltiplas AZs (disponibilidade).

### Exemplo prático
*Imagine a criação de uma aplicação web na AWS*
* Criar uma VPC com rede 10.0.0.0/16.
* Definir duas subnets:
*Pública (10.0.1.0/24): hospeda um EC2 Web Server acessível pela internet*

*Privada (10.0.2.0/24): hospeda um RDS Database isolado da internet*

* Usar Internet Gateway para dar internet à subnet pública.
* Usar um NAT Gateway para que a subnet privada, baixar atualizações sem ficar exposta.

## Subnet na AWS

*Na AWS (dentro do serviço VPC – Virtual Private Cloud), uma subnet é uma sub-rede, ou seja, uma parte de uma rede maior que o usuário cria e organiza para hospedar recursos (como instâncias EC2, bancos de dados, etc.)*

* A VPC é como um bairro inteiro.
* A subnet é como uma rua dentro desse bairro.
* Dentro dessa rua, o usuário coloca suas casas/recursos (servidores, bancos, lambdas conectadas, etc).

### Tipos de Subnet

* Subnet Pública

*Conectada à internet via Internet Gateway (IGW)*

*Instâncias dentro dela podem ter IP público.*

*Exemplo: EC2 de servidor web acessível pelo navegador*

* Subnet Privada

*Sem acesso direto à internet*

*Normalmente conectada à internet só através de NAT Gateway*

*Exemplo: Banco de dados ou servidores internos que não podem ser acessados de fora*

### Regras importantes

* Cada subnet fica em apenas uma Availability Zone (AZ), garantindo o isolamento e resiliência.
* Uma VPC pode ter várias subnets (públicas e privadas).
* O usuário define o intervalo de IPs (CIDR block) que cada subnet pode usar.

### Exemplo prático

* Criar uma VPC com rede 10.0.0.0/16.
* Dividir em duas subnets:
* 10.0.1.0/24 → Subnet Pública (EC2 Web Server com IP público).
* 10.0.2.0/24 → Subnet Privada (Banco de dados RDS sem internet).
* O web server fala com o banco de dados, mas só o web server está exposto à internet.

## Amazon security Group

* É um firewall virtual que controla tráfego de entrada (inbound) e saída (outbound)
* Associado a instâncias dentro de uma VPC.
* Atua no nível da instância, não da sub-rede (isso é função do NACL).

### Principais Características

* Stateful: Se o usuário permitir a entrada de um IP na porta X, a saída correspondente é automaticamente permitida, não há necessidade de criar regra de saída para responder à solicitação.
* Permissões apenas de ALLOW, não se cria regras para negar tráfego; tudo que não é permitido é negado por padrão.
* Associação múltipla: Uma instância pode ter vários Security Groups associados.
* Filtragem por protocolo, porta e IP: Permite definir regras específicas para TCP, UDP, ICMP, etc., e limitar o acesso a certos endereços IP ou intervalos.

### Regras do Security Group
* Inbound Rules (entrada): Define quem pode acessar a instância e por qual porta/protocolo.
Exemplo: permitir acesso SSH (porta 22) apenas do seu IP.
* Outbound Rules (saída): Define para onde a instância pode enviar tráfego.
Exemplo: permitir saída HTTP/HTTPS para qualquer lugar.



## Route 53

* Serviço de Domain Name System (DNS) da AWS.
*Conecta nomes de domínio (ex.: www.site.com) aos recursos da AWS ou externos (EC2, S3, ELB, IPs públicos, etc.).
* Nome “53” vem da porta padrão do DNS (TCP/UDP 53).

### Principais Funcionalidades

* Registro de Domínios: Você pode registrar novos domínios diretamente pelo Route 53.
* DNS Routing: Traduz nomes de domínio em endereços IP ou outros endpoints.
* Health Checks: Verifica se seus recursos estão online e redireciona tráfego se algum estiver fora.
* Traffic Flow (Roteamento inteligente): Permite rotear tráfego baseado em latência, geolocalização ou peso.
* Integração com AWS: Funciona de forma nativa com EC2, S3, CloudFront, ELB, etc.

### Tipos de Registro (Record Types)

* A: Nome → IPv4
* AAAA: Nome → IPv6
* CNAME: Nome → outro nome (alias)
* MX: Email servers
* TXT: Texto/Verificação (ex.: SPF, DKIM)
* Alias: Semelhante ao CNAME, mas permite apontar para recursos AWS diretamente (como S3 ou CloudFront) sem custo adicional.


## CloudFront

* Serviço de CDN (Content Delivery Network) da AWS.
* Distribui conteúdo estático e dinâmico (imagens, vídeos, HTML, APIs) globalmente.
* Usa Edge Locations para entregar conteúdo próximo do usuário, diminuindo latência.

### Principais Funcionalidades

* Distribuição de Conteúdo: Cópias do seu conteúdo são armazenadas em pontos estratégicos (Edge Locations).
* Cache: Conteúdo é armazenado próximo do usuário, reduzindo requisições ao servidor de origem.
* Integração AWS: Funciona nativo com S3, EC2, Lambda@Edge, API Gateway, Elastic Load Balancer.
* Segurança: Suporte a HTTPS, AWS Shield (proteção contra DDoS) e WAF (firewall de aplicações web).
* Lambda@Edge: Permite executar funções customizadas perto do usuário antes ou depois de servir o conteúdo.

### Como Funciona

* Usuário faz requisição ao site/API.
* CloudFront verifica o cache na Edge Location mais próxima.
* Se o conteúdo estiver em cache, entrega imediatamente.
* Se não estiver, busca do origem (S3, EC2, etc.), entrega ao usuário e salva em cache.

## Load Balancer
* Serviço que distribui automaticamente tráfego entre múltiplas instâncias (EC2, containers, etc.)
* Garante alta disponibilidade e escalabilidade do seu aplicativo.
* Na AWS, fica dentro do Elastic Load Balancing (ELB).

### Tipos de Load Balancer na AWS
* Application Load Balancer (ALB)
   * Funciona na camada 7 (HTTP/HTTPS).
   * Pode rotear tráfego baseado em URL, host, cabeçalhos ou parâmetros.
   * Ideal para aplicações web modernas e microserviços.
* Network Load Balancer (NLB)
   * Funciona na camada 4 (TCP/UDP).
   * Extremamente rápido, suporta milhões de conexões.
   * Ideal para aplicações com alto desempenho e baixa latência.
* Gateway Load Balancer (GWLB)
   * Roteia tráfego para appliances de rede, como firewalls ou sistemas de inspeção.
   * Funciona na camada 3/4.

### Principais Funcionalidades

* Distribuição de tráfego: evita sobrecarga em um servidor só.
* Alta disponibilidade: se uma instância falhar, o LB redireciona para outras saudáveis.
* Escalabilidade automática: funciona junto com Auto Scaling.
* SSL/TLS termination: pode gerenciar certificados e criptografia.
* Health checks: verifica se instâncias estão saudáveis antes de enviar tráfego.

## Resumo – AWS como uma cidade

* VPC (Virtual Private Cloud) → É o território da cidade. Você define os limites (CIDR block), ruas principais e decide quem pode entrar e sair. Tudo que você constrói (casas, prédios, empresas) existe dentro desse território.

* Subnet → São os bairros dentro da cidade.
   * Públicos: abertos para visitantes de fora (têm Internet Gateway).
   *  Privados: só moradores autorizados entram, e precisam de um “atalho” (NAT) para acessar a internet.

* Security Group → É a guarda municipal da cidade. Controla quem pode entrar em cada prédio ou casa.

   * Regras de entrada (Inbound) e saída (Outbound).
   * Stateful: se alguém entra, a resposta sai automaticamente sem precisar de regra extra.
   * Só permite o que você autoriza; tudo que não é permitido é bloqueado.

* Route 53 → É a central de endereços da cidade (cartório). Quando alguém procura sua empresa, o Route 53 traduz o nome em endereço correto (DNS → IP).
   * Pode registrar domínios, rotear tráfego e verificar se os serviços estão ativos (Health Check).
   * Permite rotear com base em latência, geolocalização ou peso.

* CloudFront → É o sistema de distribuição de correio expresso da cidade. Em vez de todo mundo ir até sua cidade para pegar encomendas, você espalha Edge Locations pelo mundo, entregando conteúdo mais rápido e com menos fila.

* Load Balancer (ALB/NLB) → É a rotatória ou semáforo inteligente que direciona o tráfego para diferentes ruas e bairros.

   * Garante que nenhuma rua fique congestionada e que todos trafeguem de forma equilibrada.
   * Realiza Health Checks para não mandar pessoas para prédios fechados.
   * Trabalha junto com Auto Scaling, equilibrando o fluxo de visitantes conforme a demanda.