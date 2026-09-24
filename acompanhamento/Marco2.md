# Relatório do Marco 2: Componentes Conexas

## 1. Contextualização
Este documento registra a análise do problema **CSES 1682 (Flight Routes Check)** adaptado para o estudo de **Componentes Conexas** em um grafo simples e não dirigido com $V = 6$ vértices e $E = 6$ arestas.

---

## 2. Definição do Grafo
* **Vértices ($V$):** $\{1, 2, 3, 4, 5, 6\}$
* **Arestas ($E$):** $\{(1, 2), (2, 3), (1, 3), (4, 5), (5, 6), (4, 6)\}$

### Listas de Adjacência:
- $1 \rightarrow [2, 3]$
- $2 \rightarrow [1, 3]$
- $3 \rightarrow [1, 2]$
- $4 \rightarrow [5, 6]$
- $5 \rightarrow [4, 6]$
- $6 \rightarrow [4, 5]$

---

## 3. Métricas das Componentes Conexas

O grafo está dividido em duas componentes conexas independentes ($CC_1 = \{1, 2, 3\}$ e $CC_2 = \{4, 5, 6\}$), ambas estruturadas como grafos completos $K_3$.

### Componente Conexa 1 ($CC_1 = \{1, 2, 3\}$):
* **Excentricidades:** $e(1) = 1, e(2) = 1, e(3) = 1$
* **Raio ($R$):** $1$
* **Diâmetro ($D$):** $1$
* **Vértices Centrais / Centro:** $\{1, 2, 3\}$

### Componente Conexa 2 ($CC_2 = \{4, 5, 6\}$):
* **Excentricidades:** $e(4) = 1, e(5) = 1, e(6) = 1$
* **Raio ($R$):** $1$
* **Diâmetro ($D$):** $1$
* **Vértices Centrais / Centro:** $\{4, 5, 6\}$

---

## 4. Rastreamento Manual do Algoritmo (DFS Recursiva)
1. **Início:** `visited = [false, false, false, false, false, false, false]`, `cc_count = 0`.
2. **Passo 1 ($i = 1$):** `visited[1]` é falso $\rightarrow$ `cc_count = 1`, chamada `dfs(1)`.
   - `visited[1] = true`. Visita vizinho `2` $\rightarrow$ `dfs(2)`.
   - `visited[2] = true`. Visita vizinho `3` $\rightarrow$ `dfs(3)`.
   - `visited[3] = true`. Vizinhos de 3 já visitados $\rightarrow$ Retorna.
   - Retorna as chamadas, concluindo a **Componente 1: `{1, 2, 3}`**.
3. **Passo 2 ($i = 2, 3$):** Vértices já marcados como visitados; ignorados.
4. **Passo 3 ($i = 4$):** `visited[4]` é falso $\rightarrow$ `cc_count = 2`, chamada `dfs(4)`.
   - `visited[4] = true`. Visita vizinho `5` $\rightarrow$ `dfs(5)`.
   - `visited[5] = true`. Visita vizinho `6` $\rightarrow$ `dfs(6)`.
   - `visited[6] = true`. Vizinhos de 6 já visitados $\rightarrow$ Retorna.
   - Retorna as chamadas, concluindo a **Componente 2: `{4, 5, 6}`**.
5. **Fim:** Todos os vértices visitados. Total de 2 componentes conexas identificadas.

---

## 5. Análise de Complexidade e Consultas
* **Complexidade de Tempo:** $\mathcal{O}(V + E)$ — Cada vértice e aresta é processado a uma taxa linear em relação ao tamanho estrutural do grafo.
* **Complexidade de Espaço:** $\mathcal{O}(V + E)$ — Ocupação de memória devida ao armazenamento da lista de adjacência, vetor de visitados e pilha de recursão.
* **Custo de Consultas de Conectividade:** $\mathcal{O}(1)$ — Mediante pré-atribuição de rótulos de componentes a cada vértice.