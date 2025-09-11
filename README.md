## ✅ Guia rápido: Conexão em instâncias EC2 (Linux x Windows)

###  Linux (Amazon Linux / Ubuntu)
- [ ] Criar instância EC2 e selecionar uma **chave `.pem`** existente ou nova.  
- [ ] Garantir que a **porta 22 (SSH)** esteja liberada no Security Group.  
- [ ] Baixar a chave `.pem` (se nova).  
- [ ] Usar cliente SSH (MobaXterm, Git Bash ou terminal) para conectar:  
  ```bash
  ssh -i "minha-chave.pem" ec2-user@<IP-PÚBLICO>
- [ ] Acessar direto com usuário padrão (ec2-user, ubuntu, etc).
- [ ] Conectado!
      
### Windows Server
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
