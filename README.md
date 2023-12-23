Following the [WASI tutorial](https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-tutorial.md), with some modifications. 

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

