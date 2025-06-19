# O que é Recursão?

**Recursão** é uma técnica de programação em que um função
**chama a si mesma** para resolver um problema maior até atingir um caso
base (condição de parada).

## Estrutura típica de uma função recursiva

```py
def funcao_recursiva(param):
    if caso_base(param):
        return resultado_simples
    else:
        return chamada_recursiva(param_menor)
```

## Exemplo simples: Fatorial

### Definição matemática

- `n! = n * (n - 1)!`
- `0! = 1`

### Implementação recursiva

```py
def fatorial(n):
    if n == 0:
        return 1
    return n * fatorial(n - 1)
```

### Etapas de execução (para `fatorial(4)`)

```bash
fatorial(4)
= 4 * fatorial(3)
= 4 * 3 * fatorial(2)
= 4 * 3 * 2 * fatorial(1)
= 4 * 3 * 2 * 1 * fatorial(0)
= 4 * 3 * 2 * 1 * 1
= 24
```

## Exemplo recursivo clássico: Fibonacci

```py
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacce(n - 2)
```

### Complexidade

- Recalcula várias vezes o mesmo valor
- Complexidade **exponencial**: `O(2ⁿ)`
- Pode ser otimizado com **memoização** ou **programação dinâmica**

## Stack e recursão

Cada chamada recursiva **empilha** uma nova execução ne memória, chamada
de **stack frame**. Qunado chegamos no caso base, as funções empilhadas
começam a ser resolvidas de trás para frente.

Isso levar a:

- Uso excessivo de memória
- Erro de stack overflow

```py
RecursionError: maximum recursion depth exceeded
```

## Recursão de Cauda (Tail Recursion)

### Definição

Uma **função está em tail recursion** se:

- A **última operação** da função **é a chamada recursiva**.

Assim, **não há mais nada a ser feito após a chamada**, então o interpretador
pode **reutilizar o stack frame atual** (em linguagens que otimizam isso).

### Exemplo: Tail recursion no fatorial

```py
def fatorial_tail(n, acumulador=1):
    if n == 0:
        return acumulador
    return fatorial_tail(n - 1, n * acumulador)
```

Para `fatorial_tail(4)`:

```bash
fatorial_tail(4, 1)
→ fatorial_tail(3, 4)
→ fatorial_tail(2, 12)
→ fatorial_tail(1, 24)
→ fatorial_tail(0, 24) → retorna 24
```

### Mas atenção:

> **Python não faz otimização recursion** (por design).  
> Isso significa que mesmo funções com recursão de cauda **ainda usam stack**.

## Alternativas práticas em Python

Como Python não otimiza tail recursion, preferimos usar **iterações** para
evitar problemas de stack.

### Fatorial com laço

```py
def fatorial_iterativo(n):
    resultado = 1
    for i in range(1, n + 1):
        resultado *= i
    return resultado
```

### Fibonacci com programação dinâmica

```py
def fibonacci_dinamico(n):
    a, b = 0, 1
    for _, in range(n):
        a, b = b, a + b
    return a
```

## Comparação entre abordagens

Função               | Tipo               | Complexidade | Stack usada? | Otimizada?
-------------------- | ------------------ | ------------ | ------------ | -------------
`fatorial`           | Recursiva normal   | O(n)         | Sim          | Não 
`fatorial_tail`      | Recursiva de cauda | O(n)         | Sim          | Não em Python
`fatorial_iterativo` | Iterativa          | O(n)         | Não          | Sim

## Casos de uso reais para recursão

Problema                                                   | Recursão?
---------------------------------------------------------- | --------------------
Árvore binária / pastas                                    | ✅ Sim
Busca em grafos (DFS)                                      | ✅ Sim
Algoritmos de divisão e conquista (merge sort, quick sort) | ✅ Sim
Números grandes sem stack overflow                         | ❌ Prefira iterativo

## Exemplo avançado: Percorrer árvore binária

```py
class No:
    def __init__(self, valor, esq=None, dir=None):
        self.valor = valor
        self.esq = esq
        self.dir = dir

def in_ordem(raiz):
    if raiz is None:
        return

    in_ordem(raiz.esq)
    print(raiz.valor)
    in_ordem(raiz.dir)
```

Essa função é recursiva e é ideal para percorrer árvores. Aqui, a **recursão é natural**.

## Conclusão

Recursão é uma ferramenta poderosa, mas deve ser usada com consciência em Python:

✅ Boa para:

- Estruturas hierárquicas (árvores, grafos)
- Problemas naturalmente recursivos

❌ Evite em:

- Funções com profundidade muito grande
- Casos onde iteração é mais clara e segura

---
