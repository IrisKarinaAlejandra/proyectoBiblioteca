[README.md](https://github.com/user-attachments/files/23313177/README.md)
# BiblioTecITTJ
# Autores IBARRA HERNANDEZ VICENTE DANIEL, JOSE VICENTE RICO MACIEL, IRIS KARINA ALEJANDRA GONZALEZ ESPINOZA

Proyecto base listo para subir a **Hostinger** (PHP + MySQL) con frontend **HTML/CSS/Bootstrap 5** y **JavaScript**.

## Características
- Login de usuario (PHP Sessions)
- CRUD de Libros y Estudiantes
- Préstamos y Devoluciones (con cálculo de multas)
- Reportes descargables (CSV)
- Importación masiva por CSV (Libros y Estudiantes)
- Validaciones institucionales:
  - Números de Control de **8 dígitos** (regex `^\d{8}$`)
  - Correos válidos solo en el dominio **@tlajomulco.tecnm.mx**
- Interfaz moderna con **tema claro/oscuro** y **cambio de fondo**

## Estructura
```
/api
  auth.php            # Login/Logout
  books.php           # CRUD Libros + import CSV
  students.php        # CRUD Estudiantes + import CSV
  loans.php           # Crear/Devolver préstamos
  fines.php           # Listar/actualizar multas (pago)
  reports.php         # CSV de préstamos, multas, inventario
  db.php              # Conexión DB (PDO)
  config.php          # Configuración (DB, ajustes)
/db
  schema.sql          # Estructura de tablas
/public
  index.html          # Login
  app.html            # Panel principal
  /css/styles.css
  /js/api.js          # Cliente para consumir API
  /js/app.js          # Lógica UI
/samples
  books_sample.csv
  students_sample.csv
```

## Requisitos en Hostinger
1. Crear una base de datos MySQL y usuario.
2. Subir todo el contenido del proyecto (carpeta `api`, `public`, etc.) al hosting.
3. Editar `/api/config.php` con tus credenciales de DB.
4. Importar `/db/schema.sql` en **phpMyAdmin**.
5. (Opcional) Crear usuario admin con el script `/api/auth.php?action=seed_admin` desde el navegador una vez configurada la DB.
   - Usuario: `admin`
   - Password: `admin123` (¡cámbialo después de entrar!)

## Seguridad
- Las contraseñas se guardan con `password_hash` (BCRYPT).
- Las sesiones de PHP se usan para autenticar.
- Todas las peticiones desde frontend usan `fetch` con `credentials: "include"`.

## CSV
- **/api/books.php?action=import_csv** (POST con `multipart/form-data` campo `file`).
- **/api/students.php?action=import_csv** (POST con `multipart/form-data` campo `file`).

## Reportes
- **/api/reports.php?type=loans|fines|inventory** (GET) => descarga CSV.

## Multas
- Configurable en `config.php` (por defecto **$5 MXN por día** de retraso).
