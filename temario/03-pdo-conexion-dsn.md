# 03. Conexión a Bases de Datos con PDO

**PDO (PHP Data Objects)** es una capa de abstracción orientada a objetos que unifica el acceso a diferentes motores de bases de datos (MySQL, PostgreSQL, SQLite, etc.).

## Instalación del driver en Linux
```bash
sudo apt install php-mysql -y
sudo systemctl restart apache2
```

## Cadena DSN y Conexión Segura

La conexión se establece instanciando un objeto `PDO` pasándole la cadena de origen de datos (*Data Source Name* - DSN):

```php
<?php
$host    = '127.0.0.1';
$db      = 'empresa_asir';$user    = 'admin_asir';
$pass    = 'PasswordSegura2026!';$charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";

$opciones = [
    // Lanza una excepción en lugar de emitir un simple warning ante errores SQL
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    // Devuelve los resultados como arrays asociativos por defecto
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    // Desactiva la emulación interna para forzar sentencias preparadas nativas en el motor
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $conexion = new PDO($dsn,$user, $pass,$opciones);
    echo "Conexión a MariaDB establecida correctamente.";
} catch (PDOException $e) {
    // Se captura el error técnico sin exponer contraseñas en pantalla
    error_log("Error de conexión SQL: " . $e->getMessage());
    die("Error crítico: No fue posible conectar con la base de datos.");
}
?>
```
