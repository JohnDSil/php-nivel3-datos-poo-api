# PHP - Nivel 3: Bases de Datos con PDO, POO y APIs REST
> Documentación basada en los módulos de Clases/Objetos, Extensiones de Bases de Datos y Servicios Web de [php.net/manual/es/](https://www.php.net/manual/es/)

Guía avanzada orientada al despliegue de aplicaciones web robustas, persistencia relacional con MariaDB/MySQL mediante sentencias preparadas y consumo de servicios modernos para 2º de ASIR.

---

## 📑 Índice de Temas

| Nº | Tema | Archivo | Conceptos Clave |
| :---: | :--- | :--- | :--- |
| **01** | Programación Orientada a Objetos: Fundamentos | [`01-poo-fundamentos.md`](temario/01-poo-fundamentos.md) | Clases, objetos, constructor (`__construct`), encapsulamiento (`public`, `private`, `protected`) |
| **02** | POO Avanzada: Herencia y Espacios de Nombres | [`02-poo-herencia-namespaces.md`](temario/02-poo-herencia-namespaces.md) | Herencia (`extends`), palabras clave `static`, `self`, `parent` y `namespace` |
| **03** | Conexión a Bases de Datos con PDO | [`03-pdo-conexion-dsn.md`](temario/03-pdo-conexion-dsn.md) | DSN de conexión, opciones de configuración (`ATTR_ERRMODE`), captura de `PDOException` |
| **04** | Consultas Seguras y Sentencias Preparadas | [`04-pdo-sentencias-preparadas.md`](temario/04-pdo-sentencias-preparadas.md) | Prevención total de Inyección SQL, marcadores con nombre (`:param`), `execute()` y `fetchAll()` |
| **05** | Transacciones ACID en PDO | [`05-pdo-transacciones.md`](temario/05-pdo-transacciones.md) | Integridad de datos, `beginTransaction()`, `commit()` y `rollBack()` |
| **06** | Servicios Web y APIs REST con JSON | [`06-json-y-apis-rest.md`](temario/06-json-y-apis-rest.md) | `json_encode()`, `json_decode()`, lectura del flujo `php://input` y respuestas REST |
| **07** | Gestión de Entorno y Dependencias con Composer | [`07-composer-y-variables-entorno.md`](temario/07-composer-y-variables-entorno.md) | `composer.json`, autoloading PSR-4 y variables de configuración protegidas en `.env` |

---

## 🛠️ Requisitos de Entorno
- Base de datos relacional **MariaDB 10.x** o **MySQL 8.0** activa.
- Extensión `php-mysql` y driver `pdo_mysql` habilitados.
- Gestor de paquetes **Composer** instalado en el sistema (`sudo apt install composer`).
