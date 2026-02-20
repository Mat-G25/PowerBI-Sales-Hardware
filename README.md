1. O Problema de Negócio
A empresa de hardware tinha um dump de vendas sujo, com erros de input manual, moedas não padronizadas e vendas canceladas que inflavam o faturamento real. O objetivo foi limpar esses dados e criar um dashboard que mostrasse o lucro líquido real por período.

2. O que foi feito tecnicamente?
ETL (Power Query):

Tratamento de Data Types (conversão de texto para data e moeda).

Uso de Locale (pt-BR vs en-US) para resolver conflitos de separadores de milhar e decimal (o erro da memória RAM de 25k).

Criação de Conditional Columns para filtrar o faturamento real (eliminando vendas canceladas).

Tratamento de erros (Replace Errors) na coluna de quantidade para garantir a integridade dos cálculos.

Data Modeling (Star Schema):

Criação de uma dCalendario usando DAX (CALENDARAUTO).

Relacionamento 1:N entre a Dimensão Tempo e a Fato Vendas.

DAX:

Criação da medida Total Revenue = SUM(Total_Venda) para cálculo dinâmico via CPU, otimizando o uso de memória RAM.

3. Qual insight (valor) foi gerado?
Identificação imediata de que vendas canceladas representavam um falso positivo no faturamento bruto.

Visualização clara da tendência de vendas (Trends) permitindo ver picos de demanda por categoria (ex: Ryzen vs GTX).
