# O que são essas estruturas?

| Estrutura          | Acesso                              | Ordem                                     | Exemplos práticos                             |
| ------------------ | ----------------------------------- | ----------------------------------------- | --------------------------------------------- |
| **Pilha (stack)**  | LIFO (último entra, primeiro sai)   | Fundo → Topo                              | Navegação de páginas, validação de parênteses |
| **Fila (queue)**   | FIFO (primeiro entra, primeiro sai) | Início → Fim                              | Filas de impressão, BFS, agendamento          |
| **Hashmap (dict)** | Acesso direto por chave             | Sem ordem (ou controlada via OrderedDict) | Contagem de frequência, cache, lookup rápido  |


## Pilha (Stack)

Conceito: último que entra é o primeira a sair (**LIFO**)

```py
stack = []
stack.append(1) # push
stack.append(2)
stack.pop()     # -> 2 (último)
```

### Exemplo prático: Validação de parênteses balanceados

```py
def valid_parentheses(s):
    pilha = []
    mapa = {')': '(', '}': '{', ']': '['}

    for c in s:
        if c in mapa.values():
            pilha.append(c)
        elif c in mapa:
            if not pilha or pilha[-1] != mapa[c]:
                return False
            pilha.pop()
    return not pilha
```

Teste:

```py
valid_parentheses("{[()]}")  # ✅ True
valid_parentheses("[(])")    # ❌ False
```

## Fila (Queue)

Conceito: Primeiro que entra é o primeiro a sair (**FIFO**)

```py
from collections import deque

fila = deque()
fila.append(1) # enqueue
fila.append(2)
fila.popleft() # -> 1 (primeiro)
```

### Exemplo prático: **BFS em uma matriz (labirinto)**

```py
def bfs_labirinto(grid, start):
    from collections import deque

    visitado = set()
    fila = deque([start])
    direcoes = [(0,1),(1,0),(0,-1),(-1,0)]

    while fila:
        i, j = fila.popleft()
        for di, dj in direcoes:
            ni, nj = i + di, j + dj
            if 0 <= ni < len(grid) and 0 <= nj < len(grid[0]):
                if grid[ni][nj] == 0 and (ni, nj) not in visitado:
                    visitado.add((ni, nj))
                    fila.append((ni, nj))
```

### Uso típico de fila

- BFS (busca em largura) em árvores ou grafos
- Simulação de processos (impressoras, jogos, tarefas)
- Sistemas onde a ordem importa (atendimento, requests etc.)

## Hashmap (Dicionário)

Conceito: estrutura **chave -> valor** com acesso O(1) na média

```py
frequencias = {}
for item in ["a", "b", "a", "c"]:
    frequencias[item] = frequencias.get(item, 0) + 1
```

### Exemplo prático: Primeiro caractere não repetido

```py
def primeiro_unico(s):
    freq = {}
    for c in s:
        freq[c] = freq.get(c, 0) + 1
    for c in s:
        if freq[c] == 1:
            return c
    return None
```

Teste:

```py
primeiro_unico("abacabad")  # → "c"
```

#### Exemplo 2: Two Sum (par de soma alvo)

```py
def two_sum(nums, alvo):
    mapa  = {}
    for i, num in enumerate(nums):
        comp = alvo - num
        if comp in mapa:
            return [mapa[comp], i]
        mapa[num] = i
```

## Quando usar cada estrutura?

| Tipo de problema                                  | Estrutura ideal |
| ------------------------------------------------- | --------------- |
| Voltar em estados anteriores (desfazer)           | Pilha           |
| Processar itens em ordem de chegada               | Fila            |
| Busca rápida por chave ou contagem                | Hashmap         |
| Verificar equilíbrio de estruturas (HTML, código) | Pilha           |
| Exploração em níveis (grafo, grid)                | Fila (BFS)      |
| Encontrar padrões ou pares rápidos                | Hashmap         |


## Combine estruturas

Exemplo: **LRU Cache** usa:

- Hashmap para acesso O(1)
- Fila duplamente ligada para controle da ordem de uso

### Exemplo bônus: Simulando chamadas recentes (Queue + Set)

```py
from collections import Queue

class RecentCalls:
    def __init__(self):
        self.calls = deque()

    def add(self, timestamp):
        self.calls.append(timestamp)
        while self.calls and self.calls[0] < timestamp - 3000:
            self.calls.popleft()
        return len(self.calls)
```

## Conclusão

**Pilha, Fila e Hashmap** são blocos fundamentais de resolução de problemas.
Dominar seus usos práticos te permite resolver:

- ✅ Algoritmos complexos com código simples
- ✅ Problemas de entrevistas e desafios de programação
- ✅ Situações reais de software: buffer, cache, navegação, análise

---
