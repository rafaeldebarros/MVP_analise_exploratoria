# MVP - Análise de Dados e Boas Práticas: Desempenho Estudantil

Este projeto consiste em uma Análise Exploratória de Dados (EDA) e preparação de base para modelagem de Machine Learning, com o objetivo de identificar variáveis correlacionadas ao desempenho de estudantes do ensino secundário em Portugal.

## 1. Descrição do Problema e Hipóteses Iniciais

O objetivo principal é analisar os resultados de estudantes em avaliações escolares (matemática e português) para identificar fatores demográficos, sociais e escolares que influenciam suas notas. O problema foi abordado como uma tarefa de regressão (para prever a nota final) e, posteriormente, de classificação (para categorizar o desempenho).

Hipóteses iniciais sugeriam que o tempo de estudo, o suporte familiar e a frequência às aulas teriam maior influência nos resultados. No decorrer da análise, observou-se que essas variáveis não apresentaram correlações lineares tão fortes quanto esperado, e outros fatores se mostraram mais relevantes.

## 2. Fonte de Dados

O dataset utilizado é o **Student Performance**, disponível publicamente no [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/320/student+performance). Ele contém 30 variáveis explicativas e 3 variáveis alvo (`G1`, `G2`, `G3` - notas do 1º, 2º e 3º períodos) para as disciplinas de matemática e português.

Os dados foram carregados diretamente do GitHub a partir dos arquivos `student-mat.csv` e `student-por.csv`.

## 3. Metodologia e Análise

### 3.1. Carregamento e Combinação de Dados

*   Os datasets de matemática e português foram carregados e combinados em um único DataFrame (`df_combinado`).
*   Uma coluna `subject` foi adicionada para identificar a disciplina de origem ('mat' ou 'por').

### 3.2. Análise Exploratória de Dados (EDA)

*   **Tipos de Variáveis e Valores Ausentes:** Verificado o tipo de cada variável e a ausência de valores nulos.
*   **Estatísticas Descritivas:** Análise das estatísticas para o DataFrame combinado e separadamente por matéria.
*   **Distribuição das Variáveis:** Visualizações (gráficos de pizza, barras e histogramas) para entender a distribuição de variáveis como sexo, idade, matéria e outras características dos alunos.

### 3.3. Engenharia de Features

*   **Variável Alvo `media final`:** Criada a média das notas `G1`, `G2`, `G3` para simplificar a variável alvo de regressão, arredondada para o inteiro mais próximo.
*   **Variável Alvo `classificacao_media_final`:** Criada uma versão categórica da `media final` (reprovado, suficiente, satisfatório, bom, excelente) para problemas de classificação.
*   **One-Hot Encoding:** Variáveis categóricas foram convertidas em formato numérico (binário) para uso em modelos de Machine Learning.
*   **Novas Features:** Algumas features foram combinadas para tentar capturar novas relações:
    *   `Alc_total`: Soma do consumo de álcool diário e de fim de semana (`Dalc` + `Walc`).
    *   `Parentedu_sum`, `Parentedu_avg`, `Parentedu_max`: Diferentes agregações da escolaridade dos pais (`Medu`, `Fedu`).
    *   `school_history`, `failures_with_schoolsup`: Combinações relacionadas a reprovações e suporte escolar.

### 3.4. Análise de Correlação

*   **Heatmaps:** Gerados mapas de calor para visualizar a correlação das features com a `media final`. `failures` (número de reprovações) mostrou-se a variável mais fortemente correlacionada (negativamente).
*   **Gráficos de Dispersão:** Analisadas as 9 variáveis mais correlacionadas com a `media final` em gráficos de dispersão, revelando insights como um ponto ótimo para o `studytime`.
*   **Multicolinearidade:** Verificada a correlação entre as features independentes para identificar possíveis problemas de multicolinearidade em modelos de regressão linear. Identificou-se alta correlação entre as variáveis derivadas da educação parental (`Parentedu_sum`, `Parentedu_avg`).


## 4. Conclusão

Este projeto demonstrou um processo completo de preparação e análise de dados para um problema de desempenho estudantil. A base de dados está agora pronta para a aplicação de diversos algoritmos de Machine Learning, tanto para regressão (usando `media final` e features escalonadas) quanto para classificação (usando `classificacao_media_final` e o dataset de treino balanceado). A análise inicial de correlações forneceu insights valiosos, e a engenharia de features e o balanceamento do dataset são passos cruciais para a construção de modelos robustos e precisos.
