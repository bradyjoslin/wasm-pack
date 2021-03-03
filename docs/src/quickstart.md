# Quickstart

1. Install `rust` using [`rustup`].
1. Install [wasm-pack].
1. Run `wasm-pack new hello-wasm`.
1. `cd hello-wasm`.
1. Run `wasm-pack build`.
1. `wasm-pack` generates files in a `pkg` dir
1. To publish to npm, run `wasm-pack publish`. You may need to login to the
   registry you want to publish to. You can login using `wasm-pack login`.

[`rustup`]: https://rustup.rs/
[Install this tool.]: https://rustwasm.github.io/wasm-pack/installer/
