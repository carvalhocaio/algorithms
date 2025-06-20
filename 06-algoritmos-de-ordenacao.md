# Algoritmos de Ordenação

## Objetivo: ordenar dados

Dado uma lista como `[5, 2, 4, 1]`, queremos reordenar para `[1, 2, 4, 5]`.

Algoritmos de ordenação variam em:

- Velocidade (complexidade)
- Estabilidade
- Simplicidade
- Espaço usado

## Tabela comparativa geral

| Algoritmo      | Complexidade (Média)           | Estável? | Espaço extra | Observações                                |
| -------------- | ------------------------------ | -------- | ------------ | ------------------------------------------ |
| Bubble Sort    | O(n²)                          | Sim      | O(1)         | Muito ineficiente                          |
| Selection Sort | O(n²)                          | Não      | O(1)         | Trocas mínimas                             |
| Insertion Sort | O(n²)                          | Sim      | O(1)         | Ótimo para listas pequenas/quase ordenadas |
| Merge Sort     | O(n log n)                     | Sim      | O(n)         | Divide e conquista, estável                |
| Quick Sort     | O(n log n) média<br>O(n²) pior | Não      | O(log n)     | Muito rápido na prática, in-place          |

## Bubble Sort

Ideia: trocar pares de elementos adjacentes se estiverem fora de ordem.

```py
def bubble_sort(lista):
    n = len(lista)
    for i in range(n):
        for j in range(0, n - i  - 1):
            if lista[j] > lista[j + 1]:
                lista[j], lista[j + 1] = lista[j + 1], lista[j]
```

## Selection Sort

Ideia: selecionar o menor elemento e colocá-lo no início da lista.

```py
def selection_sort(lista):
    n = len(lista)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if lista[j] < lista[min_idx]:
                min_idx = j
        lista[i], lista[min_idx] = lista[min_idx], lista[i]
```

## Insert Sort

Ideia: insere cada elemento na posição correta da sublista anterior ordenada.

```py
def insertion_sort(lista):
    for i in range(1, len(lista)):
        chave = lista[i]
        j = i - 1
        while j >= 0 and lista[j] > chave:
            lista[j + 1] = lista[j]
            j -= 1
        lista[j + 1] = chave
```

## Merge Sort

Ideia:
- Divide a lista em duas metades
- Ordena recursivamente as duas partes
- Combina (merge) as duas listas ordenadas

```py
def merge_sort(lista):
    if len(lista) <= 1:
        return lista

    meio = len(lista) // 2
    esquerda = merge_sort(lista[:meio])
    direita = merge_sort(lists[meio:])
    return merge(esquerda, direita)

def merge(esq, dir):
    resultado = []
    i = j = 0
    while i < len(esq) and j < len(dir):
        if esq[i] <= dir[j]:
            resultado.append(esq[i])
            i += 1
        else:
            resultado.append(dir[j])
            j += 1
    
    resultado.extend(esq[i:])
    resultado.extend(dir[j:])
    return resultado
```

Exemplo para `[4, 2, 5, 1]`:

```text
merge_sort([4, 2, 5, 1])
→ merge_sort([4, 2]) + merge_sort([5, 1])
→ merge([2, 4], [1, 5]) = [1, 2, 4, 5]
```

Complexidade:
- Divisões: log₂n
- Combinações: n
- Total: O(n log n)

Vantagens:
- Estável
- Consistente
- Boa escolha para listas muito grandes

Desvantagens:
- Usa memória extra O(n)

## Quick Sort

Ideia:
- Escolhe um **pivô**
- Coloca elementos menores à esquerda, maiores à direita
- Aplica recursão em ambas as partes


```py
def quick_sort(lista):
    if len(lista) <= 1:
        return lista

    pivô = lista[0]
    menores = [x for x in lista[1:] if x <= pivô]
    maiores = [x for x in lista[1:] if x > pivô]

    return quick_sort(menores) + [pivô] + quick_sort(maiores)
```

Exemplo para `[4, 2, 5, 1]`, pivô = 4;

```text
menores = [2, 1], maiores = [5]
→ quick_sort([2, 1]) + [4] + quick_sort([5])
→ [1, 2] + [4] + [5] = [1, 2, 4, 5]
```

Complexidade:
- Média: O(n log n)
- Pior caso (pivô ruim): O(n²)
- Em prática, com bom pivô (ex: mediana ou randomizado): muito eficiente

Vantagens:
- Muito rápido
- In-place (sem memória extra)

Desvantagens:
- Não é estável
- Sensível à escolha do pivô

## Comparação visual dos algoritmos

| Algoritmo  | Simples?  | Eficiente?        | Estável? | Em memória (in-place)? |
| ---------- | --------- | ----------------- | -------- | ---------------------- |
| Bubble     | ✅        | ❌                | ✅       | ✅                     |
| Selection  | ✅        | ❌                | ❌       | ✅                     |
| Insertion  | ✅        | ⛔ (para grandes) | ✅       | ✅                     |
| Merge Sort | ⛔        | ✅                | ✅       | ❌ (usa O(n) extra)    |
| Quick Sort | ⛔        | ✅✅              | ❌       | ✅                     |


## Teste prático

```py
import random

dados = random.sample(range(100), 10)

print("Original:", dados)
print("Merge:   ", merge_sort(dados))
print("Quick:   ", quick_sort(dados))
```

## Quando usar cada um?

| Situação                        | Algoritmo recomendado |
| ------------------------------- | --------------------- |
| Lista pequena ou quase ordenada | Insertion Sort        |
| Precisão e estabilidade         | Merge Sort            |
| Performance máxima in-place     | Quick Sort            |
| Sistema com restrição de espaço | Quick / Insertion     |


## Conclusão

Dominar algoritmos de ordenação te dá:

- Clareza sobre tempo de execução
- Base para entrevistas técnicas
- Compreensão de como bibliotecas como **sorted()** funcionam por baixo dos panos

---
