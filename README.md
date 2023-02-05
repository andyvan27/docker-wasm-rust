# Docker WASM in Rust

This is the code created when following steps from the totorial web page of Nigel Poulton. Many thanks to Nigel for put up such a nice and detailed content for us to touch WASM:

https://nigelpoulton.com/getting-started-with-docker-and-wasm/

## Install Rust

Please follow the instructions from: https://www.rust-lang.org/tools/install

## Bash Commands
```
rustup target add wasm32-wasi

cd hello-docker

cargo build --target wasm32-wasi --release

docker buildx build --platform wasi/wasm -t docker-wasm:0.1 .

docker image ls

docker image tag docker-wasm:0.1 andyvan27/docker-wasm:0.1

docker image push andyvan27/docker-wasm:0.1

docker container run --rm --name=dockerwasm \
  --runtime=io.containerd.wasmedge.v1 \
  --platform=wasi/wasm \
  andyvan27/docker-wasm:0.1
```