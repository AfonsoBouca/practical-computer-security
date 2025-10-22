# Format-String Vulnerability Lab
## Questão 1
__Task 1:__  
O objetivo desta task é fazer o programa format.c que está a correr no servidor dar crash atravez de uma vulnerabilidade de *Format String*.  

O alvo do nosso ataque é a função printf que quando recebe mais especificadores de formato do que argumentos reais, não valida os ponteiros e passa a interpretar a partir da pilha. Em vez de verificar limites, o printf vai ler bytes da pilha como se fossem endereços válidos até que eventualmente provoque um crash por segfault (acesso a endereço inválido).

Para efetuar o ataque preparamos o ambiente com o código vulnerável format.c com os comandos da imagem 1 e iniciamos o container com o comando do terminal da esquerda da imagem 2. Com o servidor pronto enviamos a mensagem "%s" * 100, obrigando o programa a ler 100 entradas da pilha e tornando o crash inevitavél como vemos na imagem 2 pela falta da mensagem "(^_^)(^_^)  Returned properly (^_^)(^_^)"

__Imagem 1:__ Preparação do ambiente na pasta *category-software/Format_String* disponível em https://github.com/seed-labs/seed-labs.
![setup](docs/logbook6/setup.png)

__Imagem 2:__ Ataque bem sucedido.
![ataque](docs/logbook6/task1_logbook6(2).png)


__format.c:__ Código vulnerável.
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/socket.h>
#include <netinet/ip.h>

/* Changing this size will change the layout of the stack.
 * Instructors can change this value each year, so students
 * won't be able to use the solutions from the past.
 * Suggested value: between 10 and 400  */
#ifndef BUF_SIZE
#define BUF_SIZE 100
#endif


#if __x86_64__
  unsigned long target = 0x1122334455667788;
#else
  unsigned int  target = 0x11223344;
#endif 

char *secret = "A secret message\n";

void dummy_function(char *str);

void myprintf(char *msg)
{
#if __x86_64__
    unsigned long int *framep;
    // Save the rbp value into framep
    asm("movq %%rbp, %0" : "=r" (framep));
    printf("Frame Pointer (inside myprintf):      0x%.16lx\n", (unsigned long) framep);
    printf("The target variable's value (before): 0x%.16lx\n", target);
#else
    unsigned int *framep;
    // Save the ebp value into framep
    asm("movl %%ebp, %0" : "=r"(framep));
    printf("Frame Pointer (inside myprintf):      0x%.8x\n", (unsigned int) framep);
    printf("The target variable's value (before): 0x%.8x\n",   target);
#endif

    // This line has a format-string vulnerability
    printf(msg);

#if __x86_64__
    printf("The target variable's value (after):  0x%.16lx\n", target);
#else
    printf("The target variable's value (after):  0x%.8x\n",   target);
#endif

}


int main(int argc, char **argv)
{
    char buf[1500];


#if __x86_64__
    printf("The input buffer's address:    0x%.16lx\n", (unsigned long) buf);
    printf("The secret message's address:  0x%.16lx\n", (unsigned long) secret);
    printf("The target variable's address: 0x%.16lx\n", (unsigned long) &target);
#else
    printf("The input buffer's address:    0x%.8x\n",   (unsigned int)  buf);
    printf("The secret message's address:  0x%.8x\n",   (unsigned int)  secret);
    printf("The target variable's address: 0x%.8x\n",   (unsigned int)  &target);
#endif

    printf("Waiting for user input ......\n"); 
    int length = fread(buf, sizeof(char), 1500, stdin);
    printf("Received %d bytes.\n", length);

    dummy_function(buf);
    printf("(^_^)(^_^)  Returned properly (^_^)(^_^)\n");

    return 1;
}

// This function is used to insert a stack frame between main and myprintf.
// The size of the frame can be adjusted at the compilation time. 
// The function itself does not do anything.
void dummy_function(char *str)
{
    char dummy_buffer[BUF_SIZE];
    memset(dummy_buffer, 0, BUF_SIZE);

    myprintf(str);
}
```
__Task 2:__  
__Task 3:__
## Questão 2
