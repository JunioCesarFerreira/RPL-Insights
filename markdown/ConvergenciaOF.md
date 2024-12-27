# Definição Iterativa OF

Definimos $OF$ iterativamente da seguinte forma:

1. **Inicialização**:

$$
OF^{(0)}(v) =
\begin{cases}
0, & \text{se } v = r, \\
+\infty, & \text{caso contrário}.
\end{cases}
$$

definimos também que $OF^{(t)}(r)=0$ para qualquer valor de $t$.

2. **Iteração**:

$$
OF^{(t+1)}(v) = \min_{u \in N(v)} \big\lbrace C(v, u) + OF^{(t)}(u) \big\rbrace, \quad \forall v \in V\setminus\lbrace r \rbrace.
$$

3. **Finalização**:

    O algoritmo retorna $OF=OF^{(t+1)}$ quando $OF^{(t+1)}(v) = OF^{(t)}(v)$, $\forall v \in V$.

## *Demonstração da Convergência*

Vamos demonstrar formalmente que a construção iterativa de $OF$ converge no modelo apresentado. A convergência é garantida pelas propriedades de **monotonicidade**, **finitude dos estados**, e **propagação topológica** da função objetivo ($OF$).

### Hipóteses

1. O grafo $G = (V, E)$ é um grafo conexo.

2. A função custo $C: E \to \mathbb{R}^+$ satisfaz $C(u, v) > 0$ para todas as arestas $(u, v) \in E$.

3. A função objetivo $OF: V \to \mathbb{R}$ é definida iterativamente como:

$$
OF^{(t+1)}(v) =
\begin{cases}
0, & \text{se } v = r, \\
\min_{u \in N_G(v)} \big(C(v, u) + OF^{(t)}(u)\big), & \text{caso contrário}.
\end{cases}
$$

Onde $r \in V$ é a raiz e $N_G(v)$ é a vizinhança de $v$ no grafo $G$.

4. A inicialização de $OF^{(0)}$ é dada por:

$$
OF^{(0)}(v) =
\begin{cases}
0, & \text{se } v = r, \\
+\infty, & \text{caso contrário}.
\end{cases}
$$

5. A convergência ocorre quando:
$$
OF^{(t+1)}(v) = OF^{(t)}(v), \quad \forall v \in V.
$$

### Prova:

#### 1. **Monotonicidade**

Pela definição de $OF^{(t+1)}(v)$, temos:

$$
OF^{(t+1)}(v) = \min_{u \in N_G(v)} \big(C(v, u) + OF^{(t)}(u)\big).
$$

Como $C(v, u) > 0$ e $\min$ seleciona o menor valor, segue que:

$$
OF^{(t+1)}(v) \leq OF^{(t)}(v), \quad \forall t \geq 0, \forall v \in V.
$$

Isso implica que a sequência $\lbrace OF^{(t)}(v) \rbrace _{t=0}^\infty$ é **monótona não crescente** para cada nó $v \in V$.

#### 2. **Finitude**

Os valores de $OF^{(t)}(v)$ são limitados inferiormente por $0$, já que:

$C(v, u) > 0$ implica que $OF(v)$ não pode assumir valores negativos.

Assim, temos:

$$
0 \leq OF^{(t+1)}(v) \leq OF^{(t)}(v), \quad \forall t \geq 0.
$$

Como $\lbrace OF^{(t)}(v) \rbrace _{t=0}^\infty$ é monótona e limitada inferiormente, segue do **teorema da convergência de sequências monótonas** que:

$$
\lim_{t \to \infty} OF^{(t)}(v) \text{ existe para todo } v \in V.
$$

#### 3. **Propagação Topológica**

O cálculo de $OF^{(t)}(v)$ em $t+1$ depende apenas dos valores $OF^{(t)}(u)$ para $u \in N_G(v)$.

Consideremos o comprimento do caminho mais curto do nó $v$ até a raiz $r$ em $G$, denotado como $d(v, r)$:

- Se $d(v, r) = 1$, então $OF^{(1)}(v)$ é computado diretamente a partir de $C(v, r)$.

- Se $d(v, r) = k$, então $OF^{(k)}(v)$ será atualizado corretamente, pois depende de $OF^{(k-1)}(u)$ dos nós $u$ a uma distância menor de $r$.

#### 4. **Convergência em $n - 1$ Iterações**

Em um grafo com $n$ nós, o comprimento máximo de qualquer caminho simples é $n - 1$ (em um grafo conexo).

Após $n - 1$ iterações, todos os nós $v \in V$ terão seus valores $OF(v)$ estabilizados, pois o custo acumulado terá sido propagado da raiz para todos os outros nós.

#### 5. **Estabilização**

Como $OF^{(t+1)}(v) \leq OF^{(t)}(v)$ e os valores são atualizados apenas quando ocorre uma redução, o algoritmo estabiliza em no máximo $n - 1$ iterações.

No ponto de estabilização, temos:

$$
OF^{(t+1)}(v) = OF^{(t)}(v), \quad \forall v \in V.
$$

Portanto, o algoritmo sempre atinge um estado estável ($OF^{(t+1)} = OF^{(t)}$) em um número finito de iterações.