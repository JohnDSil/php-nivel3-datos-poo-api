# 04. Consultas Seguras y Sentencias Preparadas

La **inyección SQL** ocurre cuando un atacante introduce código SQL dentro de campos de entrada no sanitizados (como el clásico `' OR '1'='1`).

> **Regla de Oro:** En PDO **jamás** se concatenan variables directamente en la consulta SQL con `.`. Se deben usar obligatoriamente **sentencias preparadas (`prepared statements`)**.

## Inserción y Selección con Marcadores con Nombre (`:param`)

```php
<?php
// Suponiendo la conexión establecida en $conexion

// 1. INSERCIÓN DE DATOS (CREATE)
$sqlInsert = "INSERT INTO usuarios (nombre, email, rol) VALUES (:nombre, :email, :rol)";
$stmtInsert = $conexion->prepare($sqlInsert);

$nuevoUsuario = [
    ':nombre' => 'Carlos Silva',
    ':email'  => 'csilva@dominio.local',
    ':rol'    => 'admin'
];

$stmtInsert->execute($nuevoUsuario);
echo "Usuario registrado con ID: " . $conexion->lastInsertId();


// 2. CONSULTA SEGURA CON PARÁMETROS (READ)
$sqlSelect = "SELECT id, nombre, email FROM usuarios WHERE rol = :rolBusqueda";
$stmtSelect = $conexion->prepare($sqlSelect);

// Ejecutar pasando el parámetro
$stmtSelect->execute([':rolBusqueda' => 'admin']);

// Obtener todas las filas coincidentes
$resultados =$stmtSelect->fetchAll();

foreach ($resultados as$usuario) {
    echo "ID: " . $usuario['id'] . " - Nombre: " . htmlspecialchars($usuario['nombre']) . "<br>";
}
?>
```
