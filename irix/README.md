# IRIX in this tree

- `compiler/rustc_target/src/spec/targets/mips64_sgi_irix.rs` and `spec/base/irix.rs`: the
  `mips64-sgi-irix` target (IRIX 6.5, MIPS IV, N32), `Os::Irix`, `CfgAbi::AbiN32`.
- `library/`: std's IRIX arms (`std::os::irix`, the unix `sys` modules, backtrace, unwind).
- `irix/libc`: our libc fork (branch `irix`), which `library/Cargo.toml` patches in by path.

Build a cross rustc with std for IRIX on a Linux host with `bootstrap.toml` from this directory
(it names the IRIX cross clang that links IRIX programs):

    cp irix/bootstrap.toml . && ./x.py build --stage 1 library

then `rustup toolchain link irix build/x86_64-unknown-linux-gnu/stage1` and build with
`cargo +irix build --target mips64-sgi-irix` (set the target linker in `.cargo/config.toml`).
