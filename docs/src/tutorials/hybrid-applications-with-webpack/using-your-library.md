# Run The Code

The Rust Webpack template is designed for creating monorepo-style Web applications with
Rust-generated WebAssembly and Webpack without publishing your wasm to NPM.
This portion of the tutorial will explain how to build a [Webpack] JavaScript project
that will run your WebAssembly code in the browser.

[Webpack]: https://webpack.js.org/

## Scaffold a JavaScript Project

To generate a new Rust Webpack project, we've used the [`rust-webpack`] npm template.

[`rust-webpack`]: https://github.com/rustwasm/rust-webpack-template

```
npm init rust-webpack your-package-name
```

A new project folder will be created with the name you supply.

If we look in the project, we'll see the following:

- `.gitignore`: ignores `node_modules`
- `README.md`: basic information about running and building
- `static/index.html`: a bare bones html document that includes the webpack bundle
- `js/index.js`: example JS file with a comment showing how to import and use a wasm pkg
- `package.json` and `package-lock.json`:
  - pulls in devDependencies for using webpack:
      - [`webpack`](https://www.npmjs.com/package/webpack)
      - [`webpack-cli`](https://www.npmjs.com/package/webpack-cli)
      - [`webpack-dev-server`](https://www.npmjs.com/package/webpack-dev-server)
  - defines a `start` script to run `webpack-dev-server`
- `webpack.config.js`: configuration file for bundling your JS with webpack
- `src/lib.rs`: your Rust crate code!

## Your Rust Crate

The scaffolded project includes an example Rust WebAssembly webpack crate.

Inside the `crate/src/lib.rs` file we see a `run` function that's callable from our JS file:
```rust
// This is like the `main` function, except for JavaScript.
#[wasm_bindgen(start)]
pub fn main_js() -> Result<(), JsValue> {
    // This provides better error messages in debug mode.
    // It's disabled in release mode so it doesn't bloat up the file size.
    #[cfg(debug_assertions)]
    console_error_panic_hook::set_once();


    // Your code goes here!
    console::log_1(&JsValue::from_str("Hello world!"));

    Ok(())
}
```

Now, open up the `js/index.js` file. We see our Rust-generated wasm `run` function being
called inside our JS file.

```js
import("../pkg/index.js").catch(console.error);
```

## Run The Project

To generate our Rust-compiled to wasm code, in the root directory we run:
```bash
npm run build
```
This will create our bundled JavaScript module in a new directory `dist`.

We should be ready to run our project now!
In the root directory, we'll run:

```bash
npm start
```

Then in a web browser navigate to `http://localhost:8080` and you should "Hello world!" in the developer console.

If you did congrats! You've successfully used the rust-webpack template!
