# Sesión de Iteradores y Closures en Rust: 20 Actividades y Soluciones

En esta sesión, vamos a trabajar con **iteradores** y **closures** en Rust. Los iteradores permiten recorrer secuencias de elementos de forma eficiente y los closures nos permiten capturar valores del entorno y crear funciones anónimas. Aquí tienes 20 actividades y sus respectivas soluciones con explicación.

## Actividad 1: Crear un iterador básico
**Instrucción:**
Crea un vector de números y utiliza un iterador para imprimir sus elementos.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    let mut iter = v.iter();
    
    while let Some(val) = iter.next() {
        println!("{}", val);
    }
}
```

### Solución:
El iterador recorre cada valor del vector y los imprime en cada iteración.

**Explicación:**  
El método `iter()` crea un iterador sobre los elementos del vector. El método `next()` devuelve `Some(valor)` mientras haya elementos y `None` cuando el iterador termina.

---

## Actividad 2: Usar un for loop con iteradores
**Instrucción:**
Utiliza un `for` loop para iterar sobre los elementos de un vector.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    for val in v.iter() {
        println!("{}", val);
    }
}
```

### Solución:
El bucle `for` recorre automáticamente el iterador sin necesidad de llamar a `next()` explícitamente.

**Explicación:**  
Rust permite usar un `for` loop directamente sobre cualquier estructura que implemente el trait `IntoIterator`, como los vectores.

---

## Actividad 3: Iterador mutable
**Instrucción:**
Crea un iterador mutable y modifica los elementos del vector dentro del iterador.

```rust
fn main() {
    let mut v = vec![1, 2, 3, 4, 5];
    for val in v.iter_mut() {
        *val += 1;
    }
    println!("{:?}", v);
}
```

### Solución:
El código modifica los elementos del vector aumentando cada valor en 1.

**Explicación:**  
El método `iter_mut()` crea un iterador mutable que permite modificar los elementos mientras se itera sobre ellos.

---

## Actividad 4: Consumir un iterador
**Instrucción:**
Crea un iterador sobre un vector y consume todos sus elementos con el método `for_each`.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    v.into_iter().for_each(|val| println!("{}", val));
}
```

### Solución:
El método `for_each` aplica una closure a cada valor del iterador y consume el iterador completamente.

**Explicación:**  
El método `into_iter()` consume el vector y produce un iterador que transfiere la propiedad de sus elementos. `for_each` aplica la closure a cada elemento hasta que todos sean consumidos.

---

## Actividad 5: Mapear elementos con iteradores
**Instrucción:**
Utiliza el método `map` para transformar los elementos de un vector, multiplicando cada uno por 2.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    let result: Vec<_> = v.iter().map(|x| x * 2).collect();
    println!("{:?}", result);
}
```

### Solución:
El código genera un nuevo vector donde cada elemento es el doble del valor original.

**Explicación:**  
El método `map()` transforma los elementos de un iterador aplicando una closure a cada uno y devuelve un nuevo iterador con los resultados.

---

## Actividad 6: Filtrar elementos con iteradores
**Instrucción:**
Filtra los números pares de un vector utilizando el método `filter`.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5, 6];
    let evens: Vec<_> = v.into_iter().filter(|x| x % 2 == 0).collect();
    println!("{:?}", evens);
}
```

### Solución:
El código devuelve un nuevo vector que solo contiene los números pares del vector original.

**Explicación:**  
El método `filter()` toma una closure que devuelve un booleano y crea un nuevo iterador que solo contiene los elementos para los cuales la closure devuelve `true`.

---

## Actividad 7: Encontrar el primer elemento que cumpla una condición
**Instrucción:**
Usa el método `find` para encontrar el primer número mayor que 4 en un vector.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5, 6];
    let result = v.into_iter().find(|&x| x > 4);
    println!("{:?}", result);
}
```

### Solución:
El código devuelve `Some(5)` porque es el primer número mayor que 4 en el vector.

**Explicación:**  
El método `find()` busca el primer elemento en el iterador que cumpla con la condición especificada por la closure y devuelve `Some(valor)` si lo encuentra, o `None` si no lo encuentra.

---

## Actividad 8: Sumar elementos de un iterador
**Instrucción:**
Suma todos los elementos de un vector utilizando el método `sum`.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    let sum: i32 = v.iter().sum();
    println!("Suma: {}", sum);
}
```

### Solución:
El código suma todos los elementos del vector y devuelve el valor total.

**Explicación:**  
El método `sum()` consume el iterador y devuelve la suma de sus elementos. El tipo del valor de retorno debe ser explícito para evitar ambigüedad.

---

## Actividad 9: Combinación de map y filter
**Instrucción:**
Crea un iterador que filtre los números pares y los multiplique por 2.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5, 6];
    let result: Vec<_> = v.into_iter().filter(|x| x % 2 == 0).map(|x| x * 2).collect();
    println!("{:?}", result);
}
```

### Solución:
El código devuelve `[4, 8, 12]` porque los números pares son filtrados y luego multiplicados por 2.

**Explicación:**  
Puedes encadenar múltiples métodos de iteradores como `filter` y `map` para realizar transformaciones y filtros en secuencia.

---

## Actividad 10: Usar `take` en un iterador
**Instrucción:**
Toma los primeros 3 elementos de un vector usando `take`.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5, 6];
    let result: Vec<_> = v.into_iter().take(3).collect();
    println!("{:?}", result);
}
```

### Solución:
El código devuelve `[1, 2, 3]` porque `take` limita el número de elementos a los primeros 3.

**Explicación:**  
El método `take()` crea un iterador que devuelve solo los primeros `n` elementos y luego detiene la iteración.

---

## Actividad 11: Usar `skip` en un iterador
**Instrucción:**
Omite los primeros 3 elementos de un vector usando `skip`.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5, 6];
    let result: Vec<_> = v.into_iter().skip(3).collect();
    println!("{:?}", result);
}
```

### Solución:
El código devuelve `[4, 5, 6]` porque `skip` omite los primeros 3 elementos del vector.

**Explicación:**  
El método `skip()` crea un iterador que salta los primeros `n` elementos y devuelve el resto.

---

## Actividad 12: Crear una closure básica
**Instrucción:**
Crea una closure que sume dos números y llámala.

```rust
fn main() {
    let sum = |a, b| a + b;
    println!("{}", sum(3, 4));
}
```

### Solución:
La closure suma los dos números y devuelve `7`.

**Explicación:**  
Las closures en Rust son funciones anónimas que pueden capturar valores del entorno y se pueden definir utilizando `|` para los parámetros.

---

## Actividad 13: Usar una closure con tipos explícitos
**Instrucción:**
Escribe una closure que resta dos números e incluye los tipos explícitos.

```rust
fn main() {
    let restar = |a: i32, b: i32| -> i32 { a - b };
    println!("{}", restar(10, 3));
}
```

### Solución:
La closure devuelve `7` al restar `3` de `10`.

**Explicación:**  
Aunque las closures normalmente infieren los tipos de los parámetros, puedes declarar los tipos explícitamente si lo deseas

.

---

## Actividad 14: Capturar variables con closures
**Instrucción:**
Crea una closure que capture una variable del entorno y súmale un número.

```rust
fn main() {
    let x = 10;
    let add_x = |y| y + x;
    println!("{}", add_x(5));
}
```

### Solución:
La closure devuelve `15` al sumar `5` y `10`, que es el valor de `x`.

**Explicación:**  
Las closures pueden capturar variables del entorno, lo que permite su uso dentro de la closure sin necesidad de pasarlas como parámetros.

---

## Actividad 15: Mutar variables capturadas por una closure
**Instrucción:**
Crea una closure que capture una variable mutable y modifícala dentro de la closure.

```rust
fn main() {
    let mut x = 10;
    let mut add_x = |y| {
        x += y;
        x
    };
    println!("{}", add_x(5));
}
```

### Solución:
La closure modifica `x` y devuelve `15`.

**Explicación:**  
Las closures pueden capturar variables mutables si se les permite, y pueden modificar esas variables dentro de su cuerpo.

---

## Actividad 16: Uso de closures con `iterators::filter`
**Instrucción:**
Utiliza una closure con `filter` para seleccionar números mayores a un valor en un vector.

```rust
fn main() {
    let threshold = 3;
    let v = vec![1, 2, 3, 4, 5];
    let result: Vec<_> = v.into_iter().filter(|&x| x > threshold).collect();
    println!("{:?}", result);
}
```

### Solución:
El código devuelve `[4, 5]` porque son los valores mayores que `3`.

**Explicación:**  
Las closures son útiles para operaciones como `filter`, donde puedes capturar valores del entorno, como el umbral `threshold`.

---

## Actividad 17: Usar `move` en closures
**Instrucción:**
Crea una closure que use la palabra clave `move` para transferir la propiedad de una variable capturada.

```rust
fn main() {
    let s = String::from("hello");
    let capture_string = move || println!("{}", s);
    capture_string();
    // println!("{}", s); // Error: `s` ya no es accesible
}
```

### Solución:
El uso de `move` transfiere la propiedad de `s` a la closure, por lo que `s` ya no es accesible después de la closure.

**Explicación:**  
La palabra clave `move` transfiere la propiedad de las variables capturadas a la closure, permitiendo que las use incluso después de que la variable original haya salido del ámbito.

---

## Actividad 18: Ordenar con `sort_by` y closures
**Instrucción:**
Ordena un vector de tuplas `(i32, i32)` según el segundo valor usando `sort_by` y una closure.

```rust
fn main() {
    let mut pairs = vec![(1, 2), (3, 1), (5, 3)];
    pairs.sort_by(|a, b| a.1.cmp(&b.1));
    println!("{:?}", pairs);
}
```

### Solución:
El código ordena el vector en el siguiente orden: `[(3, 1), (1, 2), (5, 3)]`.

**Explicación:**  
`sort_by()` toma una closure que define cómo comparar los elementos. En este caso, se comparan los segundos valores de las tuplas.

---

## Actividad 19: Usar closures con `iterators::fold`
**Instrucción:**
Utiliza `fold` con una closure para sumar los elementos de un vector.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    let sum = v.into_iter().fold(0, |acc, x| acc + x);
    println!("Suma: {}", sum);
}
```

### Solución:
El código suma los elementos del vector y devuelve `15`.

**Explicación:**  
`fold()` toma un valor inicial y una closure que aplica una operación acumulativa sobre los elementos del iterador.

---

## Actividad 20: Comparar dos valores con closures
**Instrucción:**
Crea una closure que compare dos números y devuelva el mayor.

```rust
fn main() {
    let max = |a: i32, b: i32| if a > b { a } else { b };
    println!("El mayor es {}", max(10, 20));
}
```

### Solución:
El código devuelve `20` porque es el mayor de los dos números.

**Explicación:**  
Puedes usar una closure para realizar comparaciones de manera concisa, utilizando la expresión `if-else` dentro de la closure.

---

Estas 20 actividades cubren una amplia gama de conceptos sobre iteradores y closures en Rust, proporcionando una sólida comprensión de cómo usarlos y combinarlos en diferentes situaciones.