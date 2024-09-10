# Lean_Flask_Jinja
Создайте свой HTML-шаблон (файл base.html).  Создайте страницы home.html и about.html, которые будут расширять шаблон и заполнять его контентом.
 Для реализации с использованием Jinja можно создать три файла:

1. `base.html` – основной шаблон, который будет содержать общие части сайта.
2. `home.html` – главная страница, которая расширяет `base.html` и добавляет контент.
3. `about.html` – страница "О нас", также расширяющая `base.html`.

### 1. `base.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Website{% endblock %}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
</head>
<body>
    <header>
        <nav>
            <ul>
                <li><a href="{{ url_for('home') }}">Home</a></li>
                <li><a href="{{ url_for('about') }}">About</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        {% block content %}
        <!-- Page content will go here -->
        {% endblock %}
    </main>

    <footer>
        <p>&copy; 2024 My Website</p>
    </footer>
</body>
</html>
```

### 2. `home.html`
```html
{% extends 'base.html' %}

{% block title %}Home{% endblock %}

{% block content %}
<h1>Welcome to My Website</h1>
<p>This is the home page content.</p>
{% endblock %}
```

### 3. `about.html`
```html
{% extends 'base.html' %}

{% block title %}About Us{% endblock %}

{% block content %}
<h1>About Us</h1>
<p>Here you can learn more about our company.</p>
{% endblock %}
```

### Использование в проекте
В Flask или другом веб-фреймворке на Python, вот как можно рендерить эти шаблоны:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('home.html')

@app.route('/about')
def about():
    return render_template('about.html')

if __name__ == '__main__':
    app.run(debug=True)
```

Этот код создаст базовый шаблон с общей структурой (шапка, футер, стили), который будет расширяться на страницах `home.html` и `about.html`.