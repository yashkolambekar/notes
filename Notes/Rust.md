
```rust
fn main () {
	println!("Hello, World!");
}
```

The first hello world function. The **main** is the first function that runs in any file.
#### Cargo

```bash
cargo new hello_cargo --bin
```

Cargo is the `npm` of  rust world and we can create rust applications using the `cargo new <appname> --bin` command. The `--bin` flag tells cargo that this is a executable that we are making and not a rust library. 

We can compile / build the project using `cargo build` and we can run it using `cargo run`. We also have the command `cargo check` which checks the code but does not compile it, `cargo check` is faster than build or run as it is does not compile to an executable, so we can run it during development many times to check for bugs / errors faster than building it every time.

**Building for release**

```bash
cargo build --release
```

We are supposed to add a `--release` flag while building for release, this makes the most optimized executable. In my testing, the default cargo app's normal build was 4MB and the release build was 400 something KB. So it cuts off all the unwanted things from it.

The release build is stored in `target/release` whereas the normal builds are saved in `target/debug`
#### A simple i/o program game

```rust
use std::io;

fn main() {
	println!("Guess the number");
	println!("Please input your guess.");
	
	let mut guess = String::new(); // Make a mutable guess variable 
	
	io::stdin().read_line(&mut guess)
		.expect("Failed to read line");

	println!("You guessed, {}", guess);
}
```

We will be able to understand this code better if we have worked with `c` or `java` before. Firstly we import the `std` library's `io` library. Then in the main function we start with greeting the user and all. 

We then define a mutable variable named `guess` with `let mut guess`, if we did not include mut, the variable will be immutable by default.

`io::stdin().read_line()` function reads the value from terminal and writes the value to the guess using the `&mut guess` reference. 

The `.expect()` function works on what is returned from the `read_line()` function, it returns either Ok or Err.

At the end, we use string constructor and insert the `guess` variable at the place of `{}`.

#### Shadowing

```rust
let mut guess = String::new();

io::stdin().read_line(&mut guess)
	.expect("Failed to read line");

let guess: u32 = guess.trim().parse()
	.expect("Please type a number!");
```

Shadowing is the concept of redefining an already defined variable, rust allows this. This is done in cases where we want to change the type of a variable without creating a new variable.

**Loop**

```rust
loop {
	// code goes here
}
```

The `loop` is an infinite loop which will keep running till some error occurs (of course the program will break) or we hit a `break` statement.

































Things to remember,
- if we add `!` in the end of a function like variable, it is a macro, not a function
