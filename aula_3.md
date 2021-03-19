
# [Aula 3](youtu.be/H1Ure6K-p9Y) - Análise Exploratória de Dados e Estimação de Densidade

A análise exploratória de dados é importante porque com um conjunto de dados, um conjunto de metadados é fornecido, que definem características do conjunto como o nome dos atributos, sua origem e ao que se referem, entre outros. Usando eles, é possível definir a estratégia para analisar esses dados.

## Estatística Descritiva

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

## Visualização dos dados

Diversos indicadores sobre os dados podem ser obtidos com a plotagem de gráficos. Entre ele podemos citar:

- ***Boxplots* ou gráficos de caixa**: Formado por "caixas", onde cada caixa representa um atributo: as linhas dentro de cada caixa são marcadas na altura da mediana, a inferior representa o primeiro quartil, a superior o terceiro quartil, e as linhas verticais inferiores e superiores representam os valores máximo e mínimo respectivamente (considerando como uma linha só, representam a amplitude do atributo).

- **Histogramas:** Gráfico de barras que demonstra para um determinado atributo, a distribuição de frequências de forma discreta. Histogramas deixam a visualização das medidas de tendência central muito claras e mostram outras características como obliquidade, curtose e centralidade (número de picos) do conjunto de dados.

## Densidade dos dados

Diversos algoritmos de mineração de dados (em especial os de predição de forma contínua) envolvem a estimativa de densidade de um conjunto. Existem duas formas de se estimar densidade:

## Abordagem paramétrica

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

## Abordagem não-paramétrica

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
