# Terminologia

- **Directed Acyclic Graph (DAG)**: Um grafo dirigido que não possui ciclos, ou seja, nenhuma sequência de arestas forma um caminho fechado. É usado como base para a construção da topologia no protocolo RPL.

- **Root**: O nó raiz do DAG, que serve como ponto de destino principal para toda a comunicação na rede. É o nó mais importante em um DODAG, geralmente responsável por interagir com redes externas.

- **Up**: Uma aresta ou direção no DODAG que aponta em direção ao nó raiz.

- **Down**: Uma aresta ou direção no DODAG que aponta para longe do nó raiz.

- **Destination Oriented Directed Acyclic Graph (DODAG)**: Um DAG orientado a destino onde todos os nós direcionam seus pacotes a um nó específico, o nó raiz.

- **Objective Function (OF)**: Uma função utilizada para determinar a proximidade relativa de um nó à raiz, com base em métricas e restrições definidas (por exemplo, número de saltos, latência, energia restante). A OF define como o Rank é calculado e influencia na construção da topologia.

- **Grounded DODAG**: Um DODAG que está conectado ao destino principal e atende a um objetivo definido pela aplicação, como o encaminhamento de dados.

- **Floating DODAG**: Um DODAG desconectado do destino principal ou que não atende a um objetivo definido. Ele é considerado "flutuante" e só suporta conectividade local.

- **Storing Nodes**: Nós que mantêm tabelas de roteamento completas, permitindo o armazenamento de informações sobre rotas para outros nós na rede.

- **Non-Storing Nodes**: Nós que não mantêm tabelas de roteamento completas. Eles encaminham pacotes com base em informações fornecidas pelo nó raiz.

- **Rank**: Um valor numérico que indica a posição de um nó em relação à raiz no DODAG. O Rank aumenta à medida que o nó está mais distante da raiz.

- **RPL Instance**: Uma instância lógica do protocolo RPL que agrupa um ou mais DODAGs, otimizados para um cenário ou aplicação específica.

- **DODAG ID**: Um identificador único atribuído ao nó raiz, que permite distinguir diferentes DODAGs dentro de uma mesma RPL Instance.

- **Parent Node**: Um nó diretamente conectado em direção à raiz no DODAG. É escolhido com base na Objective Function.

- **Child Node**: Um nó que seleciona o nó atual como seu pai e está mais distante da raiz.

- **Sub-DODAG**: Uma subárvore dentro de um DODAG, composta por um nó e todos os seus descendentes.

Essas definições são baseadas no comportamento e terminologia descritos na especificação do RPL e nas aplicações práticas do protocolo em redes LLNs.

**Referência**  
Tsvetkov, T. (2011). *RPL: IPv6 Routing Protocol for Low Power and Lossy Networks*. Technische Universität München. Disponível em: [https://doi.org/10.2313/NET-2011-07-1_09](https://doi.org/10.2313/NET-2011-07-1_09)