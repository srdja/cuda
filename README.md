# `cuda`

> Experiments with CUDA and Rust

Testing [Rust -> PTX support](https://github.com/rust-lang/rust/pull/38559)

```
# Convert a crate into a PTX module
$ xargo rustc \
    --manifest-path kernel/Cargo.toml \
    --target nvptx64-nvidia-cuda \
    --release \
    -- --emit=asm

# Inspect the module
$ find -name '*.s'
./kernel/target/nvptx64-nvidia-cuda/release/deps/kernel-b200c034da273978.s

$ head -n16 $(find -name '*.s')
//
// Generated by LLVM NVPTX Back-End
//

.version 3.2
.target sm_20
.address_size 64

        // .globl       add

.visible .entry add(
        .param .u64 add_param_0,
        .param .u64 add_param_1,
        .param .u64 add_param_2,
        .param .u64 add_param_3
)

# Test that module
$ cargo run --example add $(find -name '*.s')

$ cargo run --example memcpy $(find -name '*.s')
```

## License

The documentation is licensed under

- Creative Commons Attribution 4.0 License ([LICENSE-CC-BY](LICENSE-CC-BY)
  or https://creativecommons.org/licenses/by/4.0/legalcode)

And the source code is licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  http://www.apache.org/licenses/LICENSE-2.0)

- MIT License ([LICENSE-MIT](LICENSE-MIT) or
  https://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
licensed as above, without any additional terms or conditions.
