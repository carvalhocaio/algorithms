# O que é Backtracking?

**Backtracking** é uma técnica de busca **recursiva** que tenta
**construir soluções incrementais**, retrocedendo quando percebe que a solução atual
**não pode levar a um resultado válido**.

Em essência:

- ➕ Tenta  
- ❌ Volta atrás se der errado (backtrack)  
- 🔁 Tenta o próximo caminho  

## Estrutura geral de um algoritmo de Backtracking

```py
def backtrack(estado):
    if estado é solução:
        salvar solução
        return

    for escolha in possíveis_opções:
        aplicar escolha
        backtrack(novo_estado)
        desfazer escolha (backtrack)
```

## Exemplo clássico: Permutações

Problema: dado um vetor de números distintos, gerar todas as **permutações possíveis**.

```text
entrada = [1, 2, 3]
→ Saída: 
[
 [1, 2, 3],
 [1, 3, 2],
 [2, 1, 3],
 [2, 3, 1],
 [3, 1, 2],
 [3, 2, 1]
]
```

## Abordagem com Backtracking

A ideia é:

- Construir permutações **uma escolha por vez**
- Evitar repetir elementos já usados
- Ao voltar, **desfazer a última escolha**

### Implementação com backtracking

```py
def permutacoes(nums):
    resultado = []

    def backtrack(caminho, usados):
        if len(caminho) == len(nums):
            resultado.append(caminho[:])
            return
        for i in range(len(nums)):
            if usados[i]:
                continue

            usados[i] = True
            caminho.append(nums[i])
            backtrack(caminho, usados)
            caminho.pop() # desfaz
            usados[i] = False # desfaz

    backtrack([], [False] * len(nums))
    return resultado
```

### Visualização da árvore (para [1, 2, 3]):

```less
                  []
            /      |      \
          1        2        3
        /  \      / \      / \
      2    3    1   3    1   2
     |    |    |   |    |   |
    3    2    3   1    2   1
```

Cada **ramo da árvore** representa uma **tentativa de solução**, e o
**backtracking acontece ao voltar para um estado anterior**.

### Complexidade

- Número total de permutações: `n!`
- Complexidade de tempo: **O(n!)**
- Espaço: **O(n)** para a oilha de recursão + vetor de uso

## Outros problemas resolvidos com tracking

| Problema             | Descrição                                      |
| -------------------- | ---------------------------------------------- |
| Sudoku               | Preenche células obedecendo regras             |
| N-Rainhas            | Coloca rainhas sem se atacarem                 |
| Subconjuntos         | Todas combinações de inclusão/exclusão         |
| Labirinto            | Caminho entre dois pontos com restrições       |
| Word Search          | Encontra palavra no grid                       |
| Palindrome Partition | Divide string em partições que são palíndromos |

## Exemplo bônus: Subconjuntos (Power Set)

```py
def subconjuntos(nums):
    resultado = []

    def backtrack(caminho, i):
        if i == len(nums):
            resultado.append(caminho[:])
            return
        # incluir nums [i]
        caminho.append(nums[i])
        backtrack(caminho, i + 1)
        caminho.pop()
        # não incluir nums[i]
        backtrack(caminho, 1, + 1)

    backtrack([], 0)
    return resultado
```

Para `[1, 2]` -> Saída: `[[], [1], [1, 2], [2]]`

## Como reconhecer problemas de Backtracking?

Procure por: 

- ✅ Geração de **todas as combinações/permutações/arranjos**
- ✅ Restrições e regras para validação parcial (ex: sudoku)
- ✅ Árvore de decisão onde você pode voltar atrás

## Comparaão com outras técnicas

| Técnica              | Quando usar                                     |
| -------------------- | ----------------------------------------------- |
| Recursão simples     | Quando não há necessidade de controle de estado |
| Backtracking         | Quando há múltiplos caminhos + restrições       |
| Programação dinâmica | Quando há subproblemas com sobreposição         |
| BFS/DFS              | Quando o problema é de caminhos/grafos          |

## Conclusão

**Backtracking** é uma técnica poderosa, especialmente para problemas que exigem:

- Exploração completa de possibilidades
- Comportamento tipo "tentativa e erro"
- Soluções únicas ou múltiplas

---
