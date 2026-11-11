# Guía paso a paso · Del XAMPP a la nube

Esta guía cubre las partes II y III de la práctica: servidor local, base de datos, despliegue en la nube y pruebas finales.
Se usa **InfinityFree** porque es gratis y ya trae Apache + PHP + MySQL (lo que pide el proyecto).

---

## PARTE II · Servidor local con XAMPP

### 1. Instalar y encender XAMPP
1. Descarga XAMPP desde apachefriends.org e instálalo (deja marcados Apache, MySQL, PHP y phpMyAdmin).
2. Abre el **XAMPP Control Panel** y presiona **Start** en **Apache** y **MySQL**.
3. Ambos deben quedar en **verde**. 📸 *Captura 1: panel de XAMPP con Apache y MySQL en verde.*

> Si Apache no arranca, casi siempre es porque Skype u otro programa usa el puerto 80. Ciérralo o cambia el puerto en *Config → httpd.conf*.

### 2. Copiar el sitio
Copia la carpeta `fisioterapia-buap` dentro de `C:\xampp\htdocs\`.

### 3. Crear la base de datos
1. Entra a `http://localhost/phpmyadmin`.
2. Clic en **Nueva** → nombre: `fisioterapia_buap` → cotejamiento `utf8mb4_unicode_ci` → **Crear**.
3. Con la base seleccionada, pestaña **Importar** → **Seleccionar archivo** → `database/fisioterapia_buap.sql` → **Continuar**.
4. Verás 4 tablas: `usuarios`, `materias`, `aspirantes`, `encuestas`. 📸 *Captura 2: tablas en phpMyAdmin.*

### 4. Probar
Abre `http://localhost/fisioterapia-buap/` y prueba:
- Inicia sesión con `aspirante@buap.mx` / `fisio2026` → registra, edita y elimina una ficha (CRUD).
- Inicia sesión con `admin@buap.mx` / `admin2026` → agrega, edita y elimina una materia (CRUD).
- Responde la encuesta y revisa que los resultados cambien.

> `includes/config.php` ya viene listo para XAMPP (`localhost`, usuario `root`, sin contraseña).

---

## PARTE III · Despliegue en la nube (InfinityFree)

### 5. Crear la cuenta y el servidor
1. Entra a **infinityfree.com** → **Register** (verifica tu correo).
2. **Create Account** → elige un **subdominio gratis**, por ejemplo `fisiobuap.infinityfreeapp.com`.
   *(Ese es tu dominio: InfinityFree crea automáticamente sus registros DNS.)*
3. Espera a que la cuenta diga **Active** y entra al **Control Panel**. 📸 *Captura 3: cuenta activa y dominio.*

> **¿Dominio propio?** En *Domains → Add Domain* agrega tu dominio y, en la empresa donde lo compraste, cambia los **nameservers** por los que te muestra el panel. Los cambios de DNS pueden tardar hasta 24 h. 📸 *Captura del dominio apuntado.*

### 6. Base de datos en la nube
1. Control Panel → **MySQL Databases** → escribe `fisio` → **Create Database**.
2. Anota los datos que aparecen (los vas a necesitar):

   | Dato | Ejemplo |
   |---|---|
   | MySQL Host Name | `sql123.infinityfree.com` |
   | MySQL DB Name | `if0_37000000_fisio` |
   | MySQL User Name | `if0_37000000` |
   | MySQL Password | la contraseña de tu cuenta (botón *Show* en *Account details*) |

3. Clic en **phpMyAdmin** junto a tu base → **Importar** → `fisioterapia_buap.sql` → **Continuar**.
   📸 *Captura 4: phpMyAdmin en la nube con las 4 tablas (migración de la base de datos).*

### 7. Configurar la conexión
Abre `includes/config.php` y cambia los valores por los de tu panel:

```php
define('DB_HOST', cfg('DB_HOST', 'sql123.infinityfree.com'));
define('DB_NAME', cfg('DB_NAME', 'if0_37000000_fisio'));
define('DB_USER', cfg('DB_USER', 'if0_37000000'));
define('DB_PASS', cfg('DB_PASS', 'TuContraseñaDelHosting'));
```

### 8. Subir los archivos
**Opción A · File Manager:** Control Panel → **Online File Manager** → entra a `htdocs` → borra el `index2.html` de ejemplo → **Upload** de todos los archivos de `fisioterapia-buap` (con sus carpetas).

**Opción B · FileZilla (FTP):** usa el *FTP Hostname*, usuario y contraseña de *Account details* (puerto 21) y arrastra el contenido de `fisioterapia-buap` a `/htdocs`.

> Sube el **contenido** de la carpeta, no la carpeta: `index.php` debe quedar directo en `htdocs`.

### 9. Seguridad (HTTPS)
1. Control Panel → **Free SSL Certificates** → elige tu dominio → sigue los pasos (agrega el registro CNAME que te pide para validar) → **Install**.
2. Cuando el candado 🔒 funcione, abre `.htaccess` y quita el `#` de las 3 líneas de **Forzar HTTPS**.
3. En `.htaccess` también puedes activar la línea `ErrorDocument 404 /404.php`.

> El HTTPS es necesario para que la **PWA** se pueda instalar en el celular.

### 10. Prueba final y capturas del reporte
Abre tu URL pública (ej. `https://fisiobuap.infinityfreeapp.com`) y revisa:

- [ ] Las 3 páginas cargan con imágenes, menús desplegables, tablas y listas.
- [ ] El video y el spot de radio se reproducen y sus enlaces abren.
- [ ] Los íconos de redes sociales abren las páginas de la BUAP.
- [ ] Crear cuenta / iniciar sesión funciona.
- [ ] CRUD de fichas (insertar, consultar, actualizar, eliminar).
- [ ] CRUD de materias como administrador.
- [ ] La encuesta guarda y muestra resultados.
- [ ] En el celular aparece **Instalar app** (o *Agregar a pantalla de inicio*).

📸 **Captura 5 (la más importante):** entra como administrador a **Panel de control**. El recuadro *Servidor y base de datos* muestra **Conectado**, el motor MySQL/MariaDB, el **host remoto** (`sqlXXX.infinityfree.com`), el dominio y HTTPS. Con esa imagen compruebas servidor en la nube + dominio + conexión a la BD remota.

---

## Alternativa: Render o Railway
El código también lee la configuración de **variables de entorno** (`DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASS`, `DB_PORT`), así que en Railway puedes crear un servicio PHP + un servicio MySQL y solo poner esas variables, sin tocar `config.php`.

## Problemas comunes
| Síntoma | Solución |
|---|---|
| «No se pudo conectar a MySQL» | Revisa host, nombre de base, usuario y contraseña en `config.php`. En InfinityFree el host **no** es `localhost`. |
| Error 500 | Revisa que subiste también la carpeta `includes/` y el archivo `.htaccess`. |
| Acentos raros (Ã©) | Importa el `.sql` con cotejamiento `utf8mb4_unicode_ci`. |
| No aparece «Instalar app» | Necesitas HTTPS y abrir el sitio al menos una vez con internet. |
