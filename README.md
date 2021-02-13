# Mineração de Dados

Disciplina cursada na UFABC em 2021.1, ministrada pelo [Prof. Dr. Ronaldo Cristiano Prati](http://professor.ufabc.edu.br/~ronaldo.prati/MineracaoDados/grad2021/).

- [Mineração de Dados](#mineração-de-dados)
  - [Aula 1: Introdução](#aula-1-introdução)
    - [Definição](#definição)
    - [Processo KDD (*Knowledge Discovery from Databases*)](#processo-kdd-knowledge-discovery-from-databases)
    - [CRISP-DM (*Cross-industry standard process for data mining*)](#crisp-dm-cross-industry-standard-process-for-data-mining)
    - [TDSP (*Team Data Science Process*)](#tdsp-team-data-science-process)
    - [Outros](#outros)
  - [Aula 2 - Principais características dos dados](#aula-2---principais-características-dos-dados)
    - [Bases de dados](#bases-de-dados)
    - [Tipos de Atributos](#tipos-de-atributos)
    - [Qualidade dos dados](#qualidade-dos-dados)

## [Aula 1](https://youtu.be/udtIrcRKGS8): Introdução

### Definição

Mineração de dados é a análise de **dados observacionais** (frequentemente grandes) para encontrar **relações desconhecidas** e para sumarizar os dados em formas que sejam **compreensíveis** e **úteis** para o dono dos dados.

### Processo KDD (*Knowledge Discovery from Databases*)

![KDD](http://www2.cs.uregina.ca/~dbd/cs831/notes/kdd/kdd.gif)

Processo que leva à descoberta de conhecimento a partir de bases de dados, envolvendo as seguintes fases:

1. **Seleção** - Criação de um conjunto de dados alvo, focando em um conjunto de variáveis e exemplos em que o processo será aplicado.
2. **Limpeza e pré-processamento**, com o intuito de obter um conjunto consistente de dados.
3. **Transformação**: preparação dos dados de acordo com a técnica de modelagem a ser utilizada.
4. **Mineração de dados**: busca por padrões de interesse, dependendo dos objetivos do processo.
5. **Interpretação / avaliação**: análise dos padrões obtidos.

### CRISP-DM (*Cross-industry standard process for data mining*)

![CRISP-DM](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/CRISP-DM_Process_Diagram.png/598px-CRISP-DM_Process_Diagram.png)
Modelo de mineração de dados mais focado em valorizar a avaliação dos dados e entendimento de negócio dos dados extraídos, equiparando os processo de KDD e mineração de dados, passando pelas seguintes etapas:

1. **Entendimento do problema** -  foco na fase de entendimento dos objetivos e requisitos do processo, a partir de uma perspectiva de negócio. O resultado é a formalização como um problema de mineração de dados, e um plano inicial para atingir esses objetivos.
2. **Entendimento dos dados** - faz uma análise exploratória dos dados, para identificar problemas e descobrir os primeiros insights.
3. **Preparação dos dados** - incorpora as fases de seleção, limpeza e transformação do processo de KDD.
4. **Modelagem** - Similar à fase de mineração de dados do processo de KDD.
5. **Avaliação** - verifica se os resultados obtidos são compatíveis com os elencados na etapa de entendimento do problema.
6. **Implantação** - busca incorporar os resultados obtidos nos processos decisórios.

### [TDSP (*Team Data Science Process*)](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/overview)

![TDSP](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/media/overview/tdsp-lifecycle2.png)

Processo menos linear e mais pensado na integração com o desenvolvimento de software moderno. É baseado no SCRUM que reconhece a necessidade de uma equipe com diferentes atores, como:

- Arquiteto de solução
- Gerente de projeto
- Engenheiro de dados
- Cientista de dados
- Desenvolvedor de aplicativos
- Líder do projeto

### Outros

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

## [Aula 2](youtu.be/x2J9vgHpyuU) - Principais características dos dados

### Bases de dados

- Formas de armazenamento como arquivos, SGBD, etc.
  - Tabelas (CSV, Excel, DataFrames, etc.)
  - Pares Chave-Valor (XML, JSON, dicts, Redis, etc.)
  - Grafos e estruturas em grafos (Kafka, MongoDB, etc.)
  - *Data Warehouses*
  - Séries temporais, sequências e séries
  - Sistemas distribuídos (SQL, Hadoop, etc.) e APIs
- **Qualidade dos dados:** nenhuma base de dados é perfeita e diferentes problemas podem surgir com elas
  - Valores ausentes
  - Erro humano
  - Sensores / coletores de dados defeituosos

### Tipos de Atributos

- **Escala:** Em geral a análise exploratória dos dados é iniciada examinando os tipos de cada dado. A forma mais comum de examinar o tipo dos dados é em relação a sua escala, que determina o tipo de atividades que podem ser feitas com aquele tipo de dado.
  - **Tipos categóricos:**
    - **Nominal:** Categorias que não tem uma ordem natural, como gênero, etnia, país. Em geral, só é possível fazer operaçẽos de igualdade ou diferença para esse tipo de atributo.
    - **Ordinal:** Categorias ordenadas, como tamanhos de roupa, nível educacional. Além das operações dos nominais é possível fazer operações quantitativas (maior, menor, maior ou igual, menor e igual).
    - **Intervalar:** Valores que podem ser colocados em um intervalo contínuo, como temperatura e massa. Além das operações dos ordinais, é possível fazer operações de subtração e soma. O zero não é sua origem.
    - **Proporcional:** Valores intervalares onde o zero é a origem. Permitem operações de soma e subtração.

      | Tipo         | Operação mais complexa |
      | ------------ | ---------------------- |
      | Nominal      | =, $\neq$              |
      | Ordinal      | <, >, $\leq$, $\geq$   |
      | Intervalar   | +, -                   |
      | Proporcional | *, /                   |

  - **Tipos Assimétricos:** Dados não estruturados discretos ou contínuos onde apenas valores diferentes de 0 são relevantes. Por exemplo, vetores binários.

### Qualidade dos dados

A qualidade do modelo gerado depende diretamente da qualidade dos dados que o geraram. Por isso é muito importante garantir sua qualidade, desconsiderando apenas defeitos independentes da obtenção dos dados (erros de medição, por exemplo).

- **Dados discrepantes (*Outliers*):** Descrevem objetos que são diferentes demais do conjunto. Não significam um erro de medição e podem ser naturais, porém não representam o todo e precisam ser detectados.
- **Dados ausentes:** São problemáticos porque em geral não são analisáveis na base de dados. Podem ser:
  - ***Missing completely at random***: A probabilidade do valor ausente ocorrer não depende de outro valor da base de dados. Exemplo: Erro de gravação em um SGBD.
  - ***Missing at random***: A probabilidade do valor ausente ocorrer depende dos valores conhecidos na base de dados. Em geral é possível estimar um valor nesse caso. Exemplo: Perguntas de resposta opcional em um formulário.
  - ***Missing not at random***: A probabilidade do valor ausente ocorrer depende do próprio valor ausente. Em geral estimar valores nesse caso não é confiável, a não ser que exista outro atributo com alta correlação. Exemplo: Um formulário onde a resposta não ser informada pode ser uma característica a ser analisada, como por exemplo a tendência de pessoas com alta renda não informarem sua faixa de renda em um censo.
- **Representatividade e Viés de Seleção:** A base de dados precisa representar a população corretamente para que a análise não fique enviesada estatisticamente.
- **Desvio populacional:** Correlações, modelos e outras análises podem perder sua validade conforme certos fatores do conjunto de dados iniciais se tornam defasados. Por exemplo, mesmo que um modelo de detecção de spam seja muito eficiente, ele pode perder sua funcionalidade caso os *spammers* descubram o padrão e comecem a mandar e-mails não detectados.
