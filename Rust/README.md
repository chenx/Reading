# Rust

## Installation

https://rust-lang.org/tools/install/

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

```
Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /Users/chenx/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory is located at:

  /Users/chenx/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /Users/chenx/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /Users/chenx/.profile
  /Users/chenx/.bash_profile
  /Users/chenx/.zshenv
  /Users/chenx/.tcshrc

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-apple-darwin
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with standard installation (default - just press enter)
2) Customize installation
3) Cancel installation
> 1
```

```
info: profile set to default
info: default host triple is x86_64-apple-darwin
info: syncing channel updates for stable-x86_64-apple-darwin
info: latest update on 2026-07-16 for version 1.97.1 (8bab26f4f 2026-07-14)
info: downloading 6 components
        cargo installed                        9.08 MiB
       clippy installed                        3.35 MiB
    rust-docs installed                       22.82 MiB
     rust-std installed                       27.89 MiB
        rustc installed                       76.71 MiB
      rustfmt installed                        1.63 MiB                                                                                                                                    info: default toolchain set to stable-x86_64-apple-darwin

  stable-x86_64-apple-darwin installed - rustc 1.97.1 (8bab26f4f 2026-07-14)


Rust is installed now. Great!

To get started you may need to restart your current shell.
This would reload your PATH environment variable to include
Cargo's bin directory ($HOME/.cargo/bin).

To configure your current shell, you need to source
the corresponding env file under $HOME/.cargo.

This is usually done by running one of the following (note the leading DOT):
. "$HOME/.cargo/env"            # For sh/bash/zsh/ash/dash/pdksh
source "$HOME/.cargo/env.fish"  # For fish
source "~/.cargo/env.nu"  # For nushell
source "$HOME/.cargo/env.tcsh"  # For tcsh
. "$HOME/.cargo/env.ps1"        # For pwsh
source "$HOME/.cargo/env.xsh"   # For xonsh
```
