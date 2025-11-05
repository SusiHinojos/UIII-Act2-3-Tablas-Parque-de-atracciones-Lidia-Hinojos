# Proyecto: Parque de Atracciones

## Lenguaje: Python
## Framework: Django
## Editor: VS Code

## Procedimientos
## 1. Crear la Carpeta del Proyecto

Nombre de la carpeta: UIII_parquedeatracciones_0248

## 2. Abrir VS Code en la Carpeta

Navega hasta la carpeta UIII_parquedeatracciones_0248 y abre VS Code desde ahí.

## 3. Abrir Terminal en VS Code

Puedes abrir la terminal desde el menú de VS Code o usando el atajo de teclado.

## 4. Crear el Entorno Virtual

Desde la terminal de VS Code, ejecuta el siguiente comando para crear el entorno virtual:

python -m venv .venv

## 5. Activar el Entorno Virtual

En la terminal, activa el entorno virtual:

En Windows:

.\.venv\Scripts\activate


En Mac/Linux:

source .venv/bin/activate

## 6. Activar el Intérprete de Python

Asegúrate de que VS Code esté usando el intérprete de Python correcto desde la paleta de comandos (Ctrl + Shift + P).

## 7. Instalar Django

Con el entorno virtual activo, instala Django:

pip install django

## 8. Crear el Proyecto Django

Crea el proyecto sin duplicar la carpeta:

django-admin startproject backend_parque

## 9. Ejecutar el Servidor en el Puerto 8016

Para correr el servidor en el puerto 8016:

python manage.py runserver 8016

## 10. Acceder al Proyecto en el Navegador

Copia el link generado en la terminal y pégalo en tu navegador: http://127.0.0.1:8016

## 11. Crear la Aplicación app_parque

Dentro del directorio backend_parque, crea la aplicación app_parque:

python manage.py startapp app_parque

Modelo models.py
from django.db import models

# ==========================================
# MODELO: EMPLEADO
# ==========================================
    class Empleado(models.Model):
        id_emp = models.AutoField(primary_key=True, unique=True)
        nombre = models.CharField(max_length=50)
        apellido = models.CharField(max_length=50)
        puesto = models.CharField(max_length=40)
        telefono = models.CharField(max_length=15)
        salario = models.DecimalField(max_digits=8, decimal_places=2)
        id_atr = models.IntegerField()
    
        def __str__(self):
            return self.nombre

# ==========================================
# MODELO: CLIENTE
# ==========================================
    class Cliente(models.Model):
        id_cli = models.AutoField(primary_key=True, unique=True)
        nombre = models.CharField(max_length=50)
        apellido = models.CharField(max_length=50)
        telefono = models.CharField(max_length=15)
        correo = models.CharField(max_length=50)
        fecha_reg = models.DateField(auto_now_add=True)
        id_atr = models.IntegerField()
    
        def __str__(self):
            return self.nombre

# ==========================================
# MODELO: ATRACCIÓN
# ==========================================
    class Atraccion(models.Model):
        id_atr = models.AutoField(primary_key=True, unique=True)
        nombre = models.CharField(max_length=50)
        tipo = models.CharField(max_length=50)
        capacidad = models.IntegerField()
        estado = models.CharField(max_length=100)
        altura_min = models.DecimalField(max_digits=3, decimal_places=2)
        id_emp = models.IntegerField()
    
        def __str__(self):
            return self.nombre

## 12. Realizar Migraciones

Realiza las migraciones necesarias para crear las tablas en la base de datos:

python manage.py makemigrations
python manage.py migrate

## 13. Trabajar con el Modelo Empleado

Crea las vistas y funcionalidades correspondientes en la aplicación.

## 14. Funciones en views.py de app_parque

En views.py, crea las funciones necesarias:

inicio_parque

agregar_empleado

actualizar_empleado

realizar_actualizacion_empleado

borrar_empleado

    from django.shortcuts import render, redirect
    from .models import Empleado
    from django.http import HttpResponse
    from django.template.loader import render_to_string
    
    # Página de inicio del sistema
    def inicio_parque(request):
        return render(request, 'inicio.html')
    
    # Agregar un nuevo empleado
    def agregar_empleado(request):
        if request.method == 'POST':
            nombre = request.POST.get('nombre')
            apellido = request.POST.get('apellido')
            puesto = request.POST.get('puesto')
            telefono = request.POST.get('telefono')
            salario = request.POST.get('salario')
            id_atr = request.POST.get('id_atr')
            
            empleado = Empleado(nombre=nombre, apellido=apellido, puesto=puesto,
                                telefono=telefono, salario=salario, id_atr=id_atr)
            empleado.save()
            return redirect('ver_empleado')  # Redirigir a la lista de empleados
        return render(request, 'empleado/agregar_empleado.html')
    
    # Ver empleados (mostrar todos los empleados)
    def ver_empleado(request):
        empleados = Empleado.objects.all()  # Obtener todos los empleados
        return render(request, 'empleado/ver_empleado.html', {'empleados': empleados})
    
    # Actualizar un empleado
    def actualizar_empleado(request, id_emp):
        empleado = Empleado.objects.get(id_emp=id_emp)
        if request.method == 'POST':
            empleado.nombre = request.POST.get('nombre')
            empleado.apellido = request.POST.get('apellido')
            empleado.puesto = request.POST.get('puesto')
            empleado.telefono = request.POST.get('telefono')
            empleado.salario = request.POST.get('salario')
            empleado.id_atr = request.POST.get('id_atr')
            empleado.save()
            return redirect('ver_empleado')  # Redirigir a la lista de empleados
        return render(request, 'empleado/actualizar_empleado.html', {'empleado': empleado})
    
    # Borrar un empleado
    def borrar_empleado(request, id_emp):
        empleado = Empleado.objects.get(id_emp=id_emp)
        if request.method == 'POST':
            empleado.delete()
            return redirect('ver_empleado')  # Redirigir a la lista de empleados
        return render(request, 'empleado/borrar_empleado.html', {'empleado': empleado})


## 15. Crear la Carpeta templates en app_parque

Dentro de app_parque, crea la carpeta templates.

## 16. Archivos HTML en la Carpeta templates

Crea los siguientes archivos HTML dentro de app_parque/templates:

# base.html
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Sistema Parque de Atracciones</title>
        <!-- Bootstrap 4 CSS -->
        <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
        <!-- Header -->
        {% include 'header.html' %}
        
        <!-- Navbar -->
        {% include 'navbar.html' %}
        
        <!-- Content -->
        <div class="container mt-4">
            {% block content %}
            <!-- El contenido de cada página se inyectará aquí -->
            {% endblock %}
        </div>
    
        <!-- Footer -->
        {% include 'footer.html' %}
    
        <!-- Bootstrap JS -->
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    </body>
    </html>

# header.html
    <header class="bg-primary text-white text-center py-3">
        <h1>Sistema de Administración Parque de Atracciones</h1>
    </header>


# navbar.html
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="/">Inicio</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <a class="nav-link" href="#">Empleado</a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item" href="#">Agregar empleado</a>
                        <a class="dropdown-item" href="#">Ver empleado</a>
                        <a class="dropdown-item" href="#">Actualizar empleado</a>
                        <a class="dropdown-item" href="#">Borrar empleado</a>
                    </div>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Clientes</a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item" href="#">Agregar cliente</a>
                        <a class="dropdown-item" href="#">Ver cliente</a>
                        <a class="dropdown-item" href="#">Actualizar cliente</a>
                        <a class="dropdown-item" href="#">Borrar cliente</a>
                    </div>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Atracciones</a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item" href="#">Agregar atracción</a>
                        <a class="dropdown-item" href="#">Ver atracción</a>
                        <a class="dropdown-item" href="#">Actualizar atracción</a>
                        <a class="dropdown-item" href="#">Borrar atracción</a>
                    </div>
                </li>
            </ul>
        </div>
    </nav>
    

# footer.html
    <footer class="bg-dark text-white text-center py-3">
        <p>&copy; {{ current_year }} - Creado por Técnico en Programación Lidia Hinojos, Cbtis 128</p>
    </footer>


# inicio.html
    {% extends 'base.html' %}
    
    {% block content %}
        <div class="row">
            <div class="col text-center">
                <h2>Bienvenido al Sistema de Administración del Parque de Atracciones</h2>
                <p>Administra empleados, clientes y atracciones con facilidad.</p>
                <img src="ruta/a/imagen.jpg" alt="Parque de Atracciones" class="img-fluid">
            </div>
        </div>
    {% endblock %}


## 17. Incluir Bootstrap en base.html

En base.html, agrega Bootstrap para CSS y JS.

## 18. Crear la Barra de Navegación en navbar.html

En navbar.html, crea un menú de navegación con las siguientes opciones:

Sistema de Administración Parque de Atracciones

Inicio

# Empleado (con submenú: Agregar empleado, Ver empleado, Actualizar empleado, Borrar empleado)
##  Agregar empleado
        {% extends 'base.html' %}
        
        {% block content %}
            <h2>Agregar Empleado</h2>
            <form method="POST">
                {% csrf_token %}
                <div class="form-group">
                    <label for="nombre">Nombre</label>
                    <input type="text" class="form-control" id="nombre" name="nombre" required>
                </div>
                <div class="form-group">
                    <label for="apellido">Apellido</label>
                    <input type="text" class="form-control" id="apellido" name="apellido" required>
                </div>
                <div class="form-group">
                    <label for="puesto">Puesto</label>
                    <input type="text" class="form-control" id="puesto" name="puesto" required>
                </div>
                <div class="form-group">
                    <label for="telefono">Teléfono</label>
                    <input type="text" class="form-control" id="telefono" name="telefono" required>
                </div>
                <div class="form-group">
                    <label for="salario">Salario</label>
                    <input type="number" class="form-control" id="salario" name="salario" step="0.01" required>
                </div>
                <div class="form-group">
                    <label for="id_atr">ID Atracción</label>
                    <input type="number" class="form-control" id="id_atr" name="id_atr" required>
                </div>
                <button type="submit" class="btn btn-primary">Guardar</button>
            </form>
        {% endblock %}
    
    ##  Ver empleado
        {% extends 'base.html' %}
    
    {% block content %}
        <h2>Lista de Empleados</h2>
        <table class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>Puesto</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                {% for empleado in empleados %}
                    <tr>
                        <td>{{ empleado.id_emp }}</td>
                        <td>{{ empleado.nombre }}</td>
                        <td>{{ empleado.apellido }}</td>
                        <td>{{ empleado.puesto }}</td>
                        <td>
                            <a href="{% url 'actualizar_empleado' empleado.id_emp %}" class="btn btn-warning btn-sm">Actualizar</a>
                            <a href="{% url 'borrar_empleado' empleado.id_emp %}" class="btn btn-danger btn-sm">Borrar</a>
                        </td>
                    </tr>
                {% endfor %}
            </tbody>
        </table>
    {% endblock %}
 ## Actualizar empleado
 
    {% extends 'base.html' %}
    
    {% block content %}
        <h2>Actualizar Empleado</h2>
        <form method="POST">
            {% csrf_token %}
            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input type="text" class="form-control" id="nombre" name="nombre" value="{{ empleado.nombre }}" required>
            </div>
            <div class="form-group">
                <label for="apellido">Apellido</label>
                <input type="text" class="form-control" id="apellido" name="apellido" value="{{ empleado.apellido }}" required>
            </div>
            <div class="form-group">
                <label for="puesto">Puesto</label>
                <input type="text" class="form-control" id="puesto" name="puesto" value="{{ empleado.puesto }}" required>
            </div>
            <div class="form-group">
                <label for="telefono">Teléfono</label>
                <input type="text" class="form-control" id="telefono" name="telefono" value="{{ empleado.telefono }}" required>
            </div>
            <div class="form-group">
                <label for="salario">Salario</label>
                <

## Borrar empleado
    {% extends 'base.html' %}
    
    {% block content %}
        <h2>¿Seguro que quieres eliminar a {{ empleado.nombre }}?</h2>
        <form method="POST">
            {% csrf_token %}
            <button type="submit" class="btn btn-danger">Sí, eliminar</button>
            <a href="{% url 'ver_empleado' %}" class="btn btn-secondary">Cancelar</a>
        </form>
    {% endblock %}


Clientes (con submenú: Agregar cliente, Ver cliente, Actualizar cliente, Borrar cliente)

Atracciones (con submenú: Agregar atracción, Ver atracción, Actualizar atracción, Borrar atracción)

## 19. Crear el Pie de Página en footer.html

En footer.html, incluye:

Derechos de autor

Fecha del sistema

"Creado por Técnico en Programación Lidia Hinojos, Cbtis 128"

Mantenerlo fijo al final de la página.

## 20. Página de Inicio en inicio.html

En inicio.html, incluye información sobre el sistema y una imagen relacionada con el parque de atracciones.

## 21. Subcarpeta empleado en templates

Crea la subcarpeta empleado dentro de app_parque/templates.

## 22. Archivos HTML de Empleados

Crea los siguientes archivos dentro de app_parque/templates/empleado:

agregar_empleado.html

ver_empleado.html (muestra los empleados en una tabla con botones para ver, editar y borrar)

actualizar_empleado.html

borrar_empleado.html

## 23. No Usar forms.py

No se utilizará forms.py para la creación de formularios.

## 24. Crear urls.py en app_parque

En app_parque, crea el archivo urls.py para enlazar las funciones de views.py con las URLs correspondientes para las operaciones CRUD de empleados.
    from django.urls import path
    from . import views
    
    urlpatterns = [
        path('', views.inicio_parque, name='inicio_parque'),
        path('agregar_empleado/', views.agregar_empleado, name='agregar_empleado'),
        path('ver_empleado/', views.ver_empleado, name='ver_empleado'),
        path('actualizar_empleado/<int:id_emp>/', views.actualizar_empleado, name='actualizar_empleado'),
        path('borrar_empleado/<int:id_emp>/', views.borrar_empleado, name='borrar_empleado'),
    ]


## 25. Registrar app_parque en settings.py

    Agrega app_parque en el archivo settings.py de backend_parque.
    # settings.py
    
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_parque',  # Asegúrate de incluir tu aplicación 'app_parque'
    ]
    
    # Configuración de la base de datos
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
        }
    }
    
    # Ruta de archivos estáticos
    STATIC_URL = '/static/'
    
    # Agregar templates en settings.py
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [BASE_DIR / 'app_parque/templates'],  # Añadir el directorio de plantillas de app_parque
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]

    # Para usar la variable `current_year` en el pie de página
    from datetime import datetime
    CURRENT_YEAR = datetime.now().year


## 26. Configurar urls.py en backend_parque

Configura el archivo urls.py de backend_parque para enlazarlo con app_parque.

## 27. Registrar Modelos en admin.py y Migraciones

Registra el modelo Empleado en admin.py y realiza las migraciones correspondientes.


## 28. Diseño Visual

Utiliza colores suaves y modernos para la interfaz web.

## 29. Estructura de Carpetas y Archivos

Asegúrate de crear la estructura completa de carpetas y archivos al inicio del proyecto.

## 30. Proyecto Funcional

El proyecto debe estar completamente funcional y listo para usar.

## 31. Ejecutar Servidor en el Puerto 8016

Finalmente, ejecuta el servidor en el puerto 8016 para probar la aplicación.
## Estructura de Carpetas y Archivos
    UIII_parquedeatracciones_0248/
    │
    ├── backend_parque/   
    │   ├── backend_parque/     
    │   │   ├── __init__.py
    │   │   ├── asgi.py
    │   │   ├── settings.py  
    │   │   ├── urls.py   
    │   │   └── wsgi.py
    │   │
    │   ├── app_parque/   
    │   │   ├── __init__.py
    │   │   ├── admin.py  
    │   │   ├── apps.py
    │   │   ├── migrations/  
    │   │   │   └── __init__.py
    │   │   ├── models.py  
    │   │   ├── tests.py
    │   │   ├── views.py  
    │   │   ├── urls.py 
    │   │   └── templates/   
    │   │       ├── base.html 
    │   │       ├── footer.html   
    │   │       ├── header.html 
    │   │       ├── navbar.html  
    │   │       ├── inicio.html  
    │   │       └── empleado/ 
    │   │           ├── agregar_empleado.html
    │   │           ├── ver_empleado.html
    │   │           ├── actualizar_empleado.html
    │   │           └── borrar_empleado.html
    │   │
    │   ├── manage.py   
    │   └── db.sqlite3 
    │
    ├── .venv/        
    │   └── ...     
    
    │
    └── requirements.txt                 
