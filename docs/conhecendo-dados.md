# Conhecendo os dados

O **dataset Digital Payment Fraud Detection** contém informações sobre **7.500 transações digitais sintéticas**, incluindo valores, tipos de pagamento e indicadores de fraude (`fraud_label`). Ele reúne **variáveis numéricas e categóricas**, relacionadas a **comportamento, finanças, dispositivos e risco**, e é ideal para **análise exploratória**, **identificação de outliers** e **estudo de padrões de fraude** antes da aplicação de modelos preditivos. As análises foram realizadas com base no arquivo **Digital_Payment_Fraud_Detection_Dataset.csv**.

#### 🗃️ Descrição Geral do Dataset

O dataset possui **7.500 linhas** e **15 colunas**, contendo dados detalhados de cada transação, sem valores nulos ou registros duplicados de `transaction_id`.O campo `user_id` pode se repetir, já que cada usuário pode realizar múltiplas transações.  

**Colunas do dataset:**

| Coluna                    | Tipo       | Descrição                                     |
|----------------------------|------------|-----------------------------------------------|
| `transaction_id`           | numérica   | ID único da transação                          |
| `user_id`                  | numérica   | ID do usuário                                  |
| `transaction_amount`       | numérica   | Valor da transação                             |
| `transaction_type`         | categórica | Tipo de transação                              |
| `payment_mode`             | categórica | Método de pagamento                            |
| `device_type`              | categórica | Tipo de dispositivo utilizado                  |
| `device_location`          | categórica | Localização do dispositivo                     |
| `account_age_days`         | numérica   | Idade da conta em dias                          |
| `transaction_hour`         | numérica   | Hora da transação                               |
| `previous_failed_attempts` | numérica   | Número de tentativas falhas anteriores         |
| `avg_transaction_amount`   | numérica   | Valor médio das transações anteriores          |
| `is_international`         | categórica | Indica se a transação é internacional         |
| `ip_risk_score`            | numérica   | Score de risco associado ao IP                 |
| `login_attempts_last_24h`  | numérica   | Tentativas de login nas últimas 24 horas      |
| `fraud_label`              | categórica | Indicador de fraude (0 = não, 1 = fraudulenta)|

#### 📊 Estatísticas Descritivas do Dataset

**Colunas numéricas principais:**

| Coluna                   | Min      | 25%       | 50%       | 75%       | Max       | Média     | Std       | Moda       | Valores ausentes |
|---------------------------|----------|-----------|-----------|-----------|-----------|-----------|-----------|------------|----------------|
| transaction_amount        | 50.58    | 12272.79  | 24715.55  | 37288.38  | 49985.90  | 24813.53  | 14434.74  | 36588.25   | 0              |
| account_age_days          | 10       | 502.75    | 1018      | 1505      | 1999      | 1006.90   | 575.63    | 1018       | 0              |
| transaction_hour          | 0        | 5         | 11        | 18        | 23        | 11.44     | 6.95      | 3          | 0              |
| previous_failed_attempts  | 0        | 1         | 2         | 3         | 4         | 2.01      | 1.42      | 4          | 0              |
| avg_transaction_amount    | 102.79   | 7725.84   | 15074.81  | 22573.06  | 29994.29  | 15129.06  | 8597.76   | 2121.88    | 0              |
| is_international          | 0        | 0         | 0         | 0         | 1         | 0.10      | 0.30      | 0          | 0              |
| ip_risk_score             | 0        | 0.257     | 0.502     | 0.759     | 1         | 0.505     | 0.29      | 0.171      | 0              |
| login_attempts_last_24h   | 1        | 3         | 5         | 7         | 9         | 4.99      | 2.59      | 1          | 0              |
| fraud_label               | 0        | 0         | 0         | 0         | 1         | 0.065     | 0.25      | 0          | 0              |

**Colunas categóricas / IDs principais:**

| Coluna             | Tipo   | Moda         | Frequência | % Frequência | Valores únicos |
|-------------------|--------|-------------|------------|--------------|----------------|
| transaction_id     | object | T1          | 1          | 0.01%        | 7500           |
| user_id            | object | U1247       | 6          | 0.08%        | 5106           |
| transaction_type   | object | Payment     | 2511       | 33.48%       | 3              |
| payment_mode       | object | Card        | 1912       | 25.49%       | 4              |
| device_type        | object | Web         | 2537       | 33.83%       | 3              |
| device_location    | object | Hyderabad   | 1614       | 21.52%       | 5              |

#### 🔍📈 Analisando Outliers com IQR

Para identificar valores extremos no dataset, utilizamos o **método do Intervalo Interquartil (IQR)**, que define outliers como pontos abaixo de Q1 - 1.5*IQR ou acima de Q3 + 1.5*IQR.  

A tabela abaixo resume a **quantidade e percentual de outliers** detectados para cada variável numérica:

| Coluna                     | Count | Percentagem (%) | Min Outlier | Max Outlier |
|-----------------------------|-------|----------------|------------|------------|
| is_international            | 755   | 10.07          | 1          | 1          |
| fraud_label                 | 489   | 6.52           | 1          | 1          |
| transaction_amount          | 0     | 0.00           | -          | -          |
| account_age_days            | 0     | 0.00           | -          | -          |
| transaction_hour            | 0     | 0.00           | -          | -          |
| avg_transaction_amount      | 0     | 0.00           | -          | -          |
| previous_failed_attempts    | 0     | 0.00           | -          | -          |
| ip_risk_score               | 0     | 0.00           | -          | -          |
| login_attempts_last_24h     | 0     | 0.00           | -          | -          |

---

### 🔹 Observações

- As variáveis **`is_international`** e **`fraud_label`** apresentam outliers, mas isso é esperado, pois são **variáveis binárias** (`0` ou `1`).  
- Nenhuma outra variável numérica apresentou outliers pelo critério IQR, indicando que os valores extremos em **`transaction_amount`, `account_age_days`**, entre outras, estão dentro de um intervalo esperado.  
- O método IQR provê uma **detecção rápida e padronizada** de valores extremos, permitindo identificar casos atípicos sem distorcer as análises de tendências centrais ou dispersão.  

#### 📊 Análise Visual das Variáveis Numéricas

A seguir, são apresentados os histogramas e boxplots das variáveis numéricas do dataset. Cada gráfico permite observar a distribuição, detectar outliers e identificar padrões importantes para análise de fraude.

---

**1. `transaction_amount`** 
 ![transaction_amount](../docs/plots/distribuicao_boxplot_transaction_amount.png)
- **Histograma**: Mostra que a maioria das transações se concentra em valores médios, com alguns valores muito altos que representam outliers potenciais.  
- **Boxplot**: Destaca a presença de transações extremas, que podem indicar comportamento atípico ou possível fraude.

**2. `account_age_days`**  
 ![account_age_days](../docs/plots/distribuicao_boxplot_account_age_days.png)
- **Histograma**: A distribuição apresenta grande concentração em contas de idade média, com poucas contas muito novas ou muito antigas.  
- **Boxplot**: Visualiza esses extremos, que podem ser relevantes para padrões de risco.

**3. `transaction_hour`**  
 ![transaction_hour](../docs/plots/distribuicao_boxplot_transaction_hour.png)
- **Histograma**: Indica que a maior parte das transações ocorre em determinados horários do dia, mostrando padrões de uso.  
- **Boxplot**: Permite identificar se existem transações fora do horário comum.

**4. `previous_failed_attempts`**  
 ![previous_failed_attempts](../docs/plots/distribuicao_boxplot_failed_attempts.png)
- **Histograma**: Mostra que a maioria das transações ocorre com poucos ou nenhum histórico de tentativas falhas.  
- **Boxplot**: Destaca usuários com muitas tentativas falhas, possíveis indicadores de risco.

**5. `avg_transaction_amount`**  
 ![avg_transaction_amount](../docs/plots/distribuicao_boxplot_avg_transaction_amount.png)
- **Histograma**: Apresenta a média das transações por usuário, concentrada em valores médios com algumas altas variações.  
- **Boxplot**: Evidencia outliers, indicando usuários com comportamento de transação atípico.

**6. `is_international`**  
 ![is_international](../docs/plots/distribuicao_boxplot_is_international.png)
- **Histograma**: A grande maioria das transações é nacional (`0`), com poucas internacionais (`1`).  
- **Boxplot**: Mostra a diferença de escala entre transações nacionais e internacionais, reforçando o desbalanceamento.

**7. `ip_risk_score`**  
 ![ip_risk_score](../docs/plots/distribuicao_boxplot_ip_risk_score.png)
- **Histograma**: Indica que a maioria das transações possui score de risco moderado, com alguns valores extremos próximos de 1.  
- **Boxplot**: Permite visualizar os casos de risco alto, que podem estar associados a fraudes.

**8. `login_attempts_last_24h`**  
 ![login_attempts_last_24h](../docs/plots/distribuicao_boxplot_login_attempts_last_24.png)
- **Histograma**: Mostra que a maioria dos usuários realiza poucas tentativas de login nas últimas 24h, com alguns casos extremos.  
- **Boxplot**: Evidencia usuários com muitas tentativas, que podem representar comportamento suspeito.

**9. `fraud_label`**  
 ![fraud_label](../docs/plots/distribuicao_boxplot_fraud_label.png)
- **Histograma**: Demonstra que o dataset é desbalanceado, com poucas transações fraudulentas (`1`) em relação às não fraudulentas (`0`).  
- **Boxplot**: Mostra claramente a desigualdade de distribuição entre transações não fraudulentas e fraudulentas.

#### 🔗 Análise de Correlação entre Variáveis Numéricas

Para compreender melhor as relações entre as variáveis numéricas do dataset, construímos uma **matriz de correlação**, que mostra a intensidade e direção das associações entre as variáveis.

- Valores próximos de **1** indicam forte correlação positiva, ou seja, quando uma variável aumenta, a outra tende a aumentar.  
- Valores próximos de **-1** indicam forte correlação negativa, ou seja, quando uma variável aumenta, a outra tende a diminuir.  
- Valores próximos de **0** indicam pouca ou nenhuma correlação entre as variáveis.

![matriz_correlacao](../docs/plots/matriz_correlacao_variaceis_numericas.png)

## 🔎 Descrição dos achados

A partir da análise exploratória realizada no dataset **Digital Payment Fraud Detection**, os seguintes achados se destacam:

1. **Centralidade dos dados**  
   - A média e a mediana de `transaction_amount` são próximas (≈ 24.813 e 24.715), indicando uma distribuição relativamente simétrica, embora a moda seja maior (36.588), sugerindo que algumas transações “padrão” se repetem com valores mais altos.
   - Para `account_age_days`, a média é 1.006 dias e a mediana 1.018, indicando que a maioria das contas tem idade próxima à média, mas com algumas contas muito novas ou muito antigas, que podem ser consideradas outliers.

2. **Dispersão e outliers**  
   - O desvio padrão de `transaction_amount` (≈ 14.434) mostra uma variação significativa entre os valores, o que é esperado em transações digitais.
   - Quartis e boxplots indicam que existem transações atípicas com valores mais altos que o normal, possíveis candidatos a fraude.

3. **Relações entre variáveis**  
   - Algumas variáveis financeiras, como `avg_transaction_amount` e `transaction_amount`, apresentam correlação moderada positiva, indicando que usuários com transações anteriores altas tendem a realizar transações atuais altas.
   - Variáveis de risco como `ip_risk_score` e `is_international` apresentam associação com `fraud_label`, sugerindo que transações internacionais ou com IPs suspeitos têm maior chance de fraude.
   - Variáveis categóricas como `device_type` e `payment_mode` têm frequência alta para determinados valores (moda), mostrando padrões predominantes de uso.

4. **Distribuição de fraude**  
   - O dataset é **desbalanceado**: apenas ~6,5% das transações são fraudulentas (`fraud_label = 1`). Isso deve ser considerado na modelagem preditiva.

---


## 🛠️Ferramentas utilizadas

As análises foram realizadas utilizando a linguagem de programação **Python**, no ambiente **Google Colab**, com as seguintes bibliotecas:

| Ferramenta / Biblioteca | Aplicação |
|-------------------------|-----------|
| **Google Colab**        | Ambiente de execução interativo baseado em nuvem, ideal para análise exploratória, visualizações e execução de notebooks Python |
| **pandas**              | Manipulação de dados, cálculo de estatísticas descritivas, tratamento de valores nulos e duplicados |
| **numpy**               | Operações matemáticas e estatísticas, tipos de dados numéricos |
| **matplotlib**          | Criação de gráficos estáticos (histogramas, boxplots, dispersão) |
| **seaborn**             | Visualizações estatísticas avançadas, como mapas de calor de correlação e boxplots por classe |
| **plotly.express**      | Criação de gráficos interativos, como histogramas, scatter plots e boxplots, permitindo exploração dinâmica dos dados |
| **Jupyter Notebook / Colab Notebooks** | Organização do código, documentação das análises e geração de visualizações interativas |

> Observação: todo o código fonte utilizado está disponível na pasta `src`, permitindo reproduzir todas as análises realizadas.
