# Formalização de Modelo Matemático

---

Um modelo matemático para o protocolo RPL (Routing Protocol for Low-Power and Lossy Networks) com a topologia **DODAG (Destination-Oriented Directed Acyclic Graph)** pode ser desenvolvido considerando os seguintes componentes principais:

1. **Topologia da Rede e Definição do Grafo**  
   Representamos a rede como um grafo direcionado $G = (V, E)$, onde:
   - $V$ é o conjunto de nós na rede, incluindo sensores, atuadores e gateways.
   - $E$ é o conjunto de arestas representando as conexões entre os nós.

2. **Raiz do DODAG**  
   A topologia do DODAG é orientada em direção a um nó destino, conhecido como **raiz** $r \in V$. Todo caminho válido em $G$ é um caminho sem ciclos que conecta qualquer nó $v \in V$ à raiz $r$.

3. **Métricas e Função Objetivo**  
   Cada nó $v$ escolhe um "pai preferido" com base em uma **função objetivo** $OF(v)$, que avalia o custo da rota com base em métricas $M_i(v)$:

$$
OF(v) = \min_{u \in N(v)} \{ C(v, u) + OF(u) \}
$$

   Onde:
   - $N(v)$ é o conjunto de vizinhos de $v$.
   - $C(v, u)$ é o custo associado à aresta entre $v$ e $u$, que pode ser calculado usando métricas como:
     - Força do sinal (RSSI): $C_{RSSI}(v, u)$
     - Energia consumida: $C_{Energy}(v, u)$
     - Latência: $C_{Latency}(v, u)$
   - $OF(u)$ é o custo acumulado do nó $u$ até a raiz $r$.

4. **Construção do DODAG**  
   O DODAG é construído iterativamente:
   - Inicialmente, $OF(r) = 0$ para a raiz.
   - Cada nó $v$ calcula $OF(v)$ com base nos nós vizinhos $N(v)$, propagando as informações até que todos os nós tenham definido seus valores.

5. **Modelagem Matemática do RPL**
   O funcionamento do protocolo pode ser descrito em termos de um sistema de equações baseadas em $OF$:

$$
OF(v) = \min_{u \in N(v)} \{ C(v, u) + OF(u) \}, \quad \forall v \in V \setminus \{r\}
$$

6. **Mensagens no Protocolo**  
   O protocolo utiliza três tipos de mensagens:
   - **DIO (DODAG Information Object):** Propaga informações sobre $OF$ e ajuda na construção da topologia.
   - **DAO (Destination Advertisement Object):** Anuncia destinos alcançáveis para rotas de retorno.
   - **DIS (DODAG Information Solicitation):** Solicita informações de configuração ao DODAG.

   Formalizamos a propagação das mensagens como um sistema iterativo:

$$
M_{DIO}(v, u) = \text{Atualizar } OF(u) \text{ com base em } C(v, u) + OF(v)
$$

7. **Convergência e Propriedades**  
   - **Convergência:** O algoritmo converge para um estado estável onde $OF(v)$ é conhecido para todos os $v \in V$.
   - **Sem ciclos:** A estrutura acíclica é garantida por $C(v, u) > 0$ e pela definição do grafo como direcionado.

---

### Grafo inicial

Seja $V$ um conjunto de pontos em $\mathbb{R}^n$ ($n$ deve ser 2 ou 3 dependendo da aplicação). Definimos $\phi\in\mathbb{R}$ o raio de alcance, supondo que cada ponto possui o mesmo raio de alcance. Agora definimos o grafo $G=(V,E)$ onde $E$ é definido da seguinte forma:

$$
E:=\{(u,v)\in V\times V : d(u,v)<\phi\}
$$

sendo $d$ a distância euclidiana.

**Importante** 

A partir deste ponto, consideraremos que $G=(V,E)$ é um grafo conexo, e escolhemos um vértice $r\in V$ para ser a raiz. 

### Vizinhança
Defina $N_G:V\rightarrow 2^V$ a função que indica quais são os vizinhos de um vértice $v\in V$. 

$$
N_G(v):=\{u_1,u_2,...,u_k\}\Leftrightarrow \exists(u_i,v)\in E, \forall i\in\{1,2,...,k\}.
$$

Para simplificar a notação, denotaremos $N_G(v)$ como $Nv$, o conjunto de vizinhos de $v$ no grafo $G$.


### Função Custo
Denotamos $C:E\rightarrow \mathbb{R}^+$ a função custo ou peso da aresta. Esta função pode ser definida de várias formas, no caso mais simples *hop count* esta é constante igual a 1. Além disso, para qualquer $(u,v)\in E$, $C(u,v)>0$, esta restrição é importante para garantir que o digrafo seja aciclico.

### Função Objetivo
A função objetivo $OF:V\rightarrow\mathbb{R}$ é definida por:

$$
OF(v):=\begin{cases}
0, &\text{se }v=r,\\
\min_{u \in Nv} \big( C(v, u) + OF(u) \big), &\text{se }v\neq r.
\end{cases}
$$

Assim $OF(v)$ é o custo acumulado do nó $v$ até a raiz $r$.

Em geral precisamos definir $OF$ iterativamente, isso é feito da seguinte forma:
1. Inicialização:

$$
OF^{(0)}(v) =
\begin{cases}
0, & \text{se } v = r, \\
+\infty, & \text{caso contrário}.
\end{cases}
$$

2. Iteração:

$$
OF^{(t+1)}(v) = \min_{u \in N(v)} \big \{ C(v, u) + OF^{(t)}(u) \big \}, \quad \forall v \in V.
$$

3. Convergência:
O algoritmo para quando $OF^{(t+1)}(v) = OF^{(t)}(v)$, $\forall v \in V$.


## Construção do DODAG

Definimos o digrafo DODAG como $D = (V, E_D)$, onde $E_D$ é construído com base na função objetivo $OF$:

$$
E_D := \big \{(u, v) \in E : v = \arg \min_{w \in N_G(u)} \big( C(u, w) + OF(w) \big) \big \}.
$$

#### Propriedades do DODAG:
1. **Aciclicidade:** Garante-se que $D$ é um digrafo acíclico devido à propriedade $C(u, v) > 0$, que impede ciclos positivos no grafo.
2. **Orientação ao Destino:** Todos os caminhos convergem para o vértice raiz $r$.

#### Algoritmo de Construção:
1. Inicialização:

   $D = (V, \emptyset)$.

2. Construção Iterativa:

   Para cada $v \in V \setminus \{r\}$, identifique $u$ tal que:

$$
u = \arg \min_{w \in N_G(v)} \big( C(v, w) + OF(w) \big).
$$

   Adicione $(u, v)$ a $E_D$.

3. Finalização:

   Retorne $D = (V, E_D)$.

#### Validação do DODAG:
   A conectividade do grafo inicial $G$ e a definição de $C(u, v) > 0$ garantem que:
   - Todos os vértices $v \in V$ têm um caminho até a raiz $r$.
   - Não há ciclos no grafo resultante.


