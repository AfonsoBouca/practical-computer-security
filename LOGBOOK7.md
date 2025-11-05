# Cross-Site Scripting (XSS) Attack Lab

## Questão 1
__Task 1:__  
Na Tarefa 1, demonstrámos como injetar um fragmento de JavaScript num perfil do Elgg para provocar uma janela de alerta (XSS).

**Passos**
1. Fazer login como `alice` (`seedalice`) em `http://www.seed-server.com`.  
2. Ir a *Edit Profile* → campo *Brief description*.  
3. Inserir:
   ```html
   <script>alert('XSS');</script>
4. Guardar.

5. Fazer login como outro utilizador (ex.: boby / seedboby).

6. Visitar o perfil de alice.

7. Comprovar sucesso: 
   - Ao visitar o perfil de `alice` com outra conta aparece uma janela modal com o texto **XSS**.
   
![image](docs/logbook7/LOGBOOK7(1).png)

__Task 2:__  


__Task 3:__

__Task 4:__


## Questão 2