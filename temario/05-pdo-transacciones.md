# 05. Transacciones ACID en PDO

Una transacción garantiza que un conjunto de operaciones en la base de datos se ejecuten como una sola unidad indivisible (principio de atomicidad): o se guardan todos los cambios o no se guarda ninguno.

## Caso práctico: Transferencia entre cuentas o altas múltiples

```php
<?php
// Suponiendo la conexión PDO configurada en $conexion

try {
    // 1. Iniciar la transacción (bloquea la confirmación automática)
    $conexion->beginTransaction();

    // 2. Operación A: Restar saldo
    $stmt1 =$conexion->prepare("UPDATE cuentas SET saldo = saldo - :monto WHERE id = :origen");
    $stmt1->execute([':monto' => 500, ':origen' => 1]);

    // 3. Operación B: Sumar saldo
    $stmt2 =$conexion->prepare("UPDATE cuentas SET saldo = saldo + :monto WHERE id = :destino");
    $stmt2->execute([':monto' => 500, ':destino' => 2]);

    // 4. Si ninguna operación falló, confirmamos los cambios de forma definitiva
    $conexion->commit();
    echo "Transferencia completada con éxito.";

} catch (Exception $e) { // 5. Si algo falla, revertimos absolutamente todos los cambios efectuados$conexion->rollBack();
    error_log("Fallo en la transacción: " . $e->getMessage());
    echo "Error en la operación. Los cambios han sido cancelados.";
}
?>
```
