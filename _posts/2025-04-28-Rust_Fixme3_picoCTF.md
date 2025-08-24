---
title: Rust Fixme 3
date: 2025-04-28 12:54:17 +0600
categories: [Pico-CTF, General]
tags: [pico-ctf, easy, general] # TAG names should always be lowercase
description: Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
media_subpath: /images/picoCTF/
image:
    path: picoctf.png
---

### Getting Started

This a small rust program, the code is simple package , your task is simple, update the package and run the program, you will got your ans! lets do it!  
1\. first download the file and unzip it by following command : `gunzip filename&&tar -x -f filename`

&nbsp;    > Explain the script hook: 

&nbsp;    > file is  in tar.gz so we first unzip it by gunzip and then unzip the tar file by tar cmd.

### Errors
 
2\. you need cargo to build or run the code. if kali has cargo then type `cargo build`  . if not then install `sudo apt install cargo` . then build. 

3\. you will see a error prompt that shows unsafe  :

```rust
  --> src/main.rs:31:31
   |
31 |         let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);
   |                               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ call to unsafe function
   |
   = note: consult the function's documentation for information on how to avoid undefined behavior

For more information about this error, try `rustc --explain E0133`.
error: could not compile `rust_proj` (bin "rust_proj") due to 1 previous error.

```

&nbsp;

4\. go to src/ folder and open the main.rs file by following command `nano main.rs`

5\. you will see unsafe function is commented, uncomment the following line also to the brackets, in the down below..also if you have problem to fix then copy the full code and paste it into the `main.rs.`

```rust
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {
    // Key for decryption
    let key = String::from("CSUCKS");

    // Editing our borrowed value
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    // Create decryption object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return;
    }
    let xrc = res.unwrap();

    // Did you know you have to do "unsafe operations in Rust?
    // https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html
    // Even though we have these memory safe languages, sometimes we need to do things outside of the rules
    // This is where unsafe rust comes in, something that is important to know about in order to keep things in perspective
    
     unsafe {
        // Decrypt the flag operations 
        let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

        // Creating a pointer 
        let decrypted_ptr = decrypted_buffer.as_ptr();
        let decrypted_len = decrypted_buffer.len();
        
        // Unsafe operation: calling an unsafe function that dereferences a raw pointer
        let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);

        borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));
     }
    println!("{}", borrowed_string);
}

fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53", "63", "e1", "01", "35", "7e", "59", "60", "f6", "03", "86", "7f", "56", "41", "29", "30", "6f", "08", "c3", "61", "f9", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: ");
    decrypt(encrypted_buffer, &mut party_foul);
}

```

6\. build the file and then test and run the code by following command :

`cargo build ` 

`cargo test`

`cargo run`

Then you got the flag.
