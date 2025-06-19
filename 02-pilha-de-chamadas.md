# O que é a Pilha de Chamadas? 

## Definição

A **Pilha de Chamadas (Call Stack)** é uma estrutura de dados usada pela
linguagem de programação para:

- Controlar a execução de **funções**
- Armazenar o **contexto atual da função**
- Retornar ao ponto correto após cada chamada

> A pilha funciona com o príncipio **LIFO - Last In, First Out**.

## Analogia prática

Imagine uma pilha de pratos. Você:

- Coloca um prato em cima da pilha (chamada de função)
- Para pegar um prato, você **só pode tirar o de cima** (função mais recente)
- Quando termina, você **retira o topo da pilha**

### Exemplo simples: funções encadeadas

```py
def c():
    print("Função C")

def b():
    print("Função B - antes de chamar C")
    c()
    print("Função B - depois de chamar C")

def a():
    print("Função A - antes de chamar B")
    b()
    print("Função A - depois de chamar B")

a()
```

#### Ordem de execução na pilha

1. `a()` é chamada → entra na pilha
2. Dentro de `a()`, chamamos `b()` → entra na pilha
3. Dentro de `b()`, chamamos `c()` → entra na pilha
4. `c()` termina → sai da pilha
5. `b()` continua e termina → sai da pilha
6. `a()` termina → sai da pilha

> Cada função **só continua** quando a função chamada termina.

### Como funciona internamente

Em cada **entrad da pilha (stack frame)**, temos:

- Nome da função
- Argumentos
- Variáveis locais
- Posição de retorno

## Visualização da pilha (recursão)

Vamos analisar o exemplo do fatorial recursivo:

```py
def fatorial(n):
    if n == 0:
        return 1
    return n * fatorial(n - 1)

fatorial(3)
```

### Pilha de chamadas (topo no final):

```text
fatorial(3)
→ fatorial(2)
   → fatorial(1)
      → fatorial(0) → retorna 1
   → retorna 1 * 1 = 1
→ retorna 2 * 1 = 2
→ retorna 3 * 2 = 6
```

## Stack Overflow

Quando você chama **muitas funções recursivamente sem parar**, a pilha cresce até estourar:

```py
def chamada_infinita():
    return chamada_infinita()

chamada_infinita()
```

Resultado:

```text
RecursionError: maximum recursion depth exceeded
```

- O limite padrão da pilha em Python é cerca de **1000 chamadas**
- Você pode ajustar com `sys.setrecursionlimit(n)`, mas **não é recomendado**

## Visualizando a pilha com `traceback`

```py
import traceback

def a():
    b()

def b():
    c()

def c():
    print("Traceback atual:")
    traceback.print_stack()

a()
```

Saída (resumida):

```text
  File "main.py", line 14, in <module>
    a()
  File "main.py", line 2, in a
    b()
  File "main.py", line 5, in b
    c()
  File "main.py", line 8, in c
    traceback.print_stack()
```

Você vê o **caminho exato** de chamadas até o ponto atual.

## Pilha e Debugging

Quando ocorre um erro, o Python mostra o **stack trace** (rastro da pilha). Isso ajuda a:

- Saber **qual função causou o erro**
- Entender **qual chamou quem**
- Identificar erros recursivos e ciclos infinitos

## Pilha de chamadas na prática: debugger

Em IDEs como PyCharm, VS Code, etc., você pode:

1. Colocar **breakpoints**
2. Ver a **pilha de chamadas atual**
3. Saltar entre funções ativas
4. Inspecionar variáveis locais em cada função

### Simulando a pilha manualmente

Se você quiser **simular a recursão com uma pilha explícita**, pode usar uma lista:

```py
def fatorial_iterativo(n):
    pilha = []
    while n > 0:
        pilha.append(n)
        n -= 1

    resultado = 1
    while pilha:
        resultado *= pilha.pop()
    return resultado
```

Aqui, simulamos exatamente o que a **stack do Python** faz internamente.

## Recursão x Iteração x Stack

Abordagem           | Usa stack do Python?   | Complexidade  | Controle do fluxo
------------------- | ---------------------- | ------------- | -----------------
Recursiva comum     | ✅ Sim                 | Pode ser alta | Menor controle
Tail recursiva      | ✅ Sim (em Python)     | Igual         | Não otimizada
Iterativa com stack | ❌ (usa lista)         | Igual         | Maior controle

## Conclusão

A **pilha de chamadas** é a base da execução de função em Python e de como a recursão funciona.

✅ Saber como ela funciona te ajuda a:
- Entender recursão profundamente
- Debugar erros complexos
- Escrever código mais robusto

❌ Ignorar isso pode levar a erros como:
- RecursionError
- Lógica incorreta por perda de contexto

---
