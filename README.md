# Typst Flake

This repository contains a Nix Flake[^1] for Typst. It exports a Nix package that can build Typst's CLI using the Nix tool. It is compatible at least with the latest Typst release, and should also build the latest commits on Typst's `main` branch. Should any problems or incompatibilities arise, please contribute a fix or open an issue!

## Usage

### Compiling Typst

To build and run Typst through the Flake using its default Typst version (usually the latest release), first ensure Nix is properly installed with Flake support.[^2] Then, simply execute the command below with the appropriate arguments. For example, to compile a Typst file:

```sh
nix run github:typst/typst-flake -- compile doc.typ
```

Alternatively, you can compile Typst without running using the command below, which will output a runnable Typst binary under `result/bin/typst`:

```sh
nix build github:typst/typst-flake
```

### Compiling a specific Typst commit

To compile another Typst version or commit, you can use `--override-input` when building. Use one of the sample commands below. You can replace `0.13` in the second example with the specific commit or branch you'd like to build.

```sh
# Compile the latest main commit
nix run github:typst/typst-flake --override-input typst github:typst/typst -- --help

# Compile a specific branch: 0.13 (release 0.13.1)
nix run github:typst/typst-flake --override-input typst github:typst/typst/0.13 -- --help

# Compile a specific commit: d60ec29
nix run github:typst/typst-flake --override-input typst github:typst/typst/d60ec29 -- --help
```

### Development shell

You can use the command below to spawn a development shell. It should contain `rustc` and `cargo` so you can develop Typst as a contributor.

```sh
nix develop github:typst/typst-flake
```

## Contributing

To contribute to the flake, simply clone the repository locally, apply some changes, and build and run Typst with the same commands as above, but replacing `github:typst/typst-flake` with `.` (for the current directory). For example, to build a runnable Typst binary with your changes to the flake, use the command below:

```sh
nix build .
```

## A note on compatibility

Please note that the flake is maintained as a best-effort by the community and not officially supported by the Typst team. As such, it is not guaranteed to always be compatible with the latest Typst releases or commits, which might fail to build using the latest version of the flake. However, we will accept contributions to fix any such problems, should they arise.

## License

All code in this repository is licensed under Apache-2.0.

[^1]: Flakes (official NixOS Wiki): https://wiki.nixos.org/wiki/Flakes
[^2]: Nix installation guide (official NixOS Wiki): https://wiki.nixos.org/wiki/Nix_Installation_Guide
