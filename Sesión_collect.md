# Lección: Iterables y `collect` en Rust

## 1. Introducción a los Iterables

En Rust, un iterable es cualquier tipo que implementa el trait `IntoIterator`. Esto incluye colecciones como vectores, arrays, HashMaps, y más. Los iterables nos permiten procesar elementos de una colección de manera eficiente.

## 2. El Trait `Iterator`

El trait `Iterator` es fundamental para trabajar con iterables en Rust. Proporciona muchos métodos útiles como `map`, `filter`, `fold`, y por supuesto, `collect`.

```rust
let numbers = vec![1, 2, 3, 4, 5];
let squares: Vec<i32> = numbers.iter().map(|&x| x * x).collect();
println!("{:?}", squares); // [1, 4, 9, 16, 25]
```

## 3. El Método `collect`

`collect` es un método poderoso que consume un iterador y reúne los elementos en una nueva colección. Es increíblemente versátil y puede crear diferentes tipos de colecciones.

### 3.1 Uso Básico de `collect`

```rust
let vec = vec![1, 2, 3, 4, 5];
let doubled: Vec<i32> = vec.iter().map(|&x| x * 2).collect();
println!("{:?}", doubled); // [2, 4, 6, 8, 10]
```

### 3.2 Especificación de Tipo

A menudo, necesitamos especificar el tipo de colección que queremos crear con `collect`:

```rust
let vec = vec![1, 2, 3, 4, 5];
let set: std::collections::HashSet<_> = vec.into_iter().collect();
println!("{:?}", set); // HashSet { 5, 2, 3, 4, 1 }
```

### 3.3 El Turbofish `::<>`

Podemos usar la sintaxis "turbofish" para especificar el tipo sin una anotación de tipo completa:

```rust
let vec = vec![1, 2, 3, 4, 5];
let doubled = vec.iter().map(|&x| x * 2).collect::<Vec<i32>>();
```

### 3.4 Creando Estructuras de Datos Complejas

`collect` puede crear estructuras de datos más complejas, como un `HashMap`:

```rust
use std::collections::HashMap;

let vec = vec![(1, "one"), (2, "two"), (3, "three")];
let map: HashMap<_, _> = vec.into_iter().collect();
println!("{:?}", map); // {1: "one", 2: "two", 3: "three"}
```

## 4. Ejemplos Prácticos

### 4.1 Filtrado y Colección

```rust
let numbers = vec![1, 2, 3, 4, 5, 6];
let evens: Vec<i32> = numbers.into_iter().filter(|&x| x % 2 == 0).collect();
println!("{:?}", evens); // [2, 4, 6]
```

### 4.2 Transformación de Strings

```rust
let words = vec!["hello", "world", "rust", "programming"];
let caps: Vec<String> = words.iter().map(|s| s.to_uppercase()).collect();
println!("{:?}", caps); // ["HELLO", "WORLD", "RUST", "PROGRAMMING"]
```

### 4.3 Agrupación

```rust
use std::collections::HashMap;

let items = vec![("A", 1), ("B", 2), ("A", 3), ("C", 4), ("B", 5)];
let grouped: HashMap<&str, Vec<i32>> = items
    .into_iter()
    .fold(HashMap::new(), |mut acc, (key, val)| {
        acc.entry(key).or_insert_with(Vec::new).push(val);
        acc
    });
println!("{:?}", grouped); // {"A": [1, 3], "B": [2, 5], "C": [4]}
```

## 5. Ejercicios

1. Crea una función que tome un vector de strings y devuelva un vector con solo las palabras que comienzan con una vocal.

2. Escribe un programa que lea una lista de números del usuario y luego use `collect` para crear un `HashSet` con los números únicos.

3. Implementa una función que tome un vector de enteros y devuelva un `HashMap` donde las claves son los números y los valores son la frecuencia con la que aparecen en el vector.

## 6. Conclusión

El método `collect` es una herramienta poderosa en el ecosistema de iteradores de Rust. Te permite transformar fácilmente iteradores en colecciones concretas, lo que es crucial para el procesamiento eficiente de datos. Practicar con `collect` y otros métodos de iteradores te ayudará a escribir código Rust más idiomático y eficiente.

## 7. Recursos Adicionales

- [Documentación oficial de Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html)
- [Rust by Example: Iterators](https://doc.rust-lang.org/rust-by-example/trait/iter.html)
- [The Rust Programming Language: Processing a Series of Items with Iterators](https://doc.rust-lang.org/book/ch13-02-iterators.html)