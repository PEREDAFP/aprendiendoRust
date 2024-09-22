# Clase sobre Structs y Enums en Rust: 20 Ejercicios y Soluciones

En esta sesión, vamos a trabajar con **structs** y **enums** en Rust. Las estructuras (`struct`) nos permiten crear tipos personalizados con campos nombrados, mientras que las enumeraciones (`enum`) son útiles para definir tipos con múltiples variantes posibles. Aquí tienes 20 ejercicios con sus respectivas soluciones y explicaciones.

---

## Ejercicio 1: Definir un Struct Simple
**Instrucción:**
Crea un `struct` llamado `Persona` con los campos `nombre` y `edad`.

```rust
struct Persona {
    nombre: String,
    edad: u8,
}

fn main() {
    let persona = Persona {
        nombre: String::from("Alice"),
        edad: 30,
    };
    println!("Nombre: {}, Edad: {}", persona.nombre, persona.edad);
}
```

### Solución:
Este código crea una estructura `Persona` y un objeto que almacena el nombre y la edad.

**Explicación:**  
Un `struct` en Rust agrupa campos con tipos específicos. En este caso, tenemos un `String` y un entero (`u8`).

---

## Ejercicio 2: Crear y acceder a Struct
**Instrucción:**
Crea una instancia del `struct` `Persona` e imprime sus valores.

```rust
struct Persona {
    nombre: String,
    edad: u8,
}

fn main() {
    let persona = Persona {
        nombre: String::from("Carlos"),
        edad: 25,
    };
    println!("{} tiene {} años", persona.nombre, persona.edad);
}
```

### Solución:
El código imprime `Carlos tiene 25 años`.

**Explicación:**  
Puedes acceder a los campos de una estructura utilizando la sintaxis de punto (`.`).

---

## Ejercicio 3: Definir un Struct con Funciones Asociadas
**Instrucción:**
Añade una función asociada `nueva` que cree una nueva `Persona`.

```rust
struct Persona {
    nombre: String,
    edad: u8,
}

impl Persona {
    fn nueva(nombre: String, edad: u8) -> Persona {
        Persona { nombre, edad }
    }
}

fn main() {
    let persona = Persona::nueva(String::from("Ana"), 28);
    println!("Nombre: {}, Edad: {}", persona.nombre, persona.edad);
}
```

### Solución:
Se usa `Persona::nueva` para crear una nueva instancia de `Persona`.

**Explicación:**  
Las funciones asociadas (`impl`) permiten añadir métodos o funciones que pertenecen al `struct`. `nueva` es un constructor personalizado.

---

## Ejercicio 4: Struct con Método
**Instrucción:**
Añade un método `describir` a `Persona` que devuelva una cadena con la información de la persona.

```rust
struct Persona {
    nombre: String,
    edad: u8,
}

impl Persona {
    fn describir(&self) -> String {
        format!("{} tiene {} años", self.nombre, self.edad)
    }
}

fn main() {
    let persona = Persona {
        nombre: String::from("Luis"),
        edad: 35,
    };
    println!("{}", persona.describir());
}
```

### Solución:
El método `describir` devuelve `"Luis tiene 35 años"`.

**Explicación:**  
Los métodos en un `struct` pueden acceder a los campos utilizando `&self`, que es una referencia a la instancia actual.

---

## Ejercicio 5: Struct con Campo Opcional
**Instrucción:**
Modifica `Persona` para que el campo `email` sea opcional (`Option<String>`).

```rust
struct Persona {
    nombre: String,
    edad: u8,
    email: Option<String>,
}

impl Persona {
    fn describir(&self) -> String {
        match &self.email {
            Some(email) => format!("{} tiene {} años y su email es {}", self.nombre, self.edad, email),
            None => format!("{} tiene {} años y no tiene email", self.nombre, self.edad),
        }
    }
}

fn main() {
    let persona_con_email = Persona {
        nombre: String::from("Laura"),
        edad: 40,
        email: Some(String::from("laura@example.com")),
    };

    let persona_sin_email = Persona {
        nombre: String::from("Miguel"),
        edad: 22,
        email: None,
    };

    println!("{}", persona_con_email.describir());
    println!("{}", persona_sin_email.describir());
}
```

### Solución:
El código maneja correctamente si la persona tiene o no un email.

**Explicación:**  
`Option<T>` es un enum que se utiliza para valores opcionales, que pueden ser `Some(valor)` o `None`.

---

## Ejercicio 6: Definir un Enum Básico
**Instrucción:**
Crea un `enum` llamado `Estado` con las variantes `Activo` y `Inactivo`.

```rust
enum Estado {
    Activo,
    Inactivo,
}

fn main() {
    let estado_actual = Estado::Activo;
    
    match estado_actual {
        Estado::Activo => println!("El estado es Activo"),
        Estado::Inactivo => println!("El estado es Inactivo"),
    }
}
```

### Solución:
El código imprime `El estado es Activo`.

**Explicación:**  
Un `enum` en Rust permite definir un tipo que puede tener varias variantes. Usamos `match` para comparar el estado actual con sus variantes.

---

## Ejercicio 7: Enum con Valores Asociados
**Instrucción:**
Crea un `enum` `Direccion` que tenga variantes `Norte`, `Sur`, `Este` y `Oeste`, y añádeles valores numéricos asociados.

```rust
enum Direccion {
    Norte(i32),
    Sur(i32),
    Este(i32),
    Oeste(i32),
}

fn main() {
    let dir = Direccion::Norte(5);

    match dir {
        Direccion::Norte(dist) => println!("Ir al Norte {} km", dist),
        Direccion::Sur(dist) => println!("Ir al Sur {} km", dist),
        Direccion::Este(dist) => println!("Ir al Este {} km", dist),
        Direccion::Oeste(dist) => println!("Ir al Oeste {} km", dist),
    }
}
```

### Solución:
El código imprime `Ir al Norte 5 km`.

**Explicación:**  
Las variantes de un `enum` pueden tener valores asociados, lo que permite almacenar datos adicionales en cada variante.

---

## Ejercicio 8: Enum con Métodos
**Instrucción:**
Añade un método `describir` a `Direccion` que devuelva una descripción de la dirección y distancia.

```rust
enum Direccion {
    Norte(i32),
    Sur(i32),
    Este(i32),
    Oeste(i32),
}

impl Direccion {
    fn describir(&self) -> String {
        match self {
            Direccion::Norte(dist) => format!("Ir al Norte {} km", dist),
            Direccion::Sur(dist) => format!("Ir al Sur {} km", dist),
            Direccion::Este(dist) => format!("Ir al Este {} km", dist),
            Direccion::Oeste(dist) => format!("Ir al Oeste {} km", dist),
        }
    }
}

fn main() {
    let dir = Direccion::Este(10);
    println!("{}", dir.describir());
}
```

### Solución:
El método `describir` devuelve `Ir al Este 10 km`.

**Explicación:**  
Los `enum` también pueden tener métodos asociados al igual que los `struct`.

---

## Ejercicio 9: Enum Complejo con Varios Tipos
**Instrucción:**
Crea un `enum` `Mensaje` que tenga variantes para `Texto`, `Imagen` (con una URL) y `Video` (con URL y duración).

```rust
enum Mensaje {
    Texto(String),
    Imagen(String),
    Video { url: String, duracion: u32 },
}

fn main() {
    let msg1 = Mensaje::Texto(String::from("Hola mundo"));
    let msg2 = Mensaje::Imagen(String::from("https://imagen.com/foto.jpg"));
    let msg3 = Mensaje::Video {
        url: String::from("https://video.com/video.mp4"),
        duracion: 120,
    };

    match msg3 {
        Mensaje::Texto(texto) => println!("Mensaje de texto: {}", texto),
        Mensaje::Imagen(url) => println!("Imagen desde: {}", url),
        Mensaje::Video { url, duracion } => println!("Video desde: {} con duración de {} segundos", url, duracion),
    }
}
```

### Solución:
El código imprime la información correcta dependiendo del tipo de mensaje.

**Explicación:**  
Los `enum` pueden contener tanto valores simples como tuplas o structs, lo que permite manejar datos más complejos.

---

## Ejercicio 10: Enum y Option
**Instrucción:**
Crea un `enum` personalizado que funcione como una versión simplificada de `Option`.

```rust
enum MiOption<T> {
    Algo(T),
    Nada,
}

fn main() {
    let valor = MiOption::Algo(42);

    match valor {
        MiOption::Algo(x) => println!("Tenemos algo: {}", x),
        MiOption::Nada => println!("No tenemos nada"),
    }
}
```

### Solución:
El código imprime `Tenemos algo: 42`.

**Explicación:**  
El `enum` genérico

 `MiOption` es similar a `Option<T>`, y permite almacenar un valor o manejar un caso vacío (`Nada`).

---

## Ejercicio 11: Usar Enum para Diferenciar Tipos de Pago
**Instrucción:**
Crea un `enum` llamado `MetodoPago` con variantes para `Efectivo`, `Tarjeta`, y `Transferencia`.

```rust
enum MetodoPago {
    Efectivo(f64),
    Tarjeta(String),
    Transferencia { banco: String, monto: f64 },
}

fn main() {
    let pago = MetodoPago::Transferencia {
        banco: String::from("Banco Central"),
        monto: 1000.0,
    };

    match pago {
        MetodoPago::Efectivo(cantidad) => println!("Pago en efectivo: ${}", cantidad),
        MetodoPago::Tarjeta(numero) => println!("Pago con tarjeta: {}", numero),
        MetodoPago::Transferencia { banco, monto } => println!("Transferencia desde {} por ${}", banco, monto),
    }
}
```

### Solución:
El código imprime la información correcta sobre el método de pago utilizado.

**Explicación:**  
El uso de un `enum` permite representar diferentes tipos de pagos de manera flexible y estructurada.

---

## Ejercicio 12: Implementar Métodos en un Enum con Variantes Complejas
**Instrucción:**
Añade un método `detalles` a `MetodoPago` para devolver una cadena con los detalles del pago.

```rust
enum MetodoPago {
    Efectivo(f64),
    Tarjeta(String),
    Transferencia { banco: String, monto: f64 },
}

impl MetodoPago {
    fn detalles(&self) -> String {
        match self {
            MetodoPago::Efectivo(cantidad) => format!("Pago en efectivo de ${}", cantidad),
            MetodoPago::Tarjeta(numero) => format!("Pago con tarjeta: {}", numero),
            MetodoPago::Transferencia { banco, monto } => format!("Transferencia desde {} por ${}", banco, monto),
        }
    }
}

fn main() {
    let pago = MetodoPago::Efectivo(500.0);
    println!("{}", pago.detalles());
}
```

### Solución:
El método `detalles` devuelve una descripción de la transacción.

**Explicación:**  
Los métodos en un `enum` permiten encapsular la lógica para manejar las distintas variantes.

---

## Ejercicio 13: Struct con Referencia a Enum
**Instrucción:**
Crea un `struct` llamado `Transaccion` que contenga un campo `MetodoPago`.

```rust
enum MetodoPago {
    Efectivo(f64),
    Tarjeta(String),
    Transferencia { banco: String, monto: f64 },
}

struct Transaccion {
    id: u32,
    metodo: MetodoPago,
}

fn main() {
    let transaccion = Transaccion {
        id: 1,
        metodo: MetodoPago::Efectivo(250.0),
    };

    match transaccion.metodo {
        MetodoPago::Efectivo(cantidad) => println!("Transacción {}: Pago en efectivo de ${}", transaccion.id, cantidad),
        _ => println!("Otro método de pago"),
    }
}
```

### Solución:
El código imprime `Transacción 1: Pago en efectivo de $250`.

**Explicación:**  
Puedes combinar `struct` y `enum` para crear tipos de datos más complejos y manejarlos eficientemente.

---

## Ejercicio 14: Enum con Datos Anidados
**Instrucción:**
Crea un `enum` `Operacion` que contenga `Suma`, `Resta`, y `Multiplicacion` como variantes, cada una con dos números asociados.

```rust
enum Operacion {
    Suma(i32, i32),
    Resta(i32, i32),
    Multiplicacion(i32, i32),
}

impl Operacion {
    fn calcular(&self) -> i32 {
        match self {
            Operacion::Suma(a, b) => a + b,
            Operacion::Resta(a, b) => a - b,
            Operacion::Multiplicacion(a, b) => a * b,
        }
    }
}

fn main() {
    let operacion = Operacion::Suma(10, 20);
    println!("Resultado: {}", operacion.calcular());
}
```

### Solución:
El código imprime `Resultado: 30`.

**Explicación:**  
Los `enum` pueden contener varias operaciones con diferentes comportamientos, y los métodos permiten calcular el resultado basado en la variante.

---

## Ejercicio 15: Implementar un Enum Genérico
**Instrucción:**
Crea un `enum` genérico `Resultado` que represente `Exito` o `Error` con tipos genéricos.

```rust
enum Resultado<T, E> {
    Exito(T),
    Error(E),
}

fn main() {
    let resultado: Resultado<i32, &str> = Resultado::Exito(100);

    match resultado {
        Resultado::Exito(valor) => println!("Éxito con valor: {}", valor),
        Resultado::Error(mensaje) => println!("Error: {}", mensaje),
    }
}
```

### Solución:
El código imprime `Éxito con valor: 100`.

**Explicación:**  
Los `enum` genéricos permiten manejar éxito o error de manera flexible y reutilizable con diferentes tipos.

---

## Ejercicio 16: Usar Enums con Datos Dinámicos
**Instrucción:**
Modifica el enum `Mensaje` para que incluya una variante `Reaccion` que contenga una función closure como valor.

```rust
enum Mensaje {
    Texto(String),
    Reaccion(Box<dyn Fn()>),
}

fn main() {
    let mensaje = Mensaje::Reaccion(Box::new(|| println!("Reaccionando al mensaje")));

    match mensaje {
        Mensaje::Texto(texto) => println!("Mensaje de texto: {}", texto),
        Mensaje::Reaccion(accion) => accion(),
    }
}
```

### Solución:
El código ejecuta la closure y muestra `Reaccionando al mensaje`.

**Explicación:**  
Puedes almacenar funciones dinámicas o closures en un `enum` usando `Box<dyn Fn()>` para ejecutar lógica específica al momento de hacer `match`.

---

## Ejercicio 17: Enum con Valores Predeterminados
**Instrucción:**
Crea un `enum` `Color` que tenga valores predeterminados para `Rojo`, `Verde`, y `Azul`.

```rust
enum Color {
    Rojo,
    Verde,
    Azul,
}

impl Color {
    fn valor_rgb(&self) -> (u8, u8, u8) {
        match self {
            Color::Rojo => (255, 0, 0),
            Color::Verde => (0, 255, 0),
            Color::Azul => (0, 0, 255),
        }
    }
}

fn main() {
    let color = Color::Verde;
    let (r, g, b) = color.valor_rgb();
    println!("Color verde en RGB: ({}, {}, {})", r, g, b);
}
```

### Solución:
El código imprime `Color verde en RGB: (0, 255, 0)`.

**Explicación:**  
Puedes usar un `enum` para representar colores y asociarles valores RGB utilizando un método.

---

## Ejercicio 18: Implementar el Trait `Display` para un Enum
**Instrucción:**
Implementa el trait `Display` para el enum `Operacion`.

```rust
use std::fmt;

enum Operacion {
    Suma(i32, i32),
    Resta(i32, i32),
}

impl fmt::Display for Operacion {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        match self {
            Operacion::Suma(a, b) => write!(f, "Suma: {} + {}", a, b),
            Operacion::Resta(a, b) => write!(f, "Resta: {} - {}", a, b),
        }
    }
}

fn main() {
    let operacion = Operacion::Suma(5, 10);
    println!("{}", operacion);
}
```

### Solución:
El código imprime `Suma: 5 + 10`.

**Explicación:**  
Al implementar el trait `Display`, puedes controlar cómo se imprimen las variantes de un `enum`.

---

## Ejercicio 19: Desestructurar un Struct con Enum Interno
**Instrucción:**
Crea un `struct` que tenga un campo `estado` que sea un `enum`.

```rust
enum Estado {
    Encendido,
    Apagado,
}

struct Dispositivo {
    nombre: String,
    estado: Estado,
}

fn main() {
    let dispositivo = Dispositivo {
        nombre: String::from("Lámpara"),
        estado: Estado::Encendido,
    };

    match dispositivo.estado {
        Estado::Encendido => println!("{} está encendido", dispositivo.nombre),
        Estado::Apagado => println!("{} está apagado", dispositivo.nombre),
    }
}
```

### Solución:
El código imprime `Lámpara está encendido`.

**Explicación:**  
Un `struct` puede contener un `enum` como campo y desestructurarse utilizando `match` para acceder a sus variantes.

---

## Ejercicio 20: Usar Enum con Resultados
**Instrucción:**
Crea una función que devuelva un `Result` usando un `enum` para representar el éxito o error.

```rust
enum ErrorDivision {
    DivisionPor

Cero,
}

fn dividir(a: i32, b: i32) -> Result<i32, ErrorDivision> {
    if b == 0 {
        Err(ErrorDivision::DivisionPorCero)
    } else {
        Ok(a / b)
    }
}

fn main() {
    let resultado = dividir(10, 2);

    match resultado {
        Ok(valor) => println!("Resultado: {}", valor),
        Err(ErrorDivision::DivisionPorCero) => println!("Error: División por cero"),
    }
}
```

### Solución:
El código imprime `Resultado: 5`.

**Explicación:**  
El uso de `Result` junto con un `enum` permite manejar errores de forma segura y estructurada.

---
