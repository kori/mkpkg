 package:
   name: ripgrep
   version: 0.8.0
   description: ripgrep combines the usability of The Silver Searcher with the raw speed of grep
   license: [MIT, Unlicense]
   url: https://github.com/BurntSushi/ripgrep

   source:
     - git+https://github.com/BurntSushi/$name.git#tag=$version

   build:
     - cd "$name".git && cargo build --release

   check:
     - cd "$name".git && cargo test

   install:
     - cd "$name".git && install -D -m744 target/release/rg -t "$pkgdir"/bin/
