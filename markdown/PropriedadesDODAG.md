# Propriedades do DODAG:

1. **Aciclicidade:** $D$ é um digrafo acíclico.

2. **Orientação ao Destino:** Todos os caminhos em $D$ convergem para o vértice raiz $r$.

## Algoritmo de Construção DODAG:

1. **Inicialização**:

   $D = (V, \emptyset)$.

2. **Construção Iterativa**:

   Para cada $v \in V \setminus \{r\}$, identifique $u$ tal que:

$$
u = \arg \min_{w \in N_G(v)} \big( C(v, w) + OF(w) \big).
$$

   Adicione $(u, v)$ a $E_D$.

3. **Finalização**: Retorne $D = (V, E_D)$.

## *Demonstração das propriedades*

### 1. **Aciclicidade**

#### Hipóteses:
- $G = (V, E)$ é um grafo conexo.

- $D = (V, E_D)$ é o grafo direcionado construído a partir de $G$, onde:

$$
E_D := \lbrace (u, v) \in E : OF(v) = C(u, v) + OF(u) \rbrace.
$$

- $C(u, v) > 0$, isto é, o custo das arestas é estritamente positivo.

#### Objetivo:
Provar que $D$ é acíclico (um DAG).

#### Prova:

1. **Suposição Contrária**:

Suponha, por contradição, que $D$ contém um ciclo orientado:

$$
v_1 \to v_2 \to \cdots \to v_k \to v_1,
$$

onde $v_1, v_2, \dots, v_k$ são vértices distintos e $(v_i, v_{i+1}) \in E_D$, com $v_{k+1} = v_1$.

2. **Propriedade de $OF$ nas Arestas**:

Para cada aresta $(v_i, v_{i+1}) \in E_D$, temos que:

$$
OF(v_{i+1}) = C(v_i, v_{i+1}) + OF(v_i).
$$

3. **Custo Total no Ciclo**:

Somando ao longo do ciclo, obtemos:

$$
\sum_{i=1}^k OF(v_{i+1}) = \sum_{i=1}^k \big(C(v_i, v_{i+1}) + OF(v_i)\big).
$$

Rearranjando os termos, temos:

$$
\sum_{i=1}^k OF(v_{i+1}) - \sum_{i=1}^k OF(v_i) = \sum_{i=1}^k C(v_i, v_{i+1}).
$$

4. **Condição no Ciclo**:

Como $v_{k+1} = v_1$, temos que:

$$
\sum_{i=1}^k OF(v_{i+1}) = \sum_{i=1}^k OF(v_i).
$$

Isso implica que:

$$
\sum_{i=1}^k C(v_i, v_{i+1}) = 0.
$$

5. **Contradição**:

Como $C(v_i, v_{i+1}) > 0$ para todas as arestas, temos que:

$$
\sum_{i=1}^k C(v_i, v_{i+1}) > 0,
$$

o que contradiz a igualdade $\sum_{i=1}^k C(v_i, v_{i+1}) = 0$.


Sendo assim, a suposição de que $D$ contém um ciclo leva a uma contradição. Logo, $D$ é acíclico.


### 2. **Orientação ao Destino**

#### Hipóteses:
- $G = (V, E)$ é um grafo conexo.

- $D = (V, E_D)$ é DODAG construído a partir de $G$.

- $OF(v)$ é a função objetivo acumulada utilizada para construção DODAG, com $OF(r) = 0$, onde $r$ é a raiz.

#### Objetivo:
Provar que todos os caminhos em $D$ terminam no nó raiz $r$.

#### Prova:

1. **Propriedade da Construção de $D$**:

Para cada aresta $(u, v) \in E_D$, temos:

$$
OF(v) = C(u, v) + OF(u).
$$

Isso implica que $OF(v)$ é maior que $OF(u)$, pois $C(u, v) > 0$.

2. **Decréscimo de $OF$ ao Longo do Caminho**:

Em qualquer caminho $v_1 \to v_2 \to \cdots \to v_k$ em $D$, temos:

$$
OF(v_1) > OF(v_2) > \cdots > OF(v_k).
$$

Como $OF(v)$ é inicializado como $+\infty$ para todos os nós, exceto a raiz $r$, e $OF(r) = 0$, o valor de $OF$ decresce ao longo do caminho até atingir $OF(r) = 0$.

3. **Terminação na Raiz**:

O caminho não pode continuar indefinidamente porque:
- $D$ é finito ($|V| < \infty$).
- Não existem ciclos ($D$ é acíclico).
- O valor de $OF$ é limitado inferiormente por $OF(r) = 0$.


Logo, todos os caminhos em $D$ devem terminar no nó raiz $r$.

