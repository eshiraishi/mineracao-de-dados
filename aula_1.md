# [Aula 1](https://youtu.be/udtIrcRKGS8) - Introdução

## Definição

Mineração de dados é a análise de **dados observacionais** (frequentemente grandes) para encontrar **relações desconhecidas** e para sumarizar os dados em formas que sejam **compreensíveis** e **úteis** para o dono dos dados.

## Processo KDD (*Knowledge Discovery from Databases*)

![KDD](http://www2.cs.uregina.ca/~dbd/cs831/notes/kdd/kdd.gif)

Processo que leva à descoberta de conhecimento a partir de bases de dados, envolvendo as seguintes fases:

1. **Seleção** - Criação de um conjunto de dados alvo, focando em um conjunto de variáveis e exemplos em que o processo será aplicado.
2. **Limpeza e pré-processamento**, com o intuito de obter um conjunto consistente de dados.
3. **Transformação**: preparação dos dados de acordo com a técnica de modelagem a ser utilizada.
4. **Mineração de dados**: busca por padrões de interesse, dependendo dos objetivos do processo.
5. **Interpretação / avaliação**: análise dos padrões obtidos.

## CRISP-DM (*Cross-industry standard process for data mining*)

![CRISP-DM](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/CRISP-DM_Process_Diagram.png/598px-CRISP-DM_Process_Diagram.png)
Modelo de mineração de dados mais focado em valorizar a avaliação dos dados e entendimento de negócio dos dados extraídos, equiparando os processo de KDD e mineração de dados, passando pelas seguintes etapas:

1. **Entendimento do problema** -  foco na fase de entendimento dos objetivos e requisitos do processo, a partir de uma perspectiva de negócio. O resultado é a formalização como um problema de mineração de dados, e um plano inicial para atingir esses objetivos.
2. **Entendimento dos dados** - faz uma análise exploratória dos dados, para identificar problemas e descobrir os primeiros insights.
3. **Preparação dos dados** - incorpora as fases de seleção, limpeza e transformação do processo de KDD.
4. **Modelagem** - Similar à fase de mineração de dados do processo de KDD.
5. **Avaliação** - verifica se os resultados obtidos são compatíveis com os elencados na etapa de entendimento do problema.
6. **Implantação** - busca incorporar os resultados obtidos nos processos decisórios.

## [TDSP (*Team Data Science Process*)](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/overview)

![TDSP](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/media/overview/tdsp-lifecycle2.png)

Processo menos linear e mais pensado na integração com o desenvolvimento de software moderno. É baseado no SCRUM que reconhece a necessidade de uma equipe com diferentes atores, como:

- Arquiteto de solução
- Gerente de projeto
- Engenheiro de dados
- Cientista de dados
- Desenvolvedor de aplicativos
- Líder do projeto

## Outros

Assuntos relevantes para mineração de dados, embora não sejam mencionados no curso:

- Extração de dados
  - *Crawlers*
  - APIs
- Armazenamento e organização de dados
  - *Data Warehouse*
  - *Online Analytic Processing* (OLAP)
- Implantação
  - Serviços
  - Aplicações
  - Integração
