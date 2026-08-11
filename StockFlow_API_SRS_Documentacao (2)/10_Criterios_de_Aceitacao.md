# 10. Critérios de Aceitação

## CA-001 — Cadastro de Produto
Dado que os dados obrigatórios sejam válidos, quando o cadastro for realizado, então o produto deverá ser persistido e retornar identificador.

## CA-002 — SKU Duplicado
Dado que já exista um SKU, quando outro produto utilizar o mesmo SKU, então a API deverá rejeitar o cadastro.

## CA-003 — Entrada de Estoque
Dado um produto existente, quando uma entrada válida for registrada, então o saldo deverá ser incrementado e uma movimentação deverá ser criada.

## CA-004 — Saída de Estoque
Dado um produto com saldo suficiente, quando uma saída válida for registrada, então o saldo deverá ser decrementado e uma movimentação deverá ser criada.

## CA-005 — Estoque Insuficiente
Dado um saldo inferior à quantidade solicitada, quando uma saída for registrada, então a operação deverá ser rejeitada e o saldo deverá permanecer inalterado.

## CA-006 — Quantidade Inválida
Quando uma movimentação possuir quantidade menor ou igual a zero, então a API deverá rejeitar a solicitação.

## CA-007 — Produto Inexistente
Quando uma operação utilizar um produto inexistente, então a API deverá retornar erro apropriado.

## CA-008 — Estoque Baixo
Quando o estoque atual for menor ou igual ao estoque mínimo, então o produto deverá ser identificado como estoque baixo.

## CA-009 — Histórico
Toda entrada ou saída aceita deverá possuir registro correspondente no histórico.

## CA-010 — Documentação
A API deverá disponibilizar documentação OpenAPI/Swagger.
