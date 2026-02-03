# Lab Report: Network Mapping & Credential Auditing 🛡️
 
![Cybersecurity](https://img.shields.io/badge/Area-Offensive_Security-red)
![Tools](https://img.shields.io/badge/Tools-Nmap%20%7C%20Medusa%20%7C%20JohnTheRipper-blue)
![Environment](https://img.shields.io/badge/Lab-Metasploitable2-orange)

## 📝 Descrição do Projeto
Este repositório documenta um teste de intrusão ético (Pentest) realizado em ambiente controlado. O foco principal foi simular o ciclo de vida de um ataque, desde o reconhecimento de ativos até a exploração de vulnerabilidades em serviços de rede.

O projeto faz parte da minha formação no **Santander Cyber Segurança DIO 2025**, sob orientação da instrutora Isadora Ferrão.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
* **SO Atacante:** Kali Linux 2025.3
* **SO Alvo:** Metasploitable2 (Host Only Network)
* **Reconhecimento:** `Nmap` (Service Enumeration & OS Detection)
* **Brute Force:** `Medusa` (Remote Authentication Auditing)
* **Cryptography:** `John The Ripper 1.9.0 Jumbo` (Hash Cracking)

---

## 🚀 Fases do Laboratório

### 1. Reconhecimento (Footprinting)
Utilização do **Nmap** para identificar portas abertas e versões de serviços vulneráveis, permitindo o mapeamento da superfície de ataque do alvo.

### 2. Auditoria de Credenciais
Simulação de ataque de força-bruta via **Medusa** para validar políticas de senhas fracas em serviços ativos.

### 3. Quebra de Hashes (Cracking)
Uso do **John The Ripper** para processar e quebrar hashes extraídos, demonstrando o risco de armazenamento inseguro de credenciais.

---

## 📂 Estrutura do Repositório
* `DOCUMENTATION.md`: Relatório técnico detalhado com evidências e recomendações.
* `nmap_results/`: Logs e saídas das varreduras de rede.
* `medusa_results/`: Resultados da auditoria de autenticação.
* `hashes/`: Arquivos sanitizados para demonstração de quebra de hash.

---

## ⚖️ Aviso Legal (Disclaimer)
Este projeto tem fins **estritamente educacionais**. Todos os testes foram realizados em ambiente laboratorial isolado e autorizado. O uso destas técnicas sem autorização expressa é ilegal e antiético.

---
**Contato:** [Seu Nome] - [Seu LinkedIn](SEU_LINK_AQUI)
