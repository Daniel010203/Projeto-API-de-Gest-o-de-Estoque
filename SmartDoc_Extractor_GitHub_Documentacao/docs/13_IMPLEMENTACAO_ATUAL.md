# Implementação Atual
## Ambiente
Windows 10, Python 3.12.3, ambiente virtual `venv`, Flask funcionando localmente.

## Estrutura atual
```text
Projeto16-SmartDocExtractor/
├ app.py
├ README.md
├ requirements.txt
├ app/
│ ├ __init__.py
│ └ routes.py
├ static/
│ ├ css/style.css
│ └ js/script.js
└ templates/index.html
```

## Factory
```python
from flask import Flask
def create_app():
    app = Flask(__name__)
    from .routes import main
    app.register_blueprint(main)
    return app
```

## Rota
```python
from flask import Blueprint, render_template
main = Blueprint("main", __name__)
@main.route("/")
def home():
    return render_template("index.html")
```

## Execução
`python app.py` → `http://127.0.0.1:5000`

Durante a preparação foram corrigidos problemas de nomeação de `__init__.py`, execução/indentação e estrutura do projeto. O Flask passou a iniciar corretamente.

## Próximo ponto
Sprint 1: upload PDF → validação → extração → palavras-chave → CSV → testes.
