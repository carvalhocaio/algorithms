# O que são percursos em árvores?

## Definição

**Percorrer uma árvore** significa visitar cada nó da árvore **exatamente uma vez**, em uma 
ordem específica.

A forma como você percorre a árvore afeta:
- A ordem em que os dados são lidos
- A estrutura de algoritmos (como serialização, avaliação de expressões, buscas etc.)

## Tipos de percursos mais comuns

### Percursos em Profundidade (DFS – Depth-First Search)

1. Pré-ordem (preorder):
    - Visita: `nó → esquerda → direita`

2. Em ordem (inorder):
    - Visita: `esquerda → nó → direita`

3. Pós-ordem (postorder):
    - Visita: `esquerda → direita → nó`

### Percurso em Largura (BFS – Breadth-First Search)

- Visita por níveis: da raiz até as folhas, nível por nível da esquerda para a direita.

## Exemplo visual da árvore base

```text
        A
       / \
      B   C
     / \   \
    D   E   F
```

## Pré-ordem (Preorder)

Ordem de visita: `A B D E C F`

Uso típico:
- Clonagem/serialização de árvore
- Avaliação de expressões prefixadas

```py
def pre_ordem(no):
    if no:
        print(no.valor, end=' ')
        pre_ordem(no.esq)
        pre_ordem(no.dir)
```

## Em ordem (Inorder)

Ordem de visita: `D B E A C F`

Uso típico:
- Em **BSTs**, retorna os elementos em ordem crescente
- Conversão para lista ordenada

```py
def em_ordem(no):
    if no:
        em_ordem(no.esq)
        print(no.valor, end=' ')
        em_ordem(no.dir)
```

## Pós-ordem (Postorder)

Ordem de visita: `D E B F C A`

Uso típico:
- Deletar nós em árvores
- Avaliação de expressões pós-fixadas (RPN)
- Liberação de memória

```py
def pos_ordem(no):
    if no:
        pos_ordem(no.esq)
        pos_ordem(no.dir)
        print(no.valor, end=' ')
```

## BFS (em largura – nível por nível)

Ordem de visita: `A B C D E F`

Uso típico:
- Encontrar caminhos mais curtos (ex: em grafos)
- Conversão de árvore para lista de níveis

```py
from collections import deque

def bfs(raiz):
    if raiz is None:
        return
    fila = deque()
    fila.append(raiz)
    while fila:
        atual = fila.popleft()
        print(atual.valor, end=' ')
        if atual.esq:
            fila.append(atual.esq)
        if atual.dir:
            fila.append(atual.dir)
```

## Implementação da estrutura da árvore

```py
class No:
    def __init__(self, valor):
        self.valor = valor
        self.esq = None
        self.dir = None

# Criando a árvore do exemplo
raiz = No("A")
raiz.esq = No("B")
raiz.dir = No("C")
raiz.esq.esq = No("D")
raiz.esq.dir = No("E")
raiz.dir.dir = No("F")
```

## Tabela comparativa dos percursos

| Tipo      | Ordem de Visita         | Uso Principal                     |
| --------- | ----------------------- | --------------------------------- |
| Pré-ordem | Nó → Esquerda → Direita | Serialização, prefixo             |
| Em ordem  | Esquerda → Nó → Direita | Ordenação em BSTs                 |
| Pós-ordem | Esquerda → Direita → Nó | Deleção, avaliação pós-fixada     |
| BFS       | Nível por nível         | Caminhos mínimos, varredura geral |

## Aplicação em BST

```py
valores = [8, 3, 10, 1, 6, 14, 4, 7, 13]

# Construir BST
def inserir(raiz, valor):
    if not raiz:
        return No(valor)
    if valor < raiz.valor:
        raiz.esq = inserir(raiz.esq, valor)
    else:
        raiz.dir = inserir(raiz.dir, valor)
    return raiz

raiz_bst = None
for v in valores:
    raiz_bst = inserir(raiz_bst, v)

# Em ordem mostra: 1 3 4 6 7 8 10 13 14 (ordenado!)
em_ordem(raiz_bst)
```

## Conclusão
Percursos de árvores são
**formas fundamentais de explorar, processar e entender estruturas hierárquicas**. Saber quando
usar cada um te ajuda a:

- ✅ Buscar, ordenar e avaliar
- ✅ Otimizar algoritmos em árvores e grafos
- ✅ Trabalhar com árvores em sistemas reais: arquivos, expressões, índices, linguagens...

---
