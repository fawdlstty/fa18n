# fa18n

[![version](https://img.shields.io/badge/dynamic/toml?url=https%3A%2F%2Fraw.githubusercontent.com%2Ffawdlstty%2Ffa18n%2Fmain%2Ffa18n%2FCargo.toml&query=package.version&label=version)](https://crates.io/crates/fa18n)
![status](https://img.shields.io/github/actions/workflow/status/fawdlstty/fa18n/rust.yml)

Modern i18n support library base on faml

## Manual

Steps:

1. Add `fa18n` to your `Cargo.toml`

```toml
[build-dependencies]
fa18n = "0.1.0"
```

2. Create i18n resources:

```
i18n/
  en.faml
  zh.faml
```

`en.faml`:

```faml
[i18n.en]

hello0 = "hello world"
Hello = "hello {name:str}"
```

`zh.faml`:

```faml
[i18n.zh]

hello0 = "你好，世界"
Hello = "你好，{name:str}"
```

3. Create `build.rs` and add code:

```rust
fn main() {
    fa18n::generate_rust("i18n/", "src/i18n.rs").unwrap();
}
```

4. Write `main.rs` code:

```rust
pub mod i18n;

use crate::i18n::*;

fn main() {
    let hello = I18n::hello("maria".to_string());
    println!("{}", hello.translate(I18nLocale::Zh));
}
```
