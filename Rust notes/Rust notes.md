## Rust notes

Rust’s build system and package manager: **Cargo**

Creating a Project with Cargocargo new <project name>

- Creating a Project  `cargo new <project name>`
- We can build a project using `cargo build` , build a release version using `cargo build --release`.
- We can build and run a project in one step using `cargo run`.
- We can build a project without producing a binary to check for errors using `cargo check`.



`Option` and `Result`:

`Option`: 1. Some  2. None

```rust
let val: Option<u32> = get_some_val();

match val {
    Some(num) => println!("val is: {}", num),
    None => println!("val is None")
}
```

 `Result`: 1. Ok  2. Err

```rust
let sr: Result<u32, &str> = Ok(123); //or Err("You are wrong");

match sr {
    Ok(v) => println!("sr value: {}", v),
    Err(e) => println!("sr is error {}", e)
}
```

`?` question mark: return Err for the function whenever an Err occurs.

```rust
fn srst() -> Option<u32> {
    let sr: u32 = rs.get_u32_result()?;
    println!("sr is ok: {}", sr);
    
    let st: u8 = rs.get_u8_result()?;
    println!("st is ok: {}", st)
    
    Ok(sr + st as u32);
}

let sum: Option<u32> = srst();
```

 



How to alloc memory?

```rust
use std::alloc::{alloc, dealloc, Layout};

unsafe {
    let layout = Layout::new::<u16>();
    let ptr = alloc(layout);

    *(ptr as *mut u16) = 42;
    assert_eq!(*(ptr as *mut u16), 42);

    dealloc(ptr, layout);
}
```

