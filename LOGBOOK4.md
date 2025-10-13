# Environment Variable and Set-UID Lab

## Questão 1
### Tasks 1-5
Nesta primeira fase do guião somos apresentados às variáveis de ambiente e aprendemos a modificá-las.  
Na tarefa 2 verificámos que o processo pai e o processo filho partilham as mesmas variáveis de ambiente.  
Nas tarefas 3 e 4 observámos como certas chamadas de sistema propagam — ou não — essas variáveis.  
Na tarefa 5 aprendemos que programas set‑UID não recebem a variável LD_LIBRARY_PATH, embora recebam as restantes.

### Task 6
Nesta tarefa temos um programa com permissões de **root** (implementado como mostrado na imagem 1) com o seguinte excerto de código:
```bash
int main() 
{
    system("ls");
    return 0;
}
```

**Imagem 1:** Implementação do programa vulnerável
![image](task6_setup.png)

Como o programa é **set‑UID** é possivel executar código com permissões **root**, então para um atacante enganar o sistema basta fazer o programa correr o seu código.  
Neste caso específico, ao utilizar a função system, as variaveis de ambiente do utilizador são passadas até à execução da função **ls**. Como esta usa um caminho relativo, ao trocar a variável **PATH** podemos dar prioridade à execução de uma função com o mesmo nome e permissões **root**.  

Assim começamos o ataque com a implementação e compilação de uma função ls que abre um terminal (linha 1 da imagem 2):
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	system("/usr/bin/sh");
	return 0;
}
```
Após isso atualizamos a variável **PATH** para utilizar em primeiro lugar as funções defenidas na pasta atual(linha 2 da imagem 2).  
Agora apenas é necessário correr o programa com a vulnerabilidade (linha 3 da imagem 2). Dado que o programa é **set‑UID** o nosso ls é executado como **root** e temos acesso a um terminal com as mesmas permissões.
  
**Imagem 2:** Código executado pelo atacante sem permissões root
![image](task6_attack.png)

## Questão 2
### Task 8 
Nesta tarefa analisámos a segurança de um programa, catall.c, que foi concebido para ser utilizado como **set‑UID**. Este programa permite a leitura de ficheiros do sistema aos quais certos utilizadores normalmente nao tem accesso (Bob). No entanto, o programa faz uso de system() que invoca o shell do sistema onde é passada uma string, que é interpretada. O shell interpreta não só a string mas também metacaracteres, onde a partir dai, é possivel realizar um command injection.
Como mostrado na Imagem 3, criámos um ficheiro de teste task8.txt com texto simples.

**Imagem 3:** Criação do ficheiro task8.txt
![image](task8_txt.png)

Como primeiro passo, utilizamos o programa com uma versão vulnerável, com recurso ao uso de system() em vez de execve().
No entanto, como o programa tem permissões root é possivel alterar/remover ficheiros.

**Imagem 4:** Remoção do ficheiro task8.txt através de command injection - uso de system()
![image](task8_system.png)

Nesta imagem podemos verificar que ao correr ./catall task8.txt ou ./catall "task8.txt" é possivel ler o conteudo do ficheiro.
No entanto ao usar "task8.txt;rm task8.txt" como argumento, o shell executa o comando rm e conseguimos eliminar o ficheiro. É possivel confirmar isso ao tentar correr novamente o programa com o task8.txt como argumento.
Concluimso que esta versão com recurso ao uso de system(), que permite a execução de comandos arbitrários pelo utilizador, compromete a integridade do sistema.

Como segundo passo, desta vez comentamos o system() e utilizamos execve(). Após compilar e definir novamente como set-UID, corremos o programa com o ficheiro task8.txt com o mesmo conteúdo.
O ficheiro também foi lido como esperado mas desta vez, ao tentar realizar novamente o ataque com "task8.txt;rm task8.txt", retornou um erro de que o ficheiro não existia, como mostrado na imagem 5.

**Imagem 5:** Tentativa de remoção do ficheiro task8.txt através de command injection - uso de execve()
![image](task8_execve.png)

Devido ao uso de execve(), o binaŕio é executado diretamente sem invocar shell, onde o programa cat tenta abrir um ficheiro com o exato nome "task8.txt;rm task8.txt", não executanto o comando rm e mantendo a integridade do ficheiro.


## Questão 3