**Relógio Lógico de Lamport**

O Relógio Lógico de Lamport foi criado por Leslie Lamport. É um procedimento para determinar a ordem dos eventos que ocorrem. Ele fornece uma base para o Algoritmo de Relógio Vetorial mais avançado. Devido à ausência de um Relógio Global em um Sistema Operacional Distribuído, o Relógio Lógico de Lamport é necessário.

Algoritmo:

**Relação de acontecimentos anteriores (->):** a -> b, significa que 'a' aconteceu antes de 'b'.

**Relógio Lógico:** Os critérios para os relógios lógicos são:

* [C1]: Ci (a) < Ci(b), [ Ci -> Relógio Lógico, Se 'a' aconteceu antes de 'b', então o tempo de 'a' será menor que 'b' em um processo específico. ]

* [C2]: Ci(a) < Cj(b), [ O valor do relógio de Ci(a) é menor que Cj(b) ]

**Referência:**

* Processo: Pi

* Evento: Eij, onde i é o processo em número e j: jº evento no iº processo.

* tm: intervalo de tempo vetorial para mensagem m.

* Ci vetor relógio associado ao processo Pi, o jº elemento é Ci[j] e contém o valor mais recente de Pi para o tempo atual no processo Pj.

* d: tempo de desvio, geralmente d é 1.

**Regras de implementação [IR]:**

* [IR1]: Se a -> b [‘a’ aconteceu antes de ‘b’ dentro do mesmo processo] então, Ci(b) = Ci(a) + d

* [IR2]: Cj = max(Cj, tm + d) [Se houver mais processos, então tm = valor de Ci(a), Cj = valor máximo entre Cj e tm + d]

**Por exemplo:**


<p align = "center">
  <img src="https://github.com/miguelsrrobo/lamport.github.io/blob/main/lamportlogicalclkgfg.png" alt="Rinha logo" width="90%" />
</p>

    Considere o valor inicial como 1, pois é o primeiro evento e não há valor de entrada no ponto inicial:

        e11 = 1

        e21 = 1

    O valor do próximo ponto continuará aumentando em d (d = 1), se não houver nenhum valor de entrada, ou seja, seguir [IR1].

        e12 = e11 + d = 1 + 1 = 2

        e13 = e12 + d = 2 + 1 = 3

        e14 = e13 + d = 3 + 1 = 4

        e15 = e14 + d = 4 + 1 = 5

        e16 = e15 + d = 5 + 1 = 6

        e22 = e21 + d = 1 + 1 = 2

        e24 = e23 + d = 3 + 1 = 4

        e26 = e25 + d = 6 + 1 = 7

    Quando houver um valor de entrada, siga [IR2], ou seja, pegue o valor máximo entre Cj e Tm + d.

        e17 = max(7, 5) = 7, [e16 + d = 6 + 1 = 7, e24 + d = 4 + 1 = 5, máximo entre 7 e 5 é 7]

        e23 = max(3, 3) = 3, [e22 + d = 2 + 1 = 3, e12 + d = 2 + 1 = 3, máximo entre 3 e 3 é 3]

        e25 = max(5, 6) = 6, [e24 + 1 = 4 + 1 = 5, e15 + d = 5 + 1 = 6, máximo entre 5 e 6 é 6]

**Limitação:**

* No caso de [IR1], se a -> b, então C(a) < C(b) -> verdadeiro.

* No caso de [IR2], se a -> b, então C(a) < C(b) -> Pode ser verdadeiro ou não ser verdadeiro.
Sure, here is the translation of the text to Portuguese:

<p align = "center">
  <img src="https://raw.githubusercontent.com/miguelsrrobo/lamport.github.io/main/lamportclklimitationgfg.png" alt="Rinha logo" width="50%" />
</p>

Saída

        e21    e22    e23
 e11    0    0    0    
 e12    0    0    1    
 e13    0    0    0    
 e14    0    0    0    
 e15    0    -1    0    
Os timestamps dos eventos em P1:
1 2 3 4 5 
Os timestamps dos eventos em P2:
1 2 3 

Complexidade de tempo: O(e1 * e2 * (e1 + e2))
Espaço auxiliar: O(e1 + e2)

Sente-se perdido no mundo de tópicos DSA aleatórios, perdendo tempo sem progresso? É hora de mudar! Junte-se ao nosso curso DSA, onde o guiaremos em uma jornada emocionante para dominar o DSA de forma eficiente e dentro do cronograma.
Pronto para mergulhar de cabeça? Explore nosso conteúdo de demonstração gratuito e participe do nosso curso DSA, com a confiança de mais de 100.000 geeks!


* No caso de [IR1], se a -> b, então C(a) < C(b) -> verdadeiro.

* No caso de [IR2], se a -> b, então C(a) < C(b) -> Pode ser verdadeiro ou não ser verdadeiro.

**Site onde foi tirado toda as informações:**
[![geeksforgeeks Lamport’s logical clock](.github/live.png)](https://www.geeksforgeeks.org/lamports-logical-clock/)
