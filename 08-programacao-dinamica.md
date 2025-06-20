# O que é Programação Dinâmica?

É uma técnica de resolução de problemas que envolve:

> Dividir um problema em subproblemas menores e resolver
> **cada subproblema uma única vez, armazenando o resultado** para evitar recomputação.

Pré-requisito para aplicar PD?

1. **Subproblemas sobrepostos** - o problema pode ser quebrado em subproblemas repetidos
2. **Subestrutura ótima** - a solução ótima do problema depende das soluções ótimas dos subproblemas
3. **Decisão binária ou múltipla** - geralmente você escolhe a melhor entre opções


## Exemplo clássico: Fibonacci

Definição:

```py
F(0) = 0
F(1) = 1
F(n) = F(n-1) + F(n-2)
```

### Recursão pura (ineficiente)

```py
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)
```

❌ Problema: O(2^n) — repete subproblemas demais

### Top-Down com Memoização

Ideia:
- Usa recursão + cache para evitar recomputação
- Memoiza os subproblemas já resolvidos

```py
def fib_top_down(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    
    memo[n] = fib_top_down(n - 1, memo) + fib_top_down(n - 2, memo)
    return memo[n]
```

- ✅ Complexidade: O(n)
- ✅ Cacheado, simples de implementar
- ⚠️ Usa pilha de chamadas (recursão)

### Bottom-Up com Tabulação

Ideia:
- Resolve **do menor subproblema até o maior**
- Usa um array para guardar todos os resultados

```py
def fib_bottom_up(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

- ✅ Complexidade: O(n)
- ✅ Não usa recursão → sem risco de stack overflow
- ✅ Fácil de adaptar para otimização de espaço (ver abaixo)

### Bottom-Up otimizado (O(1) espaço)

```py
def fib_otimizado(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b
```

## Aplicação clássicas de PD

| Problema                         | Descrição                                    |
| -------------------------------- | -------------------------------------------- |
| Fibonacci                        | Sequência numérica                           |
| Subconjunto com soma alvo        | Subconjuntos que somam a um valor específico |
| Knapsack (Mochila 0/1)           | Selecionar itens com peso/custo              |
| LCS (Longest Common Subsequence) | Subsequência comum entre strings             |
| Edit Distance (Levenshtein)      | Transformar string A em B                    |
| Min Path Sum / Grid Problems     | Caminho mínimo com restrições                |

## Comparação entre Top-Down e Bottom-Up

| Aspecto              | Top-Down (memoização) | Bottom-Up (tabulação)   |
| -------------------- | --------------------- | ----------------------- |
| Forma principal      | Recursiva             | Iterativa               |
| Ordem de resolução   | De cima para baixo    | De baixo para cima      |
| Espaço adicional     | Cache (dict/array)    | Tabela (array/matriz)   |
| Fácil de implementar | Sim                   | Um pouco mais técnico   |
| Controle do fluxo    | Menor (recursivo)     | Maior (loop controlado) |
| Stack overflow?      | Sim, se input grande  | Não                     |

## Exemplo mais complexo: Subconjunto com soma alvo (Subset Sum)

Problema: Dada uma lista `nums` e um número `target`, existe um subconjunto cuja soma é `target`?

Exemplo:  
`num = [3, 34, 4, 12, 5, 2]`, `target = 9` -> ✅ (4 + 5 ou 3 + 2 + 4)

### Top-Down (recursivo com cache)

```py
def subset_sum(nums, taget, i=0, memo=None):
    if memo is None:
        memo = {}
    if target == 0:
        return True
    if i > len(nums) or taget < 0:
        return False
    if (i, target) in memo:
        return memo[(i, target)]
    
    incluir = subset_sum(nums, target - nums[i], i + 1, memo)
    excluir = subset_sum(nums, target, i + 1, memo)
    memo[(i, target)] = incluir or excluir
    return memo[(i, target)]
```

### Bottom-Up (tabela)

```py
def subset_sum_bottom_up(nums, target):
    n = len(nums)
    dp = [[False] * (target + 1) for _ in range(n + 1)]

    for i in range(n + 1):
        dp[i][0] = True # Soma 0 sempre possível com subconjunto vazio

    for i in range(1, n + 1):
        for j in range(1, target + 1):
            if nums[i - 1] <= j:
                dp[i][j] = dp[i - 1][j] or dp[i - 1][j - nums[i - 1]]
            else:
                dp[i][j] = dp[i - 1][j]

    return dp[n][target]
```

## Como identificar um problema de PD?

1. Tem **recorrência** ou **decisão entre caminhos**?
2. Pode **dividir em subproblemas sobrepostos**?
3. Pode montar uma **tabela de soluções parciais**?

Se sim, **programação dinâmica é forte candidata!**

## Conclusão

**Programação Dinâmica** é poderosa para otimização de problemas que têm subproblemas repetidos.

- **Top-Down** é intuitivo, ótimo para prototipação rápida
- **Bottom-Up** é mais performático e escalável
- Ambas têm papel crítico em resolver problemas **exponenciais de forma eficiente**

---

