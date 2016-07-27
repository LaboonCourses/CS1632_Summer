
## Rust Cheat Sheet

### Cargo commands

These should be run from the command line.   

#### Create new standalone program project

This will make a new project under the subdirectory foo (e.g., if you are in /user/laboon, and type this command, there will be a new subdirectory /user/laboon/foo.  /user/laboon/foo/src will contain the file main.rs which will have the entry point for the program, fn main().  Go into the foo directory to run commands other than "new" such as "build" or "run".

```
cargo new foo --bin
```

#### Create new library project

```
cargo new foo
```

#### Build a cargo project without running it

```
cargo build
```

#### Build and run a cargo project

```
cargo run
```

#### Run unit tests on a project

See https://doc.rust-lang.org/book/testing.html for how to write unit tests for your Rust applicaiton.

```
cargo test
```


### Basic Function Syntax

```rust
// Function syntax
// i32 = signed 32-bit int
// u32 = unsigned
fn double_me(x: i32) -> i32 {
  return x * 2;
}

fn main() {
   let a = 4;
   let b = double_me(a);
   println!("a = {}, b = {}", a, b);
}

```

### The No-semicolon Return

```rust
// alternative to return - don't put a semicolon
// This is actually the preferred way
fn double_me(x: i32) -> i32 {
  x * 2
}
```

### Mutability

```rust
// Mutable vs immutable vars

fn main() {
   let a = 4;
   let mut b = 6;
   // not allowed!
   // a = 5;
   // allowed because variable is mutable
   b = 12; 
   println!("a is {}", a)
   
}
```

### Borrowing Refs

```rust
// Borrowed ref
fn double_me_borrow(x: &i32) -> i32 {
  return x * 2;
}
```

### Mutable refs

```rust
// mutable reference
fn double_me_mut(mut x: &mut i32) {
    // Note *x, not x!
    *x *= 2;
}

fn main() {
   let mut x = 4;
   double_me_mut(&mut x);
   println!("x = {}", x);
}
```

### Structs in Rust

```rust
// struct in rust
struct Gnome {
   height: u32,
   weight: u32
}

fn main() {
    let g: Gnome = Gnome { height: 100, weight: 200 };
    println!("This gnome weighs {} grams", g.weight);
}
```

### Modifying a Struct via a Function

```rust
// Here is where mutable borrowing is useful and easier than with primitives
struct Gnome {
   height: u32,
   weight: u32
}

fn embiggen_gnome(mut gnome_to_change: &mut Gnome) {
   gnome_to_change.height *= 3;
   gnome_to_change.weight *= 3;
}

fn main() {
    let mut g: Gnome = Gnome { height: 100, weight: 200 };
    println!("This gnome weighs {} grams", g.weight);
    embiggen_gnome(&mut g);
    println!("This gnome weighs {} grams", g.weight);
}
```

### Formatting Output

```rust
// Decimal point format
fn main() {
    let pi: f32 = 22.0 / 7.0;
    println!("pi is about {:.2} ", pi);
}
```

### Random Numbers

```rust
// Get random number
// Be sure to update your cargo.toml file, too!
// [dependencies]
// rand = "0.3.14"
extern crate rand;

use rand::Rng;

fn main() {
    let mut die_roll;
    for j in 0..10 {
    	// Generates values 1 through 6!
        die_roll = rand::thread_rng().gen_range(1, 7);
        println!("Roll {} is {}", j, die_roll);
    }
   
}
```

### Enums

```rust
// enum in rust
// The following line is only necessary if you
// are making arrays of that enum
#[derive(Copy, Clone)]
enum Animal {
  Dog,
  Cat,
  Bird
}

let a: Animal = Animal::Dog;

match a {
  Animal::Dog => println!("woof!");
  Animal::Cat => println!("meow!");
  Animal::Bird => println!("tweet!");
}

// This will not work / compile!
// if a == Animal::Dog {
//   println!("Bark");
//}
```

### Casting
```rust
fn main() {
    let num_hits: i32 = 6;
    let num_at_bats: i32 = 21;
    // Cast num_hits and num_at_bats as f32 (32-bit floats)
    let batting_average: f32 = (num_hits as f32) / (num_at_bats as f32);
    println!("batting average = {:.3}", batting_average);
}
```

### Arrays

```rust
// making arrays
// NB size must be fixed at COMPILE time
// use vectors if at run-time
fn main() {
    let primes: [i32; 5] = [2, 3, 5, 7, 11];
    // loop with iterator
    for j in primes.iter() {
        println!("{} is prime", j);
    }
}
```

### 2-D Arrays

```rust
fn main() {
    let mut matrix = [[0i32; 10]; 10];

    // Note that j and k are "usize", or
    // unsigned architecture size.
    // Cast as the appropriate type.
    for j in 0..10 {
        for k in 0..10 {
            matrix[j][k] = j as i32;
        }
    }


    // loop by value
    for j in 0..10 {
        for k in 0..10 {
            match matrix[j][k] {
                0 => print!("o"), 
                1 => print!("1"),
                2 => print!("2"),
                _ => print!("?"), // anything else
            }
        }
        println!("");
    }

}
```

### Arrays of Enums
```rust
// Remember this is necessary for arrays of enums
#[derive(Copy, Clone)]
enum Animal {
    Dog,
    Cat,
    Bird
}

fn main() {
    // 10x10 array of all dogs
    let mut b = [[Animal::Dog; 10]; 10];
    // Change a few to cats and birds
    b[0][1] = Animal::Cat;
    b[2][3] = Animal::Bird;
}
```

### Read string from user

```rust
use std::io;
use std::io::Error;

// get a string from the user
fn get_a_string() -> Result<String, Error> {
    println!("Type something");
    let mut to_return = String::new();
    io::stdin().read_line(&mut to_return).expect("FAIL");
    Ok(to_return)
}

fn main() {
    let s;
    match get_a_string() {
        Ok(n) => s = n,
        Err(n) => {
	          println!("ERROR COULD NOT READ!");
	          s = String::from("ERROR");
	       }
    }
    println!("s = {}", s);
}
```
