# CVE-2019-17558

## Identificação
- Remote Code Execution via VelocityResponseWriter in Apache Solr.  
- Afecta Solr 5.0.0 até 8.3.1.  
- Template Velocity renderizável permite execução de código arbitrário.  

## Catalogação
- Publicado: 2019-12-30; registado como RCE crítico.  
- CVSSv3: 9.8 (impacto elevado).
- Zero-day inicialmente; patches lançados posteriormente.  
- Registo público em NVD/CVE e advisories de fornecedores.

## Exploit
- PoC públicos no Exploit-DB (módulos para Solr).  
- Exploits permitem execução remota de comandos Java.  
- Alguns scanners detectam variações automatizadas.  
- Módulos Metasploit/PoC usam templates Velocity maliciosos.

## Ataques
- Exploração remota pode levar a takeover do servidor Solr.  
- Potencial para exfiltração de dados indexados.  
- Podia ser usado para pivot em infraestruturas internas.  
- Registos indicam exploits públicos.

## Correção/Contramedidas
- Aplicar patch oficial Apache Solr (versões corrigidas).  
- Desativar params.resource.loader.enabled ou VelocityResponseWriter.  
- Isolar instâncias Solr
