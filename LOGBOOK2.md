# CVE-2019-17558

## Identificação
- Remote Code Execution (RCE) através do componente VelocityResponseWriter do Apache Solr.  
- Afecta as versões do Solr 5.0.0 até 8.3.1.  
- VelocityResponseWriter utiliza o Apache Velocity para formatar resultados de pesquisa através de um template, onde há possibilidade de execução de código malicioso.
- 

## Catalogação
- Publicação: 2019-12-30.
- Categoria de Vulnerabilidade: Execute code.
- CVSS Base Score: 7.5 (v3.1) and EPSS Score: 94.47%.
- Inicialmente como um Zero-day Vulnerability.

## Exploit
- PoC públicos no Exploit-DB que visam Apache Solr através de templates Velocity maliciosos.  
- Os exploits são frequentemente usados como Remote Code Execution (RCE), ou seja, a execução de comandos Java.  
- Exploit remoto via HTTP request, através do parâmetro "params.resource.loader.enabled".
- Exploit via configset.

## Ataques
- Exploração remota pode levar a takeover do servidor Solr.  
- Potencial para exfiltração de dados indexados.  
- Podia ser usado para pivot em infraestruturas internas.  
- Registos indicam exploits públicos.

## Correção/Contramedidas
- Atualizar para a patch oficial Apache Solr (versões corrigidas).  
- Remoção do _params resource loader_.
- A renderização de templates fornecidos por configset so é permitida se o configset for considerado _trusted_.

## Referẽncias
- https://www.cvedetails.com/cve/CVE-2019-17558/
- https://nvd.nist.gov/vuln/detail/CVE-2019-17558
- https://exchange.xforce.ibmcloud.com/vulnerabilities/173628
- https://www.tenable.com/blog/cve-2019-17558-apache-solr-vulnerable-to-remote-code-execution-zero-day-vulnerability
