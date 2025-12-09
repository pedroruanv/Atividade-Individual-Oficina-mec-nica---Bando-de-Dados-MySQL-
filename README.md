README – Sistema de Gestão de Posto de Combustível

🏗️ Descrição do Projeto

Este projeto é um sistema de banco de dados relacional para um posto de combustível, permitindo gerenciar:

Funcionários e departamentos

Vendas de combustíveis

Bombas de combustível e volume abastecido

Telefones e endereços de funcionários

Dependentes de funcionários

Formas de pagamento

Itens vendidos por venda

O banco foi modelado seguindo normas de normalização e garantindo integridade referencial.



📂 Estrutura das Tabelas

1. DEPARTAMENTO

Descrição: Armazena informações dos departamentos do posto.

Atributos:

idDEPARTAMENTO INT – PK

nome VARCHAR(45)

email VARCHAR(100)

descricao VARCHAR(200)

local VARCHAR(100)

cpf_gerente CHAR(11)

Relacionamentos:

1:N com EMPREGADO (DEPARTAMENTO_idDEPARTAMENTO)

2. EMPREGADO

Descrição: Armazena informações dos funcionários.

Atributos:

cpf_empregado CHAR(11) – PK

nome VARCHAR(100)

sexo ENUM('M', 'F')

salario DECIMAL(10,2)

DEPARTAMENTO_idDEPARTAMENTO INT – FK

ENDERECO_idENDERECO INT – FK

Relacionamentos:

1:N com TELEFONE, DEPENDENTES, VENDAS

N:1 com DEPARTAMENTO

1:1 com ENDEREÇO

3. TELEFONE

Descrição: Telefones dos funcionários.

Atributos:

idTELEFONE INT – PK

numero VARCHAR(20)

EMPREGADO_cpf_empregado CHAR(11) – FK

Relacionamento: N:1 → EMPREGADO

Ação sugerida: ON DELETE CASCADE, ON UPDATE CASCADE

4. ENDEREÇO

Descrição: Endereços dos funcionários.

Atributos:

idENDERECO INT – PK

cidade VARCHAR(45)

bairro VARCHAR(45)

rua VARCHAR(100)

numero INT

complemento VARCHAR(50)

cep VARCHAR(9)

Relacionamento: 1:1 → EMPREGADO

5. DEPENDENTES

Descrição: Dependentes dos funcionários.

Atributos:

CPF VARCHAR(11) – PK

nome VARCHAR(100)

DataNasc DATE

parentesco VARCHAR(50)

EMPREGADO_cpf_empregado CHAR(11) – FK

Relacionamento: N:1 → EMPREGADO

Ação sugerida: ON DELETE CASCADE, ON UPDATE CASCADE

6. FORMAS_DE_PAGAMENTO

Descrição: Armazena os tipos de pagamento disponíveis.

Atributos:

idFORMAS_PAG INT – PK

cartao CHAR(150)

pix CHAR(150)

especie DECIMAL(10,2)

Relacionamento: 1:N com VENDAS

7. VENDAS

Descrição: Registro de vendas realizadas.

Atributos:

idVENDAS INT – PK

data DATE

valorTOTAL DECIMAL(10,2)

FORMAS_PAG_idFORMAS_PAG INT – FK

EMPREGADO_cpf_empregado CHAR(11) – FK

BOMBOMB_idBOMBCOMB INT – FK

Relacionamentos:

1:N com ITENS_VENDAS

N:1 com EMPREGADO, BOMBA_DE_COMBUSTÍVEL, FORMAS_DE_PAGAMENTO

8. ITENS_VENDAS

Descrição: Itens vendidos por cada venda.

Atributos:

idITENS_VENDAS INT – PK

combustiveis VARCHAR(?)

VENDAS_idVENDAS INT – FK

Relacionamento: N:1 → VENDAS

9. BOMBA_DE_COMBUSTÍVEL

Descrição: Bombas de combustível do posto.

Atributos:

idBOMBCOMB INT – PK

DataHora_Abastecimento DATETIME

Relacionamentos:

1:N com VENDAS

1:N com VOLUME

10. COMBUSTÍVEL

Descrição: Tipos de combustível disponíveis.

Atributos:

idItem_COMBUSTIVEL INT – PK

nome VARCHAR(100)

quantidade INT

valor DECIMAL(10,2)

BOMBOMB_idBOMBCOMB INT – FK

11. VOLUME

Descrição: Volume abastecido em cada bomba.

Atributos:

idVOLUME INT – PK

BOMBOMB_idBOMBCOMB INT – FK

🔗 Resumo dos Relacionamentos

1:N → DEPARTAMENTO → EMPREGADO

1:N → EMPREGADO → TELEFONE, DEPENDENTES, VENDAS

1:1 → EMPREGADO → ENDEREÇO

1:N → VENDAS → ITENS_VENDAS

1:N → BOMBA_DE_COMBUSTÍVEL → VENDAS, VOLUME

1:N → FORMAS_DE_PAGAMENTO → VENDAS

1:N → COMBUSTÍVEL → ITENS_VENDAS

⚙️ Observações

Todas as tabelas filhas recebem FK apontando para a tabela pai.

Uso de ON DELETE CASCADE em tabelas dependentes (TELEFONE, DEPENDENTES, ITENS_VENDAS) para manter integridade.

O modelo permite gerar relatórios detalhados por vendas, funcionário, bomba, combustível e forma de pagamento.

Segue boas práticas de normalização e integridade referencial.
