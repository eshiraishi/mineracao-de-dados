# [Aula 6](https://youtu.be/LLVuK1J0Sag) - Relações nos Dados

Para estudar a relação entre dados é preciso dividi-los em duas categorias:

- Variáveis explanatórias ou independentes
- Variáveis resposta ou dependentes

Nem sempre esses papéis são claros no conjunto de dados e as vezes, dependendo da modelagem as duas variáveis podem exercer os dois papéis.

Uma ferramenta interessante para determinar o tipo de correlação é a análise exploratória e visualização dos dados. Uma forma simples de identificá-los é usar gráficos de dispersão (*scatterplots*) para buscar tanto padrões como direções, formas ou intensidade da correlação de forma qualitativa ou buscar outliers no conjunto.

No caso de relações lineares, é possível identficar se a relação é positiva ou negativa avaliando o coeficiente angular da reta estimada (redução no valor de uma variável contínua implica na redução de outra, por exemplo). Com a exceção de casos como curvas logarítmicas ou exponenciais, no caso de relações descritas por curvas mais complexas essa análise pode não ser facilmente visível de forma qualitativa.

A dispersão também pode indicar a formação de grupos (*clusters*).

## Relacionamento linear

### Coeficiente de relação (r)

Indica a força e direção da relação linear e é usado para avaliar o quão próximo de um relacionamento linear as variáveis estão:

$$
    r = \frac 1{n − 1} \sum^n_{i=1} \left(\frac{x_i − \bar x} {S_x} \right) \left(\frac{y_i − \bar y} {S_y}\right) \\
    S_k = \sqrt{\frac 1 {n−1} \sum^n_{i=1}(k_i − \bar{k})^2} \\
    \text{(Desvio amostral)}
$$

Com esse valor é possível gerar uma matriz de correlação (R) para identificar a força da correlação entre os valores.

### Regressão linear

Dado que as variáveis são relacionadas, para predizer seu comportamento é preciso encontrar a reta ótima que minimiza a distância entre os valores preditos e os valores reais. É possível usar diversos métodos, sendo o mais simples deles a aproximação por mínimos quadrados, que visa minimizar o quadrado das distâncias:
$$
    Y = aX + b \\
    b = r\left(\frac {S_x}{S_y}\right) \\
    a = \bar Y - b\bar X \\
$$

## Correlação vs. Causa

Nem sempre a correlação entre duas variáveis tem valor qualitativo e uma explicação analítica pode ser encontrada.

## Paradoxo de Simpson

Não se pode confiar cegamente nos dados e suas métricas quando se busca uma resposta analítica. Em certos contextos uma variável de confusão pode trazer informações que numericamente são verdadeiras, mas não necessariamente são verdadeiras. É preciso nesses casos analisar o contexto para entender a situação.
