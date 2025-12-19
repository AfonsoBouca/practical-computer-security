# Public Key Infrastructures
## Tarefa 1
O objetivo desta tarefa é criar e analizar um certificado CA raíz. Assim seguimos as instruções do guião e criamos 2 ficheiros: **index.txt** e **serial**, contendo o segundo o valor 42.
Após isso copiamos o ficheiro de configuração de geração de certificados padrão **/usr/lib/ssl/openssl.cnf** e permitimos a criação de multiplos certificados com o mesmo sujeito.
Finalmente geramos o certificado com o comando da imagem 1 e ganhamos acesso aos ficheiros .

**Imagem 1:** Criação de um certificado raíz

![cretificate](/docs/logbook11/Task1_CA-gen.png)

Após gerar o certificado, utilizamos o seguinte comando para analizar o seu conteúdo.

```bash
openssl x509 -in ca.crt -text -noout
```

```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            2f:2c:8e:28:cc:80:2f:0a:d0:d3:fb:89:ab:0d:69:9a:2c:6d:32:b9
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: CN = www.modelCA.com, O = Model CA LTD., C = US
        Validity
            Not Before: Dec 10 09:36:45 2025 GMT
            Not After : Dec  8 09:36:45 2035 GMT
        Subject: CN = www.modelCA.com, O = Model CA LTD., C = US
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (4096 bit)
                Modulus:
                    00:a3:6d:df:d0:4d:db:e6:bb:14:96:9f:60:98:aa:
                    4d:97:35:05:4f:fb:29:38:b0:c2:c3:38:a6:6e:a1:
                    d0:5c:f1:fb:b6:f4:fd:1d:4e:ca:d8:83:e6:b9:a0:
                    d9:fd:7a:66:93:a3:ba:ef:0f:d2:8d:5e:dc:6f:3e:
                    d4:61:dc:e8:a9:77:25:fd:9d:95:1b:26:a5:c2:f1:
                    a7:68:ba:74:0a:da:0d:8c:be:09:86:27:09:bd:be:
                    3b:7a:41:72:8a:43:ad:5c:3b:21:16:42:68:46:f7:
                    c3:0b:5d:9f:f0:85:0e:98:76:6c:c8:48:6b:05:57:
                    90:a1:72:23:33:c2:8d:b2:1b:2d:94:82:f1:2e:4c:
                    1c:84:f6:44:15:7f:41:96:ea:41:71:66:70:a4:a7:
                    6c:3f:6d:e4:54:32:0e:48:82:21:ae:88:0b:b5:4e:
                    b0:03:e2:d2:2f:29:7b:4d:45:dd:c1:5d:0b:5b:28:
                    1f:3b:9e:aa:c1:a9:17:7d:a5:11:3c:d0:47:f8:a2:
                    8c:82:90:ca:ba:ad:52:23:89:52:58:b9:fc:54:33:
                    dd:ea:78:77:c6:3d:d4:4a:a7:4b:8f:3d:72:6f:9c:
                    6c:6d:ea:44:69:07:ed:02:7d:fc:d4:57:7b:91:db:
                    43:93:37:1f:1a:d5:3e:a3:a6:db:77:89:73:92:d3:
                    9f:b8:e3:8d:fd:7a:50:f9:3c:61:79:b1:b7:08:08:
                    c5:5a:b0:15:5e:e6:d8:c7:a2:11:eb:39:41:ec:c7:
                    d5:86:77:a9:a1:d0:e1:b2:c5:b3:70:06:4d:19:83:
                    35:67:0a:65:f2:b8:8a:d2:81:f2:d4:26:1a:36:38:
                    7c:ae:2b:1a:5a:98:a8:19:3d:62:5d:e0:02:3f:50:
                    0e:a7:de:13:9f:a5:09:a7:c3:af:60:07:b9:44:46:
                    46:dd:79:cc:94:33:fa:41:70:53:4b:4b:29:24:0d:
                    6e:79:78:de:17:45:56:e8:1d:63:60:19:1f:10:dc:
                    3a:55:ed:f5:ac:b3:29:89:42:94:55:d4:c4:74:3b:
                    21:44:c1:d8:44:c5:6d:fb:c1:c3:78:5e:78:f3:45:
                    c9:0a:33:d0:9d:5a:95:7d:fa:c7:a6:a7:4d:1b:f5:
                    06:5d:30:26:b2:2b:bb:9d:5a:34:1b:1b:9f:97:03:
                    40:7c:92:01:a0:ee:dd:e7:5d:7d:8b:56:ec:18:0f:
                    e7:79:36:88:23:d8:83:66:34:e5:b7:e7:f0:58:5c:
                    7a:78:4b:1b:5a:8e:1a:a5:eb:9a:ff:5f:88:98:8f:
                    6e:ab:f3:30:8b:56:3c:d3:de:00:d5:bc:2e:c5:3f:
                    4d:64:49:14:b3:f9:53:cb:63:c8:0e:e1:44:0d:f6:
                    0d:47:ab
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                54:6F:3A:27:B9:8D:CC:E6:FC:7B:61:8F:27:D2:0D:DC:AA:28:CF:87
            X509v3 Authority Key Identifier: 
                keyid:54:6F:3A:27:B9:8D:CC:E6:FC:7B:61:8F:27:D2:0D:DC:AA:28:CF:87

            X509v3 Basic Constraints: critical
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption
         6d:a8:ad:94:d9:ef:e5:8a:87:8b:e8:d4:af:1f:2d:77:a0:c8:
         14:7e:ec:f7:cf:66:b5:60:54:c9:2e:a8:97:f8:fe:79:47:61:
         bd:47:64:25:94:46:86:cf:84:1f:bf:c7:d4:b1:e0:5d:8a:c2:
         be:0e:99:69:59:a8:10:f4:75:b7:cc:07:6c:0b:2e:e3:32:6c:
         7a:5d:07:ee:3f:53:e6:ba:be:79:9e:6b:2c:38:f3:a8:4b:56:
         88:0e:b9:68:24:1b:b1:85:3e:64:77:32:c1:8a:d6:b7:1f:60:
         25:34:91:93:ef:e0:ed:e1:26:2e:59:98:95:ae:ae:2b:13:2c:
         0d:17:34:0f:bc:3d:ba:a4:f2:02:70:ad:db:36:53:4e:2b:4d:
         51:20:2d:17:99:9c:ed:f2:a3:da:29:7e:dc:c2:af:db:8a:31:
         5b:24:da:e4:bf:86:c7:ad:ed:13:68:0f:2d:6c:f5:a3:74:c0:
         89:76:74:3d:16:be:44:33:4b:41:e4:df:b6:55:a7:84:21:45:
         c5:16:02:37:73:b7:e0:b1:4f:cb:8a:75:db:08:7e:d3:c3:b7:
         39:b3:e8:34:20:b9:d9:73:2f:39:10:d1:e6:ff:26:c8:50:3e:
         eb:db:3a:9c:d3:35:44:e7:64:2e:c0:f1:49:fa:f3:00:ed:c0:
         09:78:e8:e5:5e:d5:c1:50:86:5c:21:a6:33:62:eb:22:f7:67:
         4d:24:aa:05:6f:ca:68:0a:e6:3f:31:39:35:04:31:a8:09:1d:
         5e:6b:33:3e:ac:34:e8:84:e3:0a:87:21:ac:85:be:f5:49:48:
         dc:ca:08:6d:27:24:d7:6f:4a:a8:b3:00:fa:8e:8b:f3:f8:f5:
         7b:bf:9c:9d:43:c6:2c:96:d9:12:66:43:e1:9e:e2:e8:14:99:
         0d:c6:03:f8:81:1b:c6:69:cf:10:7c:00:ce:c1:d6:66:d5:2f:
         04:e2:fa:24:ab:de:8c:f7:99:68:a7:a5:74:79:89:3a:bb:5f:
         45:de:f1:7a:65:98:8b:bf:64:de:17:5a:07:db:11:6c:ce:f6:
         04:3e:4a:8d:12:09:65:3a:75:ba:60:d1:62:eb:85:ca:0a:a1:
         83:b4:5b:81:43:1b:5b:97:a0:b1:93:1b:92:5f:f3:6e:f8:f2:
         fb:d2:93:62:5d:56:be:ba:cb:01:cf:ac:bf:0b:3e:c0:97:9b:
         60:e3:ff:ed:9e:08:c5:83:aa:cb:24:f3:89:c7:2b:cd:7b:39:
         12:48:41:cc:ab:45:ca:8a:fc:33:28:66:69:0f:65:8f:32:5b:
         45:f2:29:0c:1d:17:b5:51:45:ac:9b:45:5b:7b:f3:63:de:7b:
         4b:93:c9:99:cb:ba:9c:9e
```

A partir deste output podemos concluir que o certificado é uma **Certificate Autority** devido à extensão X509v3 Basic Constraints que está marcada como crítica:
```
    X509v3 Basic Constraints: critical
        CA:TRUE
```

A partir do certificado também comcluímos que é autoassinado devido a dois aspetos: 
- O **Issuer** é igual ao **Subject**;
- A **Subject Key Identifier** também é igual à **Autority Key Identifier**.

Estes dois fatores confirmam que se trata de um certificado raíz.

o certificado temos acesso aos parâmetros públicos do algoritmo RSA:

- Modulus (n), apresentado no campo Modulus;

- Public Exponent (e), apresentado como Exponent.

Estes valores são suficientes para realizar operações de encriptação e verificação de assinaturas RSA.

Para obter os restantes parâmetros do algoritmo RSA, necessários para desencriptação e assinatura, utilizámos o comando:
```bash
openssl rsa -in ca.key -text -noout
```

```
RSA Private-Key: (4096 bit, 2 primes)
modulus:
    00:a3:6d:df:d0:4d:db:e6:bb:14:96:9f:60:98:aa:
    4d:97:35:05:4f:fb:29:38:b0:c2:c3:38:a6:6e:a1:
    d0:5c:f1:fb:b6:f4:fd:1d:4e:ca:d8:83:e6:b9:a0:
    d9:fd:7a:66:93:a3:ba:ef:0f:d2:8d:5e:dc:6f:3e:
    d4:61:dc:e8:a9:77:25:fd:9d:95:1b:26:a5:c2:f1:
    a7:68:ba:74:0a:da:0d:8c:be:09:86:27:09:bd:be:
    3b:7a:41:72:8a:43:ad:5c:3b:21:16:42:68:46:f7:
    c3:0b:5d:9f:f0:85:0e:98:76:6c:c8:48:6b:05:57:
    90:a1:72:23:33:c2:8d:b2:1b:2d:94:82:f1:2e:4c:
    1c:84:f6:44:15:7f:41:96:ea:41:71:66:70:a4:a7:
    6c:3f:6d:e4:54:32:0e:48:82:21:ae:88:0b:b5:4e:
    b0:03:e2:d2:2f:29:7b:4d:45:dd:c1:5d:0b:5b:28:
    1f:3b:9e:aa:c1:a9:17:7d:a5:11:3c:d0:47:f8:a2:
    8c:82:90:ca:ba:ad:52:23:89:52:58:b9:fc:54:33:
    dd:ea:78:77:c6:3d:d4:4a:a7:4b:8f:3d:72:6f:9c:
    6c:6d:ea:44:69:07:ed:02:7d:fc:d4:57:7b:91:db:
    43:93:37:1f:1a:d5:3e:a3:a6:db:77:89:73:92:d3:
    9f:b8:e3:8d:fd:7a:50:f9:3c:61:79:b1:b7:08:08:
    c5:5a:b0:15:5e:e6:d8:c7:a2:11:eb:39:41:ec:c7:
    d5:86:77:a9:a1:d0:e1:b2:c5:b3:70:06:4d:19:83:
    35:67:0a:65:f2:b8:8a:d2:81:f2:d4:26:1a:36:38:
    7c:ae:2b:1a:5a:98:a8:19:3d:62:5d:e0:02:3f:50:
    0e:a7:de:13:9f:a5:09:a7:c3:af:60:07:b9:44:46:
    46:dd:79:cc:94:33:fa:41:70:53:4b:4b:29:24:0d:
    6e:79:78:de:17:45:56:e8:1d:63:60:19:1f:10:dc:
    3a:55:ed:f5:ac:b3:29:89:42:94:55:d4:c4:74:3b:
    21:44:c1:d8:44:c5:6d:fb:c1:c3:78:5e:78:f3:45:
    c9:0a:33:d0:9d:5a:95:7d:fa:c7:a6:a7:4d:1b:f5:
    06:5d:30:26:b2:2b:bb:9d:5a:34:1b:1b:9f:97:03:
    40:7c:92:01:a0:ee:dd:e7:5d:7d:8b:56:ec:18:0f:
    e7:79:36:88:23:d8:83:66:34:e5:b7:e7:f0:58:5c:
    7a:78:4b:1b:5a:8e:1a:a5:eb:9a:ff:5f:88:98:8f:
    6e:ab:f3:30:8b:56:3c:d3:de:00:d5:bc:2e:c5:3f:
    4d:64:49:14:b3:f9:53:cb:63:c8:0e:e1:44:0d:f6:
    0d:47:ab
publicExponent: 65537 (0x10001)
privateExponent:
    65:62:d7:73:71:a9:d7:44:fe:2b:c7:29:f4:eb:ca:
    00:e1:2a:af:88:9f:f5:04:6b:7f:12:d8:e5:4f:4b:
    65:2d:d5:bb:95:d6:a4:e4:e9:a0:52:8b:c3:63:0f:
    79:5a:02:e2:da:b3:30:75:bf:68:66:8e:18:11:81:
    4e:48:ee:a9:9b:3a:1d:51:32:5c:4a:a8:90:fc:bb:
    9f:93:f4:43:7b:2c:e6:c0:4a:46:48:57:99:b7:b7:
    4c:4b:e7:d3:f0:d2:4e:a2:7c:0f:44:19:4e:d5:8b:
    d1:b4:3e:71:c7:09:db:f9:b3:d8:b8:5c:74:4e:f3:
    71:c4:ce:23:e1:31:68:69:c5:e8:19:27:a8:52:1d:
    6b:3b:1f:d7:ba:3f:a5:71:24:32:46:9b:e0:f9:e0:
    84:a5:16:fe:48:a3:65:c6:1d:41:1a:33:31:42:64:
    9d:b4:8c:32:27:e8:cf:72:65:74:fc:d4:fb:b3:33:
    55:18:44:d4:a9:a2:e2:16:92:50:08:e2:6d:53:e2:
    19:69:db:ea:dd:75:54:88:6f:66:8d:d3:05:25:bc:
    29:26:9d:1f:85:e1:fa:82:38:b4:df:28:ec:26:bd:
    79:9e:d8:db:d3:c7:ec:40:de:a5:98:b4:17:33:50:
    83:b6:b1:7c:43:08:7e:1c:18:90:da:db:b1:1d:ca:
    3a:ba:2a:b5:56:8e:9b:2f:9a:f2:0b:21:d6:d9:d8:
    f0:cc:9b:0c:6b:2d:10:00:70:3f:e0:47:e6:68:e2:
    76:19:2a:14:4e:77:77:bb:7a:63:06:45:33:6d:bb:
    cc:f9:ad:16:79:05:70:fc:82:e0:f9:89:1f:c1:b7:
    d1:28:a1:ef:71:78:cc:72:41:2b:ed:21:d6:3d:71:
    79:75:7a:35:b5:b6:3a:26:2f:0b:d0:8b:01:e0:0f:
    c8:6f:76:6b:cf:bc:7b:0a:de:60:db:b6:b3:3d:e1:
    33:06:cc:45:02:fc:8c:b3:f9:0c:3c:69:9b:32:1d:
    4f:2f:d3:26:a5:ab:15:d8:67:a9:39:88:7e:90:48:
    03:cf:9d:5c:67:39:91:23:8a:2d:0f:db:e6:e3:ff:
    7b:27:33:db:8a:7c:c3:9f:d4:9f:be:d9:41:1b:af:
    62:80:28:93:09:4e:c8:d1:38:cd:86:46:b4:01:62:
    37:4f:75:5c:0a:02:a2:d0:db:77:37:a8:47:97:3d:
    9a:b0:0e:33:1d:0f:37:8f:62:af:6e:87:3b:43:f8:
    a9:fe:18:c3:0f:e2:a1:54:ac:1d:38:19:5c:87:f0:
    5e:3f:25:25:44:60:ec:3a:fd:cf:5d:92:73:c2:b5:
    fa:d6:fd:1d:ee:3b:3a:c6:97:11:d5:a4:be:2a:b4:
    bd:39
prime1:
    00:d4:ec:53:4c:d8:68:19:fe:57:c7:3e:ed:21:5d:
    94:6c:b2:be:4a:d1:e6:41:9c:ce:be:23:00:f3:a4:
    35:8e:f9:1e:5e:a6:77:34:99:9c:56:d9:6e:b5:cc:
    73:91:c6:7e:75:a3:05:b3:85:83:84:42:1d:27:cb:
    e5:1a:4d:ae:22:db:22:bd:6a:ca:29:b1:99:54:b0:
    08:a8:24:bf:5c:28:7c:d5:4a:59:a6:28:76:87:2e:
    dc:34:3a:a4:b6:12:08:99:d3:a9:94:9c:90:41:ca:
    62:6d:27:a3:48:35:90:a1:4a:ea:7d:c3:16:3a:1c:
    46:77:c4:c4:2f:45:a3:24:d1:69:6c:0f:15:e8:46:
    a6:90:a6:28:e1:c9:4c:16:09:f0:4d:a4:e5:50:18:
    84:30:4a:b1:ff:b3:e7:a2:73:89:4a:d6:f7:ff:c1:
    7c:c9:e2:86:3c:d4:02:0b:3b:63:bd:75:21:7f:5f:
    4d:74:16:5e:24:5d:e7:12:99:2c:87:c8:0a:9a:2b:
    5e:c1:90:33:22:7a:4c:ab:c9:6c:f6:5d:24:16:8d:
    5d:3a:4e:91:59:6e:1b:e0:17:66:8a:a7:e8:60:32:
    23:6d:57:67:e1:35:aa:6f:ec:68:a4:b3:c8:81:bb:
    75:53:51:a6:61:56:c7:fc:fe:10:1d:a6:27:68:74:
    7b:ef
prime2:
    00:c4:7e:2a:f2:80:fc:b0:ef:45:77:44:87:a9:10:
    73:0e:89:fe:51:ee:97:e6:1b:68:80:a3:53:de:5c:
    c8:0c:82:76:af:97:cc:24:94:1f:47:27:64:70:43:
    63:33:72:c0:f8:cd:34:06:c6:a4:37:78:17:96:24:
    97:c5:ee:be:75:a2:a9:b9:b0:b3:9a:38:9f:e4:2f:
    fa:3b:fc:78:20:8e:81:d0:ac:6d:9a:80:1b:dc:83:
    77:2e:10:da:9a:e6:a9:6f:f9:9a:bc:63:8a:f5:2d:
    3e:20:ee:28:fd:16:c3:f3:de:e1:d5:fb:3f:46:27:
    18:16:4f:98:45:d1:fb:5d:37:14:2b:b2:46:b6:7f:
    ff:3b:27:e5:51:c3:ac:f9:a6:32:7d:1c:5f:4f:e9:
    2f:79:bf:63:cc:d2:79:8c:0a:72:88:32:90:db:98:
    44:6c:6a:e6:90:86:c3:b6:ad:b8:25:ea:c6:0f:79:
    2f:75:7c:d2:73:90:b0:2b:f9:5e:74:ac:bc:b5:94:
    b3:26:ad:74:fc:eb:9b:e5:6a:b4:87:96:3a:54:45:
    2e:b8:00:37:25:70:2d:ca:b9:ca:d6:6f:82:71:bc:
    3a:0b:9c:39:09:db:e8:24:2d:35:0c:bd:56:a9:32:
    2a:51:6b:e7:14:e6:1b:35:c3:cd:8e:e4:54:3a:fa:
    e4:05
exponent1:
    69:a6:a6:22:c0:52:cf:6b:14:15:2a:95:31:74:24:
    bc:d6:e8:73:69:b9:8e:1f:07:ba:f2:d5:7b:0f:a4:
    ff:bf:7f:21:4a:0a:66:50:3e:72:1d:cb:c0:6b:a5:
    80:d4:f4:54:dc:c2:6c:74:b8:70:7c:f9:c8:90:74:
    aa:db:96:a7:77:02:c2:e8:65:4d:d0:f1:1b:43:89:
    d8:1c:fb:d2:f7:c8:11:71:a6:10:3b:8d:ac:c0:44:
    c5:a9:bf:a7:14:45:ae:46:87:a3:d5:18:03:7d:2f:
    df:a7:c6:6e:83:1d:b3:da:df:85:ed:b2:6e:bd:2e:
    fe:28:e5:8b:eb:4a:eb:6e:f9:97:83:d8:c3:fb:a2:
    94:ad:ce:25:52:e3:ed:1f:9b:5c:7b:90:c9:70:90:
    cf:01:91:57:26:e6:ae:06:14:3e:cd:72:1b:36:df:
    fb:b0:ea:18:ee:bd:e0:e2:e4:37:d3:11:ff:08:c3:
    fe:f1:46:5f:57:34:dc:56:a2:f0:f1:02:c9:c2:f1:
    6e:ac:65:a3:1a:fa:46:57:59:38:d9:b8:99:74:25:
    a9:53:e8:ed:6e:24:68:ca:53:b8:43:5e:9b:b4:e5:
    3d:51:1c:9b:74:2c:91:02:c6:5d:cb:53:97:83:f3:
    d0:96:f8:2e:de:87:b7:72:3d:7e:e8:be:2f:27:75:
    83
exponent2:
    00:a3:1d:ed:ff:34:cf:10:ff:00:d6:da:e0:17:9c:
    5d:37:73:9c:d9:5d:4d:62:2b:dc:9b:f5:7a:59:3d:
    02:a1:47:e8:c9:2a:25:c1:33:e9:a7:42:ef:61:36:
    bf:f2:64:d0:07:7b:2a:36:79:ce:b7:71:8d:7b:09:
    d3:a8:ef:e1:d2:7b:ff:93:f4:39:94:cc:6f:07:9a:
    40:8c:6d:b1:37:ad:b5:dc:8a:57:ce:8b:8d:15:89:
    59:75:b7:6e:12:6b:6b:bb:56:25:7b:40:d3:89:67:
    4e:8d:3d:c8:6f:19:e7:ff:da:45:f6:42:45:ab:b2:
    26:8f:d6:f1:9c:fc:8d:44:3b:c6:15:e4:40:49:9e:
    86:3e:10:87:91:51:f4:95:a6:bf:81:16:fd:94:b4:
    0a:c2:71:fc:a2:7b:13:86:0a:e2:3b:68:66:d2:b5:
    5c:0f:f8:ca:80:ae:2f:68:c6:5b:f9:b6:25:47:91:
    1d:b1:d5:b6:4b:53:90:bc:60:9e:66:13:43:f1:25:
    89:77:91:45:6d:f5:15:8c:e5:01:0b:11:ce:48:48:
    ca:58:db:6c:ec:3a:6c:f9:3f:35:40:c0:7f:34:75:
    c2:66:03:01:62:ca:d8:b2:b7:88:b3:93:b6:8e:6c:
    e3:ae:85:f9:e6:62:83:b2:25:62:ce:bd:83:a3:16:
    c6:15
coefficient:
    00:9d:75:ce:10:f9:ad:7e:ec:17:6f:6d:5e:b5:3b:
    c7:05:6b:26:dd:9b:26:73:8a:01:b8:eb:cf:3e:48:
    b5:49:75:c9:27:86:10:c3:b7:97:68:bc:7b:a6:ac:
    3c:91:bd:7b:1c:92:2f:c0:87:74:c6:45:02:9b:02:
    be:77:60:2c:83:96:30:a3:07:72:09:21:6f:f9:2a:
    43:52:61:49:0c:2a:2b:a3:b1:d8:76:09:03:e7:43:
    8c:09:c6:7d:9f:94:93:4f:22:e2:4a:19:85:0f:a9:
    4f:35:7f:16:7e:0d:3a:67:72:9c:b0:e5:c7:ee:f8:
    63:49:fb:0a:26:b8:fa:55:89:57:58:a9:da:97:cf:
    55:98:af:55:8f:b4:97:79:c9:b4:71:4b:b1:38:66:
    eb:94:97:60:88:ed:bd:8e:1e:3d:e4:1b:c0:a7:f4:
    ae:ae:19:25:85:b7:75:55:4d:a1:89:93:cc:b8:f2:
    96:7a:b7:99:cf:b6:d8:32:65:b2:2d:ea:ad:87:67:
    36:be:ee:f4:ae:de:a3:4a:d0:40:36:f2:77:28:42:
    a5:0b:7f:c9:bb:f4:19:ab:b1:5e:71:21:c3:db:3a:
    9b:1d:04:50:8a:a5:2d:9d:2b:4d:ea:5e:40:91:c3:
    40:12:32:f1:67:c4:36:28:0c:23:58:8e:a7:e4:b2:
    00:24

```
A partir deste output identificam-se os seguintes valores:

- Modulus (n): igual ao presente no certificado;
- Public Exponent (e): também disponível no certificado;
- Private Exponent (d): exponente privado;
- Prime1 (p): primo 1 utilizado para gerar o módulo;
- Prime2 (q): primo 2 utilizado para gerar o módulo.

## Tarefa 2
Nesta tarefa vamos obter um certificado público assinado pela nossa Certificate Authority (CA) para o website **www.bank32.com**, que tem nomes alternativos. Para tal, é necessário gerar um Certificate Signing Request (CSR), que contém a chave pública do servidor e a informação de identidade da entidade requerente, gerado através do seguinte comando:

```bash
openssl req -newkey rsa:2048 -sha256 \
    -keyout server.key -out server.csr \
    -subj "/CN=www.bank32.com/O=Bank32 Inc./C=US" \
    -addext "subjectAltName=DNS:www.bank32.com,DNS:www.bank32A.com,DNS:www.bank32B.com" \
    -passout pass:dees
```

## Tarefa 3
O objetivo desta tarefa é assinar o CSR gerado na tarefa 2.

Como o certificado contém uma extensão, é necessário adicionar ao ficheiro de configuração myCA_openssl.cnf a linha "copy_extensions = copy" para permitir que a extensão apareça no certificado final.

Com o ambiente preparado e as configurações corretas, executámos o seguinte comando para assinar o certificado:

```bash
openssl ca -config myCA_openssl.cnf -policy policy_anything \
-md sha256 -days 3650 \
-in server.csr -out server.crt -batch \
-cert ca.crt -keyfile ca.key
```

Após gerar o certificado, verificámos o seu conteúdo com o comando:

```bash
openssl x509 -in server.crt -text -noout
```

No output seguinte verifica-se que o Issuer é a CA criada por nós e que os nomes alternativos estão presentes:

## Tarefa 4

O objetivo desta tarefa é configurar um servidor Apache com suporte a HTTPS, utilizando o certificado público assinado pela nossa Certificate Authority (CA) na tarefa anterior.

Em primeiro lugar, utilizámos os comandos do Docker para criar, correr e obter um terminal num contentor. No terminal copiámos o certificado (server.crt) e a chave (server.key) para a pasta /certs no contentor e um ficheiro de configuração foi criado em /etc/apache2/sites-available/bank32_apache_ssl.conf com o seguinte conteúdo:

```apache
<VirtualHost *:443>
    DocumentRoot /var/www/bank32
    ServerName www.bank32.com
    ServerAlias www.bank32A.com
    ServerAlias www.bank32B.com
    DirectoryIndex index.html
    SSLEngine On
    SSLCertificateFile /certs/server.crt
    SSLCertificateKeyFile /certs/server.key
</VirtualHost>
```

Com a configuração completa, iniciámos o servidor com os seguintes comandos:
```bash
a2enmod ssl
a2ensite bank32_apache_ssl
service apache2 start
```

Antes de acedermos ao servidor a partir do navegador, tivemos que adicionar o certificado raiz da CA criado na tarefa 1 (ca.crt) à lista de certificados do navegador, pois, como é uma entidade certificadora privada, o navegador não a aceita por defeito.

Finalmente conseguimos aceder ao website, como vemos na imagem:

**Imagem 2:** www.bank32.com
![website](/docs/logbook11/task4_website.png)

## Tarefa 5
O objetivo desta tarefa foi demonstrar como a Infraestrutura de Chaves Públicas (PKI) consegue impedir ataques do tipo Man‑In‑The‑Middle (MITM), mesmo quando o atacante consegue intercetar o tráfego e apresentar um website falso através de HTTPS.

Nesta tarefa reconfiguramos o servidor anterior para impersonar o website www.example.com utilizando os mesmos certificados do www.bank32.com com o seguinte ficheiro:

```apache
<VirtualHost *:443> 
    DocumentRoot /var/www/bank32
    ServerName www.example.com
    ServerAlias example.com
    DirectoryIndex index.html
    SSLEngine On
    SSLCertificateFile /certs/server.crt
    SSLCertificateKeyFile /certs/server.key
</VirtualHost>
```

De seguida, para simular um ataque de envenenamento de DNS, foi alterado o ficheiro /etc/hosts da máquina da vítima, mapeando o domínio www.example.com para o endereço IP do servidor malicioso.

Ao tentar aceder ao endereço https://www.example.com através do navegador Firefox, foi apresentada uma página de aviso com a mensagem “Warning: Potential Security Risk Ahead”, impedindo o acesso ao website como vemos na imagem 3. Isto aconteceu porque o servidor apresentou um certificado de um website distinto do qual estávamos a tentar aceder.

**Imagem 3:** Ataque MITM travado pela PKI.
![alt text](docs/logbook11/task5.png)
