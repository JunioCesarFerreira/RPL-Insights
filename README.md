# RPL-Insights

Este repositório é dedicado a armazenar estudos teóricos e práticos sobre o RPL (Routing Protocol for Low-Power and Lossy Networks) e o DODAG (Destination-Oriented Directed Acyclic Graph).

Neste repositório você encontrará alguns notebooks Python explorando a teoria e o funcionamento do protocolo RPL.

## Organização do Repositório

O repositório possui dois sub-diretórios: um para notebooks Jupyter e outro para notas em Markdown. A seguir catalogamos o material destes diretórios.

### Notebooks

- [Protótipo RPL simplificado](./notebooks/rpl-dodag-first-simulation.ipynb): Neste notebook é apresentada a construção básica do DODAG utilizando uma métrica simples. 

- [Modelagem da Construção DODAG](./notebooks/basic-dodag.ipynb): Neste notebook apresentamos uma formalização matemática da construção do DODAG e um exemplo de implementação do modelo.

### Markdowns

- [Terminologia](./markdown/Terminologia.md): Terminologia utilizada no protocolo RPL. Baseada no [video](https://www.youtube.com/watch?v=kSiUGeUgJYQ) e revisada com base no [artigo](https://doi.org/10.2313/NET-2011-07-1_09).

- [Mensagens de Controle RPL](./markdown/MensagensRPL.md): Apresentação das mensagens de controle e construção da rede DODAG. 

- [Formalização da Construção DODAG](./markdown/Formalização.md): Modelagem matemática do DODAG.

    - [Construção Iterativa da Função Objetivo](./markdown/ConvergenciaOF.md).

    - [Demonstração Propriedades DODAG](./markdown/PropriedadesDODAG.md).


---

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.