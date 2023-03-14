# Page 0 - Building Sudoku without a UI

## Setup

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
    App::new()
        .add_plugins(DefaultPlugins)
        .run();
}
```

Let's go ahead and run `cargo build` one time, just to cache the Bevy's
dependencies. This will take a minute, but after this compiles should only take
a couple seconds.

---

## Design

Let's start by thinking about the basic features we need to play Sudoku.

Sudoku is played on a 9x9 grid, with some boxes in the grid starting out filled
in with a number from 1-9. The goal is to fill out the rest of the grid, such
that in each column, row, and 3x3 box each digit from 1 to 9 is only present
once.

To play Sudoku, we'll need a way to get an unsolved Sudoku board, a way to set
values inside the Sudoku board, and a way to determine if we've won or not.

<aside>
The question of how we get a "fun to play" unsolved sudoku board is
[quite](http://zhangroup.aporc.org/images/files/Paper_3485.pdf)
[hard](https://gamedev.stackexchange.com/questions/56149/how-can-i-generate-sudoku-puzzles).
We need sudoku boards which can be solved, but we might also wish to generate a
range of difficulty levels. What's easy to solve for a backtracking algorithm might be hard for a human to solve.
</aside>

We can sidestep generating the board by simply loading our puzzles from a static
directory.

Let's suppose our sudoku board data comes in this JSON format:

```json
{
  "id": 0,
  "difficulty": "medium",
  "puzzle": [
    "530070000",
    "600195000",
    "098000060",
    "800060003",
    "400803001",
    "700020006",
    "060000280",
    "000419005",
    "000080079"
  ],
  "solved": [
    "534678912",
    "672195348",
    "198342567",
    "859761423",
    "426853791",
    "713924856",
    "961537284",
    "287419635",
    "345286179"
  ]
}
```

Where the id is simply a numeric identifier, difficulty is always either "easy";
"medium"; "hard"; "expert"; or "evil", puzzle is the unsolved version of the
puzzle with non-clues replaced with 0, and solved is the solved version of the
puzzle.

In Bevy, it's normal to load things like files as `Assets`, and then to spawn them in the world as `Entities`, or rather, components attached to `Entities`.