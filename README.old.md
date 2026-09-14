# Switch

Simple CLI to switch between multiple profiles for any app that uses a file or folder for its configuration (e.g., Codex, Claude, VSCode, Cursor, SSH, Git).

## Overview

Store multiple profiles and swap your active config with one command. Works for both single files (like `~/.codex/auth.json`) and entire folders (like `~/.vscode/User`).

## Download prebuilt binaries

Continuous integration builds upload platform-specific archives for each successful run. You can download the latest artifacts here:

- Latest CI build artifacts: [release-binaries workflow](https://github.com/surajmandalcell/switch/actions/workflows/release-binaries.yml)

Artifact URLs are tied to individual runs, so open the most recent successful run to grab the archive for your platform. If you prefer to build locally, follow the setup instructions below.

## TL;DR for quick usage

```
git clone https://github.com/surajmandalcell/switch && cd switch
make install

# login to one of your codex cli account and then
switch add codex codex1

# logut of current codex cli account and login to new one and then
switch add codex codex2

# now you can freely switch between them by just one, if you have more it behaves the same
switch
# or
switch codex codex1
```

## Features

- **App‑agnostic**: Works with any file/folder config
- **Built‑in templates**: Codex, Claude, VSCode, Cursor, SSH, Git
- **Wizard setup**: `switch add` guides detection and setup
- **Cycle or target**: Cycle profiles or switch to a specific one
- **Folder support**: Back up and restore whole config directories

## Installation

### From Source

```bash
git clone https://github.com/surajmandalcell/switch.git
cd switch
go build -o ./build/switch switch.go
```

### Install Globally

```bash
# System-wide installation
sudo cp ./build/switch /usr/local/bin/

# Or install to user's ~/bin directory
mkdir -p ~/bin
cp ./build/switch ~/bin/
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc  # or ~/.bashrc
source ~/.zshrc
```

### Cross-Platform Builds

```bash
# macOS
GOOS=darwin GOARCH=arm64 go build -o ./build/switch-darwin-arm64 switch.go
GOOS=darwin GOARCH=amd64 go build -o ./build/switch-darwin-amd64 switch.go

# Linux
GOOS=linux GOARCH=amd64 go build -o ./build/switch-linux-amd64 switch.go
GOOS=linux GOARCH=arm64 go build -o ./build/switch-linux-arm64 switch.go

# Windows
GOOS=windows GOARCH=amd64 go build -o ./build/switch-windows-amd64.exe switch.go
```

## Quick Start

### 1. Add your first app/profile

```bash
switch add
# Wizard will auto-detect known apps or let you set up manually
```

### 2. Switch between profiles

```bash
# Cycle default app
switch

# Cycle specific app
switch codex

# Switch to a specific profile
switch codex work

# List apps and profiles
switch list
switch list codex
```

## Usage

### Commands

- `switch`: Cycle the default app
- `switch <app>`: Cycle profiles for an app
- `switch <app> <profile>`: Switch to a profile
- `switch add`: Launch setup wizard
- `switch add <app>`: Add a profile to an app (prompts for name)
- `switch add <app> <profile>`: Add current config as a profile
- `switch list` / `switch list <app>`: List apps or profiles
- `switch default <app>`: Set default app
- `switch config`: Open config file in editor
- `switch <app> config`: Open config file in editor

### Examples

```bash
# Quick account switching
switch                    # Cycles to next account

# Specific account switching
switch codex work         # Switches to 'work' account
switch codex personal     # Switches to 'personal' account

# Account management
switch add codex staging  # Saves current auth.json as 'staging'
switch list codex         # Shows all accounts with current indicator

# Configuration management
switch default codex      # Sets codex as the default app
switch config             # Opens ~/.switch.toml in your editor
switch codex config       # Alternative way to open config
```

## Configuration

Config is stored at `~/.switch.toml`.

Example:

```toml
[default]
  config = "codex"

[codex]
  current = "work"
  accounts = ["work", "personal"]
  auth_path = "~/.codex/auth.json"
  switch_pattern = "{auth_path}.{name}.switch"

[vscode]
  current = "dev"
  accounts = ["dev", "personal"]
  auth_path = "~/.vscode/User"
  switch_pattern = "~/.vscode/profiles/{name}.switch"
```

## Development

### Testing

```bash
make test
```

### Building

```bash
go build -o ./build/switch switch.go
```

### Contributing

PRs welcome.

## Requirements

- Go 1.24.5 or higher
- Write access to your home directory

Note: This repo uses Go's module-managed toolchain. If you see toolchain mismatch errors locally, ensure your Go is up-to-date (1.25+) or set GOTOOLCHAIN=auto in your environment.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**Suraj Mandal**

- GitHub: [@surajmandalcell](https://github.com/surajmandalcell)
- Project: [github.com/surajmandalcell/switch](https://github.com/surajmandalcell/switch)
