# Resolução de Sistemas Lineares com Eliminação de Gauss e Fatoração LU

Este documento fornece uma visão geral dos métodos de **Eliminação de Gauss com pivotamento parcial** e **Fatoração LU**, além de uma explicação detalhada do código Python que implementa esses métodos para resolver sistemas de equações lineares.

---

## Introdução aos Métodos Numéricos para Sistemas Lineares

Sistemas de equações lineares são fundamentais em diversas áreas da ciência e engenharia. Métodos numéricos, como a **Eliminação de Gauss** e a **Fatoração LU**, são amplamente utilizados para encontrar soluções eficientes para esses sistemas.

---

## Eliminação de Gauss com Pivotamento Parcial

A **Eliminação de Gauss** transforma uma matriz de coeficientes em uma forma triangular superior, facilitando a resolução do sistema por **substituição regressiva**. O **pivotamento parcial** melhora a estabilidade numérica ao posicionar o maior elemento absoluto da coluna como pivô, reduzindo erros numéricos.

### Passos da Eliminação de Gauss com Pivotamento Parcial

1. **Identificação do Pivô**: Para cada coluna, encontra-se o elemento de maior valor absoluto abaixo do pivô atual.
2. **Troca de Linhas**: Troca-se a linha atual com a linha do pivô identificado (se necessário).
3. **Eliminação**: Zera-se os elementos abaixo do pivô usando operações de linha.
4. **Substituição Regressiva**: Resolve-se o sistema triangular superior resultante.

---

## Fatoração LU com Pivotamento Parcial

A **Fatoração LU** decompõe uma matriz `A` em duas matrizes triangulares:

- `L` (triangular inferior com 1's na diagonal).
- `U` (triangular superior).

A decomposição obedece à relação `PA = LU`, onde `P` é uma matriz de permutação que registra as trocas de linhas.

### Passos da Fatoração LU com Pivotamento Parcial

1. **Inicialização**: Configura `L` como matriz identidade e `U` como cópia de `A`.
2. **Pivotamento Parcial**: Identifica e troca linhas para maximizar o pivô.
3. **Atualização de L e U**: Calcula multiplicadores e atualiza as matrizes.
4. **Resultado**: `L` armazena os multiplicadores, e `U` é a matriz triangular superior.

---

# Método de Jacobi para Resolução de Sistemas Lineares

Este projeto implementa o **método de Jacobi**, um algoritmo iterativo para resolver sistemas de equações lineares. O código inclui um exemplo de uso e uma visualização da convergência do método através de um gráfico de resíduos.

---

onde:

- `Σ_{j ≠ i}` representa a soma de todos os termos da linha `i`, exceto o elemento diagonal.
- A iteração continua até que o resíduo relativo seja menor que uma tolerância especificada.

### Critério de Convergência

- **Matriz Diagonalmente Dominante**:
  `|A_{i,i}| ≥ Σ_{j ≠ i} |A_{i,j}|` para todas as linhas `i`.
- O método converge para qualquer aproximação inicial se a matriz for diagonalmente dominante.

### Resíduo Relativo

O resíduo relativo é calculado como:

||b - A\*\*x^{(k)}|| / ||b||

onde `||·||` denota a norma Euclidiana.

---

## Implementação do Código

### Função Principal: `metodo_jacobi`

```python
def metodo_jacobi(matriz_coeficientes, vetor_constantes, tolerancia, max_iteracoes):
    # Implementação detalhada no código

## Teoria do Método de Jacobi

O método de Jacobi é um algoritmo iterativo clássico para resolver sistemas lineares da forma `A**x** = **b**`, onde:
- `A` é a matriz de coeficientes (quadrada e diagonalmente dominante para garantir convergência).
- `**b**` é o vetor de constantes.
- `**x**` é o vetor solução desconhecido.

### Fórmula Iterativa
Para cada variável `x_i` na iteração `k+1`, o método calcula:

# Comparação de Métodos para Resolução de Sistemas Lineares

Este projeto compara métodos diretos e iterativos para resolver sistemas lineares, destacando diferenças de desempenho e eficiência. As implementações incluem desde algoritmos manuais em Python puro até versões otimizadas com NumPy, com análises gráficas dos resultados.

## Funcionalidades Principais

- **Geração de Matrizes Diagonalmente Dominantes**
  Gera matrizes aleatórias onde a diagonal é ajustada para garantir convergência em métodos iterativos.
- **Métodos Diretos**
  - `Pure Gaussian`: Eliminação gaussiana com pivoteamento (implementação manual).
  - `np.linalg.solve`: Resolução otimizada via bibliotecas BLAS/LAPACK.
- **Métodos Iterativos (Jacobi)**
  - `Pure Jacobi`: Implementação iterativa com loops em Python.
  - `NumPy Jacobi`: Versão vetorizada com operações matriciais do NumPy.
- **Análise Comparativa**
  - Medição de tempo de execução e número de iterações.
  - Visualização gráfica dos resultados para diferentes dimensões de matrizes.

## Resultados Obtidos

### Gráfico de Tempo de Execução vs. Dimensão

![Tempo de Execução](/src/images/comparisons_plot.png)

- **`np.linalg.solve`** tem o menor tempo de execução, graças a otimizações de baixo nível.
- **Métodos manuais (Pure Gaussian/Pure Jacobi)** são significativamente mais lentos, especialmente para matrizes grandes.
- **Jacobi Vetorizado (NumPy)** é mais rápido que a versão pura, mas ainda depende do número de iterações.

### Gráfico de Iterações para Convergência

![Iterações](/src/images/iterations_plot.png)

- Ambos os métodos de Jacobi exigem um número similar de iterações, indicando que a vetorização acelera cada iteração, mas não reduz a quantidade necessária.

## Comparação Detalhada

| Método            | Vantagens                           | Desvantagens                             |
| ----------------- | ----------------------------------- | ---------------------------------------- |
| `np.linalg.solve` | Rápido, preciso, otimizado          | Requer matriz densa e bem condicionada   |
| `Pure Gaussian`   | Didático, sem dependências externas | Extremamente lento para grandes matrizes |
| `Pure Jacobi`     | Simples, adequado para aproximações | Lentidão devido a loops em Python        |
| `NumPy Jacobi`    | Iterações rápidas, vetorizado       | Depende da convergência iterativa        |

## Conclusões

- **Para soluções exatas:** Use `np.linalg.solve` para matrizes de qualquer tamanho.
- **Para problemas iterativos:** Prefira a versão vetorizada do Jacobi com NumPy.
- **Implementações manuais:** São viáveis apenas para estudos didáticos ou matrizes muito pequenas.

## Requisitos

- Python 3.8+
- Bibliotecas: `numpy`, `matplotlib`, `time`
```
