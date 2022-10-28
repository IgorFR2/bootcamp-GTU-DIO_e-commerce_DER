# bootcamp-GTU-DIO_e-commerce_DER
Bootcamp exercise to create an e-commerce entity-relationship diagram.
PostgreSQL variables used in description.
# Entities
* cliente - Customer
  * client_id (int) - Client Identification
  * endereco_id (int) - Client address identifier
  * nome (varchar(50)) - Client name (nickname or brand)
  * telefone (varchar(13)) - Phone number, used brazilian format (+55 (12) 9 1234-1234)
  * email (varchar(150)) - Client e-mail.
* pessoa_fisica - Customer data (person).
  * nome_completo (varchar(150)) - Full name.
  * cpf (varchar(11)) - Social number.
* pessoa_juridica - Customer data (company).
  * razao_social (varchar(250)) - Company registered name.
  * cnpj (varchar(14)) - Company's registry number (similar to social number).
* endereco - Address
  * pais (varchar(2)) - BR, CA, NZ, DE, JP, CH, IS, US, IL, etc.
  * estado (varchar(50)) - State.
  * cidade (varchar(50)) - City.
  * logradouro (varchar(50)) - Street, road, boulevard or similar's name.
  * numero (varchar(10)) - Building/Apt number (ex: 123, 134 apt. 505, 123-B-505)
  * complemento (varchar(50)) - House, loft, mansion, igloo, etc.
* pedido - Purchase
  * client_id (biginteger) - Client Identification (surrogate)
  * prazo_estorno (date) - Refund date limit
  * decricao (varchar(250)) - Client observation or message (optional)
  * frete (integer) - Delivery fee. It can be integer (require division by 100) or money type. For safety porpouses, integer was chosen.
  * status_pedido_id (int) - Status id in status_pedido
  * pagamento (int) - Payment(s). It can combine different payment methods.
  * valor (int) - Purchase value
  * data_pedido (timestamp with timezone) - Row insertion date.
* status_pedido - List of possible purchase status
  * status_pedido_id (smallint) - Status identifier
  * status (varchar(40)) - Status description
* pedido_produto - Relationship table: product and purchase
  * produto_id (integer) - Product id
  * pedido_id (integer) - Purchase id
  * quantidade (integer) - Amount
* produto - Product
  * produto_id (integer) - Product identification
  * fornecedor_id (integer) - Provider identification
  * descricao (varchar(50)) - Product description
* categoria - List of product categories
  * categoria_id - Category identifier
  * categoria (varchar(50)) - Category name (ex: bath, eletronic, kitchen, food,18+)
* produto_categoria - Multiple product categorization
  * produto_id (integer) - Product identifier
  * categoria_id (integer) - Category identifier
* produto_estoque - Product's inventory.
  * produto_id (integer) - Product identifier
  * estoque_id (integer) - Inventory identifier 
  * quantidade (integer) - Quantity in stock
* estoque - Inventory
  * estoque_id (integer) - Inventory identifier.
  * local (varchar(150)) - Location of products.
  * data_cadastro (timestamptz) - Date and hour of registry.
* fornecedor_estoque - Replenishment of inventory
  * fornecedor_id (int) - Provider identification
  * estoque_id (int) - Inventory identification
* fornecedor - Provider
  * fornecedor_id (integer) - Provider identification
  * razao_social (varchar(250)) - Company's full name.
  * cnpj (varchar(14)) - Company's registry number.
* pagamento - Payment. A single purchase can have different payment methods.
  * pagamento_id (int) - Payment identifier.
  * pedido_id (int) - Purchase identifier.
  * valor (int) - Total purchase value
  * tipo_pagamento_id (int) - Payment type identifier.
  * data_pagamento(timestamptz, nullable) - Payment confirmation date. Start NULL.
* tipo_pagamento
  * tipo_pagamento_id (int) - Payment type identifier.
  * tipo_pagamento (varchar(20)) - Payment type description
* pagamento_cartao - Card payment (Credit/Debit)
  * pagamento_id (int) - Payment identifier.
  * numero_cartao_mascarado (varchar(16)) - Card's number anonymized. 4 first and 4 last numbers visible.
  * quantidade_parcelas (integer) - Number of installments 
* parcela - Installments
  * parcela_id (integer) - Installment identification.
  * valor (integer) - Installment value
  * numero_parcela (smallint) - Installment number (ex: 1 (first), 2 (second), 3...).
  * data_vencimento (date) - Date until payment.
  * status_pagamento_id (smallint) - Payment status identification
* pagamento_boleto - Bank slip 
  * pagamento_id (int) - Payment identifier.
  * codigo_boleto (text) - Bank slip code.
  * data_vencimento (date) - Date until payment.
  * status_pagamento_id (smallint) - Payment status identification
* status_pagamento - List of possible payment status 
  * status_pagamento_id (smallint) - Payment status identification
  * status (varchar(40)) - Status description.
* entrega - Delivery
  * pedido_id (int) - Purchase identifier.
  * endereco_id (biginteger) - Delivery address identifier
  * codigo_rastreio (varchar(30)) - Track code.
  * status_entrega_id (integer) - Delivery status identifier.
* status_entrega - List of possible delivery status
  * status_entrega_id (smallint) - Delivery status identifier.
  * status (varchar(40)) - Status description.
