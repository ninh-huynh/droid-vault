## Setup docker for macOS completely free (without Docker Desktop)

```zsh
# Install docker cli client
brew install docker

# Install docker daemon
brew install colima

# Start docker daemon on foreground
colima start -f

# Using docker cli as normal

# TODO, login to Docker Hub?
```

Clean up colima when unused
```bash
colima prune
colima delete
```

## Using Docker Desktop (free for personal only)

