# [Aula 5](https://youtu.be/u6EwrvsIqB8) - Medidas de dissimilaridade e Escalonamento Multimensional

Vários algoritmos precisam medir a similaridade ou a diferença entre dois objetos, e dependendo do tipo dos dados é possível medi-la de várias formas.

Alguns exemplos (onde s é similaridade e d é dissimilaridade):

$$
    s = -d \\
    s = 1 - d \\
    s = \frac 1 {1 + d} \\
    \text{Matriz } D_{N,N} \text{ composta por } d(x_i, x_j)
$$

## Funções de distância

Propriedades de métricas de distância (nem toda função de distância é uma métrica):

$$
    d(a,b) \geq 0 \forall a, b \\
    d(a,b) = 0 \implies a = b \\
    d(a,b) = d(b,a) \\
    d(a,c) \leq d(a,b) + d(b,c)
$$

### Distância Euclidiana

É a distância mais frequentemente usada para vetores. Se é necessária apenas a relação de ordem entre elas é possível usar a distância euclidiana ao quadrado.

Em casos como similaridade do cosseno e escalonamento multidimensional pode ser interessante descrever a distância de forma vetorial:

$$
    d^2_{EUC}(a,b) = (a-b)^T(a-b) \\
    d^2_{EUC}(a,b) = a^Ta + b^Tb - 2a^Tb
$$

### Distância de Mannhattan

$$
    d_{MNH}(a, b) = \sum^M_{m=1} |a_m - b_m|
$$

### Atributos ordinais

É possível assumir que as classes representam intervalos para aplicar Euclidiana / Manhattan.

Exemplo: [F = 0, D = 1, C = 2, B = 3, A = 4]

### Atributos binários

$$
    d_{SMC} = 1 - s_{SMC} \\
    s_{SMC} = \frac{f_{00} + f_{11}}{f_{00} + f_{01} + f_{10} + f_{11}}
$$

|          |                                                 |
| -------- | ----------------------------------------------- |
| $f_{00}$ | Número de atributos em que x e y são iguais a 0 |
| $f_{11}$ | Número de atributos em que x e y são iguais a 1 |
| $f_{01}$ | Número de atributos em que x = 0, y = 1         |
| $f_{10}$ | Número de atributos em que x = 1, y = 0         |

Quando o 0 não é informativo é possível remover esse valor (Coeficiente de Jaccard):

$$
    d_{J} = 1 - s_{J} \\
    s_{J} = \frac {f_{11}} {f_{01} + f_{10} + f_{11}}
$$

### Atributos nominais

#### caso geral

A métrica mais comum é o Casamento Simples

$$
    s_{CS} = \sum^M_{m=1} (x_m = y_m ? ~ 1 ~ : ~ 0) \\

$$

#### Caso específico

- Edit Distance
- Qwerty Distance

### Outros

- Diferença entre distribuições (KL-divergence)
- Medida do cosseno (comum em mineração de textos)
- Diferença entre imagens (Similaridade Estrutural)

## Pré-processamento de atributos

Valores com escalas muito diferentes (como idade e salário por exemplo) precisam ser normalizados para que os pesos não enviesem a medida. É possível fazer isso de duas formas, e a escolha é situacional:

1. Normalizar entre [0,1]. Se o algoritmo requer que os dados estejam dentro desse intervalo esse método é ideal:
$$
    z' = \frac{z - \min(z)}{\max(z) - \min(z)}
$$
2. Transformar a média para 0 e o desvio padrão para 1. Se o algoritmo assume que os dados precisam estar normalizados esse método é ideal:
$$
    z' = \frac{z-\mu_z}{\sigma_z}
$$

Muitos algoritmos baseados em distância não aceitam atributos nominais, sendo necessárias abordagens como convertê-los para um conjunto de atributos binários (representação *one-of-K*):

Exemplo: `{'Aluno', 'Técnico', 'Docente'} -> {001, 010, 100}`

O inverso pode ser necessário, precisando converter valores numéricos para categóricos (discretização). Existem 2 formas:

1. Largura Fixa: Separar o intervalo dos dados ([min(z), max(z)]) em intervalos igualmente espaçados (*buckets*) especificados pelo usuário.
2. Frequência Fixa: Separar o intervalo dos dados ([min(z), max(z)]) em intervalos com aproximadamente o mesmo número de objetos, com o número de intervalos especificados pelo usuário.

## Escalonamento Multidimensional

É possível obter uma matriz de distância a partir do conjunto de dados. Mas dados podem ser ausentes por questões como confidencialidade ou distâncias obtidas subjetivamente (estimativa). É possível gerar uma aproximação dos dados com base na matriz?

Essa estimativa é possível ao minimizar o quadrado da diferença entre as distâncias par a par e a projeção (geralmente em um espaço de menor dimensão):
$$
    \text{Stress}(X_1, \cdots , X_n) = \sqrt{\left(\sum^n_{i=1}\sum^n_{j=1, ~j\neq i}(||x_i, x_j||-d_{i,j})^2\right)}
$$
Nesse contexto d é a métrica de dissimilaridade entre dois pontos no espaço original e ||a,b|| é uma métrica de dissimilaridade no espaço projetado.

Existem diversas formas de otimização iterativa para calcular a projeção. O método clássico funciona da seguinte forma:

1. Calcular $D^2_{N,N}$
2. Calcular $B = (-1 / 2)CD^2_{N,N}C$ onde C é uma matriz central (equivalente a subtrair a média de todos os elementos de $D^2_{N,N}$)
3. Calcular os auto-valores e auto-vetores de B
4. Calcular $\tilde{X} = E_p\Lambda_p^{1/2}$ (Ep é a matriz com auto-vetores e $\Lambda$ é a matriz diagonal de auto-valores)
