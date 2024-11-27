# Pipeline de Dados End-to-End no Azure
Este projeto apresenta uma solução completa de pipeline de engenharia de dados, desenvolvida para resolver um problema de negócios fictício. O objetivo é aprofundar o aprendizado sobre pipelines de dados e explorar as tecnologias disponíveis na plataforma Azure, criando um fluxo integrado e eficiente de coleta, transformação e análise de dados.

## Visão geral do projeto

![modulo_43-4.png](https://github.com/jaquessonoliveira/Projeto-Ingestao-de-Dados--em-Streaming/blob/main/Arquitetura%20Engenharia%20de%20dados.png)

Este projeto aborda uma necessidade crítica de negócios ao construir um pipeline de dados integrado na plataforma Azure. O fluxo abrange a extração de dados de clientes e vendas de um banco de dados SQL Server local, a transformação desses dados na nuvem e a geração de insights acionáveis por meio de um painel interativo no Power BI. O painel exibirá os principais indicadores de desempenho (KPIs), como distribuição de gênero e vendas por categoria de produto, permitindo que as partes interessadas filtrem e analisem os dados de forma dinâmica, com base em critérios como data, categoria de produto e gênero.

## Requisitos de negócios

A empresa identificou uma lacuna na compreensão da demografia de clientes, especialmente na distribuição por gênero e seu impacto nas compras de produtos. Para atender a essa necessidade, os seguintes requisitos foram definidos:

1. **Análise de vendas por gênero e categoria de produto**: um painel que exiba o total de produtos vendidos, a receita total gerada e a segmentação de clientes por gênero.
2. **Filtragem personalizada de dados**: capacidade de aplicar filtros dinâmicos por categoria de produto, gênero e períodos específicos.
3. **Interface intuitiva**: uma plataforma de fácil utilização, que permita às partes interessadas explorar os dados e realizar consultas de forma eficiente.

## Visão geral da solução

Para atender aos requisitos identificados, a solução foi estruturada em quatro componentes principais:

1. **Ingestão de Dados**: 
    - Extração de dados de clientes e vendas de um banco de dados SQL Server local.
    - Carregamento dos dados para o Azure Data Lake Storage (ADLS) utilizando o Azure Data Factory (ADF).

2. **Transformação dos Dados**:
    - Processamento e limpeza dos dados no Azure Databricks.
    - Organização dos dados em camadas Bronze (dados brutos), Silver (dados limpos) e Gold (dados prontos para análises e agregações).

3. **Carregamento e Visualização**:
    - Armazenamento dos dados transformados no Azure Synapse Analytics para análises avançadas.
    - Desenvolvimento de um painel interativo no Power BI, permitindo a visualização de insights demográficos e de vendas.

4. **Automação**:
    - Agendamento do pipeline para execução diária, garantindo a atualização contínua dos dados e relatórios.

## Tecnologias utilizadas:

- **Azure Data Factory (ADF)**: Responsável pela orquestração do pipeline, incluindo a movimentação e integração dos dados entre serviços.
- **Azure Data Lake Storage (ADLS)**: Armazena dados em diferentes estágios (brutos, transformados e prontos para análise).
- **Azure Databricks**: Realiza a limpeza, transformação e preparação dos dados em camadas estruturadas (Bronze, Silver, Gold).
- **Azure Synapse Analytics**: Fornece um repositório central para armazenamento e consultas analíticas de alto desempenho usando SQL.
- **Power BI**: Utilizado para criar relatórios e painéis interativos com base nos dados processados.
- **Azure Key Vault**: Gerencia credenciais, chaves e segredos, garantindo a segurança do pipeline.
- **SQL Server (On-Premises)**: Atua como a fonte inicial dos dados de clientes e vendas.

### Etapa 1: Configuração do Ambiente no Azure

1. **Criação do Grupo de Recursos**: 
   - Configurar um novo grupo de recursos para organizar os serviços necessários no Azure.
2. **Provisão de Serviços**:
   - Criar uma instância do Azure Data Factory para orquestração do pipeline.
   - Configuração do Azure Data Lake Storage (ADLS ) com contêineres dedicados para as camadas `bronze`, `silver` e `gold`.
   - Provisionar um espaço de trabalho para:
        - Azure Databricks, para processamento e transformação de dados.
        - Azure Synapse Analytics, para armazenamento e análises de dados.
   - Configurar o Azure Key Vault para gerenciamento seguro de credenciais e segredos.

### Etapa 2: Ingestão de dados

1. **Configuração do SQL Server**: 
   - Instalar o SQL Server e o SQL Server Management Studio (SSMS) em um ambiente local.
   - Restaurar o banco de dados AdventureWorks como fonte de dados para o pipeline.
2. **Ingestão de Dados com Azure Data Factory (ADF)**: 
   - Configurar pipelines no ADF para extrair os dados do SQL Server.
   - Carregar os dados extraídos na camada `bronze` do Azure Data Lake Storage (ADLS), mantendo a estrutura original dos dados.

### Etapa 3: Transformação de dados

1. **Configuração do Data Lake no Databricks**: 
   - Configurar o acesso do Azure Databricks ao Azure Data Lake Storage (ADLS), utilizando credenciais seguras armazenadas no Azure Key Vault.
2. **Processamento e Transformação de Dados**: 
   - Utilizar notebooks do Databricks para realizar a limpeza e agregação dos dados, movendo-os da camada `bronze` para a `silver` e, em seguida, para a `gold`.

### Etapa 4: Carregamento e relatórios de dados

1. **Carregamento de Dados no Synapse**: 
   - Configurar um pool de SQL no Azure Synapse Analytics para armazenar os dados da camada `gold`.
   - Carregar os dados processados da camada gold no Synapse, garantindo que estejam prontos para consultas analíticas de alto desempenho.
2. **Criação do Painel no Power BI**: 
   - Estabelecer a conexão entre o Power BI e o Synapse para acessar os dados carregados.
   - Desenvolver visualizações interativas e um painel que atenda aos requisitos de negócios, destacando KPIs, distribuição por gênero e vendas por categoria de produto.

   Para visualizar o Dashboard de forma totalmente interativa é só clicar neste link ([Dashboard](https://app.powerbi.com/view?r=eyJrIjoiYmE5MTBiOTUtNzdhZS00YzNjLTlmZDQtYmVhNzVjZWM0Y2Y5IiwidCI6IjE0Y2JkNWE3LWVjOTQtNDZiYS1iMzE0LWNjMGZjOTcyYTE2MSIsImMiOjh9)): 

### Etapa 5: Automação e monitoramento

1. **Programação de Pipelines**: 
   - Configurar o Azure Data Factory (ADF) para agendar a execução diária dos pipelines, garantindo que os dados sejam atualizados regularmente.
2. **Monitoramento das Execuções**: 
   - Utilizar as ferramentas de monitoramento integradas no ADF para rastrear o status das execuções e identificar possíveis falhas.
   - Configurar alertas e notificações no Azure Monitor para reportar problemas críticos.
   - Acompanhar métricas de desempenho e logs de execução no ADF e no Synapse para assegurar a eficiência do pipeline.

### Etapa 6: Segurança e Governança

1. **Gerenciamento de Acesso**: 
   - Configurar o Controle de Acesso Baseado em Função (RBAC) no Azure para garantir que apenas usuários autorizados tenham acesso aos recursos.
   - Usar o Azure Entra ID (antigo Active Directory) para gerenciar permissões, atribuir funções e autenticar usuários com segurança.
2. **Proteção de Dados Sensíveis (sugestão adicional)**:
   - Configurar o Azure Key Vault para armazenar segredos, como strings de conexão e credenciais.

### Etapa 7: Teste de ponta a ponta

1. **Testar Pipelines e Gatilhos**: 
   - Inserir novos registros no banco de dados SQL para simular dados reais.
   - Verificar se os pipelines do Azure Data Factory são executados corretamente, transferindo e processando os dados através das camadas `bronze`, `silver` e `gold`.
   - Garantir que os dados processados sejam carregados com sucesso no Azure Synapse Analytics.
   - Confirmar que o painel do Power BI é atualizado automaticamente, refletindo as mudanças nos dados de forma precisa.

## Conclusão

Este projeto apresenta uma solução integrada de ponta a ponta, projetada para analisar a demografia dos clientes e seu impacto nas vendas. A automação do pipeline de dados assegura que as partes interessadas tenham acesso contínuo a insights atualizados, permitindo tomadas de decisão mais estratégicas e baseadas em dados confiáveis.