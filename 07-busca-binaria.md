# O que é Busca Binária?

**Busca binária** é um algoritmo eficiente para encontrar um elemento em
uma **estrutura ordenada**. Ele divide o espaço de busca pela metade a
cada passo.

## Complexidade

- **Melhor caso**: O(1) (achamos de primeira)
- **Pior caso**: O(log n) (divide a lista até achar ou falhar)
- Muito mais eficiente que busca linear **O(n)** em grandes conjuntos

## Busca Binária em Array Ordenado

Pré-requisito: o array **precisa estar ordenado!**

## Implementação Iterativa

```py
def buscar_binaria(lista, alvo):
    esquerda = 0
    direita = len(lista) - 1

    while esquerda <= direita:
        meio = (esquerda + direita) // 2
        if lista[meio] == alvo:
            return meio
        elif lista[meio] < alvo:
            esquerda = meio + 1
        else:
            direita = meio - 1
    return -1 # não encontrado
```

## Implementação Recursiva

```py
def busca_binaria_rec(lista, alvo, esq=0, dir=None):
    if dir is None:
        dir = len(lista) - 1
    if esq > dir:
        return -1

    meio = (esq + dir) // 2
    if lista[meio] == alvo:
        return meio
    elif lista[meio] < alvo:
        return busca_binaria_rec(lista, alvo, meio + 1, dir)
    else:
        return busca_binaria_rec(lista, alvo, esq, meio - 1)
```

## Exemplo visual: `lista = [1, 3, 5, 7, 9]`, alvo = 7

1. meio = 2 -> lista[2] = 5
2. 5 < 7 -> busca em `[7, 9]`
3. meio = 3 -> lista[3] = 7 ✅ achou!

## Busca Binária em Árvore de Busca (BST)

Pré-requisito: A árvore precisa ser uma **árvore binária de busca**, ou seja:

Para cada nó:
    - "Esquerda < nó"
    - "Direita > nó"

### Classe da árvore

```py
class No:
    def __init__(self, valor):
        self.valor = valor
        self.esq = None
        self.dir = None
```

### Busca recursiva em BST

```py
def buscar_bst(no, alvo):
    if no is None:
        return False
    if no.valor == alvo:
        return True
    elif alvo < no.valor:
        return buscar_bst(no.esq, alvo)
    else:
        return buscar_bst(no.dir, alvo)
```

### Exemplo:

```text
       10
      /  \
     5    15
    / \     \
   2   7     20
```

Buscar `7`:

1. 7 < 10 -> vai para a esquerda
2. 7 < 5 -> vai para a direita
3. 7 == 7 ✅ achou!

## Comparação: Array vs BST

| Característica         | Array Ordenado        | BST (balanceado)         |
| ---------------------- | --------------------- | ------------------------ |
| Complexidade           | O(log n)              | O(log n)                 |
| Pré-requisito          | Ordenação             | BST válida               |
| Busca iterativa fácil? | Sim                   | Sim, mas menos comum     |
| Inserção/remoção       | Custo alto (reordena) | Mais eficiente em árvore |
| Uso típico             | Dados estáticos       | Dados dinâmicos          |

## Cuidado com BST desbalanceada

Exemplo de inserções: [1, 2, 3, 4, 5]

Árvore resultante:

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

Agora a **buscar binária em árvore vira O(n)** (igual à busca linear)

Solução: usar **árvores balanceadas** (AVL, Red-Black, etc.)

## Exemplo completo com inserção e busca

```py
def inserir_bst(raiz, valor):
    if raiz is None:
        return No(valor)
    if valor < raiz.valor:
        raiz.esq = inserir_bst(raiz.esq, valor)
    else:
        raiz.dir = inserir_bst(raiz.dir, valor)
    
    return raiz

# Criar árvore
valores = [10, 5, 15, 2, 7, 20]
raiz = None
for v in valores:
    raiz = inserir_bst(raiz, v)

# Buscar valor
print(buscar_bst(raiz, 7)) # True
print(buscar_bst(raiz, 99)) # False
```

## Busca Binária é base para...

- Autocompletar
- Pesquisa em dicionários
- Implementações de `bisect` em Python
- Árvores B+ em bancos de dados

## Conclusão 

Busca binária é um dos algoritmos mais importantes da computação. Ela é:

- ✅ Eficiente (O(log n))
- ✅ Simples de implementar
- ✅ Fundamento para algoritmos mais complexos

---
