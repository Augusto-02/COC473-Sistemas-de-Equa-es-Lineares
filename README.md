\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{amsmath}
\usepackage{hyperref}
\usepackage{graphicx}
\usepackage{geometry}
\geometry{a4paper, margin=1in}
\title{Análise Comparativa de Métodos para Resolução de Sistemas Lineares}
\author{Seu Nome}
\date{\today}

\begin{document}

\maketitle

\section{Introdução}
Este documento descreve os códigos implementados para resolver sistemas lineares com matrizes diagonalmente dominantes utilizando diferentes abordagens:
\begin{itemize}
\item Solução direta por Eliminação Gaussiana implementada em Python puro (utilizando listas).
\item Resolução iterativa pelo método de \textbf{Jacobi} implementado em Python puro (listas).
\item Solução direta utilizando a função otimizada \texttt{np.linalg.solve} do \texttt{NumPy}.
\item Resolução iterativa pelo método de Jacobi utilizando operações vetorizadas do \texttt{NumPy}.
\end{itemize}
Além disso, foram desenvolvidos testes para comparar o desempenho (tempo de execução e número de iterações nos métodos iterativos) para diferentes dimensões das matrizes geradas.

\section{Descrição dos Códigos}

\subsection{Geração de Matrizes Diagonalmente Dominantes}
O código utiliza a função \texttt{generate_diagonally_dominant_matrix} para criar matrizes de dimensão $n\times n$ onde cada elemento fora da diagonal é sorteado aleatoriamente no intervalo $[-10,10]$, e o elemento diagonal é definido como:
\[
A*{ii} = \sum*{j=1}^{n} \left|A\_{ij}\right| + \delta,\quad \delta \in (1,10)
\]
Isso garante que a matriz seja diagonalmente dominante e, portanto, o sistema linear possua solução única.

\subsection{Soluções Diretas}
Duas abordagens diretas foram implementadas:
\begin{enumerate}
\item \textbf{Pure Gaussian:} Utiliza eliminação gaussiana com pivoteamento, operando com listas Python. As funções \texttt{gaussian_factorize} e \texttt{gaussian_solve} implementam a fatoração e a solução do sistema, respectivamente.
\item \textbf{NumPy linalg.solve:} Utiliza a função nativa \texttt{np.linalg.solve} para resolver o sistema linear de forma rápida e eficiente.
\end{enumerate}

\subsection{Métodos Iterativos (Jacobi)}
Também foram implementadas duas versões do método iterativo de Jacobi:
\begin{enumerate}
\item \textbf{Pure Jacobi:} Implementado com listas Python. A função \texttt{jacobi_method} itera a atualização do vetor solução até que a norma do resíduo relativo (definida como
\[
\text{erro} = \frac{\| b - A x \|}{\|b\|}
\]
) seja inferior a uma tolerância dada ou até atingir o número máximo de iterações.
\item \textbf{NumPy Jacobi:} Versão vetorizada que utiliza operações matriciais do NumPy para maior desempenho.
\end{enumerate}

\subsection{Medição de Tempo e Comparação}
A função \texttt{run_comparisons} executa todos os métodos para uma lista de dimensões especificadas e coleta:
\begin{itemize}
\item O tempo de execução para cada método.
\item O número de iterações realizadas pelos métodos iterativos (Jacobi puro e NumPy Jacobi).
\end{itemize}
Posteriormente, as funções \texttt{plot_comparisons} e \texttt{plot_iterations} geram gráficos:
\begin{enumerate}
\item \textbf{Gráfico 1:} Tempo de execução versus dimensão da matriz (eixo $y$ em escala logarítmica) para todos os métodos.
\item \textbf{Gráfico 2:} Número de iterações necessárias para os métodos iterativos, comparados em função da dimensão.
\end{enumerate}

\section{Comentários sobre os Gráficos e Comparações}
\subsection{Gráfico de Tempo de Execução vs. Dimensão}
No primeiro gráfico, são comparados os tempos de execução dos quatro métodos:
\begin{itemize}
\item \textbf{Pure Gaussian:} Em geral, apresenta desempenho decrescente conforme a dimensão cresce, devido à implementação em listas, que não é tão otimizada para operações matriciais.
\item \textbf{NumPy linalg.solve:} Mostra os melhores tempos de execução graças às otimizações internas do NumPy.
\item \textbf{Pure Jacobi:} Embora seja iterativo, sua implementação em Python puro tende a ter tempos maiores, especialmente para dimensões elevadas.
\item \textbf{NumPy Jacobi:} A versão vetorizada melhora significativamente o desempenho em relação à implementação pura, mas ainda depende do número de iterações necessárias para convergência.
\end{itemize}
A escala logarítmica permite visualizar melhor as diferenças de desempenho entre os métodos conforme a dimensão da matriz aumenta.

\subsection{Gráfico de Iterações (Métodos Iterativos)}
No segundo gráfico, são mostrados os números de iterações necessárias para que os métodos iterativos (Jacobi puro e NumPy Jacobi) atinjam a tolerância definida:
\begin{itemize}
\item É possível observar que, conforme a dimensão da matriz aumenta, em geral, o número de iterações necessárias pode se estabilizar ou crescer ligeiramente, dependendo da estrutura da matriz.
\item A similaridade entre as contagens de iterações para ambas as versões indica que a convergência do método de Jacobi é mais influenciada pelas propriedades da matriz do que pela implementação (puro ou vetorizada).
\end{itemize}

\subsection{Comparações Gerais}
De modo geral, a comparação mostra que:
\begin{itemize}
\item As implementações utilizando \texttt{NumPy} (direto e iterativo) oferecem desempenho superior em termos de tempo de execução, especialmente para matrizes de alta dimensão.
\item Métodos iterativos, apesar de possuírem a vantagem de não exigir a fatoração completa, dependem fortemente da estrutura da matriz (diagonalmente dominante garante convergência, mas o número de iterações pode variar).
\item A implementação direta com \texttt{np.linalg.solve} é a mais eficiente para problemas que cabem na memória e quando a matriz é bem condicionada.
\end{itemize}

\section{Conclusão}
Os códigos apresentados demonstram a diversidade de abordagens para resolver sistemas lineares. Enquanto os métodos diretos (especialmente via \texttt{NumPy}) são rápidos e eficientes, os métodos iterativos podem ser vantajosos em situações onde a matriz é esparsa ou quando se deseja uma solução aproximada com controle sobre a tolerância de erro. A comparação gráfica dos tempos de execução e das iterações fornece insights valiosos sobre a escalabilidade e a eficiência das técnicas utilizadas.

\section{Como Executar}
Para reproduzir os resultados:
\begin{enumerate}
\item Certifique-se de ter o \texttt{Python} e as bibliotecas \texttt{NumPy} e \texttt{Matplotlib} instalados.
\item Execute o código integrado (por exemplo, via \texttt{python main.py}) para que os testes sejam realizados e os gráficos sejam exibidos.
\item Consulte os gráficos gerados para analisar os desempenhos comparativos.
\end{enumerate}

\end{document}
