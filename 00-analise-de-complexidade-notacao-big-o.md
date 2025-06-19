# O que é Análise de Complexidade?

## Objetivo

Análise de complexidade serve para **avaliar a eficiência de algoritmos**, medindo:

- **Tempo de execução** (tempo que o algoritmo leva para rodar)
- **Uso de memória** (espaço ocupado na RAM)

Em vez de medir o tempo real (que depende de muitos fatores), usamos
**uma abstração matemática** para entender como o algoritmo
**se comporta quando o tamanho da entrada cresce**.

## Big O: A ideia central

A notação **Big O** descreve o **comportamento assintótico** de um algoritmo. Ou
seja, como ele se comporta **quando o tamanho da entrada tende ao infinito (n → ∞)**.

### Exemplo intuitivo

Imagine que você está procurando uma pessoa numa lista telefônica:

- **Busca Linear (O(n))**: Você olha um nome por vez.
- **Busca Binária (O(log n))**: Você dobra o intervalo a cada passo, como um jogo de "mais ou menos".
- **Busca Exaustiva em todas as combinações (O(2ⁿ))**: Tenta todas as possibilidades.

## Tabela com as complexidades mais comuns

Notação    | Nome         | Exemplo
---------- | ------------ | -------
O(1)       | Constante    | Acesso direto a um elemento
O(log n)   | Logarítmica  | Busca binária
O(n)       | Linear       | Laço simples
O(n log n) | Quase linear | Merge sort, Quick sort
O(n²)	   | Quadrática   | Dois loops aninhados
O(2ⁿ)      | Exponencial  | Algoritmos recursivos ruins
O(n!)      | Fatorial     | Permutação completa

## Exemplos em Python

### O(n) - Tempo linear

```py
def somar_elementos(lista):
    total = 0
    for elemento in lista:
        total += elemento
    return total
```

- Preciamos visitar todos o `n` elementos.
- Complexidade: O(n)

### O(n²) - Tempo quadrático

```py
def pares_unicos(lista):
    pares = []
    for i in range(len(lista)):
        for j in range(i + 1, len(lista)):
            pares.append((lists[i], lista[j]))
    return pares
```

- Dois loops aninhados: cada elemento é comparado com todos os outros
- Complexidade: O(n²)

### O(log n) - Busca binária

```py
def busca_binaria(lista, alvo):
    inicio, fim = 0, len(lista) - 1
    while inicio <= fim:
        meio = (inicio + fim) // 2
        if lista[meio] == alvo:
            return meio
        elif lista[meio] < alvo:
            inicio = meio + 1
        else:
            fim = meio - 1
    return -1
```

- A cada iteração, descartamos metada da lista.
- Complexidade: O(log n)

### O(2ⁿ) - Recursão exponencial (ineficiente)

```py
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

- Altamente ineficiente: muitos cálculos repetidos
- Complexidade: O(2ⁿ)

⚡ Dica: usar programação dinâmica reduz para O(n).

## Como calcular a complexidade de uma função

1. Identifique loops: Cada loop sobre `n` contribui com O(n)
2. Loops aninhados? Multiplique: dois loops -> O(n²)
3. Funções recursivas? Monte a **árvore de recursão** ou use **Master Theorem**
4. Ignore constantes e termos menores:
    - O(2n + 10) -> O(n)
    - O(n + log n) -> O(n)

## Exemplo prático do dia a dia

Suponha que você está limpando uma lista de emails duplicados:

```py
def limpar_duplicados(lista):
    return list(set(lista))
```

- Conversão para `set` é O(n) (no geral).
- Resultado é uma operação linear.

Agora, se usássemos:

```py
def limpar_duplicados_ineficiente(lista):
    resultado = []
    for item in lista:
        if item not in resultado:
            resultado.append(item)
    return resultado
```

- `if item not in resultado` é O(n)
- Total: O(n²)

## Por que isso importa?

- Algoritmos rápidos poupam CPU, bateria, custos em nuvem, etc.
- Soluções escaláveis são mais rebustas em sistemas reais.
- Entrevistas técnicas (ex: FAANG) exigem saber estimar a complexidade.

## Dica para medir tempo na prática

```py
import time

def exemplo():
    time.sleep(1)

inicio = time.time()
exemplo()
fim = time.time()

print(f"Tempo: {fim - inicio:.4f} segundos")
```

## Conclusão

Análise de complexidade (Big O) é uma ferramenta
**fundamental para projetar, avaliar e melhorar algoritmos**. Entendê-la te dá:

- Clareza sobre o que está acontecendo por trás dos panos
- Capacidade de identificar gargalos de desempenho
- Vantagem em entrevistas e no trabalho real

---
