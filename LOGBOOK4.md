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

## Questão 3