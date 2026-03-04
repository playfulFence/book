# `esp-generate`

[`esp-generate`][esp-generate] is a project generation tool that assists users in creating a functional project with most of their desired configurations pre-applied.

## Installation

To install `esp-generate`:

```shell
cargo install esp-generate --locked
```

You can also directly download pre-compiled [release binaries][release-binaries] or use [`cargo-binstall`][cargo-binstall].

## What `esp-generate` Сonfigures

`esp-generate` provides more than dependency selection: it applies a known set of crates and feature combinations corresponding to the chosen template options, reducing the amount of manual configuration required to produce a working project.

Enabling various options may add additional crates to `Cargo.toml` of the generated project. Certain capabilities require supporting libraries to function correctly. The templates aim to keep the dependency set minimal while ensuring the generated project is functional and immediately runnable.

All generated projects are based on `esp-hal`. Depending on the selected options, `esp-generate` adds the required support crates (for example `demft` logging, heap allocation, async executors etc.) and applies the appropriate feature flags so that the configuration is internally consistent.

Wireless connectivity provided by `esp-radio`, as stated in [Ancillary Crates](../../introduction/ancillary-crates.md) chapter, relies on `esp-rtos`. For this reason, enabling Wi-Fi or BLE causes `esp-generate` to include this crate and configure it with the `esp-radio` feature, providing the scheduling and runtime integration required for reliable operation. When Embassy support is enabled, `esp-rtos` also serves as the integration point for async execution on supported chips, with a corresponding feature enabled in the template project. For IP networking, the templates include the surrounding networking components. This typically includes `smoltcp`, `embassy-net` for async networking, when Embassy is enabled.

Some options have coupled configurations. Logging is configured either via `defmt` or `log` with a corresponding frontend. Certain crates are also included as part of the standard baseline because they support common embedded workflows. For example, `esp-bootloader-esp-idf` includes additional support of 2nd stage bootloader, and `critical-section` is included because many embedded crates rely on it to implement interrupt-critical regions.

> [!TIP]
> Each version of `esp-generate` targets a specific version of the ecosystem crates. Make sure to update `esp-generate` if you want to use the latest released versions.

[release-binaries]: https://github.com/esp-rs/esp-generate/releases
[cargo-binstall]: https://github.com/cargo-bins/cargo-binstall
[esp-generate]: https://github.com/esp-rs/esp-generate
