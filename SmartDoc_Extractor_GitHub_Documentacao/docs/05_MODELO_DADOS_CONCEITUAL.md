# Capítulo 9 — Modelo de Dados Conceitual
## Entidades
Usuário, Perfil, Documento, Modelo Documental, Campo, Regra de Extração, Extração, Valor Extraído, Validação, Workflow, Auditoria e Exportação.

## Relacionamentos
Perfil 1:N Usuário; Usuário 1:N Documento; Modelo 1:N Campo; Campo 1:N Regra; Documento 1:N Extração; Extração 1:N Valor Extraído; Campo 1:N Valor Extraído; Valor 1:N Validação; Documento 1:N Workflow; Documento 1:N Auditoria; Usuário 1:N Exportação.

## Princípios
IDs únicos, integridade referencial, hash para duplicidade, histórico, versionamento de modelos/regras e separação entre definição de campos e valores extraídos.
