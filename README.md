# Como fazer algumas reduções e provar que é NP-Completo

---

## 01. Cobertura Mínima de Vértices é NP-completo

### ❓ O que é cobertura de vértices?

Dado um grafo, uma **cobertura de vértices** é um conjunto de vértices tal que todas as arestas tocam pelo menos um vértice da cobertura.

### 🧠 Exemplo:

```
A — B — C
```

Cobertura = {B}

* A aresta (A,B) toca B.
* A aresta (B,C) também toca B.

### ✅ Pertence à NP

Sim, pois dado um subconjunto de vértices, podemos verificar em tempo polinomial se todas as arestas estão cobertas por ele.

### 🔁 Redução de Conjunto Independente

Existe uma relação direta:

Um conjunto S é **independente** ⇔ V \ S é uma **cobertura de vértices**.

### ✏️ Exemplo com gráfico:

```
Grafo G:
A — B
|     |
C — D

Conjunto Independente: {A, D}
Cobertura de Vértices: {B, C}
```

---

## 02. Clique é NP-completo

### ❓ O que é um clique?

É um conjunto de vértices em que **todos os pares estão conectados** por uma aresta.

### 🧠 Exemplo:

```
Clique de 3 vértices:
A — B
 \  |
   C
```

### ✅ Pertence à NP

Sim. Dado um conjunto de vértices, podemos verificar em tempo polinomial se todos estão conectados entre si.

### 🔁 Redução de Conjunto Independente para Clique

* Um conjunto independente de tamanho k no grafo G equivale a um clique de tamanho k no **grafo complementar** $\overline{G}$.

### ✏️ Exemplo com gráfico:

```
G:
A — B     C

\overline{G}:
A     B — C

Conjunto Independente em G: {A, C}
→ Clique de tamanho 2 em \overline{G}: {A, C}
```

---

## 03. Grafo Hamiltoniano é NP-completo

### ❓ O que é um ciclo hamiltoniano?

Um ciclo que passa por **todos os vértices exatamente uma vez** e retorna ao vértice inicial.

### ✅ Pertence à NP

Sim. Dado um ciclo, podemos verificar se ele passa por todos os vértices exatamente uma vez em tempo polinomial.

### 🔁 Redução de 3-SAT para Hamiltoniano

Construímos gadgets (subgrafos específicos) que representam as variáveis e cláusulas, conectados de forma a simular a lógica da fórmula booleana.

### ✏️ Exemplo com gráfico (simplificado):

```
Fórmula: (x1 ∨ ¬x2)

Grafo:
[x1_true]---[clause1]---[x2_false]
```

O ciclo hamiltoniano existe apenas se for possível escolher valores consistentes que satisfaçam a fórmula.

---

## 04. Caixeiro Viajante (TSP) é NP-completo

### ❓ O que é o problema do TSP?

Dado um conjunto de cidades e distâncias, existe um caminho de **custo ≤ k** que passa por todas e retorna à origem?

### ✅ Pertence à NP

Sim. Dado um caminho, podemos somar os custos e verificar se atende ao limite k em tempo polinomial.

### 🔁 Redução de Hamiltoniano para TSP

* Construímos uma instância do TSP onde:

  * Arestas do grafo original têm custo 1.
  * Arestas inexistentes têm custo 2.
* Um ciclo de custo igual ao número de vértices indica ciclo hamiltoniano.

### ✏️ Exemplo com gráfico:

```
G:
A — B — C
|         |
E — D — F

TSP:
Custo 1 para arestas de G
Custo 2 para outras arestas
```

---

## 05. Coloração Mínima de Vértices é NP-completo

### ❓ O que é coloração de vértices?

É uma atribuição de cores aos vértices tal que **vértices adjacentes tenham cores diferentes**. Queremos saber se é possível usar **k cores**.

### ✅ Pertence à NP

Sim. Podemos verificar se uma coloração é válida em tempo polinomial.

### 🔁 Redução de Clique para Coloração

* Uma clique de tamanho k exige k cores distintas.
* Logo, se o grafo tem clique de tamanho k, ele **não pode** ser colorido com menos de k cores.

### ✏️ Exemplo com gráfico:

```
Clique de tamanho 3:
A — B
 \  |
   C

→ Necessita de 3 cores distintas.
```