# O que é um grafo? 

Um **grafo** é uma estrutura de dados usada para representar **relações**
entre objetos. Ele é composto por:

- **Vértices (nós)**: os elementos (ex: cidades, pessoas)
- **Arestas**: as conexões entre os vértices (ex: estrada, amizade)

## Tipos de grafos

| Tipo                  | Exemplo                     |
| --------------------- | --------------------------- |
| Não direcionado       | A—B (vai e volta)           |
| Direcionado (digrafo) | A→B (só vai)                |
| Ponderado             | A—(3)—B (com peso)          |
| Cíclico / Acíclico    | Com ou sem ciclos (ex: DAG) |

## Representações principais

1. Lista de Adjacência
    - Cada vpertice armazena uma **lista dos seus vizinhos**.
    - Economiza memória para grafos **esparsos** (com poucas arestas).

2. Matriz de Adjacência
    - Usa uma **matriz NxN** onde `mat[i][j]` indica se há aresta entre `i` e `j`.
    - Útil em grafos **densos** ou para **consultas rápidas**.

## Exemplo: Grafo simples

```text
Vértices: A, B, C
Arestas: A–B, A–C
```

Vértices indexados: A = 0, B = 1, C = 2

### Representação 1: Lista de Adjacência

```py
grafo = {
    0: [1, 2],  # A → B, C
    1: [0],     # B → A
    2: [0]      # C → A
}
```

Acesso: quem são os vizinhos de A?

```py
grafo[0]  # [1, 2]
```

### Representação 2: Matriz de Adjacência

```py
#        A  B  C
matriz = [
    [0, 1, 1],  # A
    [1, 0, 0],  # B
    [1, 0, 0],  # C
]
```

Há aresta de A para B?

```py
matriz[0][1]  # 1 → Sim
```

### Comparação entre as duas

| Critério                      | Lista de Adjacência | Matriz de Adjacência |
| ----------------------------- | ------------------- | -------------------- |
| Memória                       | O(V + E)            | O(V²)                |
| Testar se aresta (u,v) existe | O(grau(u))          | O(1)                 |
| Iterar vizinhos               | O(grau(u))          | O(V)                 |
| Ideal para...                 | Grafos esparsos     | Grafos densos        |
| Direcionado?                  | Sim                 | Sim                  |
| Ponderado?                    | Sim (com tuplas)    | Sim (com números)    |


### Versão com pesos (ponderado)

Lista de adjacência ponderada

```py
grafo = {
    0: [(1, 5), (2, 2)],  # A → B (5), C (2)
    1: [(0, 5)],
    2: [(0, 2)]
}
```

Matriz ponderada

```py
#        A  B  C
matriz = [
    [0, 5, 2],  # A
    [5, 0, 0],  # B
    [2, 0, 0],  # C
]
```

## Implementação com nomes

```py
vertices = ['A', 'B', 'C']
indice = {nome: i for i, nome in enumerate(vertices)}
```

Acessar:

```py
matriz[indice['A']][indice['B']]
```

## Exemplo com diagrafo direcionado

### Grafo:

```text
A → B
B → C
```

### Lista:

```py
grafo = {
    'A': ['B'],
    'B': ['C'],
    'C': []
}
```

### Matriz:

```text
    A B C
A [ 0 1 0 ]
B [ 0 0 1 ]
C [ 0 0 0 ]
```

## Construindo a matriz dinamicamente

```py
def cria_matriz(n):
    return [[0] * n for _ in range(n)]

def adiciona_aresta(matriz, u, v):
    matriz[u][v] = 1
```

## Quando usar o quê?

| Caso de uso                                   | Representação ideal  |
| --------------------------------------------- | -------------------- |
| Muitos vértices, poucas arestas               | Lista de adjacência  |
| Preciso verificar aresta rápido               | Matriz de adjacência |
| Algoritmos como Dijkstra                      | Lista (com pesos)    |
| Algoritmos de Floyd-Warshall (todos os pares) | Matriz               |
| Manipulação frequente de conexões             | Matriz               |


## Conclusão

A escolha da representação de grafos **afeta diretamente a performance** dos algoritmos
aplicados sobre eles. Saber como e quando usar:

- **Lista de Adjacência** te dá eficiência espacial e iteração rápida.
- **Matriz de Adjacência** facilita a simplifica algoritmos baseados em matriz.

---
