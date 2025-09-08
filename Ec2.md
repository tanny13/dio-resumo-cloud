\# Maquinas virtuais( EC2), storage (EBS e S3) e backup (AMI, Snapshot) da AWS



\## EC2



\* EC2, são maquinas virtuais na aws podendo ser composta dos sistemas operacionais windows ou Linux, possuem cpu, memória, dico, rede e sistema operacional.

\* O EC2 é do tipo Iaas, infraestrutura como recursos, nesse caso o gerenciamento do maquina virtual é de responsabilidade do desenvolvedor/cliente.



\### Tipos de instâncias EC2

!\[imagem tipos de instancias EC2](assets/instancias-ec2.png)

\* Cada tipo de instâncias oferece diferentes recursos computacionais.

!\[imagem recursos instancias EC2](assets/tipos-instancias.png)



\## Storage



\### EBS

\* É uma storage que pode ser anexado em qualquer instância EC2, possui um volume de armazenamento, funciona como um HD externo.

\* Pode ser usado para armazenamento de banco de dados; MySQL, PostgreSQL, e oracle

\* Armazenar dados para app webs e logs de sistemas.



\### S3

\* É um serviço de armazenamento de objetos ou recursos em nuvem, ideal para armazenar de forma segura um grande volume de dados de forma escalável.



\## Backup



\### Criação e uso de imagens AMI

\* No EC2 o AMI é uma imagem de máquina virtual pré-configurada, inclui as informações necessárias para iniciar uma instância como o sistema operativo, o servidor de aplicações e as aplicações.

\* Pode ser criadas a partir de instâncias em execução ou paradas, permitindo capturar um instantâneo do seu ambiente configurado.

\* A AWS possui AMIs públicas e privadas e permite a criação de uma AMI personalizada.

\* É possível personalizar uma instância e em seguida criar uma AMI a partir dela, facilitando a replicação do ambiente de trabalho.



\### Snapshot (Backup)

\* É um serviço de backup nativo do AWS e faz backup dos volumes do EBS em um determinado momento.

\* É possível configurar e programar a frequência, o seu armazenamento é feito no S3.

\* A diferença entre uma AMI e uma Snapshot, é que uma AMI faz o backup de um servidor inteiro, incluindo todos os volumes EBS anexados, o Snapshot é uma cópia pontual de uma determinado volume do EBS e salvo no S3.







