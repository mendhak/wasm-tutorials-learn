Following the [WASI tutorial](https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-tutorial.md), with some modifications. 


## C

Basic C code, compiled to wasm with clang, run with wasmtime. 

Get the clang compiler. 

    wget https://github.com/WebAssembly/wasi-sdk/releases/download/wasi-sdk-21/wasi-sdk-21.0-linux.tar.gz
    tar xf wasi-sdk-21.0-linux.tar.gz
    ./wasi-sdk-21.0/bin/clang demo.c -o demo.wasm

Build the .wasm file. 

    ./wasi-sdk-21.0/bin/clang demo.c -o demo.wasm

Get wasmtime.

    wget https://github.com/bytecodealliance/wasmtime/releases/download/v16.0.0/wasmtime-v16.0.0-x86_64-linux.tar.xz
    tar xf wasmtime-v16.0.0-x86_64-linux.tar.xz


Run the file which copies a file from one place to another. 

    echo "Hello world" > hello.txt
    ./wasmtime-v16.0.0-x86_64-linux/wasmtime --dir=. demo.wasm ./hello.txt output.txt
    cat output.txt


## Web Assembly Text

Directly execute the text. 

    ./wasmtime-v16.0.0-x86_64-linux/wasmtime demo2.wat

Use `wabt` to convert the web assembly text to binary. 

    wget https://github.com/WebAssembly/wabt/releases/download/1.0.34/wabt-1.0.34-ubuntu.tar.gz
    tar xf wabt-1.0.34-ubuntu.tar.gz
    ./wabt-1.0.34/bin/wat2wasm demo2.wat
    ./wasmtime-v16.0.0-x86_64-linux/wasmtime demo2.wasm
