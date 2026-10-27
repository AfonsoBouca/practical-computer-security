# Hash Length Extension Attack Lab

## Authenticated download
O objetivo desta tarefa é realizar um download legítimo a partir do servidor. O website disponibiliza uma interface que aceita pedidos HTTP com o seguinte formato:

```
http://www.seedlab-hashlen.com/?myname=<Nome>&uid=<Uid>&lstcmd=1&mac=<MAC>
```

Para aceder ao webside de forma autorizada utilizamos as credenciais:
- **Name:** `<user>`
- **UID:** `<uid>`
- **Key:** `<lab-secret>` (not included)

A autenticação do pedido requer a geração de um **MAC** baseado na key secreta e nos parâmetros presentes no URL. O servidor utiliza o formato:
```
    <Key>:myname=<Nome>&uid=<Uid>&lstcmd=1
```

Assim, com o mac obtido através do comando da figura 1, geramos o seguinte URL que faz um pedido válido de download ao servidor, completando a tarefa 1:

```
http://<authorised-lab-host>/?myname=<user>&uid=<uid>&lstcmd=1&download=secret.txt&mac=<valid-mac>
```

**Imagem 1:** Comando para obter um mac válido com as credenciais fornecidas 
![geração do mac](/docs/logbook10/task1_terminal.png)

**Imagem 2:** Download bem sucedido
![Download bem sucedido](/docs/logbook10/task1_sucess.png)

## SHA-256 padding
Nesta tarefa temos como objetivo calcular o padding da mensagem seguinte:
```
<lab-secret>:myname=<user>&uid=<uid>&lstcmd=1
```

O tamanho do bloco da SHA-256 é 64 bytes logo, como a mensagem tem 43 bytes de comprimento, o pading terá **64-43 = 21** bytes.

O padding para SHA-256 é gerado por 1 byte **\x80** seguido de **zeros** e por fim **8 bytes** com o número de bits na  mensagem.

Para obter a quantidade de zeros necessários removemos ao tamanho do padding 9 bytes (o byte inicial mais os 8 bytes para o comprimento) e obtemos o valor **21 - 9 = 12**.

Por último calculamos o valor hexadecimal dos bits da mensagem e obtivemos **43 * 8 = 344 bits = \x158**.

Assim obtivemos o seguinte padding:
```
\x80
\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\x00\x00\x00\x01\x58
```

## Length-extension attack
O objetivo desta tarefa é realizar o download do ficheiro secret.txt sabendo apenas o MAC de um pedido válido, sem conhecer a chave secreta. O pedido original válido e o seu mac pode ser encontrado na imagem 3.

**Imagem 3:** Criação do mac do pedido válido.
![alt text](/docs/logbook10/image-1.png)

Para criar um pedido novo que inclua o comando de download sem conhecer a chave, utilizamos o código **length_ext.c**, que implementa o Hash Length Extension Attack e retorna um novo MAC que será válido para a mensagem estendida.

**length_ext.c:**
```c
#include <stdio.h>
#include <arpa/inet.h>
#include <openssl/sha.h>
int main(int argc, const char *argv[])
{
    int i;
    unsigned char buffer[SHA256_DIGEST_LENGTH];
    SHA256_CTX c;
    SHA256_Init(&c);
    for(i=0; i<64; i++)
        SHA256_Update(&c, "*", 1);

    // MAC of the original message M (padded)
    /* Initialise this state with the digest from an authorised lab request. */

    // Append additional message
    SHA256_Update(&c, "&download=secret.txt", 20);
    SHA256_Final(buffer, &c);
    for(i = 0; i < 32; i++) {
        printf("%02x", buffer[i]);
    }
    printf("\n");
    return 0;
}
```

**Imagem 4:** Mac da mensagem estendida.
![evil mac](/docs/logbook10/task3_new-mac.png)

Utilizando o padding calculado na Task 2, concatenámos o mesmo e a nova mensagem (“&download=secret.txt”) ao pedido original e aplicámos o novo MAC gerado pelo programa. O URL completo enviado ao servidor foi o seguinte, sendo este válido como verificamos na imagem 5:

```
www.<authorised-lab-host>/?myname=<user>&uid=<uid>&lstcmd=1<sha256-padding>&download=secret.txt&mac=<extended-mac>
```

**Imagem 5:** Ataque bem sucedido.
![evil mac](/docs/logbook10/task3_sucess.png)