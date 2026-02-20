# Dicionário de Dados

## Tabela: clientes
Descrição: armazena dados cadastrais dos clientes.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_cliente | INT | Sim | PK | auto incremento | identificador do cliente |
| nome | VARCHAR(120) | Sim | - | - | nome completo |
| email | VARCHAR(160) | Sim | UNIQUE | formato válido | email principal |
| telefone | VARCHAR(20) | Não | - | - | telefone de contato |
| data_cadastro | TIMESTAMP | Sim | - | default current_timestamp | data de criação |

## Tabela: enderecos
Descrição: endereços vinculados aos clientes.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_endereco | INT | Sim | PK | auto incremento | identificador do endereço |
| id_cliente | INT | Sim | FK | ref clientes(id_cliente) | cliente dono do endereço |
| logradouro | VARCHAR(150) | Sim | - | - | rua/avenida |
| numero | VARCHAR(20) | Sim | - | - | número do endereço |
| cidade | VARCHAR(80) | Sim | - | - | cidade |
| estado | CHAR(2) | Sim | - | UF válida | estado |
| cep | VARCHAR(10) | Sim | - | formato CEP | cep |

## Tabela: categorias
Descrição: classificação dos produtos.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_categoria | INT | Sim | PK | auto incremento | identificador da categoria |
| nome_categoria | VARCHAR(80) | Sim | UNIQUE | - | nome da categoria |

## Tabela: produtos
Descrição: catálogo de produtos.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_produto | INT | Sim | PK | auto incremento | identificador do produto |
| id_categoria | INT | Sim | FK | ref categorias(id_categoria) | categoria do produto |
| nome_produto | VARCHAR(140) | Sim | - | - | nome do produto |
| preco_unitario | NUMERIC(10,2) | Sim | - | > 0 | preço atual |
| custo_unitario | NUMERIC(10,2) | Sim | - | >= 0 | custo estimado |
| ativo | BOOLEAN | Sim | - | default true | status de venda |

## Tabela: vendedores
Descrição: vendedores responsáveis pelos pedidos.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_vendedor | INT | Sim | PK | auto incremento | identificador do vendedor |
| nome_vendedor | VARCHAR(120) | Sim | - | - | nome do vendedor |
| email | VARCHAR(160) | Sim | UNIQUE | formato válido | email do vendedor |
| regiao | VARCHAR(50) | Sim | - | - | região de atuação |

## Tabela: estoque
Descrição: controle de saldo por produto.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_estoque | INT | Sim | PK | auto incremento | identificador do registro |
| id_produto | INT | Sim | FK | ref produtos(id_produto) | produto |
| quantidade_disponivel | INT | Sim | - | >= 0 | saldo em estoque |
| atualizado_em | TIMESTAMP | Sim | - | default current_timestamp | última atualização |

## Tabela: pedidos
Descrição: cabeçalho dos pedidos realizados.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_pedido | INT | Sim | PK | auto incremento | identificador do pedido |
| id_cliente | INT | Sim | FK | ref clientes(id_cliente) | cliente comprador |
| id_vendedor | INT | Sim | FK | ref vendedores(id_vendedor) | vendedor responsável |
| data_pedido | TIMESTAMP | Sim | - | default current_timestamp | data/hora do pedido |
| status_pedido | VARCHAR(30) | Sim | - | domínio de status | status atual |

## Tabela: itens_pedido
Descrição: itens associados aos pedidos.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_item_pedido | INT | Sim | PK | auto incremento | identificador do item |
| id_pedido | INT | Sim | FK | ref pedidos(id_pedido) | pedido associado |
| id_produto | INT | Sim | FK | ref produtos(id_produto) | produto vendido |
| quantidade | INT | Sim | - | > 0 | quantidade comprada |
| preco_unitario_item | NUMERIC(10,2) | Sim | - | > 0 | preço no momento da venda |

## Tabela: pagamentos
Descrição: informações de pagamento por pedido.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_pagamento | INT | Sim | PK | auto incremento | identificador do pagamento |
| id_pedido | INT | Sim | FK | ref pedidos(id_pedido) | pedido pago |
| forma_pagamento | VARCHAR(30) | Sim | - | domínio de formas | método de pagamento |
| valor_pago | NUMERIC(10,2) | Sim | - | > 0 | valor pago |
| status_pagamento | VARCHAR(30) | Sim | - | domínio de status | status do pagamento |
| data_pagamento | TIMESTAMP | Não | - | - | data/hora da confirmação |

## Tabela: entregas
Descrição: acompanhamento logístico dos pedidos.

| Coluna | Tipo | Obrigatório | Chave | Regra | Descrição |
|---|---|---|---|---|---|
| id_entrega | INT | Sim | PK | auto incremento | identificador da entrega |
| id_pedido | INT | Sim | FK | ref pedidos(id_pedido) | pedido entregue |
| data_envio | TIMESTAMP | Não | - | - | data de envio |
| data_entrega_prevista | TIMESTAMP | Não | - | - | previsão de entrega |
| data_entrega_real | TIMESTAMP | Não | - | - | entrega efetiva |
| status_entrega | VARCHAR(30) | Sim | - | domínio de status | status logístico |
