# Ejercicios y Soluciones: Iterables en Rust

## Ejercicios

1. Crea un vector con los números del 1 al 10 y usa `collect` para crear otro vector con solo los números pares.

2. Dada una cadena de texto, usa iteradores para contar cuántas veces aparece cada carácter y almacena el resultado en un `HashMap`.

3. Crea una función que tome un vector de strings y devuelva un vector con solo las palabras que tienen más de 5 letras.

4. Usa `zip` para combinar dos vectores de igual longitud en un vector de tuplas.

5. Implementa una función que tome un vector de números y devuelva la suma de los cuadrados de los números pares.

6. Crea un iterador que genere los primeros 10 números de la secuencia de Fibonacci y colecciónalos en un vector.

7. Dado un vector de strings, crea un nuevo vector que contenga la longitud de cada string.

8. Usa `flat_map` para crear un vector que contenga todas las letras individuales de un vector de palabras.

9. Implementa una función que tome un vector de números y devuelva un `HashSet` con los números que aparecen más de una vez.

10. Crea un iterador que genere números primos y usa `take` para obtener los primeros 10 primos en un vector.

11. Dado un vector de tuplas `(String, i32)`, usa `collect` para crear un `HashMap` donde las claves sean las strings y los valores sean los números.

12. Implementa una función que tome un vector de números y devuelva un vector con la suma acumulativa en cada posición.

13. Usa `chain` para combinar dos vectores en un solo iterador y luego filtra para obtener solo los números impares.

14. Crea una función que tome un string y devuelva un vector de tuplas `(char, usize)` donde cada tupla contiene un carácter único y su posición en el string.

15. Implementa el patrón productor-consumidor usando canales e iteradores en Rust.

16. Usa `enumerate` y `collect` para crear un `HashMap` donde las claves sean índices y los valores sean elementos de un vector.

17. Crea un iterador personalizado que genere una secuencia de números triangulares y usa `take_while` para obtener todos los números triangulares menores que 100.

18. Implementa una función que simule una baraja de cartas y use `shuffle` para mezclarlas.

19. Usa `windows` para encontrar la suma máxima de tres números consecutivos en un vector.

20. Implementa un iterador que genere los números de la secuencia de Collatz para un número dado y usa `collect` para almacenarlos en un vector.

## Soluciones

1. Números pares del 1 al 10:
```rust
let numbers: Vec<i32> = (1..=10).collect();
let even_numbers: Vec<i32> = numbers.into_iter().filter(|&x| x % 2 == 0).collect();
assert_eq!(even_numbers, vec![2, 4, 6, 8, 10]);
```

2. Contar ocurrencias de caracteres:
```rust
use std::collections::HashMap;

fn count_chars(s: &str) -> HashMap<char, usize> {
    s.chars().fold(HashMap::new(), |mut acc, c| {
        *acc.entry(c).or_insert(0) += 1;
        acc
    })
}

let result = count_chars("hello world");
assert_eq!(result.get(&'l'), Some(&3));
assert_eq!(result.get(&'o'), Some(&2));
```

3. Palabras con más de 5 letras:
```rust
fn long_words(words: Vec<String>) -> Vec<String> {
    words.into_iter().filter(|w| w.len() > 5).collect()
}

let words = vec!["short".to_string(), "medium".to_string(), "long_word".to_string()];
let long = long_words(words);
assert_eq!(long, vec!["medium".to_string(), "long_word".to_string()]);
```

4. Combinar vectores con `zip`:
```rust
let v1 = vec![1, 2, 3];
let v2 = vec!['a', 'b', 'c'];
let combined: Vec<(i32, char)> = v1.into_iter().zip(v2.into_iter()).collect();
assert_eq!(combined, vec![(1, 'a'), (2, 'b'), (3, 'c')]);
```

5. Suma de cuadrados de números pares:
```rust
fn sum_of_squares_of_even(numbers: Vec<i32>) -> i32 {
    numbers.into_iter()
           .filter(|&x| x % 2 == 0)
           .map(|x| x * x)
           .sum()
}

let result = sum_of_squares_of_even(vec![1, 2, 3, 4, 5]);
assert_eq!(result, 20); // 2^2 + 4^2 = 4 + 16 = 20
```

6. Secuencia de Fibonacci:
```rust
struct Fibonacci {
    curr: u32,
    next: u32,
}

impl Iterator for Fibonacci {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.curr + self.next;
        self.curr = self.next;
        self.next = new_next;
        Some(self.curr)
    }
}

let fib = Fibonacci { curr: 0, next: 1 };
let first_10: Vec<u32> = fib.take(10).collect();
assert_eq!(first_10, vec![1, 1, 2, 3, 5, 8, 13, 21, 34, 55]);
```

7. Longitud de cada string:
```rust
let words = vec!["hello".to_string(), "world".to_string()];
let lengths: Vec<usize> = words.iter().map(|s| s.len()).collect();
assert_eq!(lengths, vec![5, 5]);
```

8. Letras individuales de palabras:
```rust
let words = vec!["rust", "is", "fun"];
let letters: Vec<char> = words.into_iter().flat_map(|s| s.chars()).collect();
assert_eq!(letters, vec!['r', 'u', 's', 't', 'i', 's', 'f', 'u', 'n']);
```

9. Números que aparecen más de una vez:
```rust
use std::collections::HashSet;

fn find_duplicates(numbers: Vec<i32>) -> HashSet<i32> {
    let mut seen = HashSet::new();
    numbers.into_iter().filter(|&x| !seen.insert(x)).collect()
}

let duplicates = find_duplicates(vec![1, 2, 3, 2, 1, 4]);
assert_eq!(duplicates, [1, 2].into_iter().collect());
```

10. Primeros 10 números primos:
```rust
fn is_prime(n: u32) -> bool {
    if n <= 1 { return false; }
    (2..=((n as f64).sqrt() as u32)).all(|i| n % i != 0)
}

let primes: Vec<u32> = (2..).filter(|&n| is_prime(n)).take(10).collect();
assert_eq!(primes, vec![2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
```

11. Crear HashMap de tuplas:
```rust
use std::collections::HashMap;

let tuples = vec![("a".to_string(), 1), ("b".to_string(), 2)];
let map: HashMap<String, i32> = tuples.into_iter().collect();
assert_eq!(map.get("a"), Some(&1));
assert_eq!(map.get("b"), Some(&2));
```

12. Suma acumulativa:
```rust
fn cumulative_sum(numbers: Vec<i32>) -> Vec<i32> {
    numbers.iter().scan(0, |acc, &x| { *acc += x; Some(*acc) }).collect()
}

let result = cumulative_sum(vec![1, 2, 3, 4]);
assert_eq!(result, vec![1, 3, 6, 10]);
```

13. Combinar vectores y filtrar impares:
```rust
let v1 = vec![1, 2, 3];
let v2 = vec![4, 5, 6];
let odd_numbers: Vec<i32> = v1.into_iter()
                              .chain(v2.into_iter())
                              .filter(|&x| x % 2 != 0)
                              .collect();
assert_eq!(odd_numbers, vec![1, 3, 5]);
```

14. Caracteres y sus posiciones:
```rust
fn char_positions(s: &str) -> Vec<(char, usize)> {
    s.char_indices().map(|(i, c)| (c, i)).collect()
}

let result = char_positions("hello");
assert_eq!(result, vec![('h', 0), ('e', 1), ('l', 2), ('l', 3), ('o', 4)]);
```

15. Productor-consumidor con canales e iteradores:
```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        for i in 1..=5 {
            tx.send(i).unwrap();
        }
    });

    let sum: i32 = rx.iter().sum();
    assert_eq!(sum, 15);
}
```

16. HashMap de índices y elementos:
```rust
use std::collections::HashMap;

let vec = vec!['a', 'b', 'c'];
let map: HashMap<usize, char> = vec.into_iter().enumerate().collect();
assert_eq!(map.get(&0), Some(&'a'));
assert_eq!(map.get(&1), Some(&'b'));
assert_eq!(map.get(&2), Some(&'c'));
```

17. Números triangulares menores que 100:
```rust
struct TriangularNumbers {
    n: u32,
}

impl Iterator for TriangularNumbers {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        self.n += 1;
        Some(self.n * (self.n + 1) / 2)
    }
}

let triangular = TriangularNumbers { n: 0 };
let result: Vec<u32> = triangular.take_while(|&x| x < 100).collect();
assert_eq!(result, vec![1, 3, 6, 10, 15, 21, 28, 36, 45, 55, 66, 78, 91]);
```

18. Barajar cartas:
```rust
use rand::seq::SliceRandom;
use rand::thread_rng;

fn shuffle_deck() -> Vec<String> {
    let suits = vec!["♠", "♥", "♦", "♣"];
    let values = vec!["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"];
    
    let mut deck: Vec<String> = suits.into_iter()
        .flat_map(|s| values.iter().map(move |&v| format!("{}{}", v, s)))
        .collect();
    
    deck.shuffle(&mut thread_rng());
    deck
}

let shuffled = shuffle_deck();
assert_eq!(shuffled.len(), 52);
```

19. Suma máxima de tres números consecutivos:
```rust
fn max_triple_sum(numbers: &[i32]) -> i32 {
    numbers.windows(3)
           .map(|w| w.iter().sum())
           .max()
           .unwrap_or(0)
}

let result = max_triple_sum(&[1, 2, 3, 4, 5, 6]);
assert_eq!(result, 15); // 4 + 5 + 6 = 15
```

20. Secuencia de Collatz:
```rust
struct Collatz {
    n: u64,
}

impl Iterator for Collatz {
    type Item = u64;

    fn next(&mut self) -> Option<Self::Item> {
        if self.n == 1 {
            None
        } else {
            let current = self.n;
            self.n = if self.n % 2 == 0 { self.n / 2 } else { 3 * self.n + 1 };
            Some(current)
        }
    }
}

fn collatz_sequence(start: u64) -> Vec<u64> {
    Collatz { n: start }.collect()
}

let sequence = collatz_sequence(13);
assert_eq!(sequence, vec![13, 40, 20, 10, 5, 16, 8, 4, 2, 1]);
```