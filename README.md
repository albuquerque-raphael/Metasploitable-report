README.md

```markdown
# Relatório Lab — Nmap, Medusa e John The Ripper

**Autor:** Raphael Cordeiro Cavalcanti de Albuquerque  
**Curso:** Santander Cyber Segurança DIO 2025 — Ethical Hacking  
**Data:** 24/10/2015  
**Instrutora:** Isadora Ferrão  
**Ambiente:** Kali Linux 2025.3 (atacante) | Metasploitable2 (alvo)  
**Rede:** Host Only  

---

## Descrição
Este repositório contém o relatório técnico e as evidências do teste de intrusão ético realizado em ambiente laboratorial controlado, com foco em:
- Mapeamento de rede (`nmap`)
- Ataque de força-bruta controlado (`medusa`)
- Quebra de hashes (`John The Ripper 1.9.0 Jumbo`)

O relatório documenta passo a passo o processo, resultados e recomendações de mitigação.

---

## Estrutura
DOCUMENTATION.md → relatório técnico completo
README.md → resumo e contexto
.gitignore → exclusões de logs, wordlists e evidências sensíveis
nmap_results/ → varreduras Nmap
medusa_results/ → resultados do Medusa
hashes/ → hashes e saídas do John (privado ou sanitizado)
screenshots/ → imagens do teste (recomendado: privado)

yaml
Copiar código

---

## Aviso Legal
> Este projeto tem fins **estritamente educacionais**.  
> Todos os testes foram realizados em ambiente controlado e autorizado.  
> O uso não autorizado desses procedimentos em sistemas de terceiros é ilegal.