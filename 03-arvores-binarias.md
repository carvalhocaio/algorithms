# O que é uma Árvore Binária?

## Conceito

Uma **árvore binária** é uma estrutura de dados **hierárquica** onde cada **nó**
tem no máximo:

- **dois filhos**, chamados:
    - **esquerdo**: (left)
    - **direito**: (right)

## Terminologia importante

Termo       	| Significado
--------------- | -------------------------------------------------
Raiz (root)     | O primeiro nó da árvore
Nó (node)	    | Um elemento da árvore
Folha (leaf)    | Nó sem filhos
Subárvore	    | Qualquer árvore contida dentro de um nó
Altura (height)	| Número de arestas do nó até a folha mais distante
Nível (level)	| Distância do nó até a raiz

## Exemplo de Árvore Binária (genérica)

```text
        A
       / \
      B   C
     /   / \
    D   E   F
```

### Essa árvore:

- Tem 6 nós
- A raiz é `A`
- `D`, `E`, `F` são folhas
- `B`, `C` são nós internos

### Implementação em Python

```py
class No:
    def __init__(self, valor):
        self.valor = valor
        self.esq = None
        self.dir = None
```

Criando a árvore acima:

```py
raiz = No("A")
raiz.esq = No("B")
raiz.dir = No("C")
raiz.esq.esq = No("D")
raiz.dir.esq = No("E")
raiz.dir.dir = No("F")
```

## Tipos de percursos em árvore binária

Tipo       | Ordem
---------- | -------------------------
Pré-ordem  | Raiz → Esquerda → Direita
Em ordem   | Esquerda → Raiz → Direita
Pós-ordem  | Esquerda → Direita → Raiz
Em largura | Nível por nível (BFS)

```py
def em_ordem(no):
    if no is not None:
        em_ordem(no.esq)
        print(no.valor, end=" ")
        em_ordem(no.dir)
```

## Árvore Binária de Busca (BST - Binary Search Tree)

### Conceito

É uma árvore binária com **regra adicional de ordenação**:

Para cada nó:
- Os valores à esquerda são menores
- Os valores à direita são maiores

#### Exemplo de BST:

```text
       8
      / \
     3   10
    / \    \
   1   6    14
      / \   /
     4   7 13
```

### Implementação de BST em Python

```py
class NoBST:
    def __init__(self, valor):
        self.valor = valor
        self.esq = None
        self.dir = None

def inserir(raiz, valor):
    if raiz is None:
        return NoBST(valor)
    if valor < raiz.valor:
        raiz.esq = inserir(raiz.esq, valor)
    else:
        raiz.dir = inserir(raiz.dir, valor)
    return raiz
```

Criando a árvore:

```py
valores = [8, 3, 10, 1, 6, 14, 4, 7, 13]
raiz = None
for v in valores:
    raiz = inserir(raiz, v)
```

### Busca em BST

```py
def buscar(raiz, valor):
    if raiz is None:
        return False
    if raiz.valor == valor:
        return True
    if valor < raiz.valor:
        return buscar(raiz.esq, valor)
    else:
        return buscar(raiz.dir, valor)
```

#### Eficiência:

- **Melhor caso (árvore balanceada)**: O(log n)
- **Pior caso (árvore degenerada para lista)**: O(n)

## Comparação: Binária vs BST

Característica      | Árvore Binária           | Árvore Binária de Busca (BST)
------------------- | ------------------------ | ------------------------------------
Estrutura           | Máximo 2 filhos por nó   | Mesma estrutura
Ordem dos elementos | Arbitrária               | Ordenada: esq < nó < dir
Busca               | Ineficiente (sem padrão) | Eficiente (usa propriedade da ordem)
Inserção            | Livre                    | Segue regra de ordenação
Aplicações típicas  | Representar hierarquias  | Armazenamento eficiente, lookup

## Problemas com BST: desbalanceamento

Se os valores forem inseridos em ordem crescente, por exemplo:

```py
valores = [1, 2, 3, 4, 5]
```

A árvore será como:

```text
1
 \
  2
   \
    3
     \
      4
       \
        5
```

-> Vira uma **lista encadeada** com complexidade O(n)

✅ Solução: usar árvores balanceadas, como:

- AVL Trees
- Red-Black Trees
- Splay Trees

## Quando usar cada uma?

Situação                                    | Use
------------------------------------------- | -------------------
Dados sem ordem e sem busca                 | Árvore binária
Busca frequentemente ordenados              | BST
Alta performance garantida em qualquer caso | AVL / Red-Black BST
Visualização de hierarquia (ex: pastas)     | Árvore binária

## Conclusão

**Árvores binárias** são a base, mas **BSTs** são árvores com regra de ordenação que
otimizam operações de busca, inserção e remoção. Entender as diferenças te permite:

- Escolher a estrutura correta para cada problema
- Escrever algoritmos mais eficientes
- Preparar-se para entrevistas com problemas clássicos de árvores

---

