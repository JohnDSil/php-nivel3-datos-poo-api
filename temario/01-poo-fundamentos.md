# 01. Programación Orientada a Objetos: Fundamentos

La Programación Orientada a Objetos (POO) permite agrupar datos (atributos o propiedades) y comportamientos (métodos o funciones) en entidades reutilizables llamadas clases.

## Clases, Atributos y el Constructor

El constructor `__construct()` es un método mágico que PHP ejecuta automáticamente cada vez que se crea una instancia (`new`) de la clase:

```php
<?php
class Servidor {
    // Modificadores de acceso: public, private, protected
    private string $hostname;
    private string $ip;
    private int $ramGb;

    // Constructor para inicializar el objeto
    public function __construct(string $hostname, string $ip, int $ramGb) {
        $this->hostname = $hostname;
        $this->ip       = $ip;
        $this->ramGb    = $ramGb;
    }

    // Método público (Getter)
    public function getDetalles(): string {
        return "Host: {$this->hostname} | IP: {$this->ip} | RAM: {$this->ramGb}GB";
    }
}

// Instanciación del objeto
$srv01 = new Servidor("web-prod", "192.168.10.20", 32);
echo $srv01->getDetalles();
?>
```

## Encapsulamiento y Visibilidad

- `public`: El miembro puede ser accedido y modificado desde cualquier parte del código.
- `private`: El miembro solo puede ser utilizado dentro de la propia clase que lo define.
- `protected`: El miembro solo puede ser utilizado dentro de la propia clase y en clases que hereden de ella.
