# Especificação da API REST
Base: `/api/v1`

| Método | Endpoint | Função |
|---|---|---|
| POST | /auth/login | Autenticar |
| POST | /documents | Upload |
| POST | /documents/batch | Lote |
| GET | /documents | Pesquisa |
| GET | /documents/{id} | Detalhes |
| POST | /documents/{id}/process | Processar |
| GET | /documents/{id}/extractions | Extrações |
| PATCH | /documents/{id}/extractions/{field_id} | Corrigir |
| POST | /documents/{id}/approve | Aprovar |
| POST | /documents/{id}/reject | Rejeitar |
| GET/POST | /exports | Exportação |
| GET | /dashboard/summary | Indicadores |
| GET/POST | /models | Modelos |
| GET/POST | /rules | Regras |
| GET | /audit-logs | Auditoria |

Códigos: 400, 401, 403, 404, 409, 422, 500, 503.

Segurança: JWT/OAuth2 conforme evolução, RBAC, HTTPS, rate limiting, logs e OpenAPI.
