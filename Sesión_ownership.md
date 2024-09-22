# Sesión de Ownership en Rust: 20 Actividades y Soluciones

Bienvenido a la sesión sobre **ownership** en Rust. El concepto de propiedad (ownership) es fundamental en Rust para gestionar la memoria de manera eficiente y evitar errores comunes como el uso de memoria no válida. En esta sesión, trabajaremos con 20 actividades que te ayudarán a comprender este concepto clave.

## Actividad 1: Propiedad básica
**Instrucción:**
Crea una variable de tipo `String` y muévela a otra variable. Intenta usar la primera variable después de moverla.

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    println!("{}", s1); // Error
}
```

### Solución:
Este código causará un error de compilación. En Rust, cuando una variable se mueve a otra, la primera variable ya no es válida.

**Explicación:**  
Cuando `s1` es movido a `s2`, `s1` deja de ser válido. Rust no permite usar variables después de moverlas para evitar errores de acceso a memoria inválida.

---

## Actividad 2: Clonación de variables
**Instrucción:**
Modifica el código anterior para que funcione utilizando la función `clone()`.

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1.clone();
    println!("{}", s1); // Funciona
}
```

### Solución:
Aquí, clonamos el valor de `s1` en `s2`, por lo que ambas variables son válidas y contienen copias del mismo valor.

**Explicación:**  
El método `clone()` crea una copia profunda del valor, lo que permite que ambas variables sean independientes.

---

## Actividad 3: Ownership en funciones
**Instrucción:**
Pasa un `String` a una función y observa el comportamiento del ownership.

```rust
fn main() {
    let s = String::from("hello");
    takes_ownership(s);
    println!("{}", s); // Error
}

fn takes_ownership(some_string: String) {
    println!("{}", some_string);
}
```

### Solución:
Este código fallará porque `s` se ha movido a la función `takes_ownership` y ya no es válido después de la llamada.

**Explicación:**  
Cuando pasas un valor por parámetro, la propiedad se transfiere a la función a menos que el tipo implemente la característica `Copy` o se pase por referencia.

---

## Actividad 4: Pasar por referencia
**Instrucción:**
Modifica el código anterior para pasar el `String` por referencia.

```rust
fn main() {
    let s = String::from("hello");
    takes_ownership(&s);
    println!("{}", s); // Funciona
}

fn takes_ownership(some_string: &String) {
    println!("{}", some_string);
}
```

### Solución:
Pasar el valor por referencia permite que la propiedad permanezca con la variable original.

**Explicación:**  
Al pasar una referencia (`&s`), no se transfiere la propiedad. Esto permite que el valor sea utilizado en la función sin perder acceso a él fuera de ella.

---

## Actividad 5: Mutabilidad y referencias
**Instrucción:**
Crea una función que modifique un `String` pasado por referencia mutable.

```rust
fn main() {
    let mut s = String::from("hello");
    change(&mut s);
    println!("{}", s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world!");
}
```

### Solución:
Este código agrega `", world!"` al final del `String`.

**Explicación:**  
Una referencia mutable (`&mut`) permite modificar el valor subyacente. Solo puedes tener una referencia mutable activa a la vez por razones de seguridad.

---

## Actividad 6: Doble mutabilidad
**Instrucción:**
Intenta crear dos referencias mutables a la misma variable en el mismo alcance.

```rust
fn main() {
    let mut s = String::from("hello");
    let r1 = &mut s;
    let r2 = &mut s; // Error
    println!("{}, {}", r1, r2);
}
```

### Solución:
El compilador arrojará un error porque no puedes tener dos referencias mutables al mismo tiempo.

**Explicación:**  
Rust previene condiciones de carrera y otros errores concurrentes limitando la mutabilidad simultánea.

---

## Actividad 7: Referencias inmutables múltiples
**Instrucción:**
Crea varias referencias inmutables a una variable y accede a ellas.

```rust
fn main() {
    let s = String::from("hello");
    let r1 = &s;
    let r2 = &s;
    println!("{}, {}", r1, r2); // Funciona
}
```

### Solución:
Este código funcionará sin errores, permitiendo múltiples referencias inmutables.

**Explicación:**  
Puedes tener múltiples referencias inmutables, ya que no cambian el valor y no presentan riesgo de condiciones de carrera.

---

## Actividad 8: Combinación de mutable e inmutable
**Instrucción:**
Intenta crear una referencia mutable e inmutable en el mismo bloque.

```rust
fn main() {
    let mut s = String::from("hello");
    let r1 = &s;
    let r2 = &mut s; // Error
    println!("{}, {}", r1, r2);
}
```

### Solución:
Este código causará un error porque no puedes tener una referencia mutable mientras existen referencias inmutables.

**Explicación:**  
Para garantizar la seguridad de datos, Rust no permite tener referencias mutables si ya hay referencias inmutables activas.

---

## Actividad 9: Devolver propiedad
**Instrucción:**
Crea una función que devuelva un `String`, transfiriendo su propiedad al llamador.

```rust
fn main() {
    let s = gives_ownership();
    println!("{}", s);
}

fn gives_ownership() -> String {
    let some_string = String::from("hello");
    some_string
}
```

### Solución:
El `String` es devuelto y su propiedad se transfiere a la variable `s` en `main`.

**Explicación:**  
Las funciones pueden devolver valores y, con ellos, la propiedad del recurso.

---

## Actividad 10: Referencias de retorno
**Instrucción:**
Intenta devolver una referencia a un valor local dentro de una función.

```rust
fn main() {
    let r = dangle();
    println!("{}", r); // Error
}

fn dangle() -> &String {
    let s = String::from("hello");
    &s // Error
}
```

### Solución:
Este código no compila porque el valor al que apunta la referencia es destruido al finalizar la función.

**Explicación:**  
Las referencias no pueden apuntar a datos que ya no existen. Rust evita referencias colgantes.

---

## Actividad 11: Transferencia de propiedad a través de tuplas
**Instrucción:**
Transfiere la propiedad de un `String` utilizando una tupla.

```rust
fn main() {
    let s1 = String::from("hello");
    let (s2, len) = calculate_length(s1);
    println!("{} tiene longitud {}", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len();
    (s, length)
}
```

### Solución:
El `String` es retornado junto con su longitud, preservando la propiedad.

**Explicación:**  
Rust permite retornar múltiples valores usando tuplas, lo que facilita la transferencia de propiedad junto con otros datos.

---

## Actividad 12: Transferencia de propiedad a través de structs
**Instrucción:**
Transfiere la propiedad de un `String` dentro de una `struct`.

```rust
struct User {
    username: String,
}

fn main() {
    let user1 = User {
        username: String::from("Alice"),
    };
    println!("{}", user1.username);
}
```

### Solución:
El `String` se mueve a la `struct` y la propiedad se transfiere a `user1`.

**Explicación:**  
Los valores de tipo `String` se transfieren a una estructura cuando son movidos a uno de sus campos.

---

## Actividad 13: Referencias en structs
**Instrucción:**
Intenta almacenar una referencia en una `struct`.

```rust
struct User<'a> {
    username: &'a str,
}

fn main() {
    let name = "Alice";
    let user1 = User { username: &name };
    println!("{}", user1.username);
}
```

### Solución:
Este código utiliza un tiempo de vida explícito (`'a`) para asegurar que la referencia en la `struct` sea válida.

**Explicación:**  
Rust requiere que especifiques los tiempos de vida (`lifetimes`) cuando almacenas referencias en structs para asegurar que las referencias sean válidas.

---

## Actividad 14: Propiedad en colecciones
**Instrucción:**
Crea un vector de `String` y transfiere la propiedad de sus elementos a través de iteración.

```rust
fn main() {
    let v = vec![String::from("a"), String::from("b"), String::from("c")];
    for s in v {
        println!("{}", s);
    }
    // println!("{:?}", v); // Error


}
```

### Solución:
La propiedad de cada `String` se transfiere durante la iteración, por lo que `v` ya no es válido después del bucle.

**Explicación:**  
Iterar sobre un vector mueve sus valores si no usas referencias, invalidando el vector original.

---

## Actividad 15: Referencias en colecciones
**Instrucción:**
Itera sobre un vector de `String` utilizando referencias.

```rust
fn main() {
    let v = vec![String::from("a"), String::from("b"), String::from("c")];
    for s in &v {
        println!("{}", s);
    }
    println!("{:?}", v);
}
```

### Solución:
Aquí iteramos sobre referencias, por lo que la propiedad del vector no se transfiere y sigue siendo válido después del bucle.

**Explicación:**  
Puedes iterar sobre referencias para evitar mover la propiedad de los elementos de un vector.

---

## Actividad 16: Error de borrow checker
**Instrucción:**
Genera un error intencional con el borrow checker usando referencias mutables.

```rust
fn main() {
    let mut s = String::from("hello");
    let r1 = &s;
    let r2 = &mut s; // Error
    println!("{}", r1);
}
```

### Solución:
El compilador no permitirá mezclar referencias mutables e inmutables simultáneamente.

**Explicación:**  
El borrow checker de Rust asegura que no puedas mezclar referencias mutables con inmutables, evitando condiciones de carrera.

---

## Actividad 17: Propiedad con tipos primitivos
**Instrucción:**
Muestra el comportamiento del ownership con tipos primitivos.

```rust
fn main() {
    let x = 5;
    let y = x;
    println!("{}, {}", x, y);
}
```

### Solución:
El código funcionará porque los tipos primitivos implementan el trait `Copy`.

**Explicación:**  
Los tipos primitivos como enteros implementan `Copy`, lo que significa que cuando se asignan a otra variable, se copia su valor en lugar de mover la propiedad.

---

## Actividad 18: Propiedad de tipos no primitivos
**Instrucción:**
Crea un ejemplo similar con un tipo no primitivo como `String`.

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    println!("{}", s1); // Error
}
```

### Solución:
El código fallará porque `String` no implementa `Copy`, lo que provoca la transferencia de propiedad a `s2`.

**Explicación:**  
Los tipos no primitivos no implementan `Copy` por defecto, ya que involucran memoria dinámica.

---

## Actividad 19: Transferencia de propiedad en una función
**Instrucción:**
Crea una función que tome un `String` y lo devuelva.

```rust
fn main() {
    let s = String::from("hello");
    let s = take_and_return(s);
    println!("{}", s);
}

fn take_and_return(s: String) -> String {
    s
}
```

### Solución:
La propiedad del `String` se transfiere a la función y luego se devuelve al llamador.

**Explicación:**  
Puedes transferir propiedad de variables a funciones y devolverlas, pero esto implica mover el valor de un lugar a otro.

---

## Actividad 20: Propiedad compartida con Rc<T>
**Instrucción:**
Usa `Rc<T>` para compartir propiedad entre múltiples partes de tu código.

```rust
use std::rc::Rc;

fn main() {
    let s = Rc::new(String::from("hello"));
    let s1 = Rc::clone(&s);
    let s2 = Rc::clone(&s);
    println!("{} {}", s1, s2);
}
```

### Solución:
El tipo `Rc<T>` permite compartir propiedad entre múltiples partes del programa sin transferir la propiedad.

**Explicación:**  
`Rc<T>` es un contador de referencias que permite múltiples propietarios de un mismo valor sin transferir la propiedad.

---
