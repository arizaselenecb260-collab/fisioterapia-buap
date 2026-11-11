# Reporte técnico · Proyecto Final «Construye Aplicaciones Web»

**CBTIS 260 · Grupo “B”**
**Integrantes:** ______________________________________________
**Carrera elegida:** Licenciatura en Fisioterapia · BUAP
**URL pública del sitio:** https://______________________________

---

## 1. Requerimientos y prototipo
- Carrera: Licenciatura en Fisioterapia (Facultad de Medicina BUAP, sedes Puebla y Teziutlán, 8 semestres, 342 créditos).
- Pantallas: Inicio · Plan de Estudios · Egreso y Campo Laboral · Registro e Inscripciones · Encuesta · Inicio de sesión · Panel del administrador.
- *(Pegar aquí la foto del boceto en papel o digital.)*

## 2. Identidad visual
- Logotipo hecho en Paint: `assets/img/logo.png`. *(Pegar imagen.)*
- Paleta: azul marino `#003B5C`, turquesa `#00A896`, dorado `#F5B731`.
- Misión y visión: ver la página de Inicio.

## 3. Servidor local (XAMPP)
📸 Captura: XAMPP Control Panel con Apache y MySQL en verde.

## 4. Páginas, menús, listas, tablas y multimedia
| Requisito | Dónde se cumple |
|---|---|
| 3 páginas temáticas | `plan.php`, `campo.php`, `registro.php` |
| Menús desplegables | Barra de navegación (Plan de Estudios, Egreso y Campo Laboral, Registro e Inscripciones) |
| Listas ordenadas / desordenadas | Ruta de ingreso y requisitos (`<ol>`), perfil de ingreso y compromiso social (`<ul>`) |
| Tablas | Materias por semestre, áreas de formación, costos, campo laboral |
| Enlaces a sonido y video | Spot MP3 y video MP4 (Inicio, Plan de estudios y pie de página) |
| Imágenes con enlace a redes oficiales | Íconos de Facebook, Instagram, X, YouTube, TikTok y sitio BUAP en el pie |

📸 Capturas de cada página.

## 5. Formularios y autenticación
- Inicio de sesión y registro de cuenta (contraseñas cifradas con `password_hash`).
- Formulario de satisfacción: 10 preguntas × 3 opciones (`encuesta.php`).
- Apartado de campo laboral y compromiso social con datos del INEGI 2020.

📸 Capturas: login, ficha registrada, encuesta y resultados.

## 6. Base de datos y CRUD
Tablas: `usuarios`, `materias`, `aspirantes`, `encuestas`.

| Operación | Captura |
|---|---|
| Insertar ficha / materia | 📸 |
| Consultar (lista con buscador) | 📸 |
| Actualizar | 📸 |
| Eliminar | 📸 |

## 7. Servidor en la nube
- Plataforma: InfinityFree · Sistema: Linux · Servidor web: Apache · Intérprete: PHP · BD: MySQL/MariaDB.
- Seguridad: certificado SSL (HTTPS), contraseñas cifradas, consultas preparadas (anti inyección SQL), token CSRF, carpetas `includes/` y `database/` bloqueadas con `.htaccess`.

📸 Captura: panel de InfinityFree con la cuenta activa y el dominio.
📸 Captura: certificado SSL instalado.

## 8. Migración de la base de datos
📸 Captura: exportación en phpMyAdmin local (archivo `.sql`).
📸 Captura: importación en phpMyAdmin de la nube con las 4 tablas.

## 9. Prueba final
📸 Captura: **Panel de control → Servidor y base de datos** mostrando «Conectado», host remoto, dominio y HTTPS.
📸 Captura: sitio abierto desde el celular / app instalada.

## Conclusiones
_____________________________________________________________________
