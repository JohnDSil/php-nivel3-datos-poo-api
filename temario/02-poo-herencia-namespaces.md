# 02. POO Avanzada: Herencia y Espacios de Nombres

## Herencia (`extends`)

Permite que una clase especializada reutilice o modifique la lógica de una clase base (padre):

```php
<?php
class EquipoRed {
    protected string $ip;

    public function __construct(string $ip) {
        $this->ip =$ip;
    }

    public function getIp(): string {
        return $this->ip;
    }
}

class Router extends EquipoRed {
    private int $puertos;

    public function __construct(string $ip, int$puertos) {
        parent::__construct($ip); // Llama al constructor de la clase padre
        $this->puertos =$puertos;
    }

    public function getResumen(): string {
        return "Router en " . $this->getIp() . " con " . $this->puertos . " interfaces.";
    }
}

$cisco = new Router("10.0.0.1", 24);
echo $cisco->getResumen();
?>
```

## Espacios de Nombres (`namespace`)

Los *namespaces* resuelven el problema de colisión de nombres cuando se utilizan bibliotecas externas, organizando el código en paquetes jerárquicos:

```php
<?php
namespace Infraestructura\Red;

class Cortafuegos {
    public function aplicarReglas(): void {
        echo "Reglas de iptables aplicadas.";
    }
}
?>
```

Para consumirlo desde otro fichero:

```php
<?php
use Infraestructura\Red\Cortafuegos;

$fw = new Cortafuegos();$fw->aplicarReglas();
?>
```
