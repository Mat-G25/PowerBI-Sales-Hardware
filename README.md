Business Problem
Uma varejista de hardware enfrentava dificuldades para consolidar seu faturamento real devido à baixa qualidade dos dados provenientes de um sistema legado. O dump de dados apresentava inconsistências de formatação (padrões regionais mistos), entradas de texto em colunas numéricas e inclusão de pedidos cancelados no montante bruto, gerando uma visão inflada e imprecisa da saúde financeira da empresa.

Tech Stack
Power BI (Visualização e Engine)

Power Query (M/ETL)

DAX (Cálculos de Medida)

Etapas do Projeto
1. ETL & Data Cleaning (Power Query)

Padronização de Moeda: Utilização de Change Type with Locale para tratar divergências entre pontos e vírgulas, evitando distorções de escala (ex: correção de itens que saltavam de 250 para 25.000).

Tratamento de Erros: Aplicação de Replace Errors em colunas de quantidade para tratar inputs manuais inválidos (strings) sem interromper o fluxo de cálculo.

Lógica de Negócio Injetada: Criação de coluna condicional para zerar o Preço_Efetivo de transações com status "Cancelado", garantindo que a métrica de faturamento reflita apenas o capital efetivamente entrado.

2. Modelagem de Dados (Star Schema)

Arquitetura: Implementação de modelo Estrela para otimização de performance.

Dimensão Tempo: Desenvolvimento de uma dCalendario via DAX (CALENDARAUTO) para habilitar análises de série temporal contínua e garantir a integridade dos filtros de data.

Relacionamentos: Estabelecimento de relação 1:N entre dCalendario[Date] e vendas_hardware[Data_Venda].

3. Medidas DAX

Total Revenue: Total Revenue = SUM(vendas_hardware[Total_Venda])

Nota: Opção por Medida em vez de Coluna Calculada para otimizar o uso de memória RAM e garantir cálculos dinâmicos baseados no contexto de filtro do usuário.

Insights Gerados
Faturamento Real: Identificação de que o faturamento bruto estava 15% acima do real devido aos pedidos cancelados não tratados anteriormente.

Sazonalidade: Visualização de picos de venda correlacionados a categorias específicas de hardware (CPUs vs GPUs).

Como Visualizar
O arquivo .pbix está disponível na pasta /reports deste repositório.
