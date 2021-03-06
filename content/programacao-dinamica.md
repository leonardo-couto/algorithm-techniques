# Programação Dinâmica

É uma técnica de resolução de problemas que consiste em dividir o problema em mais de uma parte, resolver essas partes individualmente e combinar os resultados, parecido com o método de divisão e conquista. A programação dinâmica difere da divisão e conquista pois é aplicada a problemas onde as partes dos subproblemas gerados ao dividir o problema original se repetem e o calculo delas é reaproveitado.

Para podermos aplicar a programação dinâmica o problema precisa primeiro poder ser quebrado em partes menores. Por exemplo, a sequência de Fibonacci (0, 1, 1, 2, 3, 5, 8, 13, 19, 32, ...) é definida como `f(n) = f(n-1) + f(n-2)`. Ou em Java:

```Java
int fibonacci(int n) {
  if (n <= 0) return 0;
  if (n == 1) return 1;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

A própria definição da série de Fibonacci já divide o problema de calcular `f(n)` em dois problemas menores, o de calcular `f(n-1)` e `f(n-2)`. Portanto o código acima é um exemplo da técnica de divisão e conquista. Ao executar esse código temos a seguinte árvore de execução:

<p align="center"><img src="../imgs/fibonacci.png?raw=true" alt="Fibonacci Tree" title="Fibonacci Tree"></p>

`f(n)` vai executar de `f(n-1)` e `f(n-2)`, por sua vez, `f(n-1)` vai executar `f(n-2)` e `f(n-3)` e assim por diante.

Expandindo a árvore de chamadas para `f(7)` temos:

<p align="center"><img src="../imgs/fibonacci7.png?raw=true" alt="Expanded Fibonacci Tree for f(7)" title="Expanded Fibonacci Tree for f(7)"></p>

Todos os valores da árvore que não estão marcados em azul são valores repetidos, pois aparecem em algum lugar da linha azul. O método de programação dinâmica reaproveita o cálculo desses valores para diminuir o tempo de execução do algoritmo. A solução para a cálculo do Fibonacci usando essa técnica é começar a calcular os valores de baixo para cima até chegar no valor de f(n).

```Java
int fibonacci(int n) {
  if (n <= 0) return 0;
  int prev = 0;
  int current = 1;
  for (int i = 2; i <= n; i++) {
    int next = current + prev; // f(n) = f(n - 1) + f(n - 2)
    prev = current;
    current = next;
  }
  return current;
}
```
Executando o algoritmo anterior, para `f(47)` o tempo de execução foi de aproximadamente `22500ms`, com a versão usando programação dinâmica o tempo de execução na mesma máquina foi de apenas `0.007ms`.

Nem todos os problemas podem ser quebrados em problemas menores e nem todos os problemas que podem ser quebrados tem subproblemas em comum. Portanto o primeiro passo para tentar aplicar esse método é tentar dividir o problema em problemas menores, se for possível, analisar se os problemas menores se repetem.

Saber dividir o problema e identificar os subproblemas comuns é uma tarefa bastante difícil. A melhor maneira para desenvolver uma intuição de como usar programação dinâmica é vendo exemplos e resolvendo diferentes problemas. Abaixo segue uma lista de exemplos de soluções que usam essa técnica.

 * [Multiplicação de matrizes](https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_din%C3%A2mica#Exemplo_Multiplica.C3.A7.C3.A3o_de_Cadeia_de_Matrizes_.5B2.5D) (Português).
 * [Explicação alternativa e outros exemplos](http://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/dynamic-programming.html) (Português). 
 * [Dijkstra](https://en.wikipedia.org/wiki/Dijkstra's_algorithm) (Inglês).
