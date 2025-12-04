# AGENTS.md

## Repository Overview

This repository contains development container configurations for various projects. It's organized as a collection of containerized development environments under the `projects/` directory.

## Project Structure

```
devcontainers/
├── projects/          # Container configurations for different projects
│   └── yazi/         # Yazi file manager development environment
│       └── Dockerfile
├── LICENSE           # CC0 1.0 Universal license
└── README.md         # Repository description
```

## Available Projects

### yazi-dev
A development container for the yazi file manager project.

**Build Command:**
```bash
podman build --build-arg USERNAME=<username> --build-arg UID=<uid> --build-arg GID=<gid> -t yazi-dev projects/yazi/
```

**Run Command:**
```bash
podman run -it --name yazi-dev-container yazi-dev
```

**Features:**
- Based on Fedora Linux
- Rust stable toolchain pre-installed
- Cargo (Rust package manager) pre-installed
- Jujutsu (jj) installed via cargo
- Fish shell as default
- Customizable user with specified UID/GID
- Automatically clones https://github.com/xeysz/yazi to $HOME/workspace using jujutsu --colocate
- Development tools (@development-tools, git) included
- Cargo bin path automatically configured for fish shell
- Development tools (@development-tools, git) included

## Container Configuration Pattern

Each project follows this pattern:
- Dedicated directory under `projects/`
- Dockerfile with parameterized user configuration
- Standard ARG parameters: USERNAME, UID, GID
- Repository cloning to $HOME/workspace
- Development environment setup

## Working with Devcontainers

### Adding New Projects
1. Create new directory under `projects/`
2. Add Dockerfile with user parameterization
3. Follow the established pattern for consistency

### Building Containers
Always pass the user parameters using podman:
- `USERNAME`: The username for the default user
- `UID`: User ID for permission matching
- `GID`: Group ID for permission matching

### Repository Management
- This repository uses git for version control
- License: CC0 1.0 Universal (public domain)
- No CI/CD configurations currently present

## Gotchas

- All Dockerfiles should support user parameterization
- Fish shell is used as the default shell for all containers
- Fish configuration should be added to ~/.config/fish/conf.d/filename.fish where filename describes the contents
- Repository cloning should happen as the specified user
- Default working directory should be $HOME/workspace
- Use Fedora Linux as base image (docker.io/library/fedora) for consistency with existing containers
- Containers are managed using podman, not docker
- Use dnf package manager for package installation
