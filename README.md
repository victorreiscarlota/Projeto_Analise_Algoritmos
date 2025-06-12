# Como fazer algumas reduções e provar que é NP-Completo

---

## Conceitos Básicos

### 🔵 Classe P

Problemas que podem ser resolvidos **em tempo polinomial**. Ou seja, há um algoritmo que resolve o problema eficientemente (tempo limitado por um polinômio do tamanho da entrada).

### 🔵 Classe NP

Problemas cuja solução pode ser **verificada em tempo polinomial**. A solução pode não ser fácil de encontrar, mas se alguém te der uma "resposta", você consegue verificar rápido se está certa.

### 🔵 Classe co-NP

Problemas cuja **negação** pode ser verificada em tempo polinomial.

---

## 01. Verificar se um número é primo está em NP e co-NP

### ❓ O que é ser primo?

Um número $n > 1$ é primo se **só for divisível por 1 e por ele mesmo**.

### ✅ Está em NP

Dado um número primo, podemos verificar que ele **não possui divisores entre 2 e √n**. Basta testar a divisão por todos esses números — isso leva tempo proporcional a √n, que é polinomial em relação ao tamanho da entrada (log n).

### ✅ Está em co-NP

Se alguém disser que **n não é primo**, pode nos dar um **divisor d** com $1 < d < n$. Testar se d divide n também é fácil e polinomial.

### ✏️ Exemplo:

Queremos saber se 29 é primo. Testamos divisores de 2 até √29 ≈ 5.38 → testamos 2, 3, e 5.

```
Verificações:
29 % 2 ≠ 0
29 % 3 ≠ 0
29 % 5 ≠ 0 → ✅ É primo
```

---

## 02. Conjunto Independente Máximo pertence à NP

### ❓ O que é um conjunto independente?

É um conjunto de vértices tal que **nenhum par de vértices no conjunto tem uma aresta entre eles**.

### ✅ Está em NP

Dado um conjunto, basta verificar se existe alguma aresta ligando dois vértices dentro dele. Isso leva tempo polinomial.

### ✏️ Exemplo com gráfico:

```
G:
A — B
 
C — D

Conjunto independente: {A, D}
→ Não existe aresta entre A e D → válido
```

---

## 03. Emparelhamento Máximo está em P

### ❓ O que é um emparelhamento?

É um conjunto de arestas tal que **nenhum vértice aparece em mais de uma aresta**.

### ✅ Está em P

Dado um grafo, podemos usar algoritmos como Edmonds ou matching em grafos bipartidos para encontrar esse emparelhamento **em tempo polinomial**. Conceitualmente:

* Repetidamente procuramos pares de vértices que ainda não foram emparelhados e os conectamos.
* Garantimos que nenhum vértice seja reutilizado.

### ✏️ Exemplo:

```
G:
A — B
C — D

Emparelhamento: {(A,B), (C,D)}
→ Cada vértice só aparece uma vez
```

---

## 04. Verificar se um número pertence à sequência de Fibonacci está em NP e co-NP

### ❓ O que é a sequência de Fibonacci?

Cada termo é a soma dos dois anteriores: 0, 1, 1, 2, 3, 5, 8, 13...

### ✅ Está em NP

Dado um número, podemos gerar os termos da sequência até ultrapassá-lo, e verificar se ele está na lista — isso leva tempo polinomial.

### ✅ Está em co-NP

Se alguém diz que **n não está na sequência**, pode nos dar dois termos consecutivos de Fibonacci entre os quais n cairia — verificamos se n está fora do intervalo.

### ✏️ Exemplo:

Número 21 → Geramos: 0, 1, 1, 2, 3, 5, 8, 13, 21 → ✅ Está

---

## 05. Verificar se uma sequência está ordenada está em NP e co-NP

### ❓ O que é verificar se uma sequência está ordenada?

Queremos saber se os números estão em **ordem crescente** (ou decrescente).

### ✅ Está em NP

Dada a sequência, verificamos para cada i se $a_i ≤ a_{i+1}$. Isso leva tempo linear → polinomial.

### ✅ Está em co-NP

Para provar que **não** está ordenada, basta mostrar **um par fora de ordem**. Podemos verificar isso rapidamente.

### ✏️ Exemplo:

Sequência: \[1, 3, 5, 2]

```
1 < 3 → OK
3 < 5 → OK
5 < 2 → ❌ Fora de ordem → não está ordenada
```

---

# Problemas NP-Completos com Reduções e Exemplos

---

## 01. Cobertura Mínima de Vértices é NP-completo

### ❓ O que é cobertura de vértices?

Um conjunto de vértices que toca todas as arestas do grafo.

### ✅ Pertence à NP

Dado um subconjunto, verificamos se toda aresta toca pelo menos um dos vértices do subconjunto.

### 🔁 Redução de Conjunto Independente

Existe uma relação direta:
Um conjunto S é **independente** ⇔ V \ S é uma **cobertura de vértices**.

### ✏️ Exemplo:

```
G:
A — B — C

Cobertura mínima: {B}
→ Arestas (A,B) e (B,C) tocadas por B
```

---

## 02. Clique é NP-completo

### ❓ O que é um clique?

Conjunto de vértices em que **todos os pares estão conectados**.

### ✅ Pertence à NP

Dado um conjunto, verificamos se todos os pares têm arestas entre si.

### 🔁 Redução de Conjunto Independente para Clique

* Um conjunto independente de tamanho k em G ↔ clique de tamanho k no grafo complementar $\overline{G}$.

### ✏️ Exemplo:

```
G:
A — B     C

\overline{G}:
A     B — C

Conjunto Independente: {A, C} → Clique em \overline{G}
```

---

## 03. Grafo Hamiltoniano é NP-completo

### ❓ O que é um ciclo hamiltoniano?

Caminho que passa por **todos os vértices uma vez** e retorna ao início.

### ✅ Pertence à NP

Dado um ciclo, verificamos se ele contém todos os vértices uma vez.

### 🔁 Redução de 3-SAT para Hamiltoniano

Construímos subgrafos (gadgets) que representam variáveis e cláusulas conectadas de forma lógica.

### ✏️ Exemplo (simplificado):

```
Fórmula: (x1 ∨ ¬x2)

Grafo:
[x1_true]---[clause1]---[x2_false]
```

---

## 04. Caixeiro Viajante (TSP) é NP-completo

### ❓ O que é o TSP?

Existe um caminho que passa por todas as cidades **com custo total ≤ k**?

### ✅ Pertence à NP

Dado o caminho, somamos os custos e verificamos se ≤ k.

### 🔁 Redução de Hamiltoniano para TSP

* Arestas do grafo original têm custo 1
* Arestas faltantes têm custo 2
* Se existir ciclo custo = n → há ciclo Hamiltoniano

### ✏️ Exemplo:

```
G:
A — B — C
|         |
E — D — F

TSP:
Arestas do grafo original → custo 1
Demais → custo 2
```

---

## 05. Coloração Mínima de Vértices é NP-completo

### ❓ O que é coloração?

Atribuir cores aos vértices tal que **vértices vizinhos tenham cores diferentes**.

### ✅ Pertence à NP

Verificar se uma coloração com k cores é válida → tempo polinomial.

### 🔁 Redução de Clique para Coloração

Se grafo tem clique de tamanho k → precisa de ≥ k cores.

### ✏️ Exemplo:

```
Grafo:
A — B
 \ |
   C

→ Necessita de 3 cores diferentes
```
