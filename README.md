# Processo de Importação e Análise de Dados Contábeis
Este repositório contém scripts SQL para importar dados de operadoras de planos de saúde e realizar análises financeiras a partir desses dados. O processo envolve a criação de tabelas, importação de arquivos CSV, transformação de dados e execução de consultas SQL para análises específicas.
## Estrutura do Banco de Dados
O script cria três tabelas no banco de dados:

1. OPERADORAS_ATIVAS: Armazena informações sobre operadoras de planos de saúde ativas.

2. TEMP_DADOS: Tabela temporária para armazenar dados importados temporariamente.

3. DEMONSTRACOES_CONTABEIS: Tabela permanente para armazenar dados transformados e prontos para análises.

### Tabela OPERADORAS_ATIVAS
| Coluna                  | Tipo    | Descrição                                      |
|-------------------------|---------|------------------------------------------------|
| REGISTRO_ANS             | INT     | Chave primária                                 |
| CNPJ                    | VARCHAR | Número de registro CNPJ da operadora           |
| RAZAO_SOCIAL            | VARCHAR | Razão social da operadora                      |
| NOME_FANTASIA           | VARCHAR | Nome fantasia da operadora                     |
| MODALIDADE              | VARCHAR | Modalidade do plano de saúde                   |
| LOGRADOURO              | VARCHAR | Endereço da operadora (logradouro)             |
| NUMERO                  | VARCHAR | Número do endereço da operadora                |
| COMPLEMENTO             | VARCHAR | Complemento do endereço da operadora           |
| BAIRRO                  | VARCHAR | Bairro do endereço da operadora                |
| CIDADE                  | VARCHAR | Cidade do endereço da operadora                |
| UF                      | VARCHAR | Unidade Federativa (Estado) do endereço        |
| CEP                     | VARCHAR | Código de Endereçamento Postal da operadora    |
| DDD                     | VARCHAR | Código de Discagem Direta da operadora         |
| TELEFONE                | VARCHAR | Número de telefone da operadora                |
| FAX                     | VARCHAR | Número de fax da operadora                     |
| ENDERECO_ELETRONICO     | VARCHAR | Endereço eletrônico (e-mail) da operadora      |
| REPRESENTANTE           | VARCHAR | Nome do representante legal da operadora       |
| CARGO_REPRESENTANTE     | VARCHAR | Cargo do representante legal da operadora      |
| REGIAO_DE_COMERCIALIZACAO | VARCHAR | Região de comercialização da operadora         |
| DATA_REGISTRO_ANS       | DATE    | Data de registro da operadora na ANS           |


### Tabela TEMP_DADOS
| Coluna               | Tipo         | Descrição                                    |
|----------------------|--------------|----------------------------------------------|
| DATA_REFERENCIA      | DATE         | Data de referência dos dados                  |
| REG_ANS              | INT          | Chave estrangeira para a tabela OPERADORAS_ATIVAS |
| CD_CONTA_CONTABIL    | VARCHAR(20)  | Código da conta contábil                      |
| DESCRICAO            | VARCHAR(200) | Descrição da conta contábil                   |
| VALOR_SALDO_INICIAL  | VARCHAR(20)  | Valor do saldo inicial (temporário)           |
| VALOR_SALDO_FINAL    | VARCHAR(20)  | Valor do saldo final (temporário)             |

### Tabela DEMONSTRACOES_CONTABEIS
| Coluna               | Tipo      | Descrição                                    |
|----------------------|-----------|----------------------------------------------|
| ID                   | SERIAL    | Chave primária autoincrementada              |
| DATA_REFERENCIA      | DATE      | Data de referência dos dados                  |
| REG_ANS              | INT       | Chave estrangeira para a tabela OPERADORAS_ATIVAS |
| CD_CONTA_CONTABIL    | VARCHAR(20)  | Código da conta contábil                      |
| DESCRICAO            | VARCHAR(200) | Descrição da conta contábil                   |
| VALOR_SALDO_INICIAL  | NUMERIC   | Valor do saldo inicial (transformado)        |
| VALOR_SALDO_FINAL    | NUMERIC   | Valor do saldo final (transformado)          |

## Importação de Dados
Os dados das operadoras ativas são importados a partir do arquivo CSV 'Relatorio_cadop.csv' para a tabela OPERADORAS_ATIVAS. Além disso, os dados financeiros de diferentes trimestres dos anos de 2022 e 2023 são importados para a tabela temporária TEMP_DADOS.

## Transformação de Dados
Os dados financeiros importados têm valores numéricos com vírgula como separador decimal. Antes de inserir na tabela permanente, os valores são transformados, substituindo a vírgula por ponto.

## Análises Financeiras
O script realiza duas consultas SQL para identificar as 10 operadoras com maiores despesas na categoria 'EVENTOS/ SINISTROS CONHECIDOS OU AVISADOS DE ASSISTÊNCIA A SAÚDE MEDICO HOSPITALAR' nos últimos trimestre e ano, respectivamente.

## Execução do Script
1. Execute o script SQL no seu ambiente PostgreSQL.
2. Certifique-se de que os arquivos CSV estão localizados no caminho especificado no script.

## Requisitos
PostgreSQL instalado.
Observação: Certifique-se de substituir os caminhos dos arquivos CSV pelos caminhos reais no seu sistema.

Este README fornece uma visão geral do processo. Caso haja dúvidas ou melhorias, sinta-se à vontade para ajustar conforme necessário.
