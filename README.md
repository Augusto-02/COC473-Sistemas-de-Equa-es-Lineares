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

![Tempo de Execução](images/comparisons_plot.png)

- **`np.linalg.solve`** tem o menor tempo de execução, graças a otimizações de baixo nível.
- **Métodos manuais (Pure Gaussian/Pure Jacobi)** são significativamente mais lentos, especialmente para matrizes grandes.
- **Jacobi Vetorizado (NumPy)** é mais rápido que a versão pura, mas ainda depende do número de iterações.

### Gráfico de Iterações para Convergência

![Iterações](images/iterations_plot.png)

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
