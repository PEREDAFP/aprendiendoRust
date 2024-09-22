# Lección: Entrada y Salida en Rust

## 1. Introducción

En esta lección, aprenderemos cómo realizar operaciones de entrada y salida en Rust, específicamente cómo pedir datos por pantalla y mostrar mensajes.

## 2. Mostrar mensajes por pantalla

Para mostrar mensajes por pantalla en Rust, utilizamos la macro `println!()`. Esta macro imprime texto en la consola y añade automáticamente un salto de línea al final.

Ejemplo:

```rust
fn main() {
    println!("Hola, mundo!");
}
```

También podemos usar la macro `print!()` si no queremos un salto de línea al final:

```rust
fn main() {
    print!("Esto no tiene salto de línea");
    print!(" y esto está en la misma línea.");
}
```

## 3. Pedir datos por pantalla

Para pedir datos por pantalla, necesitamos usar la biblioteca estándar `std::io`. Aquí hay un proceso paso a paso:

1. Importar la biblioteca necesaria:
   ```rust
   use std::io;
   ```

2. Crear una variable mutable para almacenar la entrada:
   ```rust
   let mut input = String::new();
   ```

3. Usar `io::stdin().read_line(&mut input)` para leer la entrada:
   ```rust
   io::stdin().read_line(&mut input).expect("Error al leer la línea");
   ```

4. Procesar la entrada según sea necesario.

Ejemplo completo:

```rust
use std::io;

fn main() {
    println!("Por favor, ingrese su nombre:");
    
    let mut nombre = String::new();
    
    io::stdin()
        .read_line(&mut nombre)
        .expect("Error al leer la línea");
    
    println!("Hola, {}!", nombre.trim());
}
```

## 4. Ejercicios

Aquí tienes 20 ejercicios para practicar la entrada y salida en Rust, junto con sus soluciones:

1. Escribe un programa que pida al usuario su nombre y lo salude.

2. Crea un programa que pida dos números y muestre su suma.

3. Haz un programa que pida la edad del usuario y diga si es mayor de edad.

4. Escribe un programa que pida un número y muestre su tabla de multiplicar del 1 al 10.

5. Crea un programa que pida una temperatura en Celsius y la convierta a Fahrenheit.

6. Haz un programa que pida el radio de un círculo y muestre su área.

7. Escribe un programa que pida un año y diga si es bisiesto o no.

8. Crea un programa que pida una palabra y diga si es un palíndromo.

9. Haz un programa que pida tres números y muestre el mayor de ellos.

10. Escribe un programa que pida un número y diga si es par o impar.

11. Crea un programa que pida una frase y cuente cuántas vocales tiene.

12. Haz un programa que pida un número y muestre la suma de sus dígitos.

13. Escribe un programa que pida una cadena y la muestre al revés.

14. Crea un programa que pida el nombre y la edad de tres personas y muestre la edad promedio.

15. Haz un programa que pida un número y muestre todos sus divisores.

16. Escribe un programa que pida una base y un exponente, y calcule la potencia.

17. Crea un programa que pida una cadena y cuente cuántas palabras tiene.

18. Haz un programa que pida un número y muestre si es primo o no.

19. Escribe un programa que pida una hora en formato 24h y la convierta a formato 12h.

20. Crea un programa que pida una cadena y la convierta a "leet speak" (reemplaza algunas letras por números).

## 5. Soluciones

1. Saludo personalizado:
```rust
use std::io;

fn main() {
    println!("Por favor, ingresa tu nombre:");
    let mut nombre = String::new();
    io::stdin().read_line(&mut nombre).expect("Error al leer el nombre");
    println!("Hola, {}!", nombre.trim());
}
```

2. Suma de dos números:
```rust
use std::io;

fn main() {
    println!("Ingresa el primer número:");
    let mut num1 = String::new();
    io::stdin().read_line(&mut num1).expect("Error al leer el número");
    let num1: i32 = num1.trim().parse().expect("Por favor, ingresa un número válido");

    println!("Ingresa el segundo número:");
    let mut num2 = String::new();
    io::stdin().read_line(&mut num2).expect("Error al leer el número");
    let num2: i32 = num2.trim().parse().expect("Por favor, ingresa un número válido");

    println!("La suma es: {}", num1 + num2);
}
```

3. Verificar mayoría de edad:
```rust
use std::io;

fn main() {
    println!("Por favor, ingresa tu edad:");
    let mut edad = String::new();
    io::stdin().read_line(&mut edad).expect("Error al leer la edad");
    let edad: u32 = edad.trim().parse().expect("Por favor, ingresa un número válido");

    if edad >= 18 {
        println!("Eres mayor de edad");
    } else {
        println!("Eres menor de edad");
    }
}
```

4. Tabla de multiplicar:
```rust
use std::io;

fn main() {
    println!("Ingresa un número para ver su tabla de multiplicar:");
    let mut num = String::new();
    io::stdin().read_line(&mut num).expect("Error al leer el número");
    let num: i32 = num.trim().parse().expect("Por favor, ingresa un número válido");

    for i in 1..=10 {
        println!("{} x {} = {}", num, i, num * i);
    }
}
```

5. Conversor de Celsius a Fahrenheit:
```rust
use std::io;

fn main() {
    println!("Ingresa la temperatura en Celsius:");
    let mut celsius = String::new();
    io::stdin().read_line(&mut celsius).expect("Error al leer la temperatura");
    let celsius: f64 = celsius.trim().parse().expect("Por favor, ingresa un número válido");

    let fahrenheit = (celsius * 9.0 / 5.0) + 32.0;
    println!("{}°C es igual a {}°F", celsius, fahrenheit);
}
```

6. Área de un círculo:
```rust
use std::io;
use std::f64::consts::PI;

fn main() {
    println!("Ingresa el radio del círculo:");
    let mut radio = String::new();
    io::stdin().read_line(&mut radio).expect("Error al leer el radio");
    let radio: f64 = radio.trim().parse().expect("Por favor, ingresa un número válido");

    let area = PI * radio * radio;
    println!("El área del círculo es: {:.2}", area);
}
```

7. Año bisiesto:
```rust
use std::io;

fn main() {
    println!("Ingresa un año:");
    let mut año = String::new();
    io::stdin().read_line(&mut año).expect("Error al leer el año");
    let año: u32 = año.trim().parse().expect("Por favor, ingresa un año válido");

    if (año % 4 == 0 && año % 100 != 0) || (año % 400 == 0) {
        println!("{} es un año bisiesto", año);
    } else {
        println!("{} no es un año bisiesto", año);
    }
}
```

8. Verificar palíndromo:
```rust
use std::io;

fn main() {
    println!("Ingresa una palabra:");
    let mut palabra = String::new();
    io::stdin().read_line(&mut palabra).expect("Error al leer la palabra");
    let palabra = palabra.trim().to_lowercase();

    if palabra == palabra.chars().rev().collect::<String>() {
        println!("{} es un palíndromo", palabra);
    } else {
        println!("{} no es un palíndromo", palabra);
    }
}
```

9. Mayor de tres números:
```rust
use std::io;

fn main() {
    let mut numeros = Vec::new();
    
    for i in 1..=3 {
        println!("Ingresa el número {}:", i);
        let mut num = String::new();
        io::stdin().read_line(&mut num).expect("Error al leer el número");
        let num: i32 = num.trim().parse().expect("Por favor, ingresa un número válido");
        numeros.push(num);
    }

    let mayor = numeros.iter().max().unwrap();
    println!("El mayor número es: {}", mayor);
}
```

10. Número par o impar:
```rust
use std::io;

fn main() {
    println!("Ingresa un número:");
    let mut num = String::new();
    io::stdin().read_line(&mut num).expect("Error al leer el número");
    let num: i32 = num.trim().parse().expect("Por favor, ingresa un número válido");

    if num % 2 == 0 {
        println!("{} es par", num);
    } else {
        println!("{} es impar", num);
    }
}
```

11. Contar vocales:
```rust
use std::io;

fn main() {
    println!("Ingresa una frase:");
    let mut frase = String::new();
    io::stdin().read_line(&mut frase).expect("Error al leer la frase");
    let frase = frase.trim().to_lowercase();

    let vocales = "aeiou";
    let count = frase.chars().filter(|c| vocales.contains(*c)).count();

    println!("La frase tiene {} vocales", count);
}
```

12. Suma de dígitos:
```rust
use std::io;

fn main() {
    println!("Ingresa un número:");
    let mut num = String::new();
    io::stdin().read_line(&mut num).expect("Error al leer el número");
    let num: u32 = num.trim().parse().expect("Por favor, ingresa un número válido");

    let suma = num.to_string().chars().map(|d| d.to_digit(10).unwrap()).sum::<u32>();
    println!("La suma de los dígitos es: {}", suma);
}
```

13. Invertir cadena:
```rust
use std::io;

fn main() {
    println!("Ingresa una cadena:");
    let mut cadena = String::new();
    io::stdin().read_line(&mut cadena).expect("Error al leer la cadena");
    let cadena = cadena.trim();

    let invertida: String = cadena.chars().rev().collect();
    println!("La cadena invertida es: {}", invertida);
}
```

14. Promedio de edades:
```rust
use std::io;

fn main() {
    let mut edades = Vec::new();

    for i in 1..=3 {
        println!("Ingresa el nombre de la persona {}:", i);
        let mut nombre = String::new();
        io::stdin().read_line(&mut nombre).expect("Error al leer el nombre");

        println!("Ingresa la edad de {}:", nombre.trim());
        let mut edad = String::new();
        io::stdin().read_line(&mut edad).expect("Error al leer la edad");
        let edad: u32 = edad.trim().parse().expect("Por favor, ingresa una edad válida");

        edades.push(edad);
    }

    let promedio: f64 = edades.iter().sum::<u32>() as f64 / edades.len() as f64;
    println!("La edad promedio es: {:.2}", promedio);
}
```

15. Mostrar divisores:
```rust
use std::io;

fn main() {
    println!("Ingresa un número:");
    let mut num = String::new();
    io::stdin().read_line(&mut num).expect("Error al leer el número");
    let num: u32 = num.trim().parse().expect("Por favor, ingresa un número válido");

    println!("Los divisores de {} son:", num);
    for i in 1..=num {
        if num % i == 0 {
            print!("{} ", i);
        }
    }
}
```

16. Calcular potencia:
```rust
use std::io;

fn main() {
    println!("Ingresa la base:");
    let mut base = String::new();
    io::stdin().read_line(&mut base).expect("Error al leer la base");
    let base: i32 = base.trim().parse().expect("Por favor, ingresa un número válido");

    println!("Ingresa el exponente:");
    let mut exp = String::new();
    io::stdin().read_line(&mut exp).expect("Error al leer el exponente");
    let exp: u32 = exp.trim().parse().expect("Por favor, ingresa un número válido");

    let resultado = base.pow(exp);
    println!("{} elevado a la {} es: {}", base, exp, resultado);
}
```

17. Contar palabras:
```rust
use std::io;

fn main() {
    println!("Ingresa una cadena:");
    let mut cadena = String::new();
    io::stdin().read_line(&mut cadena).expect("Error al leer la cadena");
    let cadena = cadena.trim();

    let palabras = cadena.split_whitespace().count();
    println!("La cadena tiene {} palabras", palabras);
}
```

18. Verificar número primo:
```rust
use std::io;

fn es_primo(n: u32) -> bool {
    if n <= 1 {
        return false;
    }
    for i in 2..=(n as f64).sqrt() as u32 {
        if n % i == 0 {
            return false;
        }
    }
    true
}

fn main() {
    println!("Ingresa un número:");
    let mut num = String::new();
    io::stdin().read_line(&mut num).expect("Error al leer el número");
    let num: u32 = num.trim().parse().expect("Por favor, ingresa un número válido");

    if es_primo(num) {
        println!("{} es primo", num);
    } else {
        println!("{} no es primo", num);
    }
}
```

19. Convertir hora de 24h a 12h:
```rust
fn convert_to_12h(hour: u32, minute: u32) -> (u32, u32, &'static str) {
    let period = if hour >= 12 { "PM" } else { "AM" };
    let hour_12 = match hour {
        0 => 12,
        13..=23 => hour - 12,
        _ => hour,
    };
    (hour_12, minute, period)
}

fn main() {
    println!("Ingresa una hora en formato 24h (HH:MM):");
    
    let mut input = String::new();
    io::stdin().read_line(&mut input).expect("Error al leer la entrada");
    
    let parts: Vec<&str> = input.trim().split(':').collect();
    if parts.len() != 2 {
        println!("Formato incorrecto. Por favor, usa HH:MM");
        return;
    }
    
    let hour: u32 = match parts[0].parse() {
        Ok(h) if h < 24 => h,
        _ => {
            println!("Hora inválida. Debe estar entre 00 y 23");
            return;
        }
    };
    
    let minute: u32 = match parts[1].parse() {
        Ok(m) if m < 60 => m,
        _ => {
            println!("Minutos inválidos. Deben estar entre 00 y 59");
            return;
        }
    };
    
    let (hour_12, minute_12, period) = convert_to_12h(hour, minute);
    
    println!("En formato 12h: {:02}:{:02} {}", hour_12, minute_12, period);
}
```

20. Crea un programa que pida una cadena y la convierta a "leet speak" (reemplaza algunas letras por números).
```rust 
use std::io;

fn to_leet_speak(s: &str) -> String {
    s.chars().map(|c| match c.to_lowercase().next().unwrap() {
        'a' => '4',
        'e' => '3',
        'i' => '1',
        'o' => '0',
        'l' => '1',
        's' => '5',
        't' => '7',
        _ => c
    }).collect()
}

fn main() {
    println!("Ingresa una cadena para convertir a leet speak:");
    
    let mut input = String::new();
    io::stdin().read_line(&mut input).expect("Error al leer la entrada");
    
    let leet = to_leet_speak(input.trim());
    
    println!("En leet speak: {}", leet);
}
```