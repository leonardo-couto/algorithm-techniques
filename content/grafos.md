# Grafos

Um grafo é uma estrutura que representa um conjunto de vertices (ou nós) conectados entre si por arestas. As arestas podem ou não ser direcionadas dependendo do tipo do grafo.

<p align="center"><img src="imgs/6n-graf.png?raw=true" alt="Simple Graph" title="Simple Graph"><br><sub>Desenho de um grafo não direcionado simples</sub></p>

## Estrutura de dados

Existem várias formas de representar um grafo computacionalmente. Duas das mais comuns são:

### Lista de Adjacências
O Grafo é um conjunto de nós e um nó é uma estrutura que contém o valor do nó em si e um conjunto de nós vizinhos. Dois nós são considerados vizinhos se eles compartilham uma aresta. Exemplo:

```Java
class Graph<T> {
  Set<Node<T>> nodes;
}

class Node<T> {
  T valor;
  Set<Node<T>> vizinhos;
}
```
### Matriz de adjacência
Uma matriz bi-dimensional em que as linhas representam nós de origem e as colunas os de destino. Aqui cada vértice é identificado por um inteiro (índice da matriz). Existe uma aresta entre os nós `i`, e `j` se a matriz de adjacência `M` conter um valor `M[i][j] = true`.

```Java
boolean[][] grafo;
```

Esse modelo é interessante para grafos com até uma certa quantidade de vértices. Para grafos esparsos e com muitos vértices o modelo de lista de adjacências é mais indicado.

## Busca

Para percorrer um grafo sem correr o risco de entrar em um loop infinito é necessário lembrar quais nós já foram percorridos pelo algoritmo de busca. Uma maneira de conseguir isso é associar um estado para cada nó e atualizar esse estado durante a busca.

### Busca em profundidade

Na busca em profundidade os nós vizinhos são explorados recursivamente, indo em cada ramo do grafo até onde é possível, antes de voltar para trás e explorar os demais vizinhos.

<p align="center"><img src="imgs/depth-first-search.gif?raw=true" alt="Depth first search example" title="Depth first search example" width="250px" height="250px"><br><sub>Exemplo de execução de uma busca em profundidade (<a href="https://commons.wikimedia.org/wiki/File:Depth-First-Search.gif">fonte</a>)</sub></p>

Implementação em Java:

```Java
void dfs(Node node) {
  node.label = DISCOVERED;
  for (Node n : node.neighbours()) {
    if (n.label != DISCOVERED) {
      dfs(n);
    }
  }
}
```

### Busca em largura

Na busca em largura é usado uma fila para visitar todos os vizinhos antes de explorar o próximo nível.

<p align="center"><img src="imgs/breadth-first-search.gif?raw=true" alt="Breadth first search example" title="Breadth first search example" width="250px" height="250px"><br><sub>Exemplo de execução de uma busca em largura (<a href="https://commons.wikimedia.org/wiki/File:Breadth-First-Search-Algorithm.gif">fonte</a>)</sub></p>

Implementação em Java:

```Java
void bfs(Node root) {
  Queue<Node> queue = new LinkedList<>();
  queue.add(root);

  while (!queue.isEmpty()) {
    Node current = queue.remove();
    current.label = DISCOVERED;

    for (Node n : current.neighbours()) {
      if (n.label != DISCOVERED) {
        queue.add(n);
      }
    }
  }
}
```
