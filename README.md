## Page 0 - Building Sudoku without a UI

First, we'll follow the "Getting Started" book by setting up our local
workspace. Our cargo.toml will look like this:

```toml
[package] name = "bevy_sudoku_game" version = "0.1.0" edition = "2021"

[workspace] resolver = "2" # Important! wgpu/Bevy needs this!

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies] bevy = "0.10"

# Enable a small amount of optimization in debug mode

[profile.dev] opt-level = 1

# Enable high optimizations for dependencies (incl. Bevy), but not for our code:

[profile.dev.package."*"] opt-level = 3
```

##### We won't be using the dynamic feature (we're on a Windows machine), but you can [enable it](https://bevyengine.org/learn/book/getting-started/setup/#enable-fast-compiles-optional) if you wish. We'll also stick to stable rust for now.

Then, we can setup our `main.rs` as follows:

```rust
use bevy::prelude::*;

fn main() {
    App::new().run();
}
```

Let's go ahead and run `cargo build` one time, just to cache the Bevy's
dependencies.
