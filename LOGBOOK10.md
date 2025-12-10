# Hash Length Extension Attack Lab

## Tarefa 1
O objetivo desta tarefa é realizar um download legítimo a partir do servidor. O website disponibiliza uma interface que aceita pedidos HTTP com o seguinte formato:

```
http://www.seedlab-hashlen.com/?myname=<Nome>&uid=<Uid>&lstcmd=1&mac=<MAC>
```

Para aceder ao webside de forma autorizada utilizamos as credenciais:
- **Nome:** DanielPinto
- **Uid:** 1001
- **Key:** 123456

A autenticação do pedido requer a geração de um **MAC** baseado na key secreta e nos parâmetros presentes no URL. O servidor utiliza o formato:
```
    <Key>:myname=<Nome>&uid=<Uid>&lstcmd=1
```

Assim, com o mac obtido através do comando da figura 1, geramos o seguinte URL que faz um pedido válido de download ao servidor, completando a tarefa 1:

```
http://www.seedlab-hashlen.com/?myname=DanielPinto&uid=1001&lstcmd=1&download=secret.txt&mac=be01fc794a36ac6aec0332217ff7770cb65b32dad3520a443f11606b768bca68
```

**Imagem 1:** Comando para obter um mac válido com as credenciais fornecidas 
![geração do mac](/docs/logbook10/task1_terminal.png)

**Imagem 2:** Download bem sucedido
![Download bem sucedido](/docs/logbook10/task1_sucess.png)

## Task 2
123456:myname=DanielPinto&uid=1001&lstcmd=1
Comprimento: 43 bytes

padding binário é:
\x80
\x00 x12
\x00\x00\x00\x00\x00\x00\x01\x58


calculo do mac :
```
echo -n "123456:myname=DanielPinto&uid=1001&lstcmd=1&download=secret.txt\x80\x00x12\x00\x00\x00\x00\x00\x00\x01\x58" | sha256sum
```

![alt text](/docs/logbook10/image.png)


## Task 3

![alt text](/docs/logbook10/image-1.png)

```
http://www.seedlab-hashlen.com/?myname=DanielPinto&uid=1001&lstcmd=1&download=secret.txt&mac=612ca45834715ab11b04d2ef20dfc0fad969432b8e8b2ace4c9176d7d217059d
```