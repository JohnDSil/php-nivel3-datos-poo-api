# 06. Servicios Web y APIs REST con JSON

Una API REST intercambia información estructurada (generalmente en formato JSON) entre clientes (aplicaciones móviles, frontends en JavaScript u otros servidores) y el backend.

## 1. Envío de Respuestas en JSON

```php
<?php
header("Content-Type: application/json; charset=UTF-8");
header("Access-Control-Allow-Origin: *"); // Permite peticiones CORS si aplica

$respuesta = [
    "status" => "success",
    "timestamp" => time(),
    "servidores" => [
        ["id" => 1, "nodo" => "edge-01", "estado" => "activo"],
        ["id" => 2, "nodo" => "edge-02", "estado" => "mantenimiento"]
    ]
];

// Conversión de array PHP a formato JSON
echo json_encode($respuesta, JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
?>
```

## 2. Recepción de Peticiones JSON (`php://input`)

Cuando un cliente envía datos en formato JSON mediante un método HTTP POST o PUT, los datos no se guardan en el array `$_POST`. Se deben leer directamente del flujo de entrada del servidor:

```php
<?php
header("Content-Type: application/json; charset=UTF-8");

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Leer el cuerpo crudo de la petición HTTP
    $cuerpoPeticion = file_get_contents("php://input");

    // Decodificar el JSON a array asociativo
    $datos = json_decode($cuerpoPeticion, true);

    if (json_last_error() !== JSON_ERROR_NONE || !isset($datos['nombre_servicio'])) {
        http_response_code(400); // 400 Bad Request
        echo json_encode(["error" => "Estructura JSON inválida o datos incompletos."]);
        exit;
    }

    // Procesar datos...
    http_response_code(201); // 201 Created
    echo json_encode([
        "mensaje" => "Servicio {$datos['nombre_servicio']} registrado correctamente.",
        "codigo"  => 201
    ]);
}
?>
```
