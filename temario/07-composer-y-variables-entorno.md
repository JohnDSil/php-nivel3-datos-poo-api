# 07. Gestión de Entorno y Dependencias con Composer

En proyectos reales de administración y despliegue, jamás se deben guardar credenciales de bases de datos o claves secretas dentro del código fuente subido a repositorios de GitHub.

## 1. Composer y el archivo `composer.json`

Composer es el gestor de dependencias de PHP. Permite instalar bibliotecas de terceros y cargar automáticamente nuestras propias clases (Autoloading PSR-4).

```json
{
    "name": "asir/sistema-gestion",
    "description": "API de gestión de infraestructura",
    "require": {
        "vlucas/phpdotenv": "^5.5"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

Comandos habituales en la terminal de Linux:
```bash
# Instalar las librerías declaradas
composer install

# Regenerar el cargador automático de clases
composer dump-autoload
```

## 2. Variables de Entorno Seguras con `.env`

Cree un archivo llamado `.env` en la raíz (este fichero **debe añadirse a `.gitignore`** para que nunca se suba a GitHub):

```ini
DB_HOST=127.0.0.1
DB_NAME=empresa_prod
DB_USER=root
DB_PASS=ClaveSecretaDeProduccion99!
```

En su código PHP, cargue las variables protegidas usando el cargador automático de Composer (`vendor/autoload.php`):

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

// Inicializar la lectura del fichero .env
$dotenv = Dotenv\Dotenv::createImmutable(__DIR__);$dotenv->load();

// Acceso seguro a las credenciales mediante la variable superglobal $_ENV
$dbHost =$_ENV['DB_HOST'];
$dbPass =$_ENV['DB_PASS'];

echo "Conectando al host seguro: " . $dbHost;
?>
```
