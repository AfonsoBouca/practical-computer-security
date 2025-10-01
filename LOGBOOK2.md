# CVE-2019-17558

## Identificação
- O CVE-2019-17558 é uma vulnerabilidade registada que afeta o Apache Solr 5.0.0 até 8.3.1, permitindo execução remota de código (RCE) via VelocityResponseWriter.
- O Apache Solr permaneceu vulnerável a um zero-day durante semanas após a publicação de código de prova de conceito (PoC) para o CVE-2019-17558.
- VelocityResponseWriter utiliza o Apache Velocity para formatar resultados de pesquisa através de templates, onde há possibilidade de execução de código malicioso.

## Catalogação
- Publicação: 2019-12-30.
- Está catalogada com um grau de gravidade alto: CVSS Base Score: 7.5 (v3.1).
- Tem uma probabilidade elevada de ser explorada: EPSS Score: 94.47%.

## Exploit
- Existe PoC público no Exploit-DB e um módulo Metasplot que automatiza o exploit.
- O módulo Metasploit explora o Solr (versão abaixo da 8.3.0) que, através de um HTTP POST request para a Config API, há a ativação do parâmetro _params.resource.loader_.
- O atacante identifica primeiro os nomes dos cores Solr disponíveis no alvo.
- É enviado um POST especialmente criado à Config API para ativar params.resource.loader=true no solrconfig.xml, permitindo o uso do parâmetro velocity em pedidos posteriores, o que pode conduzir a RCE.

## Ataques
- Pela pesquisa realizada, não foi encontrada nenhum relato pũblico de um ataque bem sucedido.
- Um potencial ataque permitiria um utilizador remoto executar código no servidor Solr e instalar backdoors e também permitiria roubar dados/documentos indexados pelo Solr.

## Correção/Contramedidas
- Atualizar para a patch oficial Apache Solr ou para versões ≥ 8.4, de forma a corrigir a vulnerabilidade.
- Desactivar ou restringir o acesso à Config API.
- Desativar VelocityResponseWriter ou restringir templates, garantir que _params.resource.loader.enabled _não está activo.
- A renderização de templates fornecidos por configset so é permitida se o configset for considerado _trusted_.

## Referẽncias
- https://www.cvedetails.com/cve/CVE-2019-17558/
- https://nvd.nist.gov/vuln/detail/CVE-2019-17558
- https://exchange.xforce.ibmcloud.com/vulnerabilities/173628
- https://www.tenable.com/blog/cve-2019-17558-apache-solr-vulnerable-to-remote-code-execution-zero-day-vulnerability
- https://www.exploit-db.com/exploits/48338
- https://www.extrahop.com/resources/detections/cve-2019-17558-apache-solr-exploit