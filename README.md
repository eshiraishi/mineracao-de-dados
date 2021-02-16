# Mineração de Dados

Disciplina cursada na UFABC em 2021.1, ministrada pelo [Prof. Dr. Ronaldo Cristiano Prati](http://professor.ufabc.edu.br/~ronaldo.prati/MineracaoDados/grad2021/).

- [Mineração de Dados](#mineração-de-dados)
  - [Aula 1 - Introdução](#aula-1---introdução)
    - [Definição](#definição)
    - [Processo KDD (*Knowledge Discovery from Databases*)](#processo-kdd-knowledge-discovery-from-databases)
    - [CRISP-DM (*Cross-industry standard process for data mining*)](#crisp-dm-cross-industry-standard-process-for-data-mining)
    - [TDSP (*Team Data Science Process*)](#tdsp-team-data-science-process)
    - [Outros](#outros)
  - [Aula 2 - Principais características dos dados](#aula-2---principais-características-dos-dados)
    - [Bases de dados](#bases-de-dados)
    - [Tipos de Atributos](#tipos-de-atributos)
    - [Qualidade dos dados](#qualidade-dos-dados)
  - [Aula 3 - Análise Exploratória de Dados e Estimação de Densidade](#aula-3---análise-exploratória-de-dados-e-estimação-de-densidade)
    - [Estatística Descritiva](#estatística-descritiva)
    - [Visualização dos dados](#visualização-dos-dados)
    - [Densidade dos dados](#densidade-dos-dados)
    - [Abordagem paramétrica](#abordagem-paramétrica)
    - [Abordagem não-paramétrica](#abordagem-não-paramétrica)
  - [Aula 4 - Análise Exploratória de Dados (EDA) com Python e Pandas](#aula-4---análise-exploratória-de-dados-eda-com-python-e-pandas)

## [Aula 1](https://youtu.be/udtIrcRKGS8) - Introdução

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

## [Aula 3](youtu.be/H1Ure6K-p9Y) - Análise Exploratória de Dados e Estimação de Densidade

A análise exploratória de dados é importante porque com um conjunto de dados, um conjunto de metadados é fornecido, que definem características do conjunto como o nome dos atributos, sua origem e ao que se referem, entre outros. Usando eles, é possível definir a estratégia para analisar esses dados.

### Estatística Descritiva

O primeiro passo da análise exploratória é tomar as estatísticas descritivas do conjunto, mais especificamente:

- **Medidas de tendência central:** O valor típico para certo atributo (média, mediana, moda)
- **Dispersão:** O quanto os valores do conjunto variam da tendência central (variância, desvio padrão)

**Exemplo:** O Quarteto de Anscombe é uma base de dados muito simples (com 11 objetos e 2 atributos cada), que mostra quatro versões de uma mesma base de ddados que embora estejam dispersos de formas muito distintas, suas medidas de tendência central são quase idênticas.

![Gráficos do Quarteto de Anscombe](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Anscombe%27s_quartet_3.svg/1200px-Anscombe%27s_quartet_3.svg.png)
![Medidas de Tendência Central para o Quarteto de Anscombe](https://5ce827599a409a488a3c361c.static-01.com/l/images/207a623a392baeded6139fb4a463144d84ef50f4.png)

Outras medidas de estatística descritiva úteis são:

- **Quartil:** divide o conjunto de dados em 4 grupos que compõe 25% do grupo, e medem características como concentração e dispersão da mediana, por exemplo.
  |          |              |
  | -------- | ------------ |
  | Primeiro | Mínimo - 25% |
  | Segundo  | 25% - 50%    |
  | Terceiro | 50% - 75%    |
  | Quarto   | 75% - Máximo |
- **Amplitude interquartil:** Mede a variância entre quartis.
- **Obliquidade (*skewness*):** mede a assimetria da cauda de uma distribuição. Distribuições simétricas tem $v \approx 0$, e caudas para esquerda ou direita são indicadas por $v < 0$ ou $v > 0$.
  $$
    v = \frac {\mu_3} {\sigma^3} \\
    \mu_3: \text{Terceiro momento}
  $$
- **Curtose ou achatamento:** Mede a concentração ou dispersão de valores de um conjunto em relação à distribuição Gaussiana. É divida em 3 classes:
  - **Mesocúrtica ($Kurt \approx 0$):** similar à Normal.
  - **Leptocúrtica ($Kurt \gtrapprox 0$):** Mais fechada (menos achatada) que a Normal.
  - **Platicúrtica ($Kurt \lessapprox 0$):** Mais aberta (mais achatada) que a Normal.
  $$
    Kurt = \frac {\mu_4} {\sigma^4} -3 \\~\\
    \mu_4: \text{Quarto momento}
  $$

### Visualização dos dados

Diversos indicadores sobre os dados podem ser obtidos com a plotagem de gráficos. Entre ele podemos citar:

- ***Boxplots* ou gráficos de caixa**: Formado por "caixas", onde cada caixa representa um atributo: as linhas dentro de cada caixa são marcadas na altura da mediana, a inferior representa o primeiro quartil, a superior o terceiro quartil, e as linhas verticais inferiores e superiores representam os valores máximo e mínimo respectivamente (considerando como uma linha só, representam a amplitude do atributo).

- **Histogramas:** Gráfico de barras que demonstra para um determinado atributo, a distribuição de frequências de forma discreta. Histogramas deixam a visualização das medidas de tendência central muito claras e mostram outras características como obliquidade, curtose e centralidade (número de picos) do conjunto de dados.

### Densidade dos dados

Diversos algoritmos de mineração de dados (em especial os de predição de forma contínua) envolvem a estimativa de densidade de um conjunto. Existem duas formas de se estimar densidade:

### Abordagem paramétrica

Nessa abordagem assume-se um modelo de distribuição para uma variável. Embora Traga mais rigidez para o modelo, também traz maior previsibilidade.
  
Para essa abordagem é preciso saber anteriormente a distribuição dos dados (e assumir que os dados futuros terão a mesma distribuição). Ela independe do modelo usado, embora a distribuição Normal seja quase sempre a considerada.
$$
  p(x~;~ \mu, \sigma^2) = \frac 1 {\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}} \\~\\
  \mu: \text{ Define o centro da distribuição} \\
  \sigma^2: \text{Define a concentração dos valores. 68\% está abaixo de }\sigma.
$$
A melhor forma de encontrar os parâmetros que otimizam o modelo é usando o Estimador de Máxima Verossimilhança ou MLE (*Maximum Likelihood Estimate*), uma alternativa simples com boa convergência.
$$
  L(\theta) = \prod^N_{n=1}p(x_n ~ ; ~ \theta)
$$
A função de verossimilhança (L) não é uma densidade de probabilidades em si, e sim uma função de $\theta$ em função das amostras. Ao maximizar o valor de L, se descobre os parâmetros cujo modelo melhor descreve o conjunto de dados.

Frequentemente se otimiza $\log L$ ao invés de L.
$$
  \theta_{ML} = \argmax_\theta L(\theta) \\ ~ \\
  \theta_{ML} \text{ , com algumas ressalvas, pode ser tal que } \\ ~ \\
  L'(\theta) = 0 \\
  L''(\theta) < 0 \\ ~ \\
  \text{ e os parâmetros sejam válidos.}
$$
Se a distribuição for Normal, por exemplo, os parâmetros serão calculados da seguinte forma:
$$
  \theta = \{\mu, \sigma^2\} \\
  p(x~;~ \mu, \sigma^2) = \frac 1 {\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}} \\
  \ln p(x~;~ \mu, \sigma^2) = \ln 1 - \frac 1 2 \ln(2\pi\sigma^2) - \frac 1 {2\sigma^2}(x - \mu)^2 \\
  \ln p(x~;~ \mu, \sigma^2) = -\frac 1 2 \ln(2 \pi \sigma^2) - \frac 1 {2\sigma^2}(x - \mu)^2
$$
Substituindo em $L(\theta)$:
$$
  L(\theta) = \sum^N_{n=1} \ln p(x_n ~;~ \theta) = \sum^N_{n=1} -\frac 1 2 \ln(2 \pi \sigma^2) - \frac 1 {2\sigma^2}(x_n - \mu)^2 \\
  L(\theta) = -\frac N 2 \ln(2\pi) - \frac N 2 \ln(\sigma^2) - \frac 1 {2\sigma^2}\sum^N_{n=1} (x_n - \mu)^2
$$
Derivando $L(\theta)$:
$$
  \frac{dL(\theta)}{d\mu} = -\frac 1 {2\sigma^2} \sum^N_{n=1}\frac{d}{d\mu} (xn - \mu)^2 \\
  \frac{dL(\theta)}{d\mu} = -\frac 1 {2\sigma^2}\sum^N_{n=1}2(x_n-\mu)(-1) = \frac 1 {\sigma^2} \sum^N_{n=1}(x_n - \mu)
$$
Igualando a 0:
$$
  \frac {dL(\theta)} {d\mu} = 0 \implies \frac 1 {\sigma^2} \sum^N_{n=1}(x_n - \mu) = 0 \\
  \sum^N_{n=1}(x_n - \mu) = 0 \\
  \sum^N_{n=1}x_n - N\mu = 0 \\
  \sum^N_{n=1}x_n = N\mu \\
  \mu = \frac{\sum^N_{n=1}x_n}N
$$
Estimando a variância (para simplificar, considere $\theta_1 = \sigma^2$):
$$
  L(\theta) = -\frac N 2 \ln (2\pi) - \frac N 2 \ln \theta_1 - \frac 1 {2\theta_1} \sum^N_{n=1}(x_n - \mu)^2 \\
  \frac{dL(\theta)}{d\theta_1} = -\frac N {2\theta_1} + \frac 1 {2(\theta_1)²}\sum^N_{n=1}(x_n-\mu)^2\left[\frac{d}{dx}\ln x\right] \\
  \frac{dL(\theta)}{d\theta_1} = -\frac N {2\theta_1} + \frac 1 {2(\theta_1)²}\sum^N_{n=1}(x_n-\mu)^2\left(\frac 1 x\right) \\
  \frac{dL(\theta)}{d\theta_1} = \frac 1 {2\theta_1}\left[-N+\frac 1 {\theta_1}\sum^N_{n=1}(x_n - \mu)^2\right]
$$
Estimando a máxima verossimilhança (igualando a 0, lembrando que $\theta_1 = \sigma^2 > 0$):
$$
  \frac{dL(\theta)}{d\theta_1} = 0 \\
  \frac 1 {2\theta_1}\left[-N + \frac 1 {\theta_1} \sum^N_{n=1}(x_n - \mu^2)\right] = 0 \\
  -N + \frac 1 {\theta_1} \sum^N_{n=1}(x_n - \mu^2) = 0 \\
  \frac 1 {\theta_1} \sum^N_{n=1}(x_n - \mu^2) = N \\
  \sum^N_{n=1}(x_n - \mu^2) = N\theta_1 \\
  \theta_1 = \frac {\sum^N_{n=1}(x_n-\mu)^2}{N} \\
  \sigma^2 = \frac {\sum^N_{n=1}(x_n-\mu)^2}{N}
$$
**Observação:** embora nesse caso específico, o impacto não seja alto desde que o número de amostras seja grande, essa abordagem não é perfeita. Ao simplificar $\theta_1$, a verossimilhança se torna enviesada (seu valor está sendo subestimado). O estimador sem viés corresponde a:
$$
  \sigma^2 = \frac {\sum^M_{n=1}(x_n - \mu)^2} {N - 1}
$$

### Abordagem não-paramétrica

Essa abordagem não usa nenhum modelo de distribuição e é úil quando não se conhece a distribuição geradora ou um bom palpite, evitando fazer suposições com resultados ruins. É mais flexível porém pode se tornar inviável quando se tem muitos atributos e precisa de um volume de dados muito maior para ser acurata.

Partindo do histograma de uma distribuição, uma solução ingênua é assumir que:
$$
  \hat{p}(x) = \frac{\text{Altura de cada intervalo}}{Nh} \\
  N: \text{Total de objetos} \\
  h: \text{Comprimento de cada intervalo}
$$
Porém, essa abordagem gera uma função com muitas descontinuidades e uma densidade uniforme para cada intervalo. Além disso, o número de intervalos usados afeta diretamente a densidade obtida.

O método das Janelas de Parzen, que considera regiões de vizinhança, melhora a estimativa. Essa abordagem inclui dois novos parâmetros ao modelo: distância e *kernel* ($K$).
$$
  \text{hipercubo unitário centrado na origem:~} \\~\\
  K(u) = \begin{Bmatrix}
    1, \text{ se }|u| < \frac 1 2 \\
    0, \text{ caso contrário}
  \end{Bmatrix} \\ ~ \\
  \hat  p (x) = \frac 1 {Nh} \sum^N_{n=1}K\left(\frac{x-x_n}h\right)
$$
É possível usar *kernels* alternativos que tragam melhor performance. Nesse caso, o *kernel* suave (contínuo) gaussiano é muito frequente e traz estimativas mais próximas:
$$
  K(u) = \frac 1 {\sqrt{2 \pi}} \exp\left[-\frac {u^2}2\right] \\~\\
  \text{Simplificação: } K(\cdot) = 0 \text{ se } |x - x_n| > 3h
$$
Desde que o pico da distribuição seja em $u=0$ e diminua conforme $|u|$ aumenta, outros *kernels* também podem ser usados. De forma mais completa:
$$
  \int K(u)du = 1 \\
  K(u) \geq 0
$$
O último fator que precisa ser determinado é a largura apropriada. Embora esse valor seja puramente numérico, valores altos ou baixos demais podem comprometer a aproximação de formas diferentes:

- Conforme $h$ reduz, o ruído dos dados impacta mais diretamente a distribuição.
- Conforme $h$ aumenta, a curva se torna mais suave, podendo simplificar demais a aproximação.

Existem diferentes heurísticas baseadas em hipóteses sobre os dados que funcionam corretamente quando as hipóteses se mostram verdadeiras. Porém em geral, esse é mais um hiperparâmetro que deve ser otimizado.

## [Aula 4 - Análise Exploratória de Dados (EDA) com Python e Pandas](https://github.com/eshiraishi/mineracao-de-dados/blob/main/04_EDA.ipynb)
