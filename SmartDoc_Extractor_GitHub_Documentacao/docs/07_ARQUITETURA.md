# Arquitetura da Solução
```text
Browser → Web UI → Flask/API → Services → Document Processing
                                  ├ PDF
                                  ├ XML
                                  ├ Excel/CSV
                                  ├ DOCX/TXT
                                  ├ Imagem/OCR
                                  └ IA
                         → Validação/Workflow → PostgreSQL
```
## Tecnologias
Python, Flask inicialmente, FastAPI conforme evolução de API, PostgreSQL, SQLAlchemy, Alembic, pandas, openpyxl, PyMuPDF/pdfplumber, ElementTree/lxml, python-docx, Pillow/OpenCV, OCR, Regex, Docker, RabbitMQ e Redis.

## Padrões
Service Layer, Repository, Factory, Strategy, Dependency Injection e SOLID.

## Estratégia
Começar modularmente e evitar microserviços prematuros; adotar filas/serviços independentes quando volume justificar.
