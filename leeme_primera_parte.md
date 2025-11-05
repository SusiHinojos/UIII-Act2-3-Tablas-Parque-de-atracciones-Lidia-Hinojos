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

## 15. Crear la Carpeta templates en app_parque

Dentro de app_parque, crea la carpeta templates.

## 16. Archivos HTML en la Carpeta templates

Crea los siguientes archivos HTML dentro de app_parque/templates:

base.html

header.html

navbar.html

footer.html

inicio.html

## 17. Incluir Bootstrap en base.html

En base.html, agrega Bootstrap para CSS y JS.

## 18. Crear la Barra de Navegación en navbar.html

En navbar.html, crea un menú de navegación con las siguientes opciones:

Sistema de Administración Parque de Atracciones

Inicio

Empleado (con submenú: Agregar empleado, Ver empleado, Actualizar empleado, Borrar empleado)

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

## 25. Registrar app_parque en settings.py

Agrega app_parque en el archivo settings.py de backend_parque.

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
