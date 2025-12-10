⛽ Sistema de Gestão de Posto de Combustível

Este projeto representa o modelo de banco de dados para um sistema de gerenciamento de um posto de combustível, incluindo funcionalidades de vendas, empregados, departamentos, controle de combustíveis e volumes, e cadastros de clientes e dependentes.

🗂️ Estrutura do Banco de Dados

O modelo utiliza MySQL e inclui as seguintes entidades principais:

👤 EMPREGADO

Descrição: Armazena informações sobre os empregados do posto.

Atributos principais:

cpf_empregado (PK)

nome

sexo (ENUM 'M', 'F')

salario

DEPARTAMENTO_idDEPARTAMENTO (FK, obrigatório)

ENDEREÇO_idENDEREÇO (FK, opcional)

Relacionamentos:

Cada empregado pertence a um departamento (linha contínua).

Pode ter telefone(s) (opcional, tracejada).

Pode ter dependentes (opcional, tracejada).

Pode realizar vendas (opcional, tracejada).

🏢 DEPARTAMENTO

Descrição: Guarda informações sobre departamentos do posto.

Atributos:

idDEPARTAMENTO (PK)

nome, email, descricao, local

cpf_gerente (FK opcional)

Relacionamento:

Um departamento pode ter vários empregados.

🏠 ENDEREÇO

Descrição: Registra os endereços dos empregados.

Atributos:

idENDEREÇO (PK)

cidade, bairro, rua, numero, complemento, cep

Relacionamento:

Pode estar associado a um empregado (opcional, tracejada).

📞 TELEFONE

Descrição: Contém os números de telefone dos empregados.

Relacionamento:

Cada telefone pertence a um empregado (opcional, tracejada).

👶 DEPENDENTES

Descrição: Cadastro de dependentes de cada empregado.

Atributos:

CPF (PK)

nome, DataNasc, parentesco

EMPREGADO_cpf_empregado (FK)

Relacionamento:

Cada dependente está vinculado a um empregado (opcional, tracejada).

💰 VENDAS

Descrição: Armazena as vendas realizadas no posto.

Atributos:

idVENDAS (PK)

data

valorTOTAL

EMPREGADO_cpf_empregado (FK, obrigatório)

BOMBCOMB_idBOMBCOMB (FK)

FORMAS_PAG_idFORMAS_PAG (FK)

Relacionamento:

Cada venda é realizada por um empregado (linha contínua).

Pode incluir itens de venda (opcional, tracejada).

🛢️ COMBUSTÍVEL

Descrição: Registra os tipos de combustíveis disponíveis.

Relacionamento:

Cada combustível pode estar em vários itens de venda (opcional, tracejada).

📦 ITENS_VENDA

Descrição: Detalha os combustíveis vendidos em cada venda.

Relacionamento:

Cada item pertence a uma venda e um tipo de combustível.

🛠️ FORMAS_PAG

Descrição: Guarda os métodos de pagamento disponíveis (cartão, PIX, espécie).

⛽ BOMBCOMB

Descrição: Registra os abastecimentos realizados nas bombas.

📊 VOLUME

Descrição: Controla o volume de combustível disponível em cada bomba.
