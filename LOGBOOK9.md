# Secret Key Encryption
## Tarefa 1
O objetivo desta tarefa era entender como a encriptação de substituição simples funciona e como utilizar o comando __tr__, que substitui cada aparência de um caracter por outro, para executar e decifrar cifras de substituição de letras em ficheiros de texto simples.

Utilizando o código __freq.py__, e com o objetivo de decifrar um texto simples, nós fomos capazes de recolher os 1,2 e 3-gramas mais comuns do texto cifrado:

```
-------------------------------------
1-gram (top 20):
n: 488
y: 373
v: 348
x: 291
u: 280
q: 276
m: 264
h: 235
t: 183
i: 166
p: 156
a: 116
c: 104
z: 95
l: 90
g: 83
b: 83
r: 82
e: 76
d: 59
-------------------------------------
2-gram (top 20):
yt: 115
tn: 89
mu: 74
nh: 58
vh: 57
hn: 57
vu: 56
nq: 53
xu: 52
up: 46
xh: 45
yn: 44
np: 44
vy: 44
nu: 42
qy: 39
vq: 33
vi: 32
gn: 32
av: 31
-------------------------------------
3-gram (top 20):
ytn: 78
vup: 30
mur: 20
ynh: 18
xzy: 16
mxu: 14
gnq: 14
ytv: 13
nqy: 13
vii: 13
bxh: 13
lvq: 12
nuy: 12
vyn: 12
uvy: 11
lmu: 11
nvh: 11
cmu: 11
tmq: 10
vhp: 10
```

__freq.py:__
```python
#!/usr/bin/env python3

from collections import Counter
import re

TOP_K  = 20
N_GRAM = 3

# Generate all the n-grams for value n
def ngrams(n, text):
    for i in range(len(text) -n + 1):
        # Ignore n-grams containing white space
        if not re.search(r'\s', text[i:i+n]):
           yield text[i:i+n]

# Read the data from the ciphertext
with open('out.txt') as f:
    text = f.read()

# Count, sort, and print out the n-grams
for N in range(N_GRAM):
   print("-------------------------------------")
   print("{}-gram (top {}):".format(N+1, TOP_K))
   counts = Counter(ngrams(N+1, text))        # Count
   sorted_counts = counts.most_common(TOP_K)  # Sort 
   for ngram, count in sorted_counts:                  
       print("{}: {}".format(ngram, count))   # Print
```

Assim comparamos os n-gramas obtidos com os mais comuns na língua inglesa e começamos a descodificar a mensagem guardada no ficheiro __in.txt__ utilizando o comando __tr__. 

Primeiro substítuimos 'ytn' por 'the' pois é o trigrama mais comum, confirmando a tentativa com os bigramas e as letras mais comuns.

Em segundo lugar, com a ajuda do preencimento parcial de outros trigramas, utilizamos a mesmo método do primeiro passo para descodificamos todos os n-gramas mais comuns e com frequências mais distintas.

Após não ser possível obter mais informação desse modo, observamos a descodificação parcial do texto e substituimos manualmente as letras restantes com base nas palavras que cohneciamos do vucabulário inglês e faziam sentido no contexto do texto, obtendo a seguinte chave final que revelou o texto __out.txt__:

``` bash
# Comando com a chave na ordem de descodificação
tr 'ytnxumvqprchbislfagzdekjow' 'THEONIASDGMRFLKWVCBUYPXQJZ' < in.txt > out.txt
# Comando com a chave em ordem alfabética
tr 'vgapnbrtmosicuxejhqyzflkdw' 'ABCDEFGHIJKLMNOPQRSTUVWXYZ' < in.txt > out.txt
```

__out.txt__:
```
THE OSCARS TURN  ON SUNDAY WHICH SEEMS ABOUT RIGHT AFTER THIS LONG STRANGE
AWARDS TRIP THE BAGGER FEELS LIKE A NONAGENARIAN TOO

THE AWARDS RACE WAS BOOKENDED BY THE DEMISE OF HARVEY WEINSTEIN AT ITS OUTSET
AND THE APPARENT IMPLOSION OF HIS FILM COMPANY AT THE END AND IT WAS SHAPED BY
THE EMERGENCE OF METOO TIMES UP BLACKGOWN POLITICS ARMCANDY ACTIVISM AND
A NATIONAL CONVERSATION AS BRIEF AND MAD AS A FEVER DREAM ABOUT WHETHER THERE
OUGHT TO BE A PRESIDENT WINFREY THE SEASON DIDNT JUST SEEM EXTRA LONG IT WAS
EXTRA LONG BECAUSE THE OSCARS WERE MOVED TO THE FIRST WEEKEND IN MARCH TO
AVOID CONFLICTING WITH THE CLOSING CEREMONY OF THE WINTER OLYMPICS THANKS
PYEONGCHANG

ONE BIG QUESTION SURROUNDING THIS YEARS ACADEMY AWARDS IS HOW OR IF THE
CEREMONY WILL ADDRESS METOO ESPECIALLY AFTER THE GOLDEN GLOBES WHICH BECAME
A JUBILANT COMINGOUT PARTY FOR TIMES UP THE MOVEMENT SPEARHEADED BY 
POWERFUL HOLLYWOOD WOMEN WHO HELPED RAISE MILLIONS OF DOLLARS TO FIGHT SEXUAL
HARASSMENT AROUND THE COUNTRY

SIGNALING THEIR SUPPORT GOLDEN GLOBES ATTENDEES SWATHED THEMSELVES IN BLACK
SPORTED LAPEL PINS AND SOUNDED OFF ABOUT SEXIST POWER IMBALANCES FROM THE RED
CARPET AND THE STAGE ON THE AIR E WAS CALLED OUT ABOUT PAY INEQUITY AFTER
ITS FORMER ANCHOR CATT SADLER QUIT ONCE SHE LEARNED THAT SHE WAS MAKING FAR
LESS THAN A MALE COHOST AND DURING THE CEREMONY NATALIE PORTMAN TOOK A BLUNT
AND SATISFYING DIG AT THE ALLMALE ROSTER OF NOMINATED DIRECTORS HOW COULD
THAT BE TOPPED

AS IT TURNS OUT AT LEAST IN TERMS OF THE OSCARS IT PROBABLY WONT BE

WOMEN INVOLVED IN TIMES UP SAID THAT ALTHOUGH THE GLOBES SIGNIFIED THE
INITIATIVES LAUNCH THEY NEVER INTENDED IT TO BE JUST AN AWARDS SEASON
CAMPAIGN OR ONE THAT BECAME ASSOCIATED ONLY WITH REDCARPET ACTIONS INSTEAD
A SPOKESWOMAN SAID THE GROUP IS WORKING BEHIND CLOSED DOORS AND HAS SINCE
AMASSED  MILLION FOR ITS LEGAL DEFENSE FUND WHICH AFTER THE GLOBES WAS
FLOODED WITH THOUSANDS OF DONATIONS OF  OR LESS FROM PEOPLE IN SOME 
COUNTRIES


NO CALL TO WEAR BLACK GOWNS WENT OUT IN ADVANCE OF THE OSCARS THOUGH THE
MOVEMENT WILL ALMOST CERTAINLY BE REFERENCED BEFORE AND DURING THE CEREMONY 
ESPECIALLY SINCE VOCAL METOO SUPPORTERS LIKE ASHLEY JUDD LAURA DERN AND
NICOLE KIDMAN ARE SCHEDULED PRESENTERS

ANOTHER FEATURE OF THIS SEASON NO ONE REALLY KNOWS WHO IS GOING TO WIN BEST
PICTURE ARGUABLY THIS HAPPENS A LOT OF THE TIME INARGUABLY THE NAILBITER
NARRATIVE ONLY SERVES THE AWARDS HYPE MACHINE BUT OFTEN THE PEOPLE FORECASTING
THE RACE SOCALLED OSCAROLOGISTS CAN MAKE ONLY EDUCATED GUESSES

THE WAY THE ACADEMY TABULATES THE BIG WINNER DOESNT HELP IN EVERY OTHER
CATEGORY THE NOMINEE WITH THE MOST VOTES WINS BUT IN THE BEST PICTURE
CATEGORY VOTERS ARE ASKED TO LIST THEIR TOP MOVIES IN PREFERENTIAL ORDER IF A
MOVIE GETS MORE THAN  PERCENT OF THE FIRSTPLACE VOTES IT WINS WHEN NO
MOVIE MANAGES THAT THE ONE WITH THE FEWEST FIRSTPLACE VOTES IS ELIMINATED AND
ITS VOTES ARE REDISTRIBUTED TO THE MOVIES THAT GARNERED THE ELIMINATED BALLOTS
SECONDPLACE VOTES AND THIS CONTINUES UNTIL A WINNER EMERGES

IT IS ALL TERRIBLY CONFUSING BUT APPARENTLY THE CONSENSUS FAVORITE COMES OUT
AHEAD IN THE END THIS MEANS THAT ENDOFSEASON AWARDS CHATTER INVARIABLY
INVOLVES TORTURED SPECULATION ABOUT WHICH FILM WOULD MOST LIKELY BE VOTERS
SECOND OR THIRD FAVORITE AND THEN EQUALLY TORTURED CONCLUSIONS ABOUT WHICH
FILM MIGHT PREVAIL

IN  IT WAS A TOSSUP BETWEEN BOYHOOD AND THE EVENTUAL WINNER BIRDMAN
IN  WITH LOTS OF EXPERTS BETTING ON THE REVENANT OR THE BIG SHORT THE
PRIZE WENT TO SPOTLIGHT LAST YEAR NEARLY ALL THE FORECASTERS DECLARED LA
LA LAND THE PRESUMPTIVE WINNER AND FOR TWO AND A HALF MINUTES THEY WERE
CORRECT BEFORE AN ENVELOPE SNAFU WAS REVEALED AND THE RIGHTFUL WINNER
MOONLIGHT WAS CROWNED

THIS YEAR AWARDS WATCHERS ARE UNEQUALLY DIVIDED BETWEEN THREE BILLBOARDS
OUTSIDE EBBING MISSOURI THE FAVORITE AND THE SHAPE OF WATER WHICH IS
THE BAGGERS PREDICTION WITH A FEW FORECASTING A HAIL MARY WIN FOR GET OUT

BUT ALL OF THOSE FILMS HAVE HISTORICAL OSCARVOTING PATTERNS AGAINST THEM THE
SHAPE OF WATER HAS  NOMINATIONS MORE THAN ANY OTHER FILM AND WAS ALSO
NAMED THE YEARS BEST BY THE PRODUCERS AND DIRECTORS GUILDS YET IT WAS NOT
NOMINATED FOR A SCREEN ACTORS GUILD AWARD FOR BEST ENSEMBLE AND NO FILM HAS
WON BEST PICTURE WITHOUT PREVIOUSLY LANDING AT LEAST THE ACTORS NOMINATION
SINCE BRAVEHEART IN  THIS YEAR THE BEST ENSEMBLE SAG ENDED UP GOING TO
THREE BILLBOARDS WHICH IS SIGNIFICANT BECAUSE ACTORS MAKE UP THE ACADEMYS
LARGEST BRANCH THAT FILM WHILE DIVISIVE ALSO WON THE BEST DRAMA GOLDEN GLOBE
AND THE BAFTA BUT ITS FILMMAKER MARTIN MCDONAGH WAS NOT NOMINATED FOR BEST
DIRECTOR AND APART FROM ARGO MOVIES THAT LAND BEST PICTURE WITHOUT ALSO
EARNING BEST DIRECTOR NOMINATIONS ARE FEW AND FAR BETWEEN
```

## Tarefa 2
Nesta tarefa estudámos o funcionamento de diferentes modos de cifração do algoritmo AES-128, observando como cada um processa e transforma texto claro durante a cifragem e decifragem.

Para isso foi criado o ficheiro __plaintext.txt__ com o seguinte texto e 1041 bytes de tamanho:
```
The European languages are members of the same family. Their separate existence is a myth.
For science, music, sport, etc, Europe uses the same vocabulary.
The languages only differ in their grammar, their pronunciation and their most common words.
Everyone realizes why a new common language would be desirable: one could refuse to pay expensive translators.
To achieve this, it would be necessary to have uniform grammar, pronunciation and more common words.
If several languages coalesce, the grammar of the resulting language is more simple and regular than that of the individual languages.
The new common language will be more simple and regular than the existing European languages.
It will be as simple as Occidental; in fact, it will be Occidental.
To an English person, it will seem like simplified English, as a skeptical Cambridge friend of mine told me what Occidental is.
The European languages are members of the same family. Their separate existence is a myth.
For science, music, sport, etc, Europe uses the same vocabulary.
```

### AES-128-ecb

Para encriptar e desencriptar o ficheiro foram executados os comandos da figura 1:

__Figura 1:__ encriptação utilizando a cifra aes-128-ecb.
![aes-128-ecb](/docs/logbook9/task2_ecb.png)

Flags especificadas:
- **`aes-128-ecb`** - especifica o modo ECB.
- **`e`**/**`d`** - encriptar/desencriptar
- **`in`** - ficheiro original.
- **`out`** - ficheiro cifrado.
- **`K`** - chave em hexadecimal.

Descrição do modo:

O modo ECB (Electronic Codebook) divide o texto em blocos de 16 bytes e cifra cada bloco independentemente dos restantes.

A principal vantagem deste modo é a paralelização total (cada bloco é processado isoladamente).

Infelizmente é inseguro e não pode ser utilizado em aplicações reais: blocos iguais de plaintext produzem blocos iguais de ciphertext pelo que padrões no texto original tornam-se facilmente visíveis no texto cifrado.

Este comportamento é particularmente evidente em ficheiros com repetições ou imagens.

### AES-128-cbc
__Figura 2:__ encriptação utilizando a cifra aes-128-cbc.
![aes-128-cbc](/docs/logbook9/task2_cbc.png)

Flags especificadas:
- **`aes-128-ecb`** - especifica o modo ECB.
- **`e`**/**`d`** - encriptar/desencriptar
- **`in`** - ficheiro original.
- **`out`** - ficheiro cifrado.
- **`K`** - chave em hexadecimal.
- **`iv`** - vetor de inicialização.

Descrição do modo:

O modo CBC (Cipher Block Chaining) introduz dependência entre blocos.

Cada bloco de texto é combinado com o bloco anterior cifrado através de XOR sendo para o primeiro bloco utilizado um vetor de inicialização aleatório, pois não existe bloco anterior. Após isso, o resultado do XOR é cifrado com AES.

Esta metodologia elimina padrões do ECB pois dois blocos iguais resultam em blocos cifrados diferentes mas torna o processo não paralelizável na cifragem.

### AES-128-ctr
__Figura 3:__ encriptação utilizando a cifra aes-128-ctr.
![aes-128-ctr](/docs/logbook9/task2_ctr.png)

Flags especificadas:
- **`aes-128-ecb`** - especifica o modo ECB.
- **`e`**/**`d`** - encriptar/desencriptar
- **`in`** - ficheiro original.
- **`out`** - ficheiro cifrado.
- **`K`** - chave em hexadecimal.
- **`iv`** - vetor de inicialização.

Descrição do modo:

O modo CTR (Counter) transforma o AES numa cifra de fluxo.

AES cifra um valor composto pelo vetor de inicialização e um contador cujo resultado funciona como keystream.

O texto é combinado com a keystream através de XOR e os blocos são completamente independentes entre si pelo que é totalmente paralelizável.

A segurança depende crucialmente de nunca reutilizar o mesmo IV com a mesma chave.

A principal diferença deste modo para os restantes é a utilização do mesmo algoritmo para a cifração e decifração como verificamos na figura 3: Obtemos o texto original cifrando ou decifrando o texto cifrado.

## Tarefa 5
O objetivo desta tarefa é entender como a corrupção de um byte no texto cifrado afeta o resultado da cifra.
Com isso em mente executamos os mesmos passos da tarefa 2 para cada modo de cifra mas antes da decifragem modificamos o byte 250 do texto cifrado para AA.

### AES-128-ecb

No modo ECB, cada bloco de 16 bytes do texto é cifrado de forma independente. Por isso, a corrupção de um único byte no texto cifrado afeta todo o bloco correspondente no texto decifrado. Ou seja, um byte corrompido no criptograma resulta na perda de 16 bytes de informação no texto final.

__Figura 4:__ Resultado da corrupção de um byte na cifra ecb.
![aes-128-ecb](/docs/logbook9/task5_ecb.png)

### AES-128-cbc

No modo CBC, cada bloco de texto é cifrado utilizando o bloco anterior cifrado e a chave AES. Como consequência, a corrupção de um único byte no texto cifrado afeta todo o bloco correspondente no texto decifrado, e ainda um byte na mesma posição do bloco seguinte devido ao xor que é feito do texto original com o texto cifrado anterior. Ou seja, a alteração propaga-se parcialmente: 16 bytes do bloco corrompido mais 1 byte no bloco seguinte são afetados.

__Figura 5:__ Resultado da corrupção de um byte na cifra cbc.
![aes-128-cbc](/docs/logbook9/task5_cbc.png)

### AES-128-ctr

No modo CTR cada byte do plaintext é combinado com um byte de keystream gerado a partir do contador e da chave AES através de XOR. Por essa razão a corrupção de um único byte no texto cifrado afeta apenas o byte correspondente no texto decifrado, sem propagar o erro para os restantes bytes.

__Figura 6:__ Resultado da corrupção de um byte na cifra ctr.
![aes-128-](/docs/logbook9/task5_ctr.png)