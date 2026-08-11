# Modelo Lógico do Banco
## Banco
PostgreSQL.

## Tabelas
profiles, users, documents, document_models, fields, extraction_rules, extractions, extracted_values, validations, workflow_events, audit_logs, exports.

## Índices principais
documents(file_hash) UNIQUE; documents(status, created_at); documents(document_type); extractions(document_id, created_at); extracted_values(field_id); audit_logs(document_id, created_at).

## Normalização
Objetivo inicial: 3ª Forma Normal. Denormalizações somente quando comprovadas por necessidade de desempenho.

## Stack
PostgreSQL + SQLAlchemy + Alembic.
