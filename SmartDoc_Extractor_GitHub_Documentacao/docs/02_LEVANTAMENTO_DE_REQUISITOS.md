# Levantamento de Requisitos
## Funcionais
RF01 Upload; RF02 Upload em massa; RF03 Monitoramento de pastas; RF04 Identificação documental; RF05 OCR; RF06 Extração por palavras-chave/Regex/IA; RF07 Campos configuráveis; RF08 Regras por modelo; RF09 Validação; RF10 Banco; RF11 Pesquisa; RF12 Exportação CSV/Excel/PDF/JSON/XML; RF13 Dashboard; RF14 Histórico; RF15 Logs; RF16 Workflow; RF17 API/ERP/BI/SAP/TOTVS/Webhooks; RF18 Notificações; RF19 IA.

## Não funcionais
Interface web responsiva; meta inicial de até 5 segundos para documentos padrão, sujeita a benchmark; disponibilidade alvo 99,5%; PostgreSQL; segurança, HTTPS, autenticação, autorização, logs, backup e LGPD; escalabilidade; processamento paralelo/assíncrono.

## Regras de negócio
Documentos duplicados devem ser identificados; cada documento possui ID único; alterações relevantes geram auditoria; campos obrigatórios devem ser validados; inválidos vão para revisão; baixa confiança pode exigir revisão manual; original preservado conforme política de retenção.
