# dsort

A lightweight Linux file-sorting daemon written in modern C++.

>  Vibe-coded by the author.

------------------------------------------------------------------------

## Features

-    **Zero Dependencies**: Uses only standard C++ libraries and Linux
    system calls.
-    **Real-time Monitoring**: Instant file sorting using `inotify`
    event tracking.
-    **TOML-like Configuration**: Clean, human-readable rules for your
    file organization.
-    **Smart Paths**: Full support for home expansion (`~`) and
    absolute paths (e.g., `/mnt/storage`).
-    **Conflict Handling**: Intelligent auto-renaming (e.g.,
    `file(1).png`) to prevent accidental data loss.
-    **Low Footprint**: Minimal CPU and RAM usage, perfect for
    background execution on Linux systems.

------------------------------------------------------------------------

## Installation

Built for Linux systems with a **C++20 compatible compiler** such as
`gcc` or `clang`.

### 1. Clone the repository

``` bash
git clone https://github.com/yourusername/dsort.git
cd dsort
```

### 2. Build and install

The provided `Makefile` compiles the binary and installs it to
`~/.local/bin`.

``` bash
make
make install
```

> **Note:** Ensure `~/.local/bin` is included in your `$PATH`.

------------------------------------------------------------------------

## Configuration

`dsort` looks for its configuration file at:

    ~/.config/dsort/config.toml

You can define which directories to watch and specify rules for file
patterns.

``` toml
# Directories to monitor
watch = ["~/Downloads", "~/Desktop"]

# Default folder for files that don't match any rules
default = "Other"

[rules]
# High-priority specific matches
"*wallhaven*" = "/home/honeypie/.wallpapers"
"*work_project*" = "~/Documents/Work"

# General extension matches
"*.pdf" = "Documents"
"*.zip" = "Archives"
"*.png" = "Images"
"*.jpg" = "Images"
```

------------------------------------------------------------------------

## Usage

`dsort` can run as a background daemon or perform a one-time cleanup.

### Run as a background daemon

``` bash
dsort --daemon
```

### One-shot scan

Scan and organize all existing files in the watched directories
immediately:

``` bash
dsort -s
```

------------------------------------------------------------------------

## Command-line Arguments

  Flag               Description
  ------------------ --------------------------------------------------------
  `-s`, `--scan`     Scan existing files and exit
  `-c`, `--config`   Path to a custom configuration file
  `-d`, `--daemon`   Start in background monitoring mode
  `--dry-run`        Show what would be moved without actually moving files

------------------------------------------------------------------------

## License

MIT License
