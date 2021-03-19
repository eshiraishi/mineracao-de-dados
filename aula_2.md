
# [Aula 2](youtu.be/x2J9vgHpyuU) - Principais características dos dados

## Bases de dados

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

## Tipos de Atributos

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

## Qualidade dos dados

A qualidade do modelo gerado depende diretamente da qualidade dos dados que o geraram. Por isso é muito importante garantir sua qualidade, desconsiderando apenas defeitos independentes da obtenção dos dados (erros de medição, por exemplo).

- **Dados discrepantes (*Outliers*):** Descrevem objetos que são diferentes demais do conjunto. Não significam um erro de medição e podem ser naturais, porém não representam o todo e precisam ser detectados.
- **Dados ausentes:** São problemáticos porque em geral não são analisáveis na base de dados. Podem ser:
  - ***Missing completely at random***: A probabilidade do valor ausente ocorrer não depende de outro valor da base de dados. Exemplo: Erro de gravação em um SGBD.
  - ***Missing at random***: A probabilidade do valor ausente ocorrer depende dos valores conhecidos na base de dados. Em geral é possível estimar um valor nesse caso. Exemplo: Perguntas de resposta opcional em um formulário.
  - ***Missing not at random***: A probabilidade do valor ausente ocorrer depende do próprio valor ausente. Em geral estimar valores nesse caso não é confiável, a não ser que exista outro atributo com alta correlação. Exemplo: Um formulário onde a resposta não ser informada pode ser uma característica a ser analisada, como por exemplo a tendência de pessoas com alta renda não informarem sua faixa de renda em um censo.
- **Representatividade e Viés de Seleção:** A base de dados precisa representar a população corretamente para que a análise não fique enviesada estatisticamente.
- **Desvio populacional:** Correlações, modelos e outras análises podem perder sua validade conforme certos fatores do conjunto de dados iniciais se tornam defasados. Por exemplo, mesmo que um modelo de detecção de spam seja muito eficiente, ele pode perder sua funcionalidade caso os *spammers* descubram o padrão e comecem a mandar e-mails não detectados.
