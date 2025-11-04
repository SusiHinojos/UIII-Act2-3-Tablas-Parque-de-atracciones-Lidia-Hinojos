# Proyecto: Parque de Atracciones

**Lenguaje**: Python  
**Framework**: Django  
**Editor**: VS Code  

---

## Procedimientos

### 1. Crear carpeta del Proyecto

- Crear la carpeta: `UIII_parquedeatracciones_0248`

### 2. Abrir VS Code sobre la carpeta

- Abrir la carpeta `UIII_parquedeatracciones_0248` en VS Code.

### 3. Abrir terminal en VS Code

- Abrir la terminal integrada dentro de VS Code.

### 4. Crear entorno virtual `.venv` desde terminal

- Ejecutar el comando en terminal para crear el entorno virtual:
  ```bash
  python -m venv .venv
5. Activar el entorno virtual
En Windows:

bash
Copiar código
.\.venv\Scripts\activate
En macOS/Linux:

bash
Copiar código
source .venv/bin/activate
6. Activar el intérprete de Python
En VS Code, selecciona el intérprete de Python desde la barra inferior o desde el comando Python: Select Interpreter.

7. Instalar Django
Ejecutar el comando para instalar Django:

bash
Copiar código
pip install django
8. Crear proyecto backend_parque sin duplicar carpeta
Ejecutar el comando:

bash
Copiar código
django-admin startproject backend_parque
9. Ejecutar servidor en el puerto 8016
Para ejecutar el servidor en el puerto 8016:

bash
Copiar código
python manage.py runserver 8016
10. Copiar y pegar el link en el navegador
El servidor estará disponible en: http://127.0.0.1:8016

11. Crear aplicación app_parque
Ejecutar el comando para crear la app:

bash
Copiar código
python manage.py startapp app_parque
Modelos en models.py
python
Copiar código
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
Procedimientos adicionales
12. Realizar migraciones (makemigrations y migrate)
Ejecutar los siguientes comandos:

bash
Copiar código
python manage.py makemigrations
python manage.py migrate
13. Trabajar con el modelo: EMPLEADO
Crear las vistas y operaciones CRUD para Empleado.

14. Vistas en views.py para operaciones CRUD en Empleado
python
Copiar código
# views.py de app_parque
from django.shortcuts import render

def inicio_parque(request):
    return render(request, 'inicio.html')

def agregar_empleado(request):
    # Código para agregar empleado
    pass

def actualizar_empleado(request):
    # Código para actualizar empleado
    pass

def realizar_actualizacion_empleado(request):
    # Código para realizar actualización de empleado
    pass

def borrar_empleado(request):
    # Código para borrar empleado
    pass
15. Crear la carpeta "templates" dentro de app_parque
Estructura de directorios:

css
Copiar código
app_parque/
└── templates/
    ├── base.html
    ├── header.html
    ├── navbar.html
    ├── footer.html
    └── inicio.html
16. Agregar Bootstrap en base.html
Incluir los enlaces a Bootstrap para CSS y JS.

17. Crear archivos HTML de la interfaz
navbar.html con opciones de menú.

footer.html con derechos de autor y fecha.

inicio.html con información del sistema.

Tareas pendientes
Modelo Cliente y Atracción: A trabajar más adelante.

Validación de entrada de datos: No se validará en este momento.

Últimos pasos
Ejecutar servidor en el puerto 8016:

bash
Copiar código
python manage.py runserver 8016
El proyecto debe ser completamente funcional.

¡Creado por: Lidia Hinojos, Técnico en programación, Cbtis 128**

markdown
Copiar código

### ¿Cómo hacerlo en GitHub?
1. En tu repositorio de GitHub, crea un archivo nuevo llamado `README.md` (o abre uno si ya existe).
2. Copia y pega el código de arriba en el archivo.
3. Guarda el archivo.
4. Realiza un *commit* y *push* para subirlo al repositorio.
