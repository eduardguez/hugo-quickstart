---
title: "Aprendiendo Rust: Básico"
author:
  name: "Eduardo Peralta Rodríguez"
date: 2020-04-26T14:07:58-05:00
draft: false
toc: true
tags: [
    "rust",
    "cargo",
    "desarrollo",
    "software",
    "programación"
]
images: [https://www.rust-lang.org/static/images/rust-logo-blk.svg]
---

## ¿Qué es Rust?

**Rust** es un lenguaje de programación de sistemas creado originalmente por **Graydon Hoare** y actualmente patrocinado por **Mozilla Research**.
Es un lenguaje de programación que le ayuda escribir software más rápido y confiable. Al equilibrar la capacidad técnica
de gran alcance y una gran experiencia de desarrollo, sin asumir el riesgo habitual de fallas o agujeros de seguridad.
Mejor aún, está diseñado para guiarlo naturalmente hacia un código eficiente en términos de velocidad y el uso de memoria.

> **"Rust es un lenguaje de programación de sistemas centrado en tres objetivos: seguridad, velocidad y concurrencia".**
> — Documentación de Rust.

Es lenguaje de programación compilado, de código abierto, multiparadigma que soporta programación por procedimientos, imperativa, funcional pura y orientado a objetos.
También admite programación genérica y metaprogramación, tanto en estilos estáticos como dinámicos.

![Rust logo](https://www.rust-lang.org/static/images/rust-logo-blk.svg)

## ¿Quién está usando Rust?

Hoy empresas grandes y pequeñas están utilizando Rust en producción en todo el mundo, incluidos: Mozilla, Coursera, Dropbox, npm, Atlassian, Postmates y otros.
Da un vistazo a la siguiente [lista de usuarios actuales](https://www.rust-lang.org/production/users).

Está siendo utilizado para el desarrollo de motores de juegos, sistemas operativos, sistemas de archivos, componentes de navegador y motores de simulación para realidad virtual.

Stack Overflow coloca a Rust como uno de los [lenguajes de programación más queridos](https://insights.stackoverflow.com/survey/2020/#technology-most-loved-dreaded-and-wanted-languages-loved)
por la comunidad por cuatro años consecutivos, seguido de cerca por Python.

## ¿Cómo se involucra Mozilla con Rust?

Rust está siendo desarrollado y patrocinado por **Mozilla** desde el año 2009. Su primer versión estable, Rust 1.0, se presento el 15 de mayo de 2015. Actualmente Mozilla
involucra Rust en su proyecto [Servo](https://servo.org/), que es un motor de navegador moderno y de alto redimiendo.

---

## Instalar Rust

Las instrucciones de instalación para cada sistema operativo pueden ser encontradas en
[rust-lang.org](https://www.rust-lang.org) en la guía [Installing Rust](https://www.rust-lang.org/tools/install).

Si está utilizando Linux o macOS, abra la terminal e ingrese el siguiente comando:

~~~
$ curl https://sh.rustup.rs -sSf | sh
~~~

El comando anterior descarga `rustup` (instalador para Rust), que incluye el compilador `rustc` y `cargo` (administrador de paquetes).

Después de que Rust haya sido instalado, puede confirmar la versión instalada fácilmente:

~~~
$ rustc --version
rustc x.y.z (abcabcabc yyyy-mm-dd)
~~~

Si ve está información a instalado Rust con éxito.

Si lo que desea es obtener la última versión de Rust, ejecute el siguiente comando:

~~~
$ rustup update
~~~

---

## Hola, Mundo!

Este es el código fuente del programa tradicional "Hello World" en Rust.

~~~
fn main() {
    println!("Hello World!");
}
~~~

A continuación, cree un archivo `main.rs` para almacenar su código Rust e ingrese el siguiente comando en la terminal (desde la ruta donde fue
guardado el archivo) para compilar su programa:

~~~
$ rustc main.rs
~~~

Después de compilar con éxito, Rust genera un ejecutable binario `main` similar a C o C++. Para ejecutar su programa ingrese el siguiente comando:

~~~
$ ./main
~~~

Independientemente de su sistema operativo la cadena `Hello World!` debe imprimirse.

También puede utilizar [Rust Playground](https://play.rust-lang.org/), una interfaz web para ejecutar código de Rust.

---

## Sintaxis

La función `main` es el primer código que se ejecuta en cada programa ejecutable de Rust. Además, el cuerpo de la función
se envuelve entre llaves `{}` y se terminan todas las expresiones con punto y coma `;`.

~~~
fn main() {
  println!("Hello World!");
}
~~~

`println!` es una macro de Rust para imprimir texto. Una macro se distingue de una función por llevar un signo de admiración `!`.

---

## Hola, Cargo!

**Cargo** es el sistema de construcción y administrador de paquetes de Rust.

A medida que escriba programas con Rust más complejos, Cargo manejara muchas tareas por usted en el mundo real, como construir
su código, descargar las bibliotecas de las que depende su código, compilar paquetes, hacer paquetes distribuibles
y cargarlos en [creates.io](https://crates.io/) para compartir su código con otras personas.

Para lograr este objetivo, Cargo hace cuatro cosas:

* Introduce dos archivos de metadatos con varios bits de información del paquete.
* Obtiene y construye las dependencias de su paquete.
* Invoca `rustc` u otra herramienta de compilación con los parámetros correctos para compilar su paquete.
* Introduce convenciones para facilitar el trabajo con paquetes Rust.

Verifique si Cargo está instalado ingresando lo siguiente en su terminal:

~~~
$ cargo --version
~~~

Para comenzar un proyecto usando Cargo en cualquier sistema operativo, ejecute lo siguiente:

~~~
$ cargo new hello_cargo
$ cd hello_cargo
$ ls -F
~~~

Cargo ha generado dos archivos y un directorio e inicializado un nuevo repositorio de `Git` por nosotros:

~~~
├── src
│   └── main.rs
├── Cargo.lock
├── Cargo.toml
~~~

* **Cargo.toml**: Archivo de **manifiesto** que contiene todos los metadatos que Cargo necesita para compilar su paquete.
* **Cargo.lock**: Archivo que realiza un seguimiento de las versiones exactas de las dependencias en su paquete.
* **src/**: Cargo aloja el código fuente en este directorio.

La estructura del archivo `Cargo.toml` es la siguiente:

~~~
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"
~~~

Dentro del encabezado de sección `[package]` se establece la información de configuración del paquete que Cargo necesita para compilarlo.

Cargo está configurado para buscar dependencias en [creates.io](https://crates.io/) de forma predeterminada, en la sección `[dependencies]`
se enumera todos los paquetes de código (cajas) de su proyecto. Sólo el nombre y una cadena de versión son necesarios.

Da un vistazo a la especificación de versiones semánticas [SemVer](https://semver.org/).

~~~
[dependencies]
time = "0.1.12"
~~~

Cargo proporciona los siguientes comandos para construir y ejecutar un proyecto:

* `cargo build` Construye el proyecto y crea un archivo ejecutable. 
  * Su ejecución por primer vez crea un nuevo archivo **Cargo.lock**.
* `cargo check` Verifica que el código pueda ser compilado.
* `cargo run` Compila el código y ejecuta el ejecutable resultante.

---

## Comentarios

Los comentarios no documentales en Rust siguen el estilo general de C++.

~~~
LINE_COMMENT:
//(~ [/ !] |//) ~\n *
|//

BLOCK_COMMENT:
/*(~ [ * !] | **| BlockCommentOrDoc ) ( BlockCommentOrDoc | ~ */) * */
| /**/
~~~

---

## Variables

Las definiciones de variables en Rust comienzan con la palabra clave `let` seguida del nombre de la variable y valor asignado.
Por defecto en Rust las variables son inmutables, aprovechando así la seguridad y fácil concurrencia.

~~~
let any_number = 5;
~~~

Sin embargo, tiene la opción de hacer que sus variables sean mutables, agregando `mut` delante de la palabra clave `let`.

~~~
let mut any_number = 5;
~~~

---

## Constantes

Una constante se declara usando la palabra clave `const`, y el tipo de dato debe ser especificado seguido de dos puntos `:`.

~~~
const MAX_POINTS: u32 = 100_000;
~~~

Las constantes no solo son inmutables por defecto, siempre son inmutables.

---

## Estáticas

La palabra clave `static` se útiliza para definir una "variable global".

~~~
static N: i32 = 5;
~~~

Solo hay una instancia para cada valor y está en una ubicación fija en la memoria.

---

## Sombreado

Es posible sombrear una variable repitiendo el mismo nombre de la variable y repitiendo el uso de `let`.

~~~
fn main() {
  let x = 5;
  let x = x + 1;
  println!("The value of x is: {}", x); // The value of x is: 6
}
~~~

Al usar la palabra clave `let`, es posible cambiar el tipo de dato y reutilizar el mismo nombre.

~~~
let spaces = "   ";
let spaces = spaces.len();
~~~

Además, el sombreado nos ahorra tener que inventar nombres diferentes para cada variable.

---

## Operadores

---

### Operadores aritméticos

Rust admite las operaciones matemáticas básicas que esperaría en otros lenguajes de programación: suma, resta, multiplicación,
división y módulo.

~~~
fn main() {
  // addition
  let sum = 5 + 10;

  // subtraction
  let difference = 95.5 - 4.3;

  // multiplication
  let product = 4 * 30;

  // division
  let quotient = 56.7 / 32.2;

  // remainder
  let remainder = 43 % 5;
}
~~~

### Operadores de comparación

`== != < > <= >=`

~~~
fn main() {
  let a = 1;
  let b = 2;

  let c = a == b;  // false
  let d = a != b;  // true
  let e = a < b;   // true
  let f = a > b;   // false
  let g = a <= a;  // true
  let h = a >= a;  // true
}
~~~

### Operadores lógicos

`! && ||`

~~~
fn main() {
  let a = true;
  let b = false;

  let c = !a;      // false
  let d = a && b;  // false
  let e = a || b;  // true
}
~~~

### Operadores bit a bit

`& | ^ << >>`

~~~
fn main() {
  let a = 1;
  let b = 2;

  let c = a & b;  //0  (01 && 10 -> 00)
  let d = a | b;  //3  (01 || 10 -> 11)
  let e = a ^ b;  //3  (01 != 10 -> 11)
  let f = a << b; //4  (Add b number of 0s to the end of a -> '01'+'00' -> 100)
  let g = a >> b; //0  (Remove b number of bits from the end of a -> o̶1̶ -> 0)
}
~~~

### Operadores de préstamo

Los operadores `&&` o `&mut` se usan al hacer referencia a una variable original; tomando prestados los datos de la misma.

~~~
fn main() {
  let mut guess = String::new();

  io::stdin().read_line(&mut guess).expect("Failed to read line");
}
~~~

El tipo de préstamo mutable, permiten tomar prestados los datos y alterar una variable, por ejemplo al leer una línea de la terminal.

---

## Tipos de datos

---

### Tipos escalares

Un tipo escalar representa un valor único.

#### Enteros

Esta declaración de tipo indica que cada variante puede ser firmada o no y tienen un tamaño explicito.

Firmado y sin firmar se refieren a si es posible que el número sea positivo o negativo.

| Longitud      | Firmado         | No firmado    |
|:------------- |:---------------:| -------------:|
| 8 bits        | i8              |           u8  |
| 16 bits	      | i16             |           u16 |
| 32 bits       | i32             |           u32 |
| 64 bits       | i32             |           u32 |
| 128 bits      | i32             |           u32 |
| arch          | isize	          |         usize |

* Una variante firmada (`i`) puede almacenar números de $-(2^{n-1})$ a $2^{n-1}-1$.

* Una variante sin firmar (`u`) puede almacenar números de 0 a $2^n-1$.

* `n` es el número de bits que usa la variante.

* Los tipos `isize` `usize` dependen de la arquitectura del computador en el que se ejecuta el programa.

#### Punto flotante

Los tipos de punto flotante de Rust son `f32` y `f64`

~~~
fn main() {
  let x = 2.0; // f64

  let y: f32 = 3.0; // f32
}
~~~

El tipo `f32` es un flotador de precisión simple y `f64` tiene doble precisión.

#### Booleanos

Un tipo booleano en Rust tiene dos valores posibles: `true` y `false`.

~~~
fn main() {
  let t = true;

  let f: bool = false; // with explicit type annotation
}
~~~

#### Caracteres

El tipo `char` de Rust tiene un tamaño de cuatro bytes y representa un valor escalar Unicode.

~~~
fn main() {
  let c = 'z';
  let z = 'ℤ';
  let heart_eyed_cat = '😻';
}
~~~

---

### Tipos compuestos

Los tipos compuestos pueden agrupar múltiples valores en un tipo.

#### Tuplas

Una tupla es una colección de valores de diferentes tipos de datos.

~~~
fn main() {
  let tup: (i32, f64, u8) = (500, 6.4, 1);
}
~~~

#### Matrices

A diferencia de una tupla, una matriz es una colección de objetos del mismo tipo de dato.

~~~
fn main() {
  let ex1a: [i32; 5] = [1, 2, 3, 4, 5];
  let ex1b = [1, 2, 3, 4, 5];
  let ex2a = [3; 5]; 
  let ex2b = [3, 3, 3, 3, 3];
}
~~~

---

## Funciones

Las funciones se declaran usando la palabra clave `fn`, y si devuelve un valor debe de especificarse el tipo de retorno después de una flecha `->`.

~~~
fn plus_one(x: i32) -> i32 {
  x + 1
}
~~~

Podemos devolver un valor con la instrucción `return`, incluso desde bucles internos o `if`s.

~~~
fn main() {
  let x = plus_one(5);
  println!("The value of x is: {}", x);
}
~~~

Además, a Rust no le importa el orden en el que define sus funciones.

---

## Flujos de control

Las expresiones más comunes que le permiten controlar el flujo de ejecución del código de Rust son expresiones `if`-`else if`-`else` y bucles.

---

### `if` / `else if` / `else`

Las expresiones `if`, `else if` y `else` le permiten bifurcar su código según las condiciones. A diferencia de JavaScript y Ruby, 
Rust no intentará automáticamente convertir tipos no booleanos a booleanos. Es necesario ser explicito y proporcionar a una sentencia `if`
un booleano como condición.

~~~
fn main() {
  let number = 6;

  if number % 4 == 0 {
      println!("number is divisible by 4");
  } else if number % 3 == 0 {
      println!("number is divisible by 3");
  } else if number % 2 == 0 {
      println!("number is divisible by 2");
  } else {
      println!("number is not divisible by 4, 3, or 2");
  }
}
~~~

Rust solo ejecuta el bloque para la primera condición verdadera, el resto lo ignora.

Debido a que `if` es una expresión, es posible usarla en la declaración de una variable. Sin embargo, los valores que tienen el potencial de ser resultados
en cada `if` deben de ser del mismo tipo.

~~~
fn main() {
  let condition = true;
  let number = if condition { 5 } else { 6 };

  println!("The value of number is: {}", number);
}
~~~

---

### `match`

Rust proporciona coincidencia de patrones a través de la palabra clave `match`, que se puede utilizar como un `switch` en C/C++.

~~~
fn main() {
  let mut guess = String::new();

  println!("Please input your guess.");

  io::stdin().read_line(&mut guess)
    .expect("Failed to read line");

  let guess: u32 = match guess.trim().parse() {
    Ok(guess) => println!("Ok!"),
    Err(_) => println!("Error :c"),
  };
}
~~~

Una expresión `match` está hecha de brazos. Un brazo consiste en un patrón y el código que debe ejecutarse si el valor dado al comienzo de la expresión `match` se ajusta al patrón de ese brazo.

---

### Bucles

Rust proporciona varios bucles: `loop`, `while` y `for`.

---

#### `loop`

La expresión `loop` denota la ejecución de un bloque de código una y otra vez (bucle infinito) o hasta que explícitamente alcance una declaración final.

~~~
fn main() {
  loop {
    println!("again!");
    break;
  }
}
~~~

Cuando `break` se encuentra, la ejecución del cuerpo del bucle infinito asociado finaliza inmediatamente, mientras que la declaración `continue` puede usarse para omitir el resto de la iteración
y comenzar una nueva.

~~~
fn main() {
  let mut counter = 0;

  let result = loop {
    counter += 1;

    if counter == 3 {
      println!("Three");
      // Skip the rest of this iteration
      continue;
    }

    if counter == 10 {
      break counter * 2;
    }
  };

  println!("The result is {}", result);
}
~~~

A diferencia de los otros tipos de bucles en Rust, `loop` puede ser usado como expresesión que retorna un valor haciendo uso de `break`.

#### `while`

La sintaxis del ciclo `while` es similar a la de otros lenguajes de programación, en la que se define una condición verdadera
que delimitará el número de veces que el código se ejecuta.

~~~
fn main() {
  let mut number = 3;

  while number != 0 {
    println!("{}!", number);
    number -= 1;
  }
  println!("LIFTOFF!!!");
}
~~~

Esta construcción elimina una gran cantidad de anidación que sería necesaria si se ha utilizado `loop`, `if`, `else` y/o `break`.

#### `for`

Como alternativa más concisa, puede usar un bucle `for` y ejecutar un código para cada elemento de una colección.

~~~
fn main() {
  let a = [10, 20, 30, 40, 50];

  for element in a.iter() {
      println!("the value is: {}", element);
  }
}
~~~

La seguridad y la concisión de los bucles `for` los convierten en la construcción de bucles más utilizada en Rust.

---

## Ejercicio 1 "Guessing Game"

## Ejercicio 2 "Fizz Buzz"

---

La implementación de algunos ejemplos relacionados con el post se pueden encontrar en [mi repositorio de Github](https://github.com/eduardguez/learning-rust).

---

## Referencias

Klabnik, S., & Nichols, C. (2019). The Rust Programming Language (Covers Rust 2018). San Francisco, CA: No Starch Press.

Madunuwan, D. (2020, 26 abril). Why Rust? Learning Rust. [https://learning-rust.github.io/docs/a1.why_rust.html](https://learning-rust.github.io/docs/a1.why_rust.html)

Preston-Werner, T. (2009). Semantic Versioning 2.0.0. [https://semver.org/](https://semver.org/)

Mozilla. (2018, 19 enero). Rust. Mozilla Research. [https://research.mozilla.org/rust/](https://research.mozilla.org/rust/)

rust-lang. (2018). Install Rust. rust-lang. [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)

rust-lang. (2018). Production users. [https://www.rust-lang.org/production/users](https://www.rust-lang.org/production/users)

Servo. (2018). Servo, the parallel browser engine. [https://servo.org/](https://servo.org/)

Stack Overflow. (2020). Stack Overflow Developer Survey 2020. [https://insights.stackoverflow.com/survey/](https://insights.stackoverflow.com/survey/2020/)