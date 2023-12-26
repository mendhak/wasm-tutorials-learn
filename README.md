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

    ./wasmtime-v16.0.0-x86_64-linux/wasmtime simple.wat

Use `wabt` to convert the web assembly text to binary. 

    wget https://github.com/WebAssembly/wabt/releases/download/1.0.34/wabt-1.0.34-ubuntu.tar.gz
    tar xf wabt-1.0.34-ubuntu.tar.gz
    ./wabt-1.0.34/bin/wat2wasm simple.wat
    ./wasmtime-v16.0.0-x86_64-linux/wasmtime simple.wasm

View it in an HTML file

    python3 -m http.server
    firefox http://localhost:8000/simple.html


## Using emscripten

Compile to a packaged HTML, using the emscripten Docker image

    docker run --rm -v $(pwd):/src -u $(id -u):$(id -g) emscripten/emsdk emcc hello.c -o hello.html 

Run the resulting HTML file
    
    python3 -m http.server
    firefox http://localhost:8000/output/hello.html


Compile to a packaged Node JS file, using the emscripten Docker image

    docker run --rm -v $(pwd):/src -u $(id -u):$(id -g) emscripten/emsdk emcc hello.c -o output/hello2.js
    node output/hello2.js

Compile hello3 to a template HTML file using the emscripten docker image 

    docker run --rm -v $(pwd):/src -u $(id -u):$(id -g) emscripten/emsdk emcc -o output/hello3.html hello3.c --shell-file shell_minimal.html -s NO_EXIT_RUNTIME=1 -s "EXPORTED_RUNTIME_METHODS=['ccall']"
    python3 -m http.server
    firefox http://localhost:8000/output/hello3.html

